---
title: Docker最新超详细版教程通俗易懂(进阶版)
copyright_author: 刘先森
copyright_author_href: 'https://novoice.top'
copyright_url: 'https://novoice.top'
copyright_info: 此文章版權歸刘先森所有，如有轉載，請註明來自原作者
tags:
  - Hexo
categories:
  - Hexo
top_img: 'https://picsum.photos/id/860/3264/2448'
copyright: true
cover: 'https://picsum.photos/id/860/3264/2448'
abbrlink: 210b5282
date: 2022-03-16 23:03:43
---

## 一、Docker Compose

### 1.简介

Docker

DockerFile build run 手动操作，单个容器！！！

当我们部署多个微服务的时候，100个微服务。每个都存在着相互依赖的关系！！

**Docker Compose 来轻松高效的管理容器。定义运行多个容器！！！**



`官方介绍`

1.定义运行多个容器

2.使用yaml配置应用服务

3.简单命令开始创建服务

> Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see [the list of features](https://docs.docker.com/compose/#features).
>
> Compose works in all environments: production, staging, development, testing, as well as CI workflows. You can learn more about each case in [Common Use Cases](https://docs.docker.com/compose/#common-use-cases).
>
> Using Compose is basically a three-step process:
>
> 1. Define your app’s environment with a `Dockerfile` so it can be reproduced anywhere.
>
> - 任何地方运行
>
> 1. Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated environment.
>
> - 定义docker-compose.yml容器
>
> 1. Run `docker compose up` and the [Docker compose command](https://docs.docker.com/compose/cli-command/) starts and runs your entire app. You can alternatively run `docker-compose up` using the docker-compose binary.
>
> - Docker-compose up使用启动项目



作业：批量容器编排

Compose是Docker开源的项目，需要我们自行安装！！！！

`Dockerfile`让服务可以在任何地方运行。Redis、Mysql、Nginx等。单个容器，一个一个去启动时非常的麻烦的

Compose:

```yaml
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

运行我们这个compose的话，就直接讲所以的服务都运行起来了。

只要文件没写错，DockerCompose可以至少运行100个服务



Compose的重要概念：

- 服务Service,容器、应用、（Web、Redis、Mysql）
- 最后组成了一个Project.一组关联的容器。 博客：Web Mysql

### 2.安装

1.下载

```shell
#官方下载地址
 sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

![image-20220314215157336](https://tva1.sinaimg.cn/large/e6c9d24egy1h09r38znm8j21cs088q4p.jpg)



2.授权

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

3.查看版本

```shell
 docker-compose version
```

![image-20220314220247460](https://tva1.sinaimg.cn/large/e6c9d24egy1h09reh4l7fj21by082wg0.jpg)

看到以上这个样子，说明docker compose已经安装好了。然后我们开始下面的内容。

### 3.体验

[官方地址](https://docs.docker.com/compose/gettingstarted/)

**step1**

```shell
 mkdir composetest
 cd composetest 
```

然后在目录下创建一个文件app.py

```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

创建需要导入的依赖包requirements.txt

```txt
flask
redis
```

**step2**

创建一个Dockerfile。应用大包为镜像

```dockerfile
# syntax=docker/dockerfile:1
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

**Step3**:

定义一个compse file    创建文件docker-compose.yml。 定义整个服务需要的环境，web

```yaml
version: "3.9"
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

**Step4:**

Build and run your app with Compose.  启动项目

```shell
docker-compose up
```

此时我们会遇到如下的错误：

![image-20220314222155706](https://tva1.sinaimg.cn/large/e6c9d24egy1h09ryec3nxj21d60a4goz.jpg)

只时候我们需要去修改下`docer-compose.yml`的版本号，我的改为了3.大家可自行修改2.2-3.3之间即可。

然后就可以成功运行了：



以前的Dockerfile可以理解为一个单机，现在使用了compose才是应用了整个docker服务，才是开始运行一个真正的项目

流程：

1.创建网络

2.执行docer-compose.yml

3.启动所有的服务   **这一步等待的时间会是特别的长特别的长，所以需要耐心的等待下**

```shell
Creating composetest_redis_1 ... done
Creating composetest_web_1   ... done
```

出现如下情况即表示启动成功了。`最好是根据官网的方式来进行操作，视频中的操作方式有些问题，版本不一致导致最后无法运行成功`

一定要有`docker-compose.yml文件才可以成功的启动，不然不可以成功启动`



![image-20220315162039036](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315162039036.png)

此时我们需要去浏览器中打开我们的服务：

http://xxxx:8000/.此时如果我们使用的是阿里云，还需要去配置安全组规则。记得对外访问的端口是8000.

**然后再去查看最后的结果，每当我们进行刷新的时候，我们就会看到，数字在不停的+1**

![docker](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/docker.gif)

![image-20220315164214790](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315164214790.png)



步骤：

1. 文件名composetest
2. 服务

```yaml
version: "3.9"
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

他会自动的生成起我们的服务，有一些我们需要去了解的默认规则。，这些`默认规则`就是我们等下需要去了解和研究的、

docker images里面下载了很多依赖，compose里面的环境全都帮我们下载好了：

![image-20220315164304956](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315164304956.png)



之前我们是run单个容器，现在我们直接一键全部都启动好了，我们不需要多余的服务去进行启动。

```shell
[root@liuhuanhuan composetest]# docker service ls
Error response from daemon: This node is not a swarm manager. Use "docker swarm init" or "docker swarm join" to connect this node to swarm and try again.
```

默认的服务名，文件名___服务名____num  未来会启动多个服务，集群的方式去进行部署，A B _num表示的就是副本的数量_

服务redis服务--->4个副本



集群中，服务至少有1个实例，弹性的进行去操作。

3.网络规则

![image-20220315165301031](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315165301031.png)



如果我们使用多个服务去启动一个项目。那么项目中的内容都在同一个网络下面，这样的话，就可以通过域名去进行访问。



![image-20220315165545181](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315165545181.png)

此时会发现，我们的网络内部加载了2个服务。我们可以直接通过域名的方式去进行访问。

如果在同一个网络下面，我们可以直接通过域名的方式去进行访问。

如果我们想要去停止一个容器的话，我们可以通过

- docker-compose down
- ctrl+c

两种方式去进行停止

![image-20220315165924083](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315165924083.png)

此时通过``ctrl+C`的方式去进行停止，那么最后停止的是将我们compose启动的所有服务都进行停止了。具体如上图所示。

以前我们都是通过	`docker run`的方式去启动容器。

那么现在我们用``docker compose`的方式，通过编写`docker-compose yaml`的方式去一键启动所有的服务，或者启动。





<font size="6px" color="red">主要步骤：</font>

1.编写`Dockerfile`

2.编写``docker-compose yaml`

3.执行`docker-compose up`

### 4.总结

1. Docker 镜像 run->(容器)
2. Dockerfile 构建镜像（服务打包）
3. docker-compose启动项目（编排、多个微服务环境）
4. Docker网络

### 5.yaml规则

docker-compose.yaml是整个compose的核心

[官网地址](https://docs.docker.com/compose/compose-file/compose-file-v3/)

```shell
# 3层
version: ""  #版本
services:  #服务
	服务1:web
		#服务配置  docker容器的配置
		images
		build
		network
		......
	服务2:redis
#第三层  其他配置	网络卷挂载，全局配置等等
volumes:
network:
configs:
.......
```



![image-20220315184633762](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315184633762.png)

在我们启动项目的时候，如果一个服务需要依赖于数据库，mysql或者nginx等等。。。。我们就可以使用depends_on的方式来启动，表示依赖于这几个容器，先启动这几个容器里面的东西，然后再启动我们的项目。

一定要多看官方文档！！！！

### 6.测试案例-wordpress博客启动

一般情况下，我们需要，先下载程序，然后安装mysql数据库，然后去配置后才能正常的启动

使用compose之后，我们只需要，按照官方的方式，操作，几步解决所有的问题。

[Quickstart: Compose and WordPress | Docker Documentation](https://docs.docker.com/samples/wordpress/)

如果需要文件的时候，我们需要新建一个Dockerfile，来build我们的服务

文件准备完毕，然后直接一键启动项目

```shell
mkdir my_wordpress/
```

```she
cd my_wordpress/
```

```shell
vim docker-compose.yml
```

```yaml
version: "3.9"
    
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  wordpress_data: {}
```

前台启动

```shell
docker -d 
docker-compose up -d # 后台启动
```

![image-20220315190459108](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315190459108.png)

### 7.微服务上线 计数器

1.新建一个项目 在目录下新增HelloController

```java
package com.example.docker_compose_demo.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.StringRedisTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

/**
 * @author liuhuanhuan
 * @version 1.0
 * @date 2022/3/15 19:25
 */
@RestController
public class HelloController {

    @Autowired
    private StringRedisTemplate redisTemplate;

    @GetMapping("/hello")
    public String hello() {
        Long views = redisTemplate.opsForValue().increment("views");
        return "hell0 + views" + views;
    }
}
```

2.编写Dockerfile

```dockerfile
FROM java:8

COPY *.jar /app.jar

CMD ["--server.port=8080"]
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app.jar"]
```

3.编写docker-compose.yml

```yaml
version: "3.9"
services:
  lhh:
    build: .
    image: lhhapp
    depends_on:
      - redis
    ports:
      - "8080:8080"
  redis:
    image: "redis:alpine"
```

4.将项目打包，和Dockerfile，docker-compose.yml一并上传到服务器上。然后执行如下命令

```shell
docker-compose up --build
```

![image-20220315201329490](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315201329490.png)



出现如上页面即表示启动成功，然后我们去看下启动的服务，并进行测试

![image-20220315201456012](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315201456012.png)

如果我们的项目需要重新部署打包，我们可以执行如下代码，项目就会重新构建并执行

```shell
docker-compose up --build
```



一个工程会有多个服务，每个服务会有对应的容器来进行启动。

## 二、Docker Swarm

集群方式部署、不是单机的方式去部署，需要至少3-4台服务器。2核4G服务器

工作模式：分为管理节点和工作节点，只有管理节点去操作工作节点，操作的所有方式都是在manager上面的。

![image-20220315205354209](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E8%AF%B4sqsqsq209.png)



### 2.1 购买服务器

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315211607464.png" alt="image-20220315211607464" style="zoom: 50%;" />





![image-20220315212217305](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315212217305.png)



<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/122%E3%81%AErd.png" alt="image-20220315212340167" style="zoom:50%;" />

4台机器上都安装上docker

### 2.2开始搭建集群

swarm的基本操作：

![image-20220315205624828](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315205624828.png)

我们需要告诉别的服务器怎么来链接我，我们去看下init的相关命令

![image-20220315210320390](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315210320390.png)

服务器分为公网和私网，我这边服务器在不同的客户端，所以还是走公网比较好一点

公网：

172.18.142.120

初始化我们的节点

```shell
docker swarm init --advertise-addr 172.18.142.120
```

![image-20220315215543059](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315215543059.png)

可以通过其他方式来加入到我们的节点中

```shell
docker swarm join 加入到一个节点中来
```

```shell
#获得令牌
docker swarm join-token manager
docker swarm join-token worker
```

![image-20220315215700760](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315215700760.png)

我们现在已经在我们的第二太服务器上面加入了我们的swarm worker

此时我们去第一台服务器上去看下我们的节点数，此时我们会发现，节点数有多了一个，

```shell
docker node ls
```

![image-20220315215825648](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315215825648.png)

![image-20220315220017485](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315220017485.png)



我们可以通过以下命令生成我们需要加入的`token`节点

```shell
docker swarm join-token manager
```

此时我们将第三台服务器加入其中来看看

![image-20220315220214671](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315220214671.png)

此时我们的集群中又多了一个节点。

![image-20220315220413613](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315220413613.png)

到此为止，我们的集群就搭建好了！！！！！

步骤：

1.生成我们的主节点init

2.加入(管理者、worker)

### 2.3 Raft一致性算法

双主双从：假设一个节点挂了，那么其他节点是否可以正常使用呢？

Raft一致性算法：保证大多数节点存货才可以使用。   只要>1就可以正常使用，集群至少大于3台机器、

测试案例：

1.将docker1机器停止。宕机了！！！ 目前我们是双主双从的机器，那么另外一台机器主节点也不行了。

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315221414328.png" alt="image-20220315221414328" style="zoom:50%;" />

我们去看下另一个主节点是否可以正常使用：

![image-20220315221506603](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315221506603.png)

此时我们发现我们的宁一个节点也挂了。

当我们重启之后，发现，原来我们的第一台机器是leader，但是重启之后，发现，原来的第二台主节点机器就变成了leader，

2.此时我们测试下，将一台worker机器的节点离开集群，看看我们的服务是否挂掉呢？

```shell
docker swarm leave
```

![image-20220315221917121](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/sq121.png)

此时我们的docker02这台机器已经离开了我们的集群。那我们再去看下是否其他的可以正常使用呢？

此时我们发现，刚刚离开集群的机器，状态变成了down,但是我们整个集群还是正常运行的。所以不受影响。

![image-20220315222015969](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315222015969.png)

此时我们考虑新增一个manager结点，我们将刚刚离开集群的机器2加入到我们的manager结点当中来。

在我们的主节点机器下运行一下代码（任意一台manager结点的机器均可以）

```shell
docker swarm join-token manager
```

然后讲生成的结果，在我们的机器2中输入：此时我们发现，刚刚我们离开集群的节点，重新上线啦，又重新回到了我们的集群当中了，但是此时它是以manager的身份加入进来的。

![image-20220315222450322](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315222450322.png)



3.worker节点就是用来工作的，管理节点才是正正来进行操作的，此时我们已经设置了3台机器作为管理节点。

4、此时我们测试下，将第一台机器暂停服务，刚刚只有2个管理节点的时候，我们停止了机器1，发现，整个集群都无法正常运行了。现在我们是3个管理节点，那么我们看下，停止了一台管理节点，其他节点的docker是否可以正常进行呢？

此时我们停止机器1：

![image-20220315222850543](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315222850543.png)

我们在去刚刚新增的机器2中看看是否整个集群可以正常运行呢？

![image-20220315222932172](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315222932172.png)

此时我们惊奇的发现，整个集群还可以正常运行，但是刚刚的那台管理节点，是属于离开的状态，因此我们的管理节点个数为2大于1，所以我们的整个集群可以正常去运行。

那么我们思考一个问题，如果将我们的机器2，也暂停呢？只剩下一个管理节点在运行，是否可以呢？

此时我们将机器2也关闭，看看，最后一个管理节点是否可以正常运行呢？

![image-20220315223229715](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315223229715.png)



此时我们已经暂停了机器2，那我们去看下最后一台管理节点，是否可以正常运行呢？

![image-20220315223309855](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220315223309855.png)

此时我们惊奇的发现，我们整个集群已经挂了，因为我们的管理节点的个数为1不大于1，所以导致了，我们整个集群处于一个崩溃的状态。

以上就是Raft算法的 一些东西，就是我们必须要有三个管理（主）节点在我们的集群中。并且随时要大于1台机器是管理节点存活，我们的集群才可以正常运行，高可用！！！！

<font size="6px" color="red">Raft协议</font>：保证大多数节点存货，才可以使用，高可用性质。

### 2.4 体会

创建服务、动态扩展服务、动态更新服务

![image-20220316214313066](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316214313066.png)



灰度发布、金丝雀发布。滚动发布，升级发布。

我们现在来启动一个项目来测试下。

```shell
docker service create -p 8088:80 --name my-nginx nginx
```

![image-20220316214636941](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316214636941.png)

```shell
docker run 容器启动！不具有扩缩容的作用
docekr service create 服务！！！具有滚动更新，扩缩容的作用，具有灰度发布，金丝雀发布等等！！！！ 
```

查看服务

```shell
docker service ps my-nginx
docker service ls
```

![image-20220316214946326](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316214946326.png)

此时的REPLIAS就是副本的个数，此时我们的服务只启动一个服务，并且只有一个副本。

此时我们在每个服务器上都运行docker run，看看，此时我们在机器1启动的服务，被分配到我们的机器2 了，其他的机器并没有开启服务。

![image-20220316215437790](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316215437790.png)

如果此时我们网站的流量变大了，那么我们需要进行扩缩容，我们看下怎么去进行操作。我们现在扩充到三个服务，怎么操作呢

```shell
docker service update --replicas 3 my-nginx
```

![image-20220316215536768](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316215536768.png)

这就是我们的动态扩缩容！！！！

此时我们3台机器应该全部要启动好了。我们随机选择一台机器来看下，我们的服务是否全部启动好了。

我们此时发现，我们的机器1还是没有启动服务，但是我们是否可以进行访问呢？

![image-20220316215827437](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316215827437.png)

那么此时如果我们去开启10个也是没有，顶多就是每个服务器多开几个容器而已t.因为我们的容器之间是隔离的。所以我们开多少个也是没有问题的。

```shell
docker service update --replicas 10 my-nginx
```

![image-20220316220221791](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316220221791.png)



只要是服务，那么在集群的任意一个节点中都可以进行访问。服务可以有多个副本，可以动态的去进行扩缩容实现高可用！！！，那么我们如果去停止这些服务呢。我们只需要将我们的副本变为1即可。

```shell
docker service update --replicas 1 my-nginx
```

输入如上代码即可。这就是我们的弹性扩缩容！！！！就可以实现我们服务的高可用和服务器的高可用

此时我们还有一个命令也可以实现这样的操作，这种方式的话，会更加简单点。我们想要扩缩容几个，就使用结果

```shell
docker service scale my-nginx=5
```

![image-20220316220912709](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316220912709.png)

按我们怎么去删除一个服务呢？

```shell
docker service rm my-nginx
```

![image-20220316221028706](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316221028706.png)

此时我们就成功的删除了我们的服务！！！

docker swarm并不难，只要会搭建集群，会启动服务，动态管理容器就可以了。

### 2.5概念总结

swarm 集群的管理和编排，docker 可以初始化一个swarm集群，其他节点可以加入。（管理和工作者）

node就是docker节点，多个节点就组成看一个网络集群。（管理和工作者）

service 任务，可以在我们的管理节点和我们的工作节点来运行，核心！！！用户访问！！！

task

![image-20220316221454984](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316221454984.png)

命令-》管理-》api->调度->工作节点（创建task容器维护创建）

服务副本和全局服务！！！



![image-20220316221952634](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316221952634.png)

调整service以什么方式运行！！！

我们刚刚所有的服务都是随机分配的，我们的工作节点和我们的manageer节点都可以跑服务。但是我们的服务分为两种，一种是全局可以跑的service，还有一种是只能在副本上跑的service。全局的我们在任意节点都可以跑，但是工作节点，智能在我们的工作节点上跑。主要是通过命令的方式来进行操作的

```shell
--mode string
Service mode(replicated or global)(default "replicated")
docker service create --mode replicated --name mytom tomcat:8 #默认的方式
docker service create --mode global --name haha alphine ping baidu.com #指定方式执行
每个节点都有自己的日志收集器，过滤，把所有日志最终再传给日志中心，服务监控，状态性能
```

扩展：网络模式  “publishMode”:”ingress”

Swarm有三种网络模式：

overlay:在一个集群当中，即使我们跨机器，也可以把他集中起来。

ingress:特殊的overlay网络！具有负载均衡的功能，IPVS VIP

![image-20220316223359999](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316223359999.png)

这个docker ingress就是我们的swarm的网络

![image-20220316223854275](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316223854275.png)

虽然我们是在不同的服务器上面，但是，我们网路实际上是同一个。ingress网络。是一个特殊的overlay网络

![image-20220316224012922](/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316224012922.png)

现在我们有4台服务器，他们的IP都是不相同的。我们现在把他们搭建了一个集群，我们将我们所有的网络都放到我们的overlay里面，那么我们的4台不同IP的服务器就可以相互ping通了。集群就变成了了一个整体了

## 三、Docker  Stack

docker-compose单机部署项目！！！

Docker stack部署，集群部署！！！

![image-20220316224718191](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316224718191.png)

~~~shell
#单机
docker-compose up -d wordpress.yaml


#集群
docker stack deploy


# docker-compose 文件，使用dockerstack案例

~~~

## 四、Docker Secret 

安全 ，配置密码，。证书等等

![image-20220316224649721](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316224649721.png)

## 五、Docker config

配置

![image-20220316224813773](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316224813773.png)

学习方式：

网站找案例，然后跑起来，查看命令帮助文档！！！去操作

