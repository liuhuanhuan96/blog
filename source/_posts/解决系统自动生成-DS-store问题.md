---
title: 解决系统自动生成.DS_store问题
tags:
  - MacOS
categories:
  - MacOS
toc: false
abbrlink: 1897
date: 2021-07-25 13:25:36
---



**.DS_Store (Desktop Services Store)**，是Apple公司的操作系统创建的一个隐藏文件，里面保存着自定义目录的图标和背景图片等元信息，听起来就好像Windows上的desktop.ini。

<!--more-->

### 问题：

一般出现如下情况时，在我们的u盘中会出现大量的.DS_Store文件

1.U盘传输文件夹到windows下，出现一堆.DS_Store

2.无论使用mac的手动压缩，zip tar等命令压缩方式，打包的程序包，发布到linux出现一堆.DS_Store这种垃圾文件，虽然对操作毫无影响，但是看着很恶心，尤其是对于程序员来说，无法忍受。更不要说系统上线时候了。





### 解决方案：

```shell
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE
```

重启即可生效





重新恢复生成

```shell
defaults delete com.apple.desktopservices DSDontWriteNetworkStores
```







