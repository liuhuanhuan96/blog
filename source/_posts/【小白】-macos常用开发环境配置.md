---
title: 【小白】 macos常用开发环境配置
tags:
  - MacOS
categories:
  - MacOS
toc: true
abbrlink: 30405
date: 2021-07-25 13:17:36
---

## table 自动补全

1. 打开终端，输入nano .inputrc 命令回车，进入编辑状态

   ```shell
   $ nano .inputrc
   ```

   <!--more-->

2. 粘贴下面的语句到文件中

   ```
   set completion-ignore-case on
   set show-all-if-ambiguous on
   TAB: menu-complete
   ```

3. 保存文件， Control + O 保存， 再按回车

4. Control + X , 退出文本编辑

5. 重启终端， 试验Tab键自动补全已经OK啦

## 新增ll命令

1.打开配置文件

```
vim ~/.bash_profile
```

2.i进入编辑模式，esc推出，:wq保存更改

```
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF
```

3.重新加载配置文件

```
source ~/.bash_profile
```

4.若此时再出现诸如一下问题

```
zsh: command not found: ll
zsh: command not found: la
zsh: command not found: l
```

5.打开文件

```
vim .zshrc
```

6.添加如下命令

```
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
```

7.保存之后使用source .zshrc

## 新增brew命令

安装时会提示安装git 安装好git后重新启动输入命令运行即可（时间比较久）

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

> https://www.mintimate.cn/2020/04/05/Homebrew/ 博客



​	本地软件库列表：brew ls

​    查找软件：brew search google（其中google替换为要查找的软件关键字）

​    查看brew版本：brew -v 更新brew版本：brew update

**现在可以输入命令open ~/.zshrc -e 或者 open ~/.bash_profile -e 整理一下重复的语句(运行 echo $SHELL 可以查看应该打开那一个文件修改)**

<img src="C:\Users\24327\Desktop\csdn博客\Library\Application Support\typora-user-images\image-20201205133049764.png" alt="image-20201205133049764" style="zoom: 50%;" />

## 新增wget 命令

```
brew install wget
```



## 新增rz/sz命令

rz 上传功能    sz 下载功能

```
brew install lrzsz
```

## Mac 提示文件损坏解决方式

> 第一种常见情况：只需要开启允许“任何来源”即可
>
> 1.在终端控制台中输入：sudo spctl --master-disable，回车,如果你的笔记本设置有开机密码，会提示要你输入密码，输入的整个过程中是看不到密码显示的，不要因为看不到输入的密码而着急，继续输入完密码后按下回车键。
>
> 2.打开系统偏好设置——>安全性与隐私，显示了任何来源，然后点击允许来自任何来源。如果没有【任何来源】的选项，可以再次执行刚才的代码进行尝试。
>
> 3.重新双击安装文件便不会再次提示“文件已损坏”了。
>
> 此时有的小伙伴发现依旧会出现“文件已损坏的提示”，此时就需要使用另外一种方式了
>
> 1.打开终端，输入： sudo xattr -r -d com.apple.quarantine，最后面加上一个空格
> 2.然后在访达->应用程序中找到你要打开的软件，拖到终端窗口中，回车执行，就可以正常打开文件了
>
> 
>
> 作者：Sugar_ping
> 链接：https://www.jianshu.com/p/4ad57723a4fc
> 来源：简书
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



## 新增maven

1. 打开配置文件

   ```
   open ~/.bash_profile
   ```

2.

```
MAVEN_HOME=/Users/light6/JavaFile/apache-maven-3.6.3export MAVEN_HOMEexport PATH=$MAVEN_HOME/bin:$PATH
```

3.保存配置

```
source .bash_profile
```

4. 创建/修改.zshrc文件
   如果有.zshrc文件则修改

   ```
   open ~/.zshrctouch ~/.zshrc# 打开后新增配置MAVEN_HOME=/Users/light6/JavaFile/apache-maven-3.6.3export MAVEN_HOMEexport PATH=$MAVEN_HOME/bin:$PATHsource ~/.bash_profilesource ~/.bash_profile
   ```

5.maven修改本地镜像地址

> Conf->settings.xml

```
<mirrors><mirror><id>alimaven</id><mirrorOf>central</mirrorOf><name>aliyun maven</name><url>http://maven.aliyun.com/nexus/content/groups/public/</url></mirror></mirrors>
```



