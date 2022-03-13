---
title: 使用hexo+github搭建个人博客
tags:
  - Hexo
  - GitHub
categories:
  - Hexo
toc: true
abbrlink: 61030
date: 2021-07-25 12:13:24
---

## 一、引言

使用github pages搭建博客的好处：

<!--more-->

> 1. 全是静态文件，访问速度快；
> 2. 免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台；
> 3. 可以随意绑定自己的域名，不仔细看的话根本看不出来你的网站是基于github的；
> 4. 数据绝对安全，基于github的版本管理，想恢复到哪个历史版本都行；
> 5. 博客内容可以轻松打包、转移、发布到其它平台；

### 环境准备

1. 注册一个github账号

2. 安装node.npm等

3. 安装git

   

   

## 二、搭建github仓库

### 2.1 创建仓库

新建一个名为`用户名.github.io`的仓库，例如，如果你的github用户名是liuhuanhuan963019，那么你就新建`liuhuanhuan963019.github.io`的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 [liuhuanhuan963019.github.io](liuhuanhuan963019.github.io)，弊端就是，我们只能创建一个这样的仓库。

**warning**:

> 注册的邮箱需要先去验证
>
> 仓库名称必须是用户名.github.io
>
> 仓库创建会有一定的延迟

### 2.2 绑定域名

一般我们是使用`用户名.github.io`来访问，为了使我们的博客更具特点，我们可以使用绑定域名的方式来操作。

域名绑定方式请参考博客：[【Hexo】基础教程(五) 阿里云域名解析 | 最爱吃大米的博客 (novoice.top)](https://novoice.top/2021/02/09/【hexo】基础教程-五-阿里云域名解析/)

然后到你的github项目根目录新建一个名为CNAME的文件（无后缀），里面填写你的域名我的是novoice.top,大家依据自己的实际情况进行填写。

### 三、配置SSH

在我们代码提交到github仓库的时候我们，需要一定的权限，此时我们就需要配置我们本地的SSH

```shell
cd ~/. ssh #检查本机已存在的ssh密钥
```

如果提示：No such file or directory 说明你是第一次使用git。

```shell
ssh-keygen -t rsa -C "邮件地址"
```

然后一直回车，最终会生成一个文件在用户目录下，打开用户目录，找到`.ssh\id_rsa.pub`文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：

将刚复制的内容粘贴到key那里，title随便填，保存。

具体操作方式参见博客：git配置本地ssh参照文章[(36条消息) Macos git配置本地ssh_最爱吃大米的博客-CSDN博客](https://liuhuanhuan.blog.csdn.net/article/details/110730314) windows方式相同

## 四、hexo写博客

### 4.1 简介

Hexo是一个简单、快速、强大的基于 Github Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题。

官网： [http://hexo.io](http://hexo.io/)
github: https://github.com/hexojs/hexo

### 4.2 安装

```shell
npm install -g hexo
```

### 4.3 初始化

新建一个名为hexo的文件夹（名字任意），比如我的是`F:\IdeaProjects\hexo`，由于这个文件夹将来就作为你存放代码的地方，所以最好不要随便放。

```shell
cd F:\IdeaProjects\hexo
hexo init
```

hexo会自动下载一些文件到这个目录，包括node_modules，目录结构如下图：

```shell
hexo g #生成
hexo s #运行辅助
hexo c #清除本地
hexo d #上传代码到github
```

`hexo s`是开启本地预览服务，打开浏览器访问 [http://localhost:4000](http://localhost:4000/) 即可看到内容，很多人会碰到浏览器一直在转圈但是就是加载不出来的问题，一般情况下是因为端口占用的缘故，因为4000这个端口太常见了，解决端口冲突问题请参考这篇文章：http://blog.liuxianan.com/windows-port-bind.html

第一次的时候就会有一篇默认的文章，hello world !!! 大家打开自己的浏览器输入localhost:4000即可查看。

### 4.4 修改主题

 [官方主题](https://hexo.io/themes/)

个人比较喜欢的主题：[hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)。

首先下载这个主题：

```shell
cd F:\IdeaProjects\hexo\themes
git clone https://github.com/litten/hexo-theme-yilia.git yilia
```

下载后的主题都在themes目录下：



修改`_config.yml`中的`theme: landscape`改为`theme: yilia`，然后重新执行`hexo g`来重新生成。

如果出现一些莫名其妙的问题，可以先执行`hexo clean`来清理一下public的内容，然后再来重新生成和发布。

### 4.5 上传到github

如果你一切都配置好了，发布上传很容易，一句`hexo d`就搞定，当然关键还是你要把所有东西配置好。由于gitee pages在维护，所以暂时只能使用github搭建。

首先，`ssh key`肯定要配置好。

其次，配置`_config.yml`中有关deploy的部分：

![image-20210725005608198](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/hexo%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA.png)

正确写法：

```
deploy:
  type: git
  repository: git@github.com:liuhuanhuan963019/liuhuanhuan963019.github.io.git
  branch: master
```

错误写法：

```
deploy:
  type: github
  repository: https://github.com/liuhuanhuan963019/liuhuanhuan963019.github.io.git
  branch: master
```

此时会报错，我们需要下载一个插件

```shell
npm install hexo-deployer-git --save
```

打开你的git bash，输入`hexo d`就会将本次有改动的代码全部提交，没有改动的不会：

### 4.6 常用的hexo命令

> hexo new "postName" #新建文章 
>
> hexo new page "pageName" #新建页面 
>
> hexo generate #生成静态页面至public目录 
>
> hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server） 
>
> hexo deploy #部署到GitHub 
>
> hexo help  # 查看帮助 
>
> hexo version  #查看Hexo的版本

简写

```shell
hexo n == hexo new hexo g == hexo generate hexo s == hexo server hexo d == hexo deploy
```

### 4.7 _config.xml

这里面都是一些全局配置，每个参数的意思都比较简单明了，所以就不作详细介绍了。

需要特别注意的地方是，冒号后面必须有一个空格，否则可能会出问题。

### 4.8 新建一个博客

定位到我们的hexo根目录，执行命令：

```shell
hexo new 'blog'
```

hexo会帮我们在`_posts`下生成相关md文件：

我们只需要打开这个文件就可以开始写博客了，

当然你也可以直接自己新建md文件，用这个命令的好处是帮我们自动生成了时间。

一般完整格式如下：

```markdown
---title: blog #文章页面上的显示名称，一般是中文date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改categories: 默认分类 #分类tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格description: 附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面---以下是正文
```

## 五、最终效果

关于hexo更多用法欢迎大家访问呢我的[csdn](https://liuhuanhuan.blog.csdn.net)

欢迎大家访问我的个人博客：[novoice.top](www.novoice.top)

