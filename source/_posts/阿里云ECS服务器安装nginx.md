---
title: 阿里云ECS服务器安装nginx
tags:
  - Nginx
  - 阿里云
categories:
  - Nginx
toc: true
abbrlink: 47617
date: 2021-07-25 14:16:14
---

### 前言:

阿里云Ecs服务器部署项目，尤其是对于前后端分离的项目，之前在博客中提到相关SpringBoot部署到服务器：

[(35条消息) SpringBoot部署到阿里云服务器_最爱吃大米的博客-CSDN博客](https://blog.csdn.net/qq_38140292/article/details/117190594?spm=1001.2014.3001.5501)

此时对于前后端分离的项目，我们需要将我们对应的前端也部署到服务器，此时我们正对基于vue的框架，我们需要安装相关环境node vue，请自行安装。

<!--more-->

### **1.安装依赖包**

```shell
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
```

### **2.下载并解压安装包**

```shell
#创建用于存在地址的文件夹
cd /usr/local
mkdir nginx
cd nginx
#从服务器下载相关nginx文件
wget http://nginx.org/download/nginx-1.13.7.tar.gz
#解压文件
tar -xvf nginx-1.13.7.tar.gz
```

### **3.安装nginx**

```shell
#进入nginx目录
cd /usr/local/nginx
#进入目录
cd nginx-1.13.7
#执行命令
./configure
#执行make命令
make
#执行make install命令
make install
```

### **4.配置nginx.conf**

这是nginx最重要的地方

```shell
# 打开配置文件
vi /usr/local/nginx/conf/nginx.conf
i 进入编辑
```

`以下为我的配置（仅供参考）`

```shell
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;

    server {
    	# 默认使用80端口，这个可以根据自己前端访问地址自行修改
        listen       80;
        server_name  localhost;

		location / {
			# 需要访问的vue项目页面
            root   /usr/project/dist;
            # vue项目地址
			try_files $uri $uri/ /index.html;
            index  index.html index.htm;
        }
		
		location /prod-api/{
			proxy_set_header Host $http_host;
			proxy_set_header X-Real-IP $remote_addr;
			proxy_set_header REMOTE-HOST $remote_addr;
			proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			# 前端访问后端的端口号！！！一定要根据自己项目进行修改
			proxy_pass http://localhost:8081/;
		}		
		location /dev-api/{
			proxy_set_header Host $http_host;
			proxy_set_header X-Real-IP $remote_addr;
			proxy_set_header REMOTE-HOST $remote_addr;
			proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			# 前端访问后端的端口号！！！一定要根据自己项目进行修改
			proxy_pass http://localhost:8081/;
		}

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
}
```

### **5.启动nginx**

```shell
/usr/local/nginx/sbin/nginx -s reload
```

`如果出现报错：nginx: [error] open() ＂/usr/local/nginx/logs/nginx.pid＂ failed`

则运行： 

```SHELL
 /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

再次启动即可！



查看nginx进程是否启动：

```shell
ps -ef | grep nginx
```

![image-20210719221837639](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91ECS%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85nginx01.png)

### **6.外部主机连接上nginx需要关闭虚拟机的防火墙：**

```shell
systemctl stop firewalld.service
```



此时去阿里云终端配置外部访问端口 80 `配置安全组规则`

![image-20210719222129168](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91ECS%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%89%E8%A3%85nginx02.png)



常用命令

```shell
# 进入目录中cd /usr/local/nginx/sbin# 启动./nginx# 关闭./nginx -s stop# 重启./nginx -s reload
```

