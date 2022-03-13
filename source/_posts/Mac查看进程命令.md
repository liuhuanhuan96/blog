---
title: Mac查看进程命令
tags:
  - MacOS
categories:
  - MacOS
toc: true
abbrlink: 20294
date: 2021-11-01 19:29:55
---



#### 1.查看进程号

```shell
ps -ef | grep 进程名
```

<!--more-->

demo：

```shell
liuhuanhuan@bogon ~ % ps -ef | grep 3306
  501 99050 57804   0  9:14下午 ttys000    0:00.00 grep 3306
```

#### 2、查看端口被哪个进程监听

```shell
sudo lsof -i:8080
```

此时必须要输入`sudo`，不然无法正常显示

#### 3.查看进程监听的端口

```shell
sudo lsof -nP | grep LISTEN | grep 3306
```

输出

```she
mysqld      129                 _mysql   29u     IPv6 0x7262f1f44e03ce3d        0t0                 TCP *:33060 (LISTEN)
mysqld      129                 _mysql   31u     IPv6 0x7262f1f44e03dafd        0t0                 TCP *:3306 (LISTEN)
```

#### 4.查看进程

```she
sudo lsof -i tcp:port
如：sudo lsof -i tcp:8080
```

显示结果

```shell
liuhuanhuan@liuhuanhuandeMacBook-Pro bin % sudo lsof -i tcp:8080
COMMAND  PID        USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    3085 liuhuanhuan   54u  IPv6 0x7262f1f46d2a67dd      0t0  TCP *:http-alt (LISTEN)
```



#### 5.杀死进程的方式

```shell
sudo kill -9 PID
如：sudo kill -9 750
```

