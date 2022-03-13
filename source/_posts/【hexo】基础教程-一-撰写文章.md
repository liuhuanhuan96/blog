---
title: 【hexo】基础教程-一-撰写文章
tags:
  - Hexo
categories:
  - Hexo
toc: true
abbrlink: 8613
date: 2021-07-25 12:14:30
---

在搭建好属于自己的博客网站之后，我们可以尝试着在网站上编写我们的第一篇文章。

[hexo官方地址](https://hexo.io/zh-cn/docs/writing)

<!--more-->

## 一、创建文章

打开建立的hexo文件，`windows`右击git bash，`macos/linux`终端进入文件位置。输入如下：其中`title`为文章的标题。

~~~shell
hexo new "title"
~~~

输入后，hexo会根据目录下`scaffolds/post.md`，在`source/_posts` 文件夹下创建一个文件，名为:`title.md`

## 二、撰写文章

Markdown 文档格式与书写方式，可参考：{% post_link Markdown-语法 Markdown-语法 %}

## 三、高级设置

[官方地址：](https://hexo.io/zh-cn/docs/front-matter)

#### （1）模板设置

当我们使用命令 `hexo new "title"` 创建文章时，Hexo 会根据 `/scaffolds/post.md` 对新文章进行初始化。

j简单来说，`/scaffolds/post.md` 文档中所规定的格式就是新文章的 **模板**。

一个简单的示例如下：

```markdown
title: {{ title }}
date: {{ date }}
tags: 
categories: 
```

#### （2）头部设置

在每篇利用 Hexo 创建的文章的开头，都会有对文章进行说明的文字，叫做 **文章头部**

文章的头部除了可以设置文章标题、发布日期等基础信息外，还可以为文章添加标签、分类等

一个简单的示例如下：

```
title: Title
date: YYYY-MM-DD HH:MM:SS
tags: [tag1, tag2, ...]
categories: category
1234
```

**注意**：属性和属性值之间必须有一个空格，否则会解析错误

#### （3）首页显示

在利用 Hexo 框架搭建的博客网站中，首页会显示文章的内容，且默认显示文章的全部内容

如果当文章太长的时候就会显得十分冗余，所以我们有必要对其进行精简

这时，我们只需在文章中使用 `<!--more-->` 标志即可，表示只会显示标志前面的内容

## 四、部署发布

~~~shell
hexo g -c
hexo s
hexo d
~~~
