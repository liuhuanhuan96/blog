---
title: 【hexo】基础教程-四-新增RSS订阅
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 44375
date: 2021-07-25 12:18:53
---

使用**hexo-generator-feed**插件生成RSS文件`atom.xml`，实现RSS订阅功能。

插件github网址：https://github.com/hexojs/hexo-generator-feed。

<!--more-->

参考文章：https://www.jianshu.com/p/2aaac7a19736，https://wxnacy.com/2018/12/12/hexo-add-rss/。

### 1、**首先添加插件，在hexo根目录下执行**

~~~shell
npm install --save hexo-generator-feed
~~~

### **2、配置`_config.yml`文件，启用插件**

~~~shell
# Extensions
plugins:
  hexo-generator-feed
#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20
~~~

### **3、在yilia主题添加RSS订阅配置**

（1）hexo 根目录下_config.yml中新增

~~~shell
# Extensions
plugins:
  hexo-generator-feed
~~~

  (2) hexo 主题目录_config.yml 中新增

~~~shell
# RSS订阅
rss: /atom.xml
~~~

### **4、生成RSS订阅文件**

~~~shell
hexo g
~~~

![【hexo】基础教程-四-新增RSS订阅01](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B%E5%9B%9B-%E6%96%B0%E5%A2%9ERSS%E8%AE%A2%E9%98%8501.png)