## 新增tomcat环境配置

```
vim ~/.bash_profile # 新增tomcat bin绝对路径export PATH=$PATH:/usr/local/apache-tomcat-8.5.60/binsource ~/.bash_profile
```



## node

```
brew install node
```



## brew 安装vue

> #安装cnpm
>
> npm install -g cnpm --registry=https://registry.npm.taobao.org
>
> #安装脚手架
>
> npm install -g vue-cli



## 安装webpack

> cnpm install webpack -g



## 安装vue脚手架

> npm install -g vue-cli
>
> 创建首个vue项目
>
> 1.在Mac中创建文件夹，名称自己起，然后在终端打开该目录，也可以用vscode 打开，在终端输入：
>
> sudo vue init webpack vue_project
>
> 坐等安装完成。
>
> 2.安装成功后切换到在终端中切换到项目根目录
>
> cd vue_peoject
>
> 3.安装项目依赖，在终端中输入：
>
> sudo npm install
>
> 4.安装依赖完成后，启动项目，在终端或者vscode终端输入：
>
> npm run dev
>
> 5.访问http://localhsot:8080，打开vue项目



## Mac OS 下 Python3 pip 配置国内源

>阿里云 http://mirrors.aliyun.com/pypi/simple/
>中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
>豆瓣 (douban) http://pypi.douban.com/simple/
>清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
>中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
>两种方式使用
>
>安装时指定
>
>~ pip install ipython -i http://mirrors.aliyun.com/pypi/simple/
>
>如果提示 host 不被信任可以加上参数 –trusted-host
>
>~ pip install ipython -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
>
>​       															macOS
>
>~ mkdir .pip   # 在用户根目录（cd~ / cd）下创建一个.pip目录
>~ cd pip
>~ touch pip.conf # 创建一个pip配置文件
>\# 写入配置
>[global]
>index-url = http://mirrors.aliyun.com/pypi/simple/
>[install]
>trusted-host = mirrors.aliyun.com



## hexo安装

### 安装

1.安装完Node.js 及 Git 后，即可使用npm来安装Hexo：

```
$ npm install -g hexo-cli
```



2.创建一个目录用来作为你的blog目录，例如 MyBlog；并在该目录中进行Hexo的初始化

```
hexo init MyBlogcd ~/MyBlog/npm install
```

新建完成后，得到以下目录：

```
·|-- _config.yml|-- package.json|-- scaffolds|-- source|   |-- _drafts|   |-- _posts|-- themes
```

至此完成了Hexo的安装及初始化,下面进行本地的预览

3.安装hexo server

```
sudo npm install hexo-server 
```

4.生成静态页面并打开hexo本地服务

```
hexo generate hexo server
```

依据命令行提示，打开 http://localhost:4000即可看到默认主题的默认页面了。

### 配置git与Github账户关联

1.打开前面创建的MyBlog目录下的 **_config.yml** 文件，在修改最下方的**deploy**为

***==注意，冒号后面一定要加空格==**

```
deploy:  type: git  repo: gihub: https://github.com/[your_account]/[your_accout].github.io.git  branch: master
```

2.安装hexo的git部署，在命令行中执行

```
npm install hexo-deployer-git --save
```

3.将生成静态页面并部署到github的仓库中

```
hexo d -g 或者hexo generatehexo deploy
```

当提示 ** INFO Deploy done: git **即上传成功，这时就可以通过 \**http://[your_account].github.io** 来访问你的个人站点了。

### hexo基本配置

