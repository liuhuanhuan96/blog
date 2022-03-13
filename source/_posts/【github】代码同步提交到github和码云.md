---
title: 【github】代码同步提交到github和码云
tags:
  - GitHub
  - Git
categories:
  - GitHub
toc: true
abbrlink: 48362
date: 2021-07-25 11:54:27
---



现在很多朋友在git clone  github代码的时候会发现速度慢的实在是难以吐槽，于是我们就像个方法，将我们的代码同步码云上，我们再去下载速度，是不是快了很多呢。>。<！！!

但是随着我们提交代码的时候，我们就面临着，代码提交到哪里呢？码云还是github呢？本文将进行详细的介绍。

<!--more-->

## 1. 远程仓库的使用

### 1.1 查看远程仓库

查看当前项目的远程仓库

~~~shell
git remote
~~~

输出

~~~shell
origin
~~~

这个`origin`就是一个指向远程仓库的名称，是你在`clone`时 `git` 为你默认创建的。

可以通过命令查看`origin`指向的远程仓库地址：

~~~shell
git remote -v
~~~

输出结果：

~~~shell
origin  https://github.com/liuhuanhuan963019/demo.git (fetch)
origin  https://github.com/liuhuanhuan963019/demo.git (push)
~~~

该命令会显示读写远程仓库的名称和地址，我这里指向的是Github。

### 1.2 远程仓库重命名

输入命令：
`git remote rename <old_remote> <new_remote>`

~~~shell 
git remote rename origin github
~~~

输入命令查看：

~~~shell
github  https://github.com/liuhuanhuan963019/demo.git (fetch)
github  https://github.com/liuhuanhuan963019/demo.git (push)
~~~

完美！！！！

### 1.3 添加另一个远程仓库

下面我们再添加Gitee上的远程仓库，首先在Gitee上创建一个空的仓库，名称与Github上相同。

然后在【克隆/下载】处复制地址。

输出添加远程仓库命令：

`git remote add <remote> <url>`

~~~shell
git remote add gitee https://gitee.com/liuhuanhuan963019/demo.git 
~~~

再来验证下是否成功，输出结果：

~~~shell
github  https://github.com/liuhuanhuan963019/demo.git (fetch)
github  https://github.com/liuhuanhuan963019/demo.git (push)
gitee  https://gitee.com/liuhuanhuan963019/demo.git (fetch)
gitee  https://gitee.com/liuhuanhuan963019/demo.git (push)
~~~

成功！！！

### 1.4 多个远程仓库的推送/拉取

多个远程仓库的时候，必须加上远程仓库的名称，以识别是哪个远程仓库，命令如下：

`git push <remote> <branch>`、`git pull <remote> <branch>`：

~~~shell
git push github master
git pull github master

git push gitee master
git pull gitee master
~~~

如果不想每次操作都带着分支，需要将本地分支与远程分支进行关联：

`git branch --set-upstream-to=<remote>/<remote_branch> <local_branch>`

~~~shell
git branch --set-upstream-to=gitee/main main
~~~

关联后就可以不指定分支了

~~~shell
git push github
git pull github

git push gitee
git pull gitee
~~~

### 1.5 移除一个远程仓库

如果想要移除一个远程仓库，可以使用下面命令：
`git remote remove <remote>`或`git remote rm <remote>`

~~~shell
git remote remove gitee
~~~

执行移除远程仓库后，该仓库在本地的所有分支与配置信息也会一并删除。

## 2. 常见错误及解决方案

### 2.1 提示未指定分支

> You asked to pull from the remote 'gitee', but did not specify
> a branch. Because this is not the default configured remote
> for your current branch, you must specify a branch on the command line.

表示本地分支与远程分支未做关联，进行关联一下即可，执行下面命令：
`git branch --set-upstream-to=<remote>/<remote_branch> <your_branch>`

~~~shell
git branch --set-upstream-to=gitee/main main
~~~

### 2.2 没有存储库的权限

当执行推送操作时，提示下面信息：

> remote: You do not have permission push to this repository
> fatal: unable to access 'https://gitee.com/gozhuyinglong/blog-demos.git/': The requested URL returned error: 403

表示没有远程仓库的权限，应该首先查看远程仓库是否公开，再检查本地账号和密码是否正确。

### 2.3 远程仓库未公开

登录Gitee，检查该代码库是否公司。若未公开，则设置为公开。

### 2.4 生成SSH Key，并添加到Github

输入下面命令来生成SSH Key，双引号内填写你的登录邮箱地址

~~~shell
ssh-keygen -t rsa -C "xxxxx@xxxxx.com" 
~~~

如果弹出下面提示，直接回车即可。（若已存在，会提示是否替换，输入Y再回车）

接下来的操作，参考作者的[本地配置ssh](https://blog.csdn.net/qq_38140292/article/details/110730314)
