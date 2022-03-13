---
title: win10 “你不能访问此共享文件夹，因为你组织的安全策略阻止未经身份验证的来宾访问。解决方案（实测有效）
tags:
  - Windows10
categories:
  - Windows10
toc: false
abbrlink: 42907
date: 2021-11-22 16:12:18
---



当别人建立好了共享文件夹之后，我们想要在我们的局域网内访问相关的文件，此时，我们出现如下提示：

<!--more-->

![image-20211122160311461](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122160311461.png)

此时我们需要修改网络配置：

如下步骤：

* window+ r 输入`gpedit.msc`

![image-20211122160506858](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122160506858.png)

* 依次打开**管理模板**->**网络**->**Lanman工作站**->**启动不安全的来宾登录**

<img src="C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20211122160731697.png" alt="image-20211122160731697" style="zoom:50%;" />

* 此时我们看到状态是未配置，我们双击，然后选择已启用

![image-20211122160835036](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122160835036.png)

![image-20211122160859975](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122160859975.png)

* 我们再重新打开，发现可以成功打开了
* ![image-20211122160945227](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122160945227.png)

