---
title: 【hexo】基础教程-二-文章新增图片上传
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 3609
date: 2021-07-25 12:16:51
---

在博客中插入视频和图片能让人通俗易懂，生动形象。下面我们简答用两种方式介绍下hexo 博客文章中新增图片

#### ***方法一：***

**hexo 添加图片插件：**

<!--more-->

~~~shell
npm install hexo-asset-image --save
~~~

也可下载官方链接地址：[hexo-asset](https://github.com/cnzsb/hexo-asset.git)

此时的下载或不下载取决于自己的[theme](https://hexo.io/themes/)主题中所包含的默认的插件是否存在。可以在不安装此插件的前提下执行如下步骤。若不行，在安装此插件后执行如下步骤：

在hexo主文件夹中`_config.yml`配置文件中，修改为 `post_asset_folder: true`， 然后新建一篇文章

~~~shell
hexo new "test"
~~~

这个时候会出现一个`test.md` 和 `test`的文件夹

![【hexo】基础教程-二-文章新增图片上传01](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B%E4%BA%8C-%E6%96%87%E7%AB%A0%E6%96%B0%E5%A2%9E%E5%9B%BE%E7%89%87%E4%B8%8A%E4%BC%A001.jpg)

将图片资源放在`test`中，文章就可以使用相对路径引用图片资源了。格式如下

~~~shell
![](image.jpg)
~~~

**上述是markdown的引用方式，图片只能在文章中显示，但无法在首页中正常显示。**

如果希望图片在文章和首页中同时显示，可以使用标签插件语法。

~~~shell
{% asset_img image.jpg This is an image %}
~~~

重新编译后 再启动服务即可。

效果可查看如下链接：https://blog.csdn.net/qq_38140292/article/details/118885686?spm=1001.2014.3001.5501



#### ***方法二：使用cdn来存储图片***

使用typora编辑md文档，除了在本地存储图片，还可以将图片上传到一些免费的CDN服务中。例如在typora中配置图片上传到配置好的github图床中，会生成对应的url地址，将地址直接拿来引用即可。具体配置方案，请参考：https://blog.csdn.net/qq_38140292/article/details/118885686?spm=1001.2014.3001.5501

