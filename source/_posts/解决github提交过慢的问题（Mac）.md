---
title: 解决github提交过慢的问题（Mac）
tags:
  - MacOS
  - GitHub
categories:
  - GitHub
toc: false
abbrlink: 32466
date: 2021-07-25 13:24:33
---

终端下输入

```shell
ping github.com
```

<!--more-->

得到如下内容

```shell
PING github.com (13.229.188.59): 56 data bytes
64 bytes from 13.229.188.59: icmp_seq=0 ttl=39 time=195.235 ms
64 bytes from 13.229.188.59: icmp_seq=1 ttl=39 time=199.842 ms
64 bytes from 13.229.188.59: icmp_seq=2 ttl=39 time=201.577 ms
```

再输入

```shell
ping github.global.ssl.fastly.net
```

得到如下内容

```shell
PING github.global.ssl.fastly.net (108.160.169.54): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
```

进入我们的host文件下

```shell
vim /etc/hosts
```

加入如下两行代码：

```shell
13.229.188.59 github.com
108.160.169.54 github.global.ssl.fastly.net
```

然后刷新DNS缓存

```shell
sudo dscacheutil -flushcache
```

然后发现速度会快很多
