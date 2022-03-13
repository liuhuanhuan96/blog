---
title: 阿里云ECS服务器安装Maven
tags:
  - 阿里云
  - Maven
categories:
  - Maven
toc: false
abbrlink: 52595
date: 2021-07-25 14:11:37
---

**一. 下载压缩包:**

官网地址: http://maven.apache.org/download.cgi

<!--more-->

![image-20210523101140539](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91ECS%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85maven1.png)

**二、上传文件**

```shell
rz
```

**三. 解压文件**

```shell
tar -zxvf apache-maven-3.8.1-bin.tar.gz
```

**四. 配置环境变量**

```shell
vi /etc/profile
export MAVEN_HOME=/usr/local/apache-maven-3.8.1
export PATH=$MAVEN_HOME/bin:$PATH 
```

![image-20210523101325611](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Maven2.png)

出现如上提示，即可表示安装成功

