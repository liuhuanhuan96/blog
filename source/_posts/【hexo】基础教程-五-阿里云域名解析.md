---
title: 【hexo】基础教程-五-阿里云域名解析
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 14014
date: 2021-07-25 12:19:50
---

hexo 搭建博客的时候，通常我们需要部署到远程服务器中，如果自己没有服务器的话，我们会选择将搭建好的项目，上传到github中，然后用过用户名.github.io来进行访问，今天本文来介绍另外一种方式，通过绑定域名的方式来查看。

<!--more-->

#### 一、域名创建

首先我们需要拥有一个字的域名，可以到阿里云[域名](https://wanwang.aliyun.com/?spm=5176.10695662.1158081.1.12334234jIVGyD)去购买，现在的域名的价格相对来说比较便宜，com的会稍微贵点，top的相对来说会比较便宜点。阿里云的域名现在需要进行备案后才可以正常使用，需要至少3个月以上的阿里云服务器实例，这个方式现在来说还是比较坑的。

#### 二、域名解析

登录[阿里云控制台](https://homenew.console.aliyun.com/home/dashboard/ProductAndService)

![【hexo】阿里云域名解析01](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E9%98%BF%E9%87%8C%E4%BA%91%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90%E4%BA%9401.png)

![【hexo】阿里云域名解析02](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E9%98%BF%E9%87%8C%E4%BA%91%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90%E4%BA%9402.png)

![【hexo】阿里云域名解析03](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E9%98%BF%E9%87%8C%E4%BA%91%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90%E4%BA%9403.png)

![【hexo】阿里云域名解析04](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E9%98%BF%E9%87%8C%E4%BA%91%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90%E4%BA%9404.png)

按照如下方式，即可完成域名的解析，此过程可能存在10分钟左右的延迟。

#### 三、hexo文件新增

在配置完域名解析之后，仍然无法访问我们的博客，此时，我们可以在hexo根目录下创建一个文件，名为CNAME，然后再文件中新增域名名称，方式如下：

![【hexo】阿里云域名解析05](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E9%98%BF%E9%87%8C%E4%BA%91%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90%E4%BA%9405.png)

在github中按照如下方式创建一个文件，在文件中填写好解析的域名地址，即阿里云中申请的域名地址。配置完，稍等片刻，即可通过解析后的域名访问自己的博客啦。

欢迎来到我的博客：[novoice.top](novoice.top)

