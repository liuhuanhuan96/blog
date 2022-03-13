---
title: 【github】提升github访问速度
tags:
  - GitHub
  - Git
categories:
  - GitHub
toc: true
abbrlink: 19598
date: 2021-07-25 11:57:17
---

此方式适用于各种操作系统，主要方式为修改host文件，添加配置的方式

#### 1.查找域名对应的ip地址，并修改hosts文件

<!--more-->

windows/Macos/linux通用的方式：

~~~shell
nslookup github.com
nslookup github.global.ssl.fastly.net
~~~



`注：尝试过fastly.Net的方式，加速的效果不是很明显，但是改为fastly.net的方式加速效果的话有着显著的提高。`

上述输出的结果为

![【github】提升github访问速度0](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A601.png)

![【github】提升github访问速度02](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A604.png)

上述图片均为windows10环境下的结果。具体参数按照自己的电脑实际情况来看。

`特别声明：网上很多博主的地址，大多数都是自己电脑的查询地址，不建议使用，最好的使用方式是查看自己本机的地址，此地址会变化，所以尽量自己动手查看下，以防万一。`

将以下内容添加到windows(==C:\Windows\System32\drivers\etc\hosts==) macos(==/etc/hosts==)中

~~~shell
13.250.177.223 github.com
157.240.8.41 github.global.ssl.fastly.net
~~~

> 新增到文件的末尾（注意windows10用户会存在文件无法修改的权限，此修改文件的方式，见下期博客）



#### 2.刷新dns缓存

macos:

~~~shell
sudo dscacheutil -flushcache
~~~

windows：

~~~shell
ipconfig /flushdns
~~~

#### 3.使用chrome插件

谷歌商店搜索github加速即可对github提升一些略微显著的效果。

