---
title: Linux 查看端口占用情况
tags:
  - Linux
categories:
  - Linux
toc: true
abbrlink: 236
date: 2021-07-25 14:17:58
---



Linux 查看端口占用情况一般可以使用 **lsof** 和 **netstat** 命令。

<!--more-->

## lsof

lsof(list open files)是一个列出当前系统打开文件的工具。

lsof 查看端口占用方式：

```shell
lsof -i:端口号
```

`案例`：

查看服务器 8080 端口的占用情况：

```shell
lsof -i:8080
```

![image-20210719232602938](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/Linux%E6%9F%A5%E7%9C%8B%E7%AB%AF%E5%8F%A3%E5%8F%B7%E5%8D%A0%E7%94%A8%E6%83%85%E5%86%B501.png)

lsof -i 需要 root 用户的权限来执行，如下图：

![image-20210719232654644](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/Linux%E6%9F%A5%E7%9C%8B%E7%AB%AF%E5%8F%A3%E5%8D%A0%E7%94%A8%E6%83%85%E5%86%B502.png)

具体参数信息如下：

- COMMAND:进程的名称   PID:进程标识符

- USER:进程所有者

- FD:文件描述符，应用程序通过文件描述符识别该文件。如cwd等

- TYPE:文件类型

- DEVICE:指定磁盘的名称

- SIZE:文件的大小

- NODE:索引节点（文件在磁盘上的标识）

- NAME:打开文件的确切名称

  更多 lsof 的命令如下：

  ```shell
  lsof -i:8080：查看8080端口占用
  lsof abc.txt：显示开启文件abc.txt的进程
  lsof -c abc：显示abc进程现在打开的文件
  lsof -c -p 1234：列出进程号为1234的进程所打开的文件
  lsof -g gid：显示归属gid的进程情况
  lsof +d /usr/local/：显示目录下被进程开启的文件
  lsof +D /usr/local/：同上，但是会搜索目录下的目录，时间较长
  lsof -d 4：显示使用fd为4的进程
  lsof -i -U：显示所有打开的端口和UNIX domain文件
  ```

## netstat

**netstat -tunlp** 用于显示 tcp，udp 的端口和进程等相关情况。

netstat查看端口号占用方式：

```shell
netstat -tunlp | gerp 8080
```

![image-20210719233320065](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/Linux%E6%9F%A5%E7%9C%8B%E7%AB%AF%E5%8F%A3%E5%8F%B7%E5%8D%A0%E7%94%A8%E6%83%85%E5%86%B503.png)

- -t （tcp）仅显示tcp相关选项
- -u  (udp) 仅显示udp相关选项
- -n  拒绝显示别名，能显示数字的全部转化为数字
- -l   仅列出在Listen的服务状态
- -p  显示建立相关链接的程序名

`案例`:

查看 8000 端口的情况，使用以下命令：

```shell
netstat -tunlp | gerp 8080
```

![image-20210719233320065](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/Linux%E6%9F%A5%E7%9C%8B%E7%AB%AF%E5%8F%A3%E5%8F%B7%E5%8D%A0%E7%94%A8%E6%83%85%E5%86%B503.png)

更多命令：

```shell
netstat -ntlp   //查看当前所有tcp端口
netstat -ntulp | grep 80   //查看所有80端口使用情况
netstat -ntulp | grep 3306   //查看所有3306端口使用情况
```

## kill

在查到端口占用的进程后，如果你要杀掉对应的进程可以使用 kill 命令：

```shell
kill -9 PID
```

案例

```shell
kill -9 31194
```

