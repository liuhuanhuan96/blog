---
title: Windows10本地共享文件配置（实测有效）
tags:
  - Windows10
categories:
  - Windows10
toc: false
abbrlink: 50561
date: 2021-11-22 15:56:26
---



1.选择需要共享的文件夹，然后右击查看`属性`,在属性中找到共享

<!--more-->



<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image0.png" alt="image-20211121223330990" style="zoom:80%;" />

2.选择，共享，然后选择对应配置，如下图：

<img src="C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20211121223510938.png" alt="image-20211121223510938" style="zoom: 80%;" />

![image-20211121223603320](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211121223603320.png)

![image-20211121223731082](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211121223731082.png)

出现如下页面即可表示设置成功

![image-20211121223800898](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211121223800898.png)

然后我们按住`windows+r`  输入`cmd`，输入`ipconfig` ，查看本地的ip地址，然后将我们的ip给同在局域网下的用户，用户通过`\\`   +` ip地址即可访问本地共享文件夹`

![image-20211121224020159](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211121224020159.png)

最后查看实现效果：我们通过远程一台新的服务器来进行访问

![image-20211122155047868](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122155047868.png)
