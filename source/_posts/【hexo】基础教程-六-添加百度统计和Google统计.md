---
title: 【hexo】基础教程-六-添加百度统计和Google统计
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 18884
date: 2021-07-25 12:20:41
---

### **简介**

百度统计和Google统计主要用于分析网站数据：流量、访客量等。

<!--more-->

![image-20210306125157943](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo-yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A1.png)

![image-20210306125319828](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo+yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A102.png)

需要注册账号，将相应的提示代码加入到博客代码中去

* 百度统计网址：[https://tongji.baidu.com](https://tongji.baidu.com/)
* Google统计网址：https://analytics.google.com/analytics/web/

### **文件地址**

yilia主题已集成，位置如下，我们只需要在主题的配置文件中进行配置即可。

* `F:\IdeaProjects\hexo\themes\yilia\layout\_partial\baidu-analytics.ejs`
* `F:\IdeaProjects\hexo\themes\yilia\layout\_partial\google-analytics.ejs`

### **配置**

`themes\yilia\_config.yml`原内容：

```shell
baidu_analytics: ''
google_analytics: ''
```

括号中填写配置对应的id即可

#### 百度

![image-20210306130119050](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo+yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A103.png)

![image-20210306130204927](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo+yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A104.png)

找到对应的配置文件：

`F:\IdeaProjects\hexo\themes\yilia\layout\_partial\baidu-analytics.ejs`

修改里面的代码为：

```shell
<% if (theme.baidu_a){ %>
<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?此处填写id";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>
<% } %>

```

#### 谷歌

**生成代码**：控制台–>（左下角）管理–>管理–>（中间）媒体资源–>（中间）跟踪信息–>跟踪代码

![image-20210306130559427](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo+yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A106.png)

![image-20210306130710805](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo+yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A107.png)

`找到代码，此操作方式与百度的方式相同，不再赘述。`

#### 配置id

```shell
baidu_analytics: '百度统计id'
google_analytics: 'Google统计id'
```

Google虽然好，但是因为墙的原因，所以有时候可能会出现问题。所以建议还是使用百度账号的使用方式。

最终效果图：

![image-20210306131030163](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90hexo%E3%80%91hexo+yilia%E6%96%B0%E5%A2%9E%E7%99%BE%E5%BA%A6%E7%BB%9F%E8%AE%A1%E5%92%8C%E8%B0%B7%E6%AD%8C%E7%BB%9F%E8%AE%A108.png)

欢迎访问我的博客:www.novoice.top



