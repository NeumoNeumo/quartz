---
id: hifi
title: hifi
aliases: []
tags: []
---

## Software

PipeWire's [parametric EQ](https://docs.pipewire.org/page_module_filter_chain.html) chains a number of biquads together. But biquads introduce nonlinear phase response as shown [here](https://thesofproject.github.io/latest/algos/eq/equalizers_tuning.html). It is recommended to use FIR (Finite Impulse Response) instead of IIR (Infinite Impulse Response).

`$HOME/.config/pipewire/pipewire.conf.d/custom.conf` :
```conf
context.properties = {
  default.clock.allowed-rates = [ 44100 48000 88200 96000 176400 192000 352800 384000 ]
}

stream.properties = {
    resample.quality = 10
}
```

## Harman's curve

- The in-room steady-state magnitude frequency response curve is measured in a listening room with reflections, while an anechoic chamber frequency response only captures the direct sound.  
- For speakers with a flat on-axis frequency response curve in an anechoic chamber, the steady-state curve in a typical listening room exhibits a gently declining curve (1dB/octave) from low to high frequencies.  
- Harman target curves are a series of curves, like Harman over-ear 2018 and Harman in-ear 2019 target curves.
- First, the steady-state magnitude frequency response of the speaker in the Harman reference listening room is adjusted to be flat. However, listeners generally perceive this sound as having too much high frequency. Subsequently, through extensive double-blind listening tests, listeners adjusted the levels of low and high frequencies based on their preferences, ultimately resulting in a target in-room curve (in-room steady-state frequency response) that most people preferred—this is the **Harman room curve**(the frequency response measured near the head rather than at the eardrum
). Interestingly, this curve closely resembles the steady-state curve naturally exhibited by high-quality speakers with a flat frequency response measured in an anechoic chamber when placed in a typical room.
- The core objective of the **Harman headphone curve**(the frequency at the eardrum response measured rather than near the head) is to use headphones to simulate the experience of listening to a pair of high-end speakers in an acoustically excellent room.
- The difference of a Harman headphone curve and a Harman room curve is a Head-Related Transfer Function(HRTF).

## Weighting

A-, B-, and C-weighting are frequency-weighting curves used in sound-level measurements to approximate the frequency sensitivity of human hearing at 40 phon, 70 phon and 100 phon.

> [!note] phon
> If a sound is perceived to be as loud as a 1kHz pure tone at L dB SPL(Sound Pressure Level), then its loudness level is L phon.

![](../00-Attachments/20260812100133.png)

A-weighting has a higher low-frequency damp than B-weighting and C-weighting because human hearing is less sensitive to low frequencies at a lower loudness level.

## EQ

In depth articles: https://www.reddit.com/r/oratory1990/wiki/index/knowledge_posts/  

Useful EQ presets
- https://www.reddit.com/r/oratory1990/wiki/index/list_of_presets/
- https://peqdb.com/
- https://squig.link/

Useful measurements
- https://huihifi.com
- https://reference-audio-analyzer.pro/en

#### Q&A

