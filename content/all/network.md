---
id: network
aliases: []
tags:
  - linux
---

## Common Sense

![](https://people.netfilter.org/pablo/nf-hooks.png)

- 在output hook与postrouting之间也可能有routing decision，如果output hook对流量进行了修改，例如标记fwmark。
- 在routing decision中根据route type判断是去往forward还是input。如果是forward，在正式forward hook执行之前会判断net.ipv4.ip_forward。
- NAT只需要通过postrouting中的masquerade实现SNAT就可以了，nft会自动根据conntrack的记录处理回包时的DNAT。
- 如果应用程序在发起一个网络请求时没有填好SIP，linux会首先根据routing decision的结果填写SIP，可以用形如`ip route get to 58.63.237.245`的指令看到linux会填写什 么src。
- tcpdump抓包的位置位于Driver RX path与Ingress之间以及Egress与Driver TX path之间。
- ip rule/route只进行路由，而无法进行更高级的流量管理，于是有了iptables。之后又有了其它工具：IPv4 用 iptables，IPv6 用 ip6tables，ARP 协议用 arptables，网桥用 ebtables，各自为政，相对混乱，而nftables则用一套语法统一所有，并解决了 iptables规则逐个线性匹配的性能瓶颈。现在原生iptables已经被废弃，实际上用的是 iptables-nft wrapper。
- linux上单张物理网卡上能够配置多个虚拟子网卡，例如macvlan。macvlan挂载在物理网卡的rx_handler上，位于Ingress处，所以你可以用tcpdump抓到macvlan处理前的包。如果`tcpdump -i macvlan0`则可以看到这个匹配这个子网卡的mac的包。
- linux上从某个网卡发包不意味着这个包的sip一定是这个网卡所绑定的ip。

### TUN vs TPROXY

tproxy相对于基于gvisor stack的tun的优势在于前者将代理软件从第三层与第四层的繁重任务中解放了出来。第三层的任务包括IP分片与重组、IP头部解析与校验和、TTL(生存时间)的维护，第四层任务包括TCP状态机、序列号与包重传、拥塞控制。tproxy就像socket编程，而tun则需要你处理原始的L3 IP数据包。而基于system stack的tun则更巧妙一些，它在本地开启一个监听端口，例如127.0.0.1:10000，然后将从tun中读到的包的目的地改为127.0.0.1:10000，再重新塞到loop设备上。那么第三层与第四层的工作就会由OS代劳，代理软件直接从127.0.0.1:10000读取干净的数据即可。但显然，这依然比tproxy慢。

### `ip route`指令输出详解

`ip -d route`可以输出更细节的信息。

1. `type`定义了内核拿到数据包后采取的行为，例如在prerouting后，`unicast`表示走向forward，`local`则表示走向input。此外还有`blackhole`直接丢弃，`unreachable`丢弃并返回ICMP报错等。
2. `proto`说明这条规则是谁写入的，kernel表示内核自动生成的，static表示手动添加的，dhcp表示动态获取的等
3. `scope`表示目的地的可达范围，可用于进行sip判断。不仅路由表有scope，网卡ip也有scope（参见`ip a`），sip的scope必须在路由表的scope的范围内。

scope表面上看上去多此一举，但可能存在这么一条记录`ip route add default via 10.27.255.254 dev wlan0`，这条记录是不包含`src`的，因此必须根据scope进行SIP决断（反之，其实如果你的路由表精确配置且已经包含了src信息，网卡不绑定ip也可以正常使用）。你经常看到有src其实是dhcp为了防止歧义给你提供的，但其实在骨干路由器中，会有几十万条路由，如果使用src，在本地ip变动时就会影响所有条目，因此一般基于scope比较。

`ip route`按照子网掩码长度从长到短的顺序进行匹配(也就是按照匹配精度从高到低)，如果有两个相同的掩码则取metric较小的。default表示0.0.0.0/0

### 虚拟环境

注意虚拟机与容器在bridge上含义是不同的。

btw, 常见虚拟化管理平台有Proxmox Virtual Environment(PVE)与VMWare ESXi。

#### 虚拟机
如 VMware, VirtualBox, KVM

- Bridged networking: 网卡可以作为虚拟网桥上的端口存在(`ip a`状态中会有`master
  <bridge>`的标识)，这对应上图的Bridge port yes，此时这张网卡跑在第二层，不会有
  ip绑定，而这个ip转移到了bridge上。
- NAT: 相当于docker的bridged mode（见下文）不过为了跨平台性，VMware等软件可能会
  尽可能用tun那一套完成所有操作，就像mihomo一样。
- host-only：虚拟机在与外界隔绝的子网中。相当于去除一些路由配置的NAT。

#### 容器
如docker，podman，LXC

- Host mode：与host共用同一个network namespace。
- Bridge mode：docker0作为bridge，容器通过veth pair与docker0相连，它们构成一个子
  网，通过NAT与外界通信。
- Container mode：与另一个已存在的容器共用network namespace
- Overlay mode：可在多个宿主机之间建立逻辑网络，基于VXLAN(MAC-in-UDP)。
- Macvlan mode：使用是linux网络macvlan的bridge模式。让物理网卡开启promiscuous
  mode(也有一些网卡Hardware MAC filtering支持，这种情况下自然无需promiscuous)，
  然后让macvlan驱动自行处理MAC地址，并把相应数据传输给不同容器的网络栈。缺陷：如
  果host发出指向container的连接，如果不加配置，这个以太网帧默认会通过物理网卡被
  直接发往外界，而为了防止回环，交换机不会把这个包再传回来，于是这个包石沉大海了。
  不过可以创建一个新的macvlan网卡并配置相应路由，让host向容器网段的数据包通过这
  个macvlan进行传输，而macvlan驱动内部是可以互通的。

## Reference
https://wiki.nftables.org/wiki-nftables/index.php/Netfilter_hooks
