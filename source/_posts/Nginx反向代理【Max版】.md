---
title: Nginx反向代理【Max版】
tags:
  - MacOS
  - Nginx
categories:
  - MacOS
  - Nginx
toc: true
abbrlink: 12862
date: 2021-11-01 19:22:17
---



### 1.安装（Macos可以使用brew来安装）

```shell l
brew install nginx
```

安装时间可能较长，稍微等待片刻。。。

<!--more-->

![image-20211012152330364](https://tva1.sinaimg.cn/large/008i3skNgy1gvck1xc414j61pe0su7ca02.jpg)

出现如上即表示安装成功

### 2.查看版本

```shell
nginx -v
```

![image-20211012153557982](https://tva1.sinaimg.cn/large/008i3skNgy1gvckeu763hj60gv01jmx302.jpg)

出现如上提示表示安装成功了。。。

### 3.启动ngin x

```shell
nginx
```

也可以使用下面的命令启动，但是配置文件nginx.conf修改后用这个命令执行可能并不生效，所以不建议使用：

### 4.查看nginx是否启动成功

在浏览器中访问http://localhost:8080/,出现如下页面表示启动成功:

![image-20211012154940986](https://tva1.sinaimg.cn/large/008i3skNgy1gvckt3s1cjj61l60aa0u102.jpg)

`注意`：端口号是在配置文件nginx.conf里面配置的，默认端口是8080,配置文件的位置是在`/usr/local/etc/nginx`

![image-20211012155330882](https://tva1.sinaimg.cn/large/008i3skNgy1gvckx376x7j60sy04p3z902.jpg)

### 5.关闭ngin x

```shell
nginx -s stop
```

### 6.重新加载nginx

```shell
nginx -s reload
```

### 7.可能遇到的问题

#### a.端口占用

> nginx: [emerg] bind() to 0.0.0.0:80 failed (48: Address already in use)

修改nginx.conf文件里的端口号即可

### 8.brew命令安装

安装 homebrew ，将以上命令粘贴至terminal，然后回车即可

```shell
 /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 9.常用的nginx命令

```shell
nginx -s reload 重新加载配置
nginx -s reopen 重启
nginx -s stop 停止
nginx -s quit 退出
nginx -V 查看版本，以及配置文件地址
nginx -v 查看版本
nginx -c filename 指定配置文件
nginx -h 帮助
```

