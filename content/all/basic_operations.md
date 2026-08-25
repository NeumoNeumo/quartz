---
id: basic_operations
title: basic_operations
aliases: []
tags:
  - CS
  - commands
  - DevOps
  - prompt
  - linux
---
# Commonly Used Commands and Operations
## apex environment
```text
# first install mamba from https://github.com/conda-forge/miniforge#mambaforge
conda config --show-sources
conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/'
mamba create -n apex python 3.9 -y
mamba install pytorch==1.12.0 torchvision==0.13.0 torchaudio==0.12.0 \ 
  cudatoolkit=11.3 cudatoolkit-dev=11.3 -c pytorch -y
mamba install omegaconf openmim timm tensorboard nltk einops datasets[vision] \
  webdataset pandarallel ftfy termcolor wandb -y
mim install mmcv-full
pip install mmsegmentation
```
### Port forwarding
```text
ssh -CfN -L 23333:gpu020:22 name@remote
ssh -C -L 23333:gpu020:22 name@remote
ssh -C -L 23333:gpu021:22 name@remote
# C: compress
# f: background
# N: Do not execute a remote command. This is useful for just forwarding ports.
# L: forward
ssh -L localPort:remote:remotePort sshServer
# Run locally. We cannot connect to `remote`. But we can connect to `sshServer` which can connect to remote. 
ssh -R localPort:remote:remotePort sshServer
# Run on `sshServer`. We can connect to neither `sshServer` nor `remote`. But `sshServer` can connect to us.
```
## Slurm
tutorial: http://172.18.34.4/
```text
srun -p gpulab02 -N1 -c2 --mem=8gb --gres=gpu:1 -q gpulab02 -t12:00:00 --pty bash
salloc -p gpulab02 -N1 -c2 --mem=8gb --gres=gpu:1 -q gpulab02 -t12:00:00 bash
salloc -p gpulab02 -w gpu021 -N1 -c2 --mem=8gb --gres=gpu:1 -q gpulab02 -t12:00:00 &
# -N, --nodes
# --mem=<size>[units]: Specify the real memory required per node. Default units are megabytes
squeue --format="%.8i %.9P %.12j %.12u %.8T %.10M %.9l %.6D %R" --me
```
## Linux
This is what cmake find_pkg use: PKG_CONFIG_PATH=$HOME/mambaforge/lib/pkgconfig
nohup: the process is independent with the terminal
&: the process runs in the background
resolvectl: show current DNS server
vim /etc/resolv.conf: change DNS server temporarily
Restart xorg GUI: sudo killall Xorg
convert filename encoding: convmv --notest -r -f cp936 -t utf8 ./
```text
mpv --force-window --sub-files=123.srt some-audio.mp3
mpv av://v4l2:/dev/video0
  = ffplay /dev/video0
wget -ci
# -c: continue getting a partially-downloaded file
# -i: input file
find . -type f -name "*.txt" = shopt -s globstar & ls /etc/{,**/}*.conf

nohup my_command > my.log 2>&1 &
echo $! > save_pid.txt
kill -9 `cat save_pid.txt`
rm save_pid.txt

lsof -Pni
# -P: no port/service conversion
# -n: no ip/hostname conversion
ss -tuapn
# -a: display both listening and non-listening
# -p: show processes
# -t: tcp
# -u: udp
# -n: no ip/hostname conversion
clang++ a.cpp -o a.out -pg & ./a.out & gprof a.out gmon.out > analysis.txt
sudo apt-get -o Acquire::https::proxy="http://localhost:7890" update
tar -cI 'xz -9 -T0' -f archive.tar.xz dir/
ffmpeg -hwaccel cuda
ffmpeg -i "concat:1.mp3|2.mp3|3.mp3|4.mp3" -acodec copy output.mp3 
ffmpeg -i input.flac -lavfi "showspectrumpic=s=1280x720:mode=combined:fscale=log:color=intensity" /tmp/spectrum.png && mvi /tmp/spectrum.png && command rm /tmp/spectrum.png
ffmpeg -i input.flac -af volumedetect -f null -
curl https://ipinfo.io # Abroad
curl https://cip.cc/ # Domestic
curl -6 https://ip.p3terx.com
# QUIC test
curl --http3-only https://1.1.1.1 -v -o /dev/null
# Cloudflare IP test
sudo -u mihomo -- curl --fail --noproxy '*' --resolve "speed.cloudflare.com:443:2606:4700:57::d9af:6a9c" --silent --show-error --max-time 10 -o /dev/null -w 'total=%{time_total}s │ start=%{time_starttransfer}s speed=%{speed_download}B/s\n' 'https://speed.cloudflare.com/__down?bytes=20000000'
cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 233 | head -n 1
cat /dev/urandom | tr -dc [:print:] | head -c 20
sudo mount -o port=12049 -t nfs 172.18.34.25:/mnt/storage /mnt/storage/
aria2c -i inputfile --all-proxy="http://localhost:7890" -m 0 -x 10 -j 32 --optimize-concurrent-downloads true --check-certificate false -c
	-m: max retries
    -j, --max-concurrent-downloads: how many files (lines in the input file) to download simultaneously
	-s, --split: how many mirrors to use to download each file, mirrors should be listed in one line
	-x, --max-connection-per-server: how many streams to use for downloading from each mirror.
	-c: continue
	-o: output file name
	-d: dir
ncal -bw3M
	-b: cal-like output
	-w: display week numbers
	-3: display the previous and the next month
	-M: Monday as the first day of the week
modprobe v4l2loopback video_nr=9 card_label=Video-Loopback exclusive_caps=1
sudo modprobe v4l2loopback video_nr=9 exclusive_caps=1 card_label="Loopback-1"
sudo modprobe -r v4l2loopback
_RJEM_MALLOC_CONF=prof_leak:true,lg_prof_sample:0,prof_final:true,prof_prefix:/tmp/jeprof cargo run
paru && rustup update && cargo install-update -a --locked && fisher update && nvm install latest && mamba update --all -y && $HOME/.config/tmux/plugins/tpm/bin/update_plugins all && pixi global update
paru -Rs (paru -Qdtq) 
curl -s "https://archlinux.org/mirrorlist/?country=CN&protocol=https&ip_version=4&use_mirror_status=on" | sed -e 's/^#Server/Server/' -e '/^#/d' | rankmirrors -n 5 -
```
record audio
```fish
pw-cat --record --target spotify --raw --format=f32 --rate=44100 --channels=2 - | \
  ffmpeg -f f32le -ar 44100 -ac 2 -i - -acodec flac -f flac -compression_level 8 -y a.flac &
sleep 1h 3m && pkill -TERM pw-cat
dunstify "Music Recorded"
```
### rclone
```text
rclone mount --daemon L40: ~/L40/
fusermount -u ~/L40
```
### terminal
```text
<C-d>: end of file
<C-M>: end pf line
<C-h>: erase character left
<C-w>: erase word left
<C-u>: erase line
<C-c>: interrupt
<C-\>: force quit
<C-z>: suspend
```
### install without sudo
```text
1. yum search <pkg>
2. rpm2cpio ~/rpm/x.rpm | cpio -id (i means extract and d means create missing directory)
3. export LD_LIBRARY_PATH / PATH / MANPATH =...; 
```
## git
index = cache area = staging area = pre-commit area
#### Good tutorials:
1. Interactive: http://onlywei.github.io/explain-git-with-d3/
2. low-level principle: https://www.lzane.com/tech/git-merge/
3. development practice: https://www.atlassian.com/git/tutorials/
#### init
```text
git config --global --list
git config --global user.name "XXX"
git config --global user.email "XXX"
git init <folder_name>
```
#### diff
```text
workspace and repo: git diff HEAD
workspace and index: git diff
index and repo: git diff --cached = git diff --staged
all: git status
```
#### commit & restore
```text
index->workspace: git restore <file> = git checkout -- <file>
repo->index: git restore --staged <file>
  (`git reset` is an old version of data recovery)
clean desolated commits right now:
  git reflog expire --expire=90.days.ago --expire-unreachable=now --all
  git gc --prune=now
  git reflog expire --expire=90.days.ago --expire-unreachable=30.days.ago --all
git reset HEAD [file]:
  | options | HEAD | index | workspace |
  | ------- | ---- | ----- | --------- |
  | --soft  | Y    | N     | N         |
  | --mixed | Y    | Y     | N         |
  | --hard  | Y    | Y     | Y         |
redo commit: git commit --amend
force push if no new commits: git push --force-with-lease (like remote amend)
  git push --force is dangerous because it will not check wheather new
  commits exist
```
#### branch
```text
new branch: git branch <branch_name>
list branch: git branch
switch branch: git switch <branch_name>
  -c: create a new branch and switch to it
switch branch: git checkout <branch_name>
  -b: create a new branch and switch to it
```
#### history
```text
git log
  --oneline: concise output
  --graph: graphic output
  --reverse: reverse the timelien
  --author=<name>
```
#### remote
```text
git remote add <alias> <url>
git remote add <alias> git@github.com:user_name/repo_name.git
git remote rm <alias>
git remote rename <old_name> <new_name>
remote list: git remote
  -v: show url
detailed imformation: git remote show <alias>
git push <alias> [branch]
git fetch <alias>
git merge <alias/remote_branch> [local_branch]
git merge <local_branch1> [local_branch2]
git pull <alias> <remote_branch>[:local_branch]
  = git fetch [alias] && git merge
```
#### others
```text
git rm = rm && git add <file_removed>
git commit -a = git add . && git commit

attach tag: git tag -a <tag_name> [hash_of_commit]
all tags: git tag

git submodule update --remote --merge # update submodule to latest
```

