---
title: 【Anaconda】conda创建虚拟环境不报错，但是虚拟环境无法生成的解决办法
tags:
  - Anaconda
  - Python
categories:
  - Python
toc: false
abbrlink: 49113
date: 2021-07-25 11:52:47
---

python新建虚拟环境，有两种方式

```python
conda create -n DeepLearning python=3.8
```

或者通过Anaconda的方式新建（可能打开Anaconda的过程很漫长。。。。）

<!--more-->

![image-20210308212646461](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Anaconda%E3%80%91conda%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83%E4%B8%8D%E6%8A%A5%E9%94%99%EF%BC%8C%E4%BD%86%E6%98%AF%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83%E6%97%A0%E6%B3%95%E7%94%9F%E6%88%90%E7%9A%84%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%9501.png)

按照上图的方式，即可安装，但是不如命令来的快一些



现在出现了一写问题！！！！

我在新建虚拟环境的时候：

```python
conda create -n pytorch python=3.7
```

出现了如下情况：

![img](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Anaconda%E3%80%91conda%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83%E4%B8%8D%E6%8A%A5%E9%94%99%EF%BC%8C%E4%BD%86%E6%98%AF%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83%E6%97%A0%E6%B3%95%E7%94%9F%E6%88%90%E7%9A%84%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%9502.png)

在新建的环境中，使用pip命令，出现错误，提示python什么什么文件丢失。意思就是找不到python执行程序。我以为是我创建错了，我删掉，重新建立，最后还是出现这个问题，最后发现是多余的环境，导致系统环境乱掉了。

清除之前未完成的conda安装的包就可以正常创建环境了。

```python
conda clean --all
```

此过程需要等待一段时间

![image-20210308213735100](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Anaconda%E3%80%91conda%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83%E4%B8%8D%E6%8A%A5%E9%94%99%EF%BC%8C%E4%BD%86%E6%98%AF%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83%E6%97%A0%E6%B3%95%E7%94%9F%E6%88%90%E7%9A%84%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%9503.png)

然后就可以正常的创建虚拟环境了

ok!!!!!!

