---
title: "Elements Desktop 下的多账户管理"
description: 
date: 2025-01-11T00:00:00+08:00
tags: [日常]    
categories: [技术] 
image: 
math: 
license: 
hidden: false
comments: true
draft: falses
---
各位新年快乐！这大概本站是2024年的第一篇文章。

最近在电脑上安装了Elements Desktop作为Matrix客户端。但到了需要多账户切换的时候可就伤了脑筋，我惊奇地发现，这个客户端居然没有多账户管理的功能！

于是我就在网上简单搜索了一下解决方案，然后简单地进行了一些改进。

~~然后决定顺便水一篇文章发出来了~~

## 系统环境

为了避免对内容理解造成影响，先介绍一下我的系统环境。

```
操作系统：Manjaro Linux x86_64
Element 版本：1.11.87
安装方式：Flatpak
```

## 解决方案：添加启动参数

### 思路

根据[这篇文档](https://ubuntu.com/community/communications/matrix/multiple-accounts)，我们可以通过添加`--profile`运行参数的方式，使客户端在一个不同的Profile中启动。

例如下面这条命令

`element-desktop --profile 0721`

会使客户端在一个名为`0721`的profile中启动。

对应profile的数据文件会存储在 `/home/[username]/.config/Element-0721`，而默认的数据文件目录则是 `/home/[username]/.config/Element`。

### 优化

经常使用命令行启动客户端并不是一件很优雅的事情，让我们对这个过程做一些小小的优化。

#### 创建桌面项（Desktop Entry）

> 吐槽：我也不知道这东西的中文名叫什么，然后搜了一下，[archlinuxcn](https://wiki.archlinuxcn.org/wiki/%E6%A1%8C%E9%9D%A2%E9%A1%B9)是这样翻译的。
>
> ~~其实就是普通的快捷方式吧~~

创建桌面项可以使客户端的启动流程更加快捷和优雅。

让我们看看怎么做吧

- 复制原有的桌面项

我的桌面项存储在`/usr/share/applications`下面，如果你的不在这里，可以自行查找一下桌面项的位置。

复制出来，放到个人的文件夹下面`~/.local/share/applications`

大概是下面这样：

``` desktop
[Desktop Entry]
Name=Element
Comment=Feature-rich client for Matrix
Exec=/usr/bin/element-desktop %u
Terminal=false
Type=Application
Icon=io.element.Element
StartupWMClass=Element
Categories=Network;InstantMessaging;Chat;IRCClient
MimeType=x-scheme-handler/element;
```

- 修改桌面项

这里`Exec`这一项是表示点击桌面项时运行的命令，而`Name`是桌面项显示出来的名字。

这里我们就改这两个字段。

首先，将`Exec`字段加上`--profile [profilename]`的启动参数，这里我们用刚才的`0721`举例

``` desktop
Exec=/usr/bin/element-desktop --profile 0721 %u
```

名字我们也可以起一个相关一些的，比如`Elements (0721)`

``` desktop
Name=Elements (0721)
```

最后我们得到的是一个新的“桌面项”，像下面这样

``` desktop
[Desktop Entry]
Name=Element (0721)
Comment=Feature-rich client for Matrix
Exec=/usr/bin/element-desktop --profile 0721 %u
Terminal=false
Type=Application
Icon=io.element.Element
StartupWMClass=Element
Categories=Network;InstantMessaging;Chat;IRCClient
MimeType=x-scheme-handler/element;
```

这样，你就可以通过在桌面上点击来轻松多开Elements了。❤️

#### 补充

不排除可能会有~~矩阵海王~~在各种站点开设~~114514~~个账号的可能性，在这里补充一下。

在你的`~/.local/share/applications`目录中，不管下面有几级目录，都是可以正确检测到“桌面项”文件，并且显示在桌面环境的启动器中的。

所以，你可以在下面再创建一个二级目录来存放你的“桌面项”们。

## 参考资料

[Using multiple Matrix accounts - Ubuntu Community](https://ubuntu.com/community/communications/matrix/multiple-accounts)