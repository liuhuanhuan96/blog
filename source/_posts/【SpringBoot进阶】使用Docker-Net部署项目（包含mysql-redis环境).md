---
title: '【SpringBoot进阶】使用Docker Net部署项目（包含mysql,redis环境）.md'
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: true
abbrlink: 10872
date: 2022-02-23 22:10:38
---

1.先准备我们需要准备打包的项目jar文件

```shell
mvn packeage 
```

出现如下即表示打包成功：

<!--more-->

![image-20211207233557859](https://tva1.sinaimg.cn/large/008i3skNgy1gx5ozm66gyj312w08sab5.jpg)

2.准备Dockerfile文件

在我们项目的同级目录下，新增一个`Dockerfile`文件，保证我们在`docker build`的时候，我们就不需要指定我们的dockerfile文件地址。

新增如下内容：

```dockerfile
FROM java:8

ADD oasys.jar /home/project/oasys.jar

CMD ["---server.port=8088"]
EXPOSE 8088
ENTRYPOINT ["java", "-jar","/home/project/oasys.jar"]
```

3.将我们的`Dockerfile`和我们打包好的jar文件上传到我们的服务器，如果没有工具的话，我们可以使用`rz` 命令来进行上传，

4.在我们拉取镜像之前，我们先去创建一个我们需要的Docker Net,

如下：

```shell
docker network create project --subnet 192.168.0.0/16
```

我们可以通过`docker network ls`查看到我们配置的网络：以下就是我们查看到的结果，可以看到我们创建的网络

```shell
[root@iZuf65oftugvcjgk2jncyeZ oasys]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
54e8f3e9829b   bridge    bridge    local
fec761935499   host      host      local
af96498edc1e   none      null      local
09c5df6f85c8   project   bridge    local
5d1b3390482e   redis     bridge    local
```

5.拉取redis镜像，启动容器

```she
docker pull redis:5.0.9-alpine3.11
```

```shell
docker run -d -p 6379:6379 --name projectRedis -v /home/project/redis/data:/data -v /home/project/redis/conf/redis.conf:/etc/redis/redis.conf --net project redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
```

我们通过` docker network inspect project`来查看下我们的网络，以下就是我们配置的redis

![image-20211207234943630](https://tva1.sinaimg.cn/large/008i3skNgy1gx5pdwa6udj31h80aimze.jpg)



6.拉取mysql镜像,启动容器

```shell
docker pull mysql:8.0
```

```shell
docker run -d -p 3306:3306 -v /home/project/mysql/conf:/etc/mysql/conf.d -v /home/project/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name=projectMysql mysql:8.0
```

我们配置我们mysql指定的地址，记住在我们启动的时候，一定要指定我们mysql的密码：

我们进入到我们的容器中进行查看：

![image-20211207235136577](https://tva1.sinaimg.cn/large/008i3skNgy1gx5pfuqvvhj31ee0godjk.jpg)

7.开始build我们的项目容器。

```shell
docker build -t oasys .
```

![image-20211207235320950](https://tva1.sinaimg.cn/large/008i3skNgy1gx5phnvrj8j31hk0k0q7f.jpg)

我们启动我们的容器：

```shell
docker run -d -p 8088:8088 --name oasys --net project -v /home/project/oasys:/home/project oasys
```

注意在我们启动项目的时候，我们在我们项目中配置的mysql链接地址，一定要选择我们之前创建的docker net网络地址！！！

![image-20211207235601250](https://tva1.sinaimg.cn/large/008i3skNgy1gx5pkfypb0j314u09ctad.jpg)

此时我们去我们创建的网络中具体去查看一下：

```shell
docker network inspect project
```

此时我们的项目已经搭建好了，我们去外部公网查看下我们的项目运行：此时看到我们的运行的项目程序如下图所示：

![image-20211207235936820](https://tva1.sinaimg.cn/large/008i3skNgy1gx5po6em1zj321z0u0gqc.jpg)

注意！！！注意！！！在我们运行mysql和redis的时候，我们一定要指定我们创建的docker net网络地址

```shell
--net project
```

指定！！！。此时我们的全部项目已经部署好了！！！
