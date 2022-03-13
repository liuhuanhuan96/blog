---
title: Nginx配置本地图片服务器
tags:
  - Nginx
categories:
  - Nginx
toc: true
abbrlink: 54429
date: 2022-02-23 22:11:03
---



## 一、Nginx介绍

Nginx就是反向代理服务器。
<!--more-->

首先我们先来看看什么是代理服务器，代理服务器一般是指局域网内部的机器通过代理服务发送请求到互联网上的服务器，代理服务器一般作用于客户端。比如GoAgent，FQ神器。



![img](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/081121520378740.png)

一个完整的代理请求过程为：客户端首先与代理服务器创建连接，然后根据代理服务器所使用的代理协议，请求对目标服务器创建连接、或则获得目标服务器的指定资源。Web代理服务器是网络的中间实体。代理位于Web客户端和Web服务器之间，扮演“中间人”的角色。 
HTTP的代理服务器既是Web服务器又是Web客户端。

代理服务器是介于客户端和Web服务器之间的另一台服务器，有了它之后，浏览器不是直接到Web服务器去取回网页，而是通过向代理服务器发送请求，信号会先送到代理服务器，由代理服务器来取回浏览器所需要的信息并传送给你的浏览器。

正向代理是一个位于客户端和原始服务器之间的服务器，为了从原始服务器取的内容，客户端向代理发送一个请求并指定目标（原始服务器），然后代理向原始服务器转交请求并将获得的内容返回给客户端，客户端必须要进行一些特别的设置才能使用正向代理。


反向代理服务器：在服务器端接收客户端的请求，然后把请求分发给具体的服务器进行处理，然后再将服务器的响应结果反馈给客户端。Nginx就是其中的一种反向代理服务器软件。
Nginx：Nginx（“engine x”），Nginx是俄罗斯人Igor Sysoev(塞索耶夫)编写的一款高性能的 HTTP 和反向代理服务器。也是一个IMAP/POP3/SMTP代理服务器，也就是说，Nginx本身就可以托管网站，进行HTTP服务处理，也可以作为反向代理服务器使用。

正向代理客户端必须设置正向代理服务器，当然前提是要知道正向代理服务器的IP地址，还有代理程序的端口。
反向代理正好与正向代理相反，对于客户端而言代理服务器就像是原始服务器，并且客户端不需要进行任何特别的设置。客户端向反向代理的命名空间中的内容发送普通请求，接着反向代理将判断向哪个原始服务器转交请求，并将获得的内容返回给客户端。

## 二、图片服务器搭建

本地安装好nginx之后，我们可以通过端口来进行访问，默认的端口是80端口，我这边由于和本地80端口冲突了，我修改为了8089。

![image-20211210195430120](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211210195430120.png)

此时我们成功启动nginx,然后在nginx目录下面，新增我们需要配置的图片路径，如下：

```shell
		#添加图片的代码
      location ~ .*\.(gif|jpg|jpeg|png)$ {  
      expires 24h;  
      root H:/radar/;#指定图片存放路径  
      access_log H:/radar/log;#图片路径  
      proxy_store on;  
      proxy_store_access user:rw group:rw all:rw;  
      proxy_temp_path         H:/radar/;#图片路径  
      proxy_redirect          off;  
      
      proxy_set_header        Host 127.0.0.1;  
      proxy_set_header        X-Real-IP $remote_addr;  
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;  
      client_max_body_size    10m;  
      client_body_buffer_size 1280k;  
      proxy_connect_timeout   900;  
      proxy_send_timeout      900;  
      proxy_read_timeout      900;  
      proxy_buffer_size       40k;  
      proxy_buffers           40 320k;  
      proxy_busy_buffers_size 640k;  
      proxy_temp_file_write_size 640k;  
      if ( !-e $request_filename)  
      {  
      proxy_pass  http://127.0.0.1:8089;  #代理访问地址
       }  
      }    
```

按照如上配置，找到我们需要的路径。然后重启服务后，就可以看到我们配置的图片了。如下图所示

![image-20211210195955312](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211210195955312.png)

此时一个简单的nginx图片服务器就搭建好了。更多的nginx的用户的话，之后会继续更新。。。。
