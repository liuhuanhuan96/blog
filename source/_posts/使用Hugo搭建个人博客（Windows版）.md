---
title: 使用Hugo搭建个人博客（Windows版）
tags:
  - Hugo
categories:
  - Hugo
toc: true
abbrlink: 17604
date: 2021-07-25 12:39:13
---

## 一、下载hugo

[Hugo官网](https://blog.csdn.net/codingriver/article/details/107718847)
[github](https://github.com/gohugoio/hugo)
下载：[下载Hugo](https://github.com/gohugoio/hugo/releases)

<!--more-->

这里下载的是`hugo_0.85.0_Windows-64bit.zip`
解压后就一个exe文件
放在文件夹`D:\hugo\bin`中，然后添加到环境变量中
执行 `hugo -version`

![image-20210725094313962](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A201.png)

## 二、创建项目

进入指定目录之后，执行如下命令：

```shell
hugo new site myblog
```

![image-20210725094639161](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A202.png)

## 三、添加主题

[官网地址：](https://www.gohugo.org/theme/)

选择自己喜欢的背景主题进行git clone 下载

![image-20210725095146858](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA03.png)

在当前项目目录内打开`config.toml`配置文件，在最后添加一行`theme = "uno"`  名称为刚刚我们拷贝的项目名称

## 四、运行项目

在项目根目录执行

```shell
hugo server -D
```

运行结果如下，表示我们项目运行成功。

![image-20210725095819041](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A206.png)

浏览器输入`localhost:1313` ,即可看到如下内容

![image-20210725095746514](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hugo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A205.png)

## 五、使用教程

 使用教程https://www.flysnow.org/2018/07/29/from-hexo-to-hugo.html
		使用教程 https://blog.csdn.net/weixin_30952535/article/details/97155453
		主題説明 https://github.com/JokerQyou/maupassant-hugo/blob/master/README_zh.md
		主題説明 https://github.com/flysnow-org/maupassant-hugo
		參考文章 https://blog.csdn.net/codingriver/article/details/107718847





