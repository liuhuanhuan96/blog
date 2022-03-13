---
title: SSH登录：WARNING REMOTE HOST IDENTIFICATION HAS CHANGED!
tags:
  - Linux
categories:
  - Linux
toc: true
abbrlink: 7478
date: 2022-02-25 19:33:27
---



在我们使用ssh链接服务器的时候。会出现如下的错误

<!--more-->

```shell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
SHA256:6zKiuPSPE90dB6PNCj1fICgA1DTrTxPFiVbl82+sS0E.
Please contact your system administrator.
Add correct host key in /c/Users/xuliugen/.ssh/known_hosts to get rid of this message.
Offending RSA key in /c/Users/xuliugen/.ssh/known_hosts:4
RSA host key for 119.19.19.19 has changed and you have requested strict checking.
Host key verification failed.
```

我们需要进行如下操作，来解决这种问题：

1.在客户端执行下述指令

```ssh
vim ~/.ssh/known_hosts
```

2.例如我的机子IP地址为：1.1.1.1  则把里面所有与IP相关的内容删掉即可.

然后再重新使用ssh链接即可

