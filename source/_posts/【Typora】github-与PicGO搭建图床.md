---
title: 【Typora】github-与PicGO搭建图床
tags:
  - Typora
  - GitHub
categories:
  - GitHub
toc: true
abbrlink: 60878
date: 2021-07-25 13:05:35
swiper_index: 3
---



Markdown使用过程中最让人头疼的恐怕就是插入图片了，添加图片的方法可查看 [简书-Markdown添加图片的三种方式](https://www.jianshu.com/p/280c6a6f2594)。简单总结，常用插入图片方法主要分为插入本地图片、插入网络图片两种。

<!--more-->

### 一、PicGo下载

[链接地址：](https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.0-beta.4)

如果觉得下载慢的话，本文提供了百度云下载：

链接: https://pan.baidu.com/s/1r0s_0jNjBcJiw047WzLAmQ  密码: hhq7


### 二、新建github 仓库

​		![【Typora】github与picgo图床设置01](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Typora%E3%80%91github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE01.png)

![【Typora】github与picgo图床设置02](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Typora%E3%80%91github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE02.png)

### 三、github token生成

`生成一个token，让PicGo可以操作你的仓库`

* 方法1（直接访问tokens界面），https://github.com/settings/tokens ，点击`Generate new token`

![【Typora】github与picgo图床设置03](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE03.jpg)

![【Typora】github与picgo图床设置04](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE04.jpg)

勾选`repo`后，滑到页面最下端，单击 `Generate token` 绿色按钮，生成token。

![【Typora】github与picgo图床设置05](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE05.jpg)

**注意，生成的token只会显示一次，建议另存为文本文件妥善保存。如果忘记了，只能重新生成新的token，每次新生成的token与之前都不同。**

* 方法2 点击主页右上角的`Settings`

  ![【Typora】github与picgo图床设置06](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE06.jpg)

后续操作与步骤一差不多

### 四、PicGo配置

***图床配置***

![【Typora】github与picgo图床设置07](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE07.jpg)

* 设定仓库名：“GitHub用户名/仓库名”
* 设定分支名：“master”
* 设定Token："上一步在github中生成的token）"
* 指定存储路径：会按照填写的路径在GitHub仓库下建立文件夹，填写 “img/” 即可 （填不填都行）
* 设定自定义域名：“https://github.com/(用户名)/(仓库名)/master”（填不填都行）

### 五、自定义配置

![【Typora】github与picgo图床设置08](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E4%B8%8Epicgo%E5%9B%BE%E5%BA%8A%E8%AE%BE%E7%BD%AE08.jpg)

使用GitHub仓库作为图床，存在的问题是国内访问github的速度很慢，可以利用 [jsDelivr CDN](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.jsdelivr.com%2F) 来加速访问。jsDelivr 是一个免费开源的 CDN 解决方案，该平台是首个打通中国大陆与海外的免费CDN服务，拥有中国政府颁发的 ICP 许可证，无须担心中国防火墙问题而影响使用。使用jsDelivr加速访问，需要将自定义域名设置为`https://cdn.jsdelivr.net/gh/用户名/图床仓库名/`。

通过此方式可以成功访问。



