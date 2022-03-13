---
title: 阿里云ECS服务器安装Mysql全过程
tags:
  - 阿里云
  - MySQL
categories:
  - MySQL
toc: true
abbrlink: 50115
date: 2021-07-25 14:15:03
sticky: 1
---

## 一、查看服务器状态

#### 1.确保服务器系统最新状态

<!--more-->

```shell
yum -y update
```

出现如下即更新成功

```shell
Replaced:
  grub2.x86_64 1:2.02-0.86.3.al7.alnx               grub2-tools.x86_64 1:2.02-0.86.3.al7.alnx              

Complete!
```

#### 	2.重启服务器

```shell
reboot
```

#### 	3.检查mysql是否已经安装

```shell
rpm -qa | grep mysql
```

如果已经安装的话，那就还看啥呢

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Mysql%E5%85%A8%E8%BF%87%E7%A8%8B.jpg" alt="img" style="zoom:50%;" />

没安装的小伙伴可以继续下面的文章哦

#### 4.下载MySql安装包

```shell
rpm -ivh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
或者
rpm -ivh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
```

#### 5.安装mysql

```shell
yum install -y mysql-server
或者
yum install mysql-community-server
```

如果显示以下内容说明安装成功
	![image-20210522224111980](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Myql.png)



#### 6.设置开机启动mysql

```shell
 systemctl enable mysqld.service
```

#### 7.检查是否已经安装了开机自动启动

```shell
systemctl list-unit-files | grep mysqld
```

如果显示以下内容说明已经完成自动启动安装

![image-20210522224226928](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Mysql2.png)

#### 8.设置开启服务

```shell
systemctl start mysqld.service
```

#### 9.查看MySql默认密码

查看默认密码后，方便我们修改为自己想要的密码

```shell
grep 'temporary password' /var/log/mysqld.log   
```

#### 10. 登陆MySql，输入用户名和密码

密码为上一步看到的默认密码

```shell
mysql -uroot -p       
```

#### 11.修改当前用户密码

```shell
SET PASSWORD = PASSWORD('xxxxxxxxx');  
```

注：直接复制粘贴上边的命令，会出现错误，错误如下：

![image-20210522225358120](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Mysql3.png)

解决方式如下：

原因：mysql为了安全，有自己的策略要求，如果我们想将其设置为我们常用的root或者123456这样的密码，需要修改策略要求，具体命令如下：

通过设置密码强度来改变，如下方式：

```shell
set global validate_password_policy=LOW;
```

然后再次在mysql命令行下执行

```shell
SET PASSWORD = PASSWORD('xxxxxxxxxx'); 
```

![image-20210522225636265](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Mysql4.png)

#### 12.开启远程登录，授权root远程登录

```shell
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'xxxxxxx' WITH GRANT OPTION;
```

#### 13.命令立即执行生效

```shell
flush privileges;
```

## 二、远程工具连接

1.使用xshell，putty等工具连接服务器

2.输入mysql -uroot -p  输入密码登录

3.use mysql

4.接下来我们可以查看一下现有用户及连接权限

```shell
select User,authentication_string,Host from user
```

mysql是为了安全考虑所以初始的时候远程是不能访问的，只能本地localhost，127.0.0.1访问。（**就相当于远程只能登录mysql这个工具，却不能以某种用户的身份访问里面的数据**（我们平时做项目都是以root用户的身份访问指定数据库数据））

5.下面我们就再添加一个root用户，密码暂时为空，允许任意Ip访问’%’

```shell
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root用户的密码' WITH GRANT OPTION;
```

6.刷新

```shell
flush privileges;
```

7.`阿里云配置实例安全组`

![image-20210522231442755](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Mysql5.png)

![image-20210522231511389](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85Mysql6.png)

![image-20210522231534521](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%96%B0%E5%A2%9EMysql7.png)

通过navicat工具连接，即可连接成功。

