---
title: SpringBoot部署到阿里云服务器
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: false
abbrlink: 10691
date: 2021-07-25 14:10:18
---

**一、本地打包**

打开项目根目录

```shell
mvn clean
mvn install
```

<!--more-->

会在项目根目录下有个target文件夹中生成项目jar文件

**二、上传jar包到服务器**

```shell
rz
```

**三、启动项目**

```shell
java -jar xxxx.jar
```

但是上面的方式在我们关闭终端窗口的时候，服务即会被关闭，通过如下方式来进行服务挂载

```shell
nohup java -jar oasys.jar &
```

