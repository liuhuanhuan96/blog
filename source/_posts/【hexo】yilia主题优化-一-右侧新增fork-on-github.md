---
title: 【hexo】yilia主题优化-一-右侧新增fork-on-github
tags:
  - Hexo
categories:
  - Hexo
toc: false
abbrlink: 50652
date: 2021-07-25 12:11:05
---

选择一张合适的图片的新增到网站的右上角，用于快速跳转到个人github等相关网站。

1.打开/themes/yilia/layout/layout.ejs  文件，新增如下代码

<!--more-->

~~~javascript
// theme.github 为_config.yml中配置，接下来会提到
<% if (theme.github && theme.github.url)  
<% # "GitHub Ribbons" %>
<a class="forkMe" style="position:absolute;z-index:999;top:0;right:0.5em;"
       href="<%=theme.github.url%>" target="_blank">
       <img src="<%- url_for('img/forkme.png') %>"
         class="attachment-full size-full" alt="Fork me on GitHub" data-recalc-dims="1"></a>
      <% } %>
~~~

2.根据<img src="<%- url_for('img/forkme.png') %>" 中所写的地址在source/img目录下添加一张图片为forkme.png

![【hexo】yilia主题优化（一）01](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91yilia%E4%B8%BB%E9%A2%98%E4%BC%98%E5%8C%9601.png)

3.在themes主题配置文件中配置 如下：

~~~shell
# GitHub Ribbons(https://github.blog/2008-12-19-github-ribbons/)
# 右上角github连接设置
github:
  # (关闭请设置为false)
#  url: https://github.com/xxxxxxxx?tab=repositories
   url: flase
~~~

效果图如下：

![【hexo】yilia主题优化（一）02](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91yilia%E4%B8%BB%E9%A2%98%E4%BC%98%E5%8C%9602.png)



