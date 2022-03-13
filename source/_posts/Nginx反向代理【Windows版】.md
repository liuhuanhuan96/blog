---
title: Nginx反向代理【Windows版】
tags:
  - Windows
  - Nginx
categories:
  - Windows
  - Nginx
toc: true
abbrlink: 35769
date: 2021-11-01 19:24:06
---



### 1.简介

Nginx (engine x) 是一个高性能的HTTP和反向代理web服务器，同时也提供了IMAP/POP3/SMTP服务。Nginx是由伊戈尔·赛索耶夫为俄罗斯访问量第二的Rambler.ru站点（俄文：Рамблер）开发的，第一个公开版本0.1.0发布于2004年10月4日。

<!--more-->

### 2.下载

下载地址：http://nginx.org/en/download.html

![image-20211012162538669](https://tva1.sinaimg.cn/large/008i3skNgy1gvcluiw814j61dl0kon2002.jpg)

这个版本可以自己任意选择

### 3.解压安装

![image-20211012162954350](https://tva1.sinaimg.cn/large/008i3skNgy1gvclyyikilj60q50a63z402.jpg)

### 4.启动服务

```shell
cd nginx-1.20.1
start nginx
nginx -t
```

![image-20211012163540303](https://tva1.sinaimg.cn/large/008i3skNgy1gvcm4yhm6qj61qs0dw40t02.jpg)

出现如上命令表示安装成功。。。。

![image-20211012163639283](https://tva1.sinaimg.cn/large/008i3skNgy1gvcm5zbys6j60o8082aau02.jpg)

```shell
tasklist /fi "imagename eq nginx.exe"
```

如上命令查看所占进程

### 5.修改端口号

如果端口被占用了，我们可以选择我们未被占用的端口

![image-20211012163839735](https://tva1.sinaimg.cn/large/008i3skNgy1gvcm82hcahj60ry0l7wgy02.jpg)

### 6.常见的nginx使用命令

```shell
nginx -s stop	  终止进程
nginx -s quit	 推出
nginx -s reload	重新加载
nginx -s reopen	重现打开
```