## pandoc
```text
pandoc --pdf-engine=xelatex --highlight-style tango --toc -N test.md -o test.pdf
  use pdflatex by default. switch to xelatex to support unicode natively
  -N adds section number
  --highlight-style tango   Default style is not clear
  -V key:value  Specify metadata. Equivalent to yaml_metadata
```
yaml_metadata:
```yaml
---
title: "My Title"
author: "Neumo"
date: \today{}
geometry: "top=2cm, bottom=1.5cm, left=2cm, right=2cm, a4paper"
colorlinks: true
header-includes:
    - \usepackage{blindtext}
---
```
## Hardware
get CPU frequency:
`cat /sys/devices/system/cpu/cpufreq/policy*/scaling_cur_freq`
get CPU energy used:
`cat /sys/class/powercap/intel-rapl/intel-rapl:*/energy_uj`
fan control:
`echo 255 > /sys/class/hwmon/hwmon4/pwm1`

## Languages
### C/CPP
`cmake -DCMAKE_BUILD_TYPE=Debug ..`
To successfully display `std::string`, please
`set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -fstandalone-debug")`
static: `g++ -static-libgcc -static-libstdc++ xxx.o`
### Python
We can use the following cmds to generate stub files for cv2:
```bash
mamba install mypy
cd $(python -c 'import cv2, os; print(os.path.dirname(cv2.__file__))')
stubgen -m cv2 -o ./
cp cv2.pyi __init__.pyi
```
colab python 3.8:
```text
!wget -O mini.sh https://repo.anaconda.com/miniconda/Miniconda3-py38_4.8.2-Linux-x86_64.sh
!chmod +x mini.sh
!bash ./mini.sh -b -f -p /usr/local
!conda install -q -y jupyter
!conda install -q -y google-colab -c conda-forge
!python -m ipykernel install --name "py38" --user
!pip install -U d2l
```

