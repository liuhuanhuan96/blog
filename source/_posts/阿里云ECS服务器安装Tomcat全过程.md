---
title: 阿里云ECS服务器安装Tomcat全过程
tags:
  - 阿里云
  - Tomcat
categories:
  - Tomcat
toc: false
abbrlink: 23233
date: 2021-07-25 14:12:51
---

一、安装tomcat之前需要先安装JDK，具体步骤参考：https://blog.csdn.net/qq_38140292/article/details/117186436?spm=1001.2014.3001.5501

<!--more-->

二、下载Tomcat

[点击下载](http://tomcat.apache.org/download-90.cgi)，下载Tomcat8

![image-20210523095000999](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91ECS%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Tomcat1.png)

三、上传Linux

```shell
rz
```

```shell
//解压即可
tar -xzvf  apache-tomcat-8.5.66.M9.tar.gz
```

四、配置环境

```shell
export CATALINA_HOME=/usr/local/tomcat                   
export PATH=$PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin
```

五、启动验证

![image-20210523095340856](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85tomcat2.png)

出现如上提示表示安装成功

六、阿里云安全组配置

![image-20210523095433501](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85tomcat3.png)



