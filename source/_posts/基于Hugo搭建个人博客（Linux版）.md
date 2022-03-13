---
title: 基于Hugo搭建个人博客（Linux版）
tags:
  - Hugo
categories:
  - Hugo
toc: true
abbrlink: 8446
date: 2021-07-25 12:37:46
---

## 一、介绍

Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。

<!--more-->

## 二、安装Hugo

到 https://github.com/gohugoio/hugo/releases 查看与CPU对应的版本下载

复制如下命令安装

```shell
wget https://github.com/gohugoio/hugo/releases/download/v0.80.0/hugo_0.80.0_Linux-64bit.deb
```

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20210724211738928.png" alt="image-20210724211738928" style="zoom:50%;" />

 进行下载，下载完后安装：

```shell
sudo dpkg -i hugo_0.80.0_Linux-64bit.deb 
```

此时使用dpkg可能提示该命令不可用，我们手动安装

```shell
yum install dpkg
```

出现如下即表示安装成功

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo(linux)01.png" alt="image-20210724212506841" style="zoom:50%;" />

然后再重新执行，安装完毕之后，我们查看下版本号

````shell
hugo version
````

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo(linux)02.png" alt="image-20210724212614216" style="zoom:50%;" />

出现如上即表示安装成功。

## 三、使用Hugo生成博客

```shell
hugo new site hugo
```

后面的名称随便自己定义`hugo`为博客名称

## 四、下载设置主题

主题官网：https://themes.gohugo.io ，找到想要的主题，点击去，复制下载命令，下载到 `myblog` 目录下的 `themes` 目录下，

例如，在 `themes` 目录下命令：

```shell
git clone https://github.com/kakawait/hugo-tranquilpeak-theme.git
```

然后进入到hugox项目工程主目录，启动项目

```shell
hugo server -t hugo-tranquilpeak-theme --buildDrafts
```

![image-20210725010544093](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo%20(linux).png)

出现如上页面表示安装成功，此时我们可以通过域名:1313进行访问。