```python
import zipfile
with zipfile.ZipFile("file.zip","r") as zip_ref:
    zip_ref.extractall("targetdir")
```
### Node
change registry:
`npm config set registry https://registry.npm.taobao.org`
check registry:
`npm config get registry`

## Prompts
### Improve academic writing skills:
1. Please revise the text to incorporate more formal vocabulary and precise terminology appropriate for an academic audience. 
2. Transform the sentences to eliminate colloquial language and enhance the overall scholarly tone of the document.
3. Enhance the clarity and coherence of the text by implementing sophisticated sentence structures and advanced language usage.
### Introduction to a freshman
1. 介绍xx。它的作用是什么？历史背景是什么？为什么要引入它？它的典型使用场景是什么？有哪些功能类似的替代品？它们的区别是什么？
2. 我是一个程序员，希望从代码层面进行理解。写一段C代码，向我演示xx
3. 这几个概念的层次结构是怎样的？它们分别负责什么部分？它们的输入输出是什么？
### Anki
Summarize as English anki cards, output in html, wrap math in <anki-mathjax> tag
### Language

你是一个精通多国语言的专家。如果输入是一个句子或一段话，则提供其翻译，并解释其中我可能不了解的词汇、短语或表达。如果输入是一个单词或短语，则介绍其词源、提供例句并列出相关词汇。如果是单词，标注其IPA音标。用中文回答。

If the following is Chinese, please translate the following sentences into formal, academic English. If the following is English, then polish it to make it more formal and academic.

我正在学习英语，但有时我的造句比较生硬，我希望你指出问题并给出改进
### Paper
写出证明的核心思想，不要陷入细节，但也不要只是粗略描述，写清符号定义。我希望我能根据你的回答自己补全文章的细节以节约阅读时间。
### Math

你现在是我的数学一对一教练。请遵守以下规则：
1. 不要一开始给完整答案。
2. 先判断题型、关键结构和可能方法。
3. 每次只给一个提示，等我回应后再继续。
4. 如果我卡住，按“弱提示—中提示—强提示—关键步骤”的顺序帮助我。
5. 对每个关键步骤，解释“为什么会想到”，而不只是说明“这样做是对的”。
6. 如果我给出解法，请优先指出第一个错误或不严谨处。
7. 最后再给完整解答、方法总结和 2-3 道变式练习。

## RAID
See [[raid_tutorial|this post]].

## Docker

Proxy: [this post](https://www.cnblogs.com/Chary/p/18096678)
Mirror: https://status.anye.xyz/

## swaylock
```bash
# PAM configuration file for the swaylock screen locker. By default, it includes
# the 'login' configuration file (see /etc/pam.d/login)

auth       requisite    pam_nologin.so
auth       required   pam_shells.so
auth       required                    pam_faillock.so      preauth
-auth      [success=3 default=ignore]  pam_systemd_home.so
auth       [success=2 default=ignore]  pam_unix.so          try_first_pass nullok
# auth       [success=1 default=bad]     pam_fprintd.so
auth       [success=1 default=bad]     pam_u2f.so nouserok origin=pam://Inspiron5409 appid=pam://Inspiron5409 authfile=/home/yuan/.config/Yubico/u2f_keys
auth       [default=die]               pam_faillock.so      authfail
auth       optional                    pam_permit.so
auth       required                    pam_env.so
auth       required                    pam_faillock.so      authsucc

# auth include login
```
