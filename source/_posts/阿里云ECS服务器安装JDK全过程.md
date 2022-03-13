---
title: 阿里云ECS服务器安装JDK全过程
tags:
  - 阿里云
  - JDK
categories:
  - JDK
toc: true
abbrlink: 14382
date: 2021-07-25 14:08:52
---

### 1.工具选择

选择合适的连接工具，如xftp、putty、Terminus等

<!--more-->

### 2、JDK下载与安装

#### 2.1 JDK下载

[oracle官网](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)

官网下载相应服务器的JDK版本

可以通过第三方ftp工具，也可以通过命令行`rz`上传文件

一般系统默认，不带有rz命令，安装rz/sz

```shell
 yum -y install lrzsz
```

#### 2.2 安装

**解压下载的压缩包：**

```shell
tar -zxvf jdk-8u291-linux-x64.tar.gz 
```

**切换到指定文件**

```shell
cd /usr
mkdir software
cd software
mv ~/jdk1.8.0_291 /usr/software/jdk1.8.0_291
```

**配置环境变量**

```shell
vi /etc/profile
```

```shell
#set java env
export JAVA_HOME=/usr/software/jdk1.8.0_291
export JRE_HOME=${JAVA_HOME}/jre    
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib    
export PATH=${JAVA_HOME}/bin:$PATH 
```

**执行命令使修改立即生效：**

```shell
source /etc/profile
```

测试安装连接

```shell
java -version
```

出现如下即表示安装成功

![image-20210523091638120](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85JDK1.png)



