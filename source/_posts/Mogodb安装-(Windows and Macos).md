---
title: Mogodb安装(Windows版)
tags:
  - MongoDB
categories:
  - MongoDB
toc: true
abbrlink: 47283
date: 2021-07-25 12:42:26
---

## 一、windows安装

### 1.官网下载

<!--more-->

[MongoDB ](https://www.mongodb.com/try/download/community)    默认是安装的最新的版本，我比较佛系，只是用来学习的，感觉没啥太大区别，就选择了默认的方式。

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/MongoDB%E5%AE%89%E8%A3%8501.png" alt="image-20210430224731190" style="zoom:50%;" />



windows版本下载的是msi文件，默认的可视化安装界面。如下图

![image-20210430224846514](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/MongoDB%E5%AE%89%E8%A3%8502.png)



双击开始安装，直接下一步：选择custom自定义安装

点击ok，然后点击next 点击之后 新版的Mongodb会主动在安装目录下创建log和data文件，这相比较早期版本有了改善 ，早期需要自己手动创建 **但我们仍然需要在data下创建db文件夹  笔者的在C:\MongoDB\data\db（记住一定要再建个db文件夹）**

![image-20210508072843189](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/MongoDB03.png)

在安装界面取消如下下载方式，由于墙的原因，下载时间很久不建议下载

![img](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/MongoDB04.png)

 **最后安装成功会弹出一个警告框，选中 Ignore 就好**

到此为止，MongoDB客户端已经安装完成。



`最后很重要的一步`：

 **由于我们已经创建了C:\MongoDB\data\db文件夹 这里就不需要再创建 否者还要创建**

然后在cmd进入C:\MongoDB\bin目录下（在windows资源管理器中shift+右键打开powershell也行）然后执行mongod -dbpath C:\MongoDB\data\db 命令  如下图（这条命令是开启服务，它会一直运行。

cmd输入如下命令：

```shell
mongod -dbpath C:\MongoDB\data\db
```

结果如下图所示 （此时表示开启了mongodb服务，如果想要一直使用的话，此页面不可关闭）

![image-20210508073324117](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/MongoDB06.png)

新建新命令页，输入`mongo` 如下图所示，此时全部的mongoDB已全部安装完毕。

![image-20210508073546061](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/MongoDB05.png)



## 二、macos安装

MongoDB 提供了 OSX 平台上 64 位的安装包，你可以在官网下载安装包。

下载地址：https://www.mongodb.com/download-center#community

![img](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%20MongoDB06.jpg)

一般是默认下载最新版本。

接下来进入终端：

```shell
# 进入 /usr/local
cd /usr/local

# 下载
sudo curl -O https://fastdl.mongodb.org/osx/mongodb-osx-ssl-x86_64-4.0.9.tgz

# 解压
sudo tar -zxvf mongodb-osx-ssl-x86_64-4.0.9.tgz
# 重命名为 mongodb 目录

sudo mv mongodb-osx-x86_64-4.0.9/ mongodb
```

安装完成后，我们可以把 MongoDB 的二进制命令文件目录（安装目录/bin）添加到 PATH 路径中：

```shell
export PATH=/usr/local/mongodb/bin:$PATH
```

创建日志及数据存放的目录：

* 数据存放路径：

  ```shell
  sudo mkdir -p /usr/local/var/mongodb
  ```

* 日志文件路径：

  ```shell
  sudo mkdir -p /usr/local/var/log/mongodb
  ```

  

接下来要确保当前用户对以上两个目录有读写的权限：

```shell
sudo chown runoob /usr/local/var/mongodb
sudo chown runoob /usr/local/var/log/mongodb
```

以上 **runoob** 是我电脑上对用户，你这边需要根据你当前对用户名来修改。

接下来我们使用以下命令在后台启动 mongodb：

```shell
mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork
```

* **--dbpath** 设置数据存放目录
* **--logpath** 设置日志存放目录
* **--fork** 在后台运行

如果不想在后端运行，而是在控制台上查看运行过程可以直接设置配置文件启动：

```shell
mongod --config /usr/local/etc/mongod.conf
```

查看 mongod 服务是否启动：

```shell
ps aux | grep -v grep | grep mongod
```

使用以上命令如果看到有 mongod 的记录表示运行成功。

启动后我们可以使用 **mongo** 命令打开一个终端：

```shell
 cd /usr/local/mongodb/bin 
 ./mongo
 MongoDB shell version v4.0.9
connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("3c12bf4f-695c-48b2-b160-8420110ccdcf") }
MongoDB server version: 4.0.9
……
```

### 使用 brew 安装

此外你还可以使用 OSX 的 brew 来安装 mongodb：

```shell
brew tap mongodb/brew
brew install mongodb-community@4.4
```

**@** 符号后面的 **4.4** 是最新版本号。

安装信息：

* 配置文件：**/usr/local/etc/mongod.conf**
* 日志文件路径：**/usr/local/var/log/mongodb**
* 数据存放路径：**/usr/local/var/mongodb**

### 运行 MongoDB

我们可以使用 brew 命令或 mongod 命令来启动服务。

brew 启动:

```
brew services start mongodb-community@4.4
```

brew 停止：

```
brew services stop mongodb-community@4.4
```

mongod 命令后台进程方式：

```
mongod --config /usr/local/etc/mongod.conf --fork
```

这种方式启动要关闭可以进入 mongo shell 控制台来实现：

```
> db.adminCommand({ "shutdown" : 1 })
```