以下是hexo配置文件 **_config.yml** 的基本内容及基本设置，更多个性化设置请参考[官方文档](https://hexo.io/zh-cn/docs/index.html)：

```shell
# Hexo Configuration## Docs: https://hexo.io/docs/configuration.html## Source: https://github.com/hexojs/hexo/# Site  ##页面信息title: Who's Blog  ##标题，即浏览器标签栏显示的内容subtitle: Why so serious?  ##副标题description:        ##描述，简介author: Charles Wei  ##作者language: zh-CN  ##语言timezone: Asia/Shanghai  ##时区# URL## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'url: http://wwww.charleswei.me  ##域名，后面自定义域名后，写在这里，用 .github.io的话，这里用默认的不用改root: /permalink: :year/:month/:day/:title/permalink_defaults:# Directory  ##文件目录，可不改source_dir: sourcepublic_dir: publictag_dir: tagsarchive_dir: archivescategory_dir: categoriescode_dir: downloads/codei18n_dir: :langskip_render:# Writing  ##静态页面生成属性，可不改new_post_name: :year-:month-:day-:title.md # File name of new postsdefault_layout: posttitlecase: false # Transform title into titlecaseexternal_link: true # Open external links in new tabfilename_case: 0render_drafts: falsepost_asset_folder: falserelative_link: falsefuture: truehighlight:   enable: true   line_number: true   auto_detect: false   tab_replace:# Category & Tag ##标签，可不改default_category: uncategorizedcategory_map:tag_map:# Date / Time format  ##时间格式，可不改## Hexo uses Moment.js to parse and display date## You can customize the date format as defined in## http://momentjs.com/docs/#/displaying/format/date_format: YYYY-MM-DDtime_format: HH:mm:ss# Pagination ##每页显示文章数，按需改## Set per_page to 0 to disable paginationper_page: 10pagination_dir: page# Extensions ##主题设置## Plugins: https://hexo.io/plugins/## Themes: https://hexo.io/themes/theme: indigo# Deployment  ##git部署关联## Docs: https://hexo.io/docs/deployment.htmldeploy:   type: git   repo: github: https://github.com/glassweichao/glassweichao.github.io.git  branch: master
```



### 主题配置

Hexo具有高定制的主题效果，你可以从Hexo的[主题库](https://hexo.io/themes/)中选择合适的主题，也可以自己制作。
以我现在使用的[indigo](https://github.com/yscoder/hexo-theme-indigo)主题为例。首先将主题库clone到MyBlog目录下的themes目录：

```bash
git clone git@github.com:yscoder/hexo-theme-indigo.git themes/indigo1
```

安装less，主题使用less作为css预处理工具：

```bash
npm install hexo-renderer-less --save1
```

安装feed,用于生吃RSS：

```bash
npm install hexo-generator-feed --save1
```

安装json-content，用于生成静态站点数据，提供搜索功能的数据源：

```bash
npm install hexo-generator-json-content --save1
```

开启标签页：

```bash
hexo new page tags1
```

修改`MyBlog/source/tags/index.md`的源数据：

```
layout: tagsnoDate: truecomments: false---1234
```

修改hexo配置文件`_config.yml`中的主题标签：

```
theme: indigo1
```

最后修改主题配置文件`MyBlog/themes/indigo/_config.yml`：

```
#添加新菜单项遵循以下规则# menu:#   link: fontawesome图标，省略前缀，本主题前缀为 icon-，必须#   text: About 菜单显示的文字，如果省略即默认与图标一致，首字母会转大写#   url: /about 链接，绝对或相对路径，必须。#   target: _blank 是否跳出，省略则在当前页面打开menu:   home:     text: 主页    url: /   archives:     url: /archives   tags:     url: /tags   github:     url: https://github.com/glassweichao     target: _blank   link:     text: 测试     url: /404rss: /atom.xml#你的头像,替换掉 indigo/source/img/logo.jpg 即可urlavatar: /img/logo.jpg# Contenttags:   title: 标签#是否开启分享share: true#是否开启搜索search: true#是否大屏幕下文章页隐藏导航hideMenu: true#是否开启toc#toc: false  关闭toctoc:   list_number: true # 是否显示数字排序#浏览器标签栏小图标favicon: /favicon.ico1234567891011121314151617181920212223242526272829303132333435363738
```

最后生成部署，来看看效果吧

```bash
hexo cleanhexo d -g
```

## mysql安装

1.brew安装

```shell
brew install mysql
```

2.安装包安装

## anaconda

官网下载 （https://repo.anaconda.com/archive/Anaconda3-2020.11-MacOSX-x86_64.pkg）



创建虚拟环境

> conda create --name DeepLearning python=3  #指定执行版本为python3
>
> conda activate DeepLearning
>
> pip3 install numpy
>
> pip3 install pandas
>
> pip3 install matplotlib
>
> pip3 install Scikit-Learn
>
> pip3 install torch torchvision torchaudio #pytorch 安装
>
> conda info --envs #查看已经安装的环境
