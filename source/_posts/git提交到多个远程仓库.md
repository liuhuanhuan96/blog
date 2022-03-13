---
title: git提交到多个远程仓库
tags:
  - GitHub
categories:
  - GitHub
toc: false
abbrlink: 42168
date: 2021-07-25 13:09:22
---



使用gitee与github的仓库地址来进行简单的演示

* `gitee`：git@gitee.com:liuhuanhuan963019/xxxx.git
* `github`： git@github.com:liuhuanhuan963019/xxxx.git

<!--more-->

查看本地仓库地址

```shell
$ git remote -v
origin  https://github.com/Esri/java-maven-starter-project.git (fetch)
origin  https://github.com/Esri/java-maven-starter-project.git (push)
```

新增gitee仓库地址

```shell
 git remote set-url --add origin https://gitee.com/liuhuanhuan963019/java-maven-starter-project.git
```

**再通过`git remote -v`查看远程版本库信息**

```shell
$ git remote -v
origin  https://github.com/Esri/java-maven-starter-project.git (fetch)
origin  https://github.com/Esri/java-maven-starter-project.git (push)
origin  https://gitee.com/liuhuanhuan963019/java-maven-starter-project.git (push)
```

```shell
git add .
git commit -m "first commit"
git push origin --all
```

