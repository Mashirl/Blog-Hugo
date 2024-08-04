---
title: "使用ASDF安装并管理多个版本的Python"
description: 
date: 2024-08-04T20:00:00+08:00
categories: [技术]
tags: [Linux]
image: /images/asdf-python.png
math: 
license: 
hidden: false
comments: true
draft: false
---
最近在运行一些Python应用的时候，发现因为Python版本太新而无法正常运行。在搜索了一通之后，发现了[ASDF](https://asdf-vm.com)这个应用，可以满足我的需求。

这里我只写我自己的操作步骤，更多的内容请查阅官方文档。

## 操作步骤

### 安装 ASDF

- 先从AUR安装ASDF (以yay为例)

参考：[官方文档](https://asdf-vm.com/guide/getting-started.html#_2-download-asdf)

`yay -S asdf-vm`

- 安装后，按照官方文档的指导修改配置文件

参考：[官方文档](https://asdf-vm.com/guide/getting-started.html#_3-install-asdf)

```

. /opt/asdf-vm/asdf.sh

```

### 安装特定版本的 Python

- 添加Python到插件列表

`asdf plugin-add python`

- 列出Python的所有版本

`asdf list-all python`

- 安装你所需要的版本

`asdf install python 3.x.y`