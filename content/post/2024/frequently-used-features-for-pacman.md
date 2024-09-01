---
title: 记几个自己常用的Pacman命令
updated: 2024-09-01 00:00:00
date: 2024-09-01 00:00:00
tags: [Linux]
categories: [技术]
---

- 删除无用依赖（类似 `apt autoremove`）

`pacman -Rsn $(pacman -Qdtq)`

- 清除缓存

`pacman -Sc`