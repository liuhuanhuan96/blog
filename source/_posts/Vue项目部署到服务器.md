---
title: Vue项目部署到服务器
tags:
  - Vue
  - Nginx
categories:
  - Vue
toc: true
abbrlink: 4434
date: 2021-07-25 12:33:04
---

### 前言

vue项目的创建请自行百度，vue部署到服务器一般需要一些容器来安装，本文采用Nginx的方式

Nginx的具体安装方式参考：[(35条消息) 阿里云ECS服务器安装Nginx_最爱吃大米的博客-CSDN博客](https://blog.csdn.net/qq_38140292/article/details/118915952?spm=1001.2014.3001.5501)

<!--more-->



### 1.vue项目打包

```shell
npm run build
```

具体方式参照自己的package.json文件方式

![image-20210719222918376](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/vue%E9%A1%B9%E7%9B%AE%E9%83%A8%E7%BD%B2%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8.png)

等待片刻。。。。。。。

打包完成，此时会在你的项目根目录下生成一个dist文件

![image-20210719223305051](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/vue%E9%83%A8%E7%BD%B2%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A802.png)

### 2.上传文件到服务器

使用 `xftp工具` 或者 `rz`命令进行上传

### 3.启动项目

由于项目是基于nginx部署，此时vue项目访问相关配置需要与Nginx方式相同。

重新启动Nginx,即可访问`xxxxx/index`