1. 调音师早就帮你调好了，还需要你自己eq吗？调音师是物理调音，难度比eq高很多，经常牵一发而动全身。DSP调音会方便很多。事实上，现在有一些耳机干脆直接自己集成电路进行DSP调音了，例如airpods pro的自适应均衡。有先进工艺何必再执着于调音仙人传统手艺？除非是将耳机当作奢侈品。
2. 为什么不自己测曲线？前提是你有隔音室或至少是安静的房间、人工耳与高精度的微型拾音器。
3. 为什么不是一个产品一个预设而是一个耳机一个预设？因为即使同一款耳机，也会有方差，尤其如果品控一般，例如[这里](https://zhuanlan.zhihu.com/p/1889705136332443687)展现了6个shp9500耳机的频响曲线。此外，耳机在生产后，如果结构没有大的损坏，例如耳罩掉了（虽然用久了耳罩磨损是不可避免的，至少我两年前买的一个皮质耳罩的耳机已经出现磨损了），以人耳的灵敏度，频响曲线几乎没有区别，参见[此文](https://www.headphonesty.com/2025/07/science-ear-pad-burn-changes-headphones-sound/)（由此也可见煲机是玄学）。[这里](https://zhuanlan.zhihu.com/p/75482749)总结了一些人耳的听力极限。
4. 为什么这么重视频率响应？因为这是所有指标中与听众偏好最相关的（参见[此文](https://aes2.org/publications/elibrary-page/?id=5270)），至少比价格更相关（见[此文](https://doi.org/10.1121/1.4984044)，除非是出于越贵越好的心理暗示）。
5. 照你这么说我可以通过调音让9.9原道秒大奥？不是。频响曲线是在输入稳定的环境下测的，既不反映耳机对模电的响应速率也不反映失真率。但当中高端耳机的本身的体质足够好的情况下，对人耳而言它们唯一的区别就是频响曲线。顺便一提，通常耳机在低频的THD+N会更高，所以强行拉高低频表现差劲的耳机的低频响应曲线可能导致整体更大的失真率，反而导致听感下降，这是需要权衡的。[这篇文章](https://pubmed.ncbi.nlm.nih.gov/29716278/)在将不同的耳机EQ成HD800后测量了它们的失真，并在真实的HD800上模拟重放了这些失真，结果是低价耳机在70-80dBA时的失真即可被感知到。
6. EQ会引入失真吗？EQ有不同的算法实现，如果使用IIR，则会引入相位失真(即，不同频率的波的群延时不同)，但人耳对此并不敏感（虽然人耳对左右耳音频的相位差异是比较敏感的，但你会左右耳用不一样的滤波器吗？），只有在短时波包中人耳才有感知到区别，例如鼓点，参见[此文](https://www.researchgate.net/publication/247027642_On_the_Audibility_of_Midrange_Phase_Distortion_in_Audio_Systems)；而采用线性相位滤波器则不会引入相位失真。
7. 为什么要追求这样的target？我听着好听不就行了？事实上这是两条路，一条是追求自己觉得好听；另一条路是寻求高保真，尊重原著，希望自己听到与音频制作者一样的内容。对于前者，实际上你就是在购买厂家的调音，那么你不设置eq即可，没有什么损失。对于后者，如果混音师使用的是正规的工作室，那么他的配置应该是直达声是平直响应的监听音箱与一个接近哈曼参考值的听音房间。那么耳机的目标就是在给定与调音师使用的一样的音频信号时重建调音师在听音房间中的耳蜗处的声场。这是有相对明确的标准的，而我们的target就是在追求这个标准，具体可见[此文](https://peqdb.com/wiki/PEQdB-White-Paper.pdf)。当然，如果混音师师考虑到自己的听众的听音设备低频缺失高频无力或自己的监听就不行，就会主动调味，那反而会导致在target下味道过重，在一些流行音乐中确实存在这样的现象。


- 但也不能唯数据论，尽管常见的参数，例如频响曲线与失真，表征了系统的许多性质，并且理论上来说，在最小相位系统中，频响曲线蕴含了系统的一切信息，包括群延时与混响。
- 然而存在以下因素影响
  - 声源与耳廓耦合会导致最小相位的假设不成立。考虑一个波从空间的两点出发(对应耳机振膜上的两点)或经过空间的两条路径，得到两个时域响应$a_1 x(t-\tau_1)$与$a_2 x(t-\tau_2)$，其中$a,\tau>0$，则连续系统的频域响应为$H(s) = e^{-s\tau_1} (a_1+a_2e^{-s(\tau_2 - \tau_1)})$，当$(\tau_2-\tau_1)(a_2-a_1)>0$时，$s$存在右半复平面的根，因此不是最小相位系统。
  - 即使是最小相位系统，我们一般看频响曲线也只看个大概，而那些容易被忽略的波动，尤其是在高频，会影响相位响应。设最小相位系统频响曲线为$|H(w)|$给出，则其相位由$-\mathcal H\{\log |H(w)|\}$给出，其中$\mathcal H\{x(t)\} = \frac{1}{\pi} \operatorname{p.v.} \int_{-\infty}^{\infty} \frac{x(\tau)}{t-\tau}\,d\tau$为Hilbert变换，可见相位受到邻域波动很大影响。
    - 这里更本质反映的是指标的可读性的问题。不同的指标是为不同的目的设计的，因此它们在解决它们所针对的问题上是有效的，但是在反映其它问题上，可能表现不佳。即使一个指标理论上具有系统的所有信息，但如果人类想仅凭肉眼与想象用它去推测另一个指标的数值，可能依然是不够准确的。
  - 即使频响曲线是光滑的、完美的并且确实是最小相位系统，测量的结果与你佩戴的结果是不一样的，尤其是高频+动圈的组合
    - 动圈的分割振动会带来更复杂的多源相位差异，并且这种差异会导致系统对耳机佩戴方式敏感。
    - 在短程，高频更容易发生干涉。平面耳机与静电耳机虽然没有分割振动，但同样存在这种问题。不过由于平面相位相对一致，对耳机佩戴方式更不敏感，更容易通过前级补偿解决。
- 并且这些因素对听感造成的影响是无法被谐波失真、非谐波失真以及粗略的频响曲线捕捉到。

## Hardware

The definition of galvanic isolation is that there is no DC conductive path between the input side and the output side—that is, there is no direct ohmic connection between them. In other words, $R_{\rm DC}(\text{input GND},\text{output GND}) \to \infty$. One practical criterion is to check whether the input and output share a common ground. For example, ordinary buck and boost converters have a common ground, so they are not galvanically isolated. A flyback converter, by contrast, transfers energy through an intermediate transformer and therefore provides galvanic isolation.

The common intuition that “current through an inductor has inertia” is essentially a consequence of the inductor equation $v=L\frac{di}{dt}$: an instantaneous change in current would require an infinite voltage. More fundamentally, the inductor equation is a special case of Faraday’s law of electromagnetic induction, $v=\frac{d\lambda}{dt}=N\frac{d\Phi}{dt}$, applied to an ideal independent inductor, for which $\lambda=Li$. In that sense, it may be more appropriate to say that the inductor itself exhibits this “inertial” behavior. In an ideal transformer modeled as perfectly coupled inductors, if the primary winding is suddenly open-circuited, the primary current can indeed drop abruptly to zero, while the secondary current changes abruptly at the same time so as to maintain continuity of the magnetic flux. For a general pair of coupled windings, the more general relations are $\lambda_p=L_p i_p+M i_s$ and $\lambda_s=M i_p+L_s i_s$.

In an ideal transformer, the magnetic permeability $\mu$ of the core is infinite. Since $B=\mu H$, for a finite $B$, we must have $H=0$. By Ampere's law $H\ell = N_p i_p - N_s i_s$, we have $N_p i_p=N_s i_s$.

> [!note] Analogy between electric and magnetic circuits
> | Electric circuit | Magnetic circuit |
> | --- | --- |
> | Voltage $V$ | MMF $\mathcal F=NI$ |
> | Current $I$ | Magnetic flux $\Phi$ |
> | Resistance $R$ | Reluctance $\mathcal R$ |
> | $I=V/R$ | $\Phi=\mathcal F/\mathcal R$ |
> 
> For a core, $\mathcal R=\frac{\ell}{\mu A}$.

When the secondary of a transformer is open-circuited, the voltage applied to the primary determines the rate of change of magnetic flux through Faraday’s law. The magnetic flux density corresponds to a certain magnetic field strength, so a magnetic field must be established. According to Ampère’s circuital law, current is required to produce this field. This current is the magnetizing current.

In fact, an ordinary inductor can be viewed as having air as its “core,” in which case its operating current is essentially the magnetizing current, although we do not usually describe it that way.

When a load is connected to the secondary of a transformer, the induced secondary voltage drives a current through the load. This secondary current produces a magnetomotive force that tends to oppose the magnetic field in the core. However, the core flux is constrained by the voltage applied to the primary. As a result, the primary current can be regarded as consisting of two components: one component, the magnetizing current, establishes the original magnetic field, while the other, the load current referred to the primary, counteracts the magnetomotive force produced by the secondary current.

The purpose of the magnetic core is to use a high-permeability material to reduce the ratio of magnetizing current to load current.

#TODO
实际变压器的 T 形等效电路

One problem that can arise in a Hi-Fi system with a shared ground is the formation of a ground loop. Sources of noise introduced into the signal ground by a ground loop include the following:

1. Electromagnetic induction: the ground loop effectively acts as a loop antenna and picks up ambient 50/60 Hz magnetic fields.
2. Current flowing through protective earth (PE): ideally, no current should flow through PE, but in practice there may be currents due to Y capacitors and small resistive leakage paths. These currents produce voltage drops, so the ground potentials at different points may differ slightly.

