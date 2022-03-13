---
title: 【hexo】基础教程-三-添加网易云音乐
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 35091
date: 2021-07-25 12:17:55
---

#### 1、打开网易云音乐首页，复制选择的背景音乐分享外链

[网易云音乐](https://music.163.com/)

<!--more-->

`但是有些尴尬的就是，我们目前只能添加一些没设置版权的音乐，有些收费或无版权的音乐是无法添加收听的。`

#### 2、搜索任意歌曲后进入详情页面：如下图

![【hexo】基础教程-三-添加网易云音乐01](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B%E4%B8%89-%E6%B7%BB%E5%8A%A0%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%9001.jpg)

#### 3、在详情页面点击生成[外链播放器](https://music.163.com/#/outchain/2/139774/)就会见到如下页面：

![【hexo】基础教程-三-添加网易云音乐02](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B%E4%B8%89-%E6%B7%BB%E5%8A%A0%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%9002.jpg)

可设置音乐播放样式大小（一般设置为默认） 

勾选设置音乐自动播放

#### 4、复制外链播放器的代码

在`themes/yilia/layout/_partial/left-col.ejs`文件`nav`标签中添加如下代码

~~~javascript
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=139774&auto=1&height=66">
</iframe>
~~~

本文修改了一些代码，用于新增一些样式和文字效果

![【hexo】基础教程-三-添加网易云音乐03](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B%E4%B8%89-%E6%B7%BB%E5%8A%A0%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%9003.jpg)

#### 5、在yilia主题配置文件中添加属性

~~~shell
# 网易云音乐插件
music:
  enable: true
  # 播放器尺寸类型(1：长尺寸、2：短尺寸)
  type: 1
  id: 139774  # 网易云分享的音乐ID(更换音乐请更改此配置项)
  autoPlay: true  # 是否开启自动播放
  # 提示文本(关闭请设置为false)
  text: '这似乎是首纯音乐，请尽情的欣赏它吧！'
~~~

效果如图所示：

![【hexo】基础教程-三-添加网易云音乐04](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B%E4%B8%89-%E6%B7%BB%E5%8A%A0%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%9004.jpg)



欢迎访问我的博客：www.novoice.top



