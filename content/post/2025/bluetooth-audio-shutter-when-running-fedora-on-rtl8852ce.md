---
title: 解决 RTL8852CE 无线网卡下的 Fedora 蓝牙音频断触问题
date: 2025-10-19 00:00:00
tags: [Linux]
categories: 
- 技术
---
## 故事的开始

我最近选择了Fedora作为我的主力Linux系统，然而刚迁移过来就遇到了蓝牙耳机音频断触的问题。

不管使用何种编码器播放音频，蓝牙音频总是随机地断连。

我尝试过把新的`wireplumber`换回了传统的`pipewire-media-session`，但并没有解决这个问题。

## 事情有了转机

我开始尝试在Google加入无线网卡型号搜索相关信息，结果搜到了[一篇Reddit帖子](https://www.reddit.com/r/linuxquestions/comments/1kdeqv6/bluetooth_audio_dropping_in_and_out_fedora_42/)，里面提到了下面这个脚本。

- [GitHub - anfreire/rtw8852c-fedora-fix](https://github.com/anfreire/rtw8852c-fedora-fix)

这个脚本通过将旧版本固件symlink到新版本固件的位置，实现固件版本的“回退”以解决这个问题。

## 结语

我并没有在这件事中做任何事情，因此，如果这篇文章的内容对你有帮助的话，请不要忘记脚本原作者[André Freire Ferreira](https://github.com/anfreire)所做出的卓越贡献。