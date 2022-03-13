---
title: 【hexo】基础教程-七-yilia添加字数统计和阅读时长
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 18156
date: 2021-07-25 15:53:29
---

## 一、安装插件

```shell
npm i –save hexo-wordcount
```

<!--more-->

## 二、文件配置

在`theme\yilia\layout\_partial\post`下创建`word.ejs`文件：

```ejs
<div style="margin-top:10px;">
    <span class="post-time">
      <span class="post-meta-item-icon">
        <i class="fa fa-keyboard-o"></i>
        <span class="post-meta-item-text">  字数统计: </span>
        <span class="post-count"><%= wordcount(post.content) %>字</span>
      </span>
    </span>

    <span class="post-time">
      &nbsp; | &nbsp;
      <span class="post-meta-item-icon">
        <i class="fa fa-hourglass-half"></i>
        <span class="post-meta-item-text">  阅读时长: </span>
        <span class="post-count"><%= min2read(post.content) %>分</span>
      </span>
    </span>
</div>
```

然后在 `themes/yilia/layout/_partial/article.ejs`中添加

```ejs
<div class="article-inner">
    <% if (post.link || post.title){ %>
      <header class="article-header">
        <%- partial('post/title', {class_name: 'article-title'}) %>
        <% if (!post.noDate){ %>
        <%- partial('post/date', {class_name: 'archive-article-date', date_format: null}) %>
        <% if(theme.word_count && !post.no_word_count){%>
          <%- partial('post/word') %>
          <% } %>
        <!-- 添加完成 -->

        <% } %>
      </header>
```

## 三、权限开启

在主题文件下的`_config.yml`中修改如下代码：

```shell
word_count:
  enable: true
  # 只在文章详情显示(不在首页显示)
  only_article_visit: true
```

最后即可看到字数啦。

实际效果：[liuhuanhuan963019.github.io](https://liuhuanhuan963019.github.io)



