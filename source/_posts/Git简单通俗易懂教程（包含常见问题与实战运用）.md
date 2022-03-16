---
title: Git简单通俗易懂教程（包含常见问题与实战运用）
copyright_author: 刘先森
copyright_author_href: 'https://novoice.top'
copyright_url: 'https://novoice.top'
copyright_info: 此文章版權歸刘先森所有，如有轉載，請註明來自原作者
tags:
  - Git
categories:
  - Git
top_img: 'https://picsum.photos/id/1003/1181/1772'
sticky: 4
copyright: true
cover: 'https://picsum.photos/id/1003/1181/1772'
abbrlink: a1359727
date: 2022-03-16 23:04:12
---

## 1.版本控制

版本控制（Revision control）是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本的软件工程技术。

- 实现跨区域多人协同开发
- 追踪和记载一个或者多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量
- 并行开发、提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担，节省时间，同时降低人为错误

简单说就是用于管理多人协同开发项目的技术。

没有进行版本控制或者版本控制本身缺乏正确的流程管理，在软件开发过程中将会引入很多问题，如软件代码的一致性、软件内容的冗余、软件过程的事物性、软件开发过程中的并发性、软件源代码的安全性，以及软件的整合等问题。

无论是工作还是学习，或者是自己做笔记，都经历过这样一个阶段！我们就迫切需要一个版本控制工具！

<img src="https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0C4qeLxMgoTg9B154ibahsUaibiaV7DgH9GTFQZj3Kyhf5fxrj6G2U5HFg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1" alt="图片" style="zoom:33%;" />



多人开发就必须要使用版本控制！

### 1.1 常见的版本控制工具

我们学习的东西，一定是当下最流行的！

主流的版本控制器有如下这些：

- **Git**
- **SVN**（Subversion）
- **CVS**（Concurrent Versions System）
- **VSS**（Micorosoft Visual SourceSafe）
- **TFS**（Team Foundation Server）
- Visual Studio Online

版本控制产品非常的多（Perforce、Rational ClearCase、RCS（GNU Revision Control System）、Serena Dimention、SVK、BitKeeper、Monotone、Bazaar、Mercurial、SourceGear Vault），现在影响力最大且使用最广泛的是Git与SVN

### 1.2 版本控制分类

**1、本地版本控制**

记录文件每次的更新，可以对每个版本做一个快照，或是记录补丁文件，适合个人用，如RCS。

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Dg3fHrbPqbNEOMO9GTjFhVaukMZWx54icS7eS2x8A7BEu0VB9ibwEhzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2、集中版本控制  SVN**

所有的版本数据都保存在服务器上，协同开发者从服务器上同步更新或上传自己的修改

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p00V4uLaibxtZI9RLpq7tkSdlWiaF92AVeZ0ib9DicqBkS2poo5u8sEU2mCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

所有的版本数据都存在服务器上，用户的本地只有自己以前所同步的版本，如果不连网的话，用户就看不到历史版本，也无法切换版本验证问题，或在不同分支工作。而且，所有数据都保存在单一的服务器上，有很大的风险这个服务器会损坏，这样就会丢失所有的数据，当然可以定期备份。代表产品：SVN、CVS、VSS

**3、分布式版本控制 	Git**

每个人都拥有全部的代码！安全隐患！

所有版本信息仓库全部同步到本地的每个用户，这样就可以在本地查看所有版本历史，可以离线在本地提交，只需在连网时push到相应的服务器或其他用户那里。由于每个用户那里保存的都是所有的版本数据，只要有一个用户的设备没有问题就可以恢复所有的数据，但这增加了本地存储空间的占用。

不会因为服务器损坏或者网络问题，造成不能工作的情况！

<img src="https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0ev8Q7qXjsTfeSwFexdA4tGjFAiaVEKQzAHdGcINXILKflI2cfk9BiawQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1" alt="图片" style="zoom:33%;" />



### 1.3 Git与SVN的主要区别

SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而工作的时候，用的都是自己的电脑，所以首先要从中央服务器得到最新的版本，然后工作，完成工作后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，对网络带宽要求较高。

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0qtEIDr2NG6rOGg1UgDu5c3ffRR8P7FD5D8BPLUEXp0hQoL7qfp3I6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Git是分布式版本控制系统，没有中央服务器，每个人的电脑就是一个完整的版本库，工作的时候不需要联网了，因为版本都在自己电脑上。协同的方法是这样的：比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。Git可以直接看到更新了哪些代码和文件！

**Git是目前世界上最先进的分布式版本控制系统。**



## 2.Git历史



同生活中的许多伟大事物一样，Git 诞生于一个极富纷争大举创新的年代。

Linux 内核开源项目有着为数众广的参与者。绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上(1991－2002年间)。到 2002 年，整个项目组开始启用一个专有的分布式版本控制系统 BitKeeper 来管理和维护代码。

Linux社区中存在很多的大佬！破解研究 BitKeeper ！

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。这就迫使 Linux 开源社区(特别是 Linux 的缔造者 Linus Torvalds)基于使用 BitKeeper 时的经验教训，开发出自己的版本系统。（2周左右！） 也就是后来的 Git！

**Git是目前世界上最先进的分布式版本控制系统。**

Git是免费、开源的，最初Git是为辅助 Linux 内核开发的，来替代 BitKeeper！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0XGLbyFDUiccCsib4L9Vkg7neJVWupfScbrjd7zm7apC8eYTzgQztNAnA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Linux和Git之父李纳斯·托沃兹（Linus Benedic Torvalds）1969、芬兰



## 3.Git环境配置

### 3.1 软件下载

打开 [git官网] https://git-scm.com/，下载git对应操作系统的版本。

所有东西下载慢的话就可以去找镜像！

官网下载太慢，我们可以使用淘宝镜像下载：http://npm.taobao.org/mirrors/git-for-windows/

<img src="https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0IXktseBR7lpvVF4bibFwiaibnGxkDm0wYicPIiaZxcUe2KuibAHj83MiaWFSQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1" alt="图片" style="zoom:50%;" />

下载对应的版本即可安装！

安装：无脑下一步即可！安装完毕就可以使用了！

### 3.2 启动Git

安装成功后在开始菜单中会有Git项，菜单下有3个程序：任意文件夹下右键也可以看到对应的程序！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0jaiaAfr2pAfWtFX57kGYqR3SlNxDlAZDkCU6IOB1YAicKxHib5yGbv9zQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Git Bash：**Unix与Linux风格的命令行，使用最多，推荐最多

**Git CMD：**Windows风格的命令行

**Git GUI**：图形界面的Git，不建议初学者使用，尽量先熟悉常用命令

### 3.3 常用的Linux命令

平时一定要多使用这些基础的命令！

1）、cd : 改变目录。

2）、cd . . 回退到上一个目录，直接cd进入默认目录

3）、pwd : 显示当前所在的目录路径。

4）、ls(ll):  都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

6）、rm:  删除一个文件, rm index.js 就会把index.js文件删除。

7）、mkdir:  新建一个目录,就是新建一个文件夹。

8）、rm -r :  删除一个文件夹, rm -r src 删除src目录

```
rm -rf / 切勿在Linux中尝试！删除电脑中全部文件！
```

9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。

10）、reset 重新初始化终端/清屏。

11）、clear 清屏。

12）、history 查看命令历史。

13）、help 帮助。

14）、exit 退出。

15）、#表示注释

### 3.4 Git配置

所有的配置文件，其实都保存在本地！

查看配置 git config -l

![image-20220316132927949](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316132927949.png)

查看不同级别的配置文件：

```git
#查看系统config
git config --system --list　　
#查看当前用户（global）配置
git config --global  --list
```



![image-20220316133052840](/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316133052840.png)

### **3.5 Git相关的配置文件：**

1）、Git\etc\gitconfig  ：Git 安装目录下的 gitconfig   --system 系统级

2）、C:\Users\Administrator\ .gitconfig   只适用于当前登录用户的配置  --global 全局

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0hcJS0rxj3qoCVvfDKh3WxwQJlSV3P15EIZuejraOwXLdic6NCB8X8oQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里可以直接编辑配置文件，通过命令设置后会响应到这里。

### 3.6 设置用户名与邮箱（用户标识，必要）

当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：

```
git config --global user.name "liuhuanhuan963019"  #名称
git config --global user.email 2432783449@qq.com   #邮箱
```

只需要做一次这个设置，如果你传递了--global 选项，因为Git将总是会使用该信息来处理你在系统中所做的一切操作。如果你希望在一个特定的项目中使用不同的名称或e-mail地址，你可以在该项目中运行该命令而不要--global选项。总之--global为全局配置，不加为某个项目的特定配置。

## 4.Git基本理论

### 4.1 三个区域

Git本地有三个工作区域：工作目录（Working Directory）、暂存区(Stage/Index)、资源库(Repository或Git Directory)。如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0NJ4L9OPI9ia1MmibpvDd6cSddBdvrlbdEtyEOrh4CKnWVibyfCHa3lzXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

<font color="red">我们先在本地目录进行修改，然后add file到我们的缓冲区当中来，然后再提交到我们的本地资源库当中来，最后再通过push,将本地仓库的代码再push到远程服务端</font>

本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0icz6X2aibIgUWzHxtwX8kicPCKpDrsiaPzZk04OlI2bzlydzicBuXTJvLEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- Directory：使用Git管理的一个目录，也就是一个仓库，包含我们的工作空间和Git的管理空间。
- WorkSpace：需要通过Git进行版本控制的目录和文件，这些目录和文件组成了工作空间。
- .git：存放Git管理信息的目录，初始化仓库的时候自动创建。
- Index/Stage：暂存区，或者叫待提交更新区，在提交进入repo之前，我们可以把所有的更新放在暂存区。
- Local Repo：本地仓库，一个存放在本地的版本库；HEAD会只是当前的开发分支（branch）。
- Stash：隐藏，是一个工作状态保存栈，用于保存/恢复WorkSpace中的临时状态。

### 4.2 工作流程

git的工作流程一般是这样的：

１、在工作目录中添加、修改文件；

２、将需要进行版本管理的文件放入暂存区域；

３、将暂存区域的文件提交到git仓库。

因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p09iaOhl0dACfLrMwNbDzucGQ30s3HnsiaczfcR6dC9OehicuwibKuHjRlzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



## 5.Git项目搭建

### 5.1 创建工作目录与常用指令

工作目录（WorkSpace)一般就是你希望Git帮助你管理的文件夹，可以是你项目的目录，也可以是一个空目录，建议不要有中文。

日常使用只要记住下图6个命令：

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0AII6YVooUzibpibzJnoOHHXUsL3f9DqA4horUibfcpEZ88Oyf2gQQNR6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 5.2 本地仓库搭建

创建本地仓库的方法有两种：一种是创建全新的仓库，另一种是克隆远程仓库。

1、创建全新的仓库，需要用GIT管理的项目的根目录执行：

```
# 在当前目录新建一个Git代码库
$ git init
```

2、执行后可以看到，仅仅在项目目录多出了一个.git目录，关于版本等的所有信息都在这个目录里面。

### 5.3 克隆远程仓库

1、另一种方式是克隆远程目录，由于是将远程服务器上的仓库完全镜像一份至本地！

```
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url]  # https://gitee.com/kuangstudy/openclass.git
```

2、去 gitee 或者 github 上克隆一个测试！

## 6.Git文件操作

### 6.1文件的四种状态

版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件
- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !
- Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

### 6.2 查看文件状态

上面说文件有4种状态，通过如下命令可以查看到文件的状态：

```
#查看指定文件状态git status [filename]
#查看所有文件状态git status
# git add .                  添加所有文件到暂存区
# git commit -m "消息内容"    提交暂存区中的内容到本地仓库 -m 提交信息
```

### 6.3 忽略文件

有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。
2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。
3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。
4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。

```
#为注释*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录
tempbuild/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

### 6.4 使用码云

> github 是有墙的，比较慢，在国内的话，我们一般使用 gitee ，公司中有时候会搭建自己的gitlab服务器

这个其实可以作为大家未来找工作的一个重要信息！

1、注册登录码云，完善个人信息

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0ebAqhteskG4GHwD01bX4lXYmxlmMGn8PRqn4aCXfaQdp3SnbBHdibtQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、设置本机绑定SSH公钥，实现免密码登录！（免密码登录，这一步挺重要的，码云是远程仓库，我们是平时工作在本地仓库！)

```
# 进入 C:\Users\Administrator\.ssh 目录
# 生成公钥ssh-keygen
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0YlK4ibQ0EMs3LmRmdiahpma8ssTQedkhyShNkibTyFBvaZWicicTfNicWQIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3、将公钥信息public key 添加到码云账户中即可！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0I5Zicrm4PEbnox9L5wjCPtPybCyrKI1JOkRWCYIY5zsX4FvI77LXXmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

4、使用码云创建一个自己的仓库！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0FSIwJb9g6Qbp99jY605xdPfh3N4l2rGpD44d6NCcdibankBUL60uODg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

许可证：开源是否可以随意转载，开源但是不能商业使用，不能转载，...  限制！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0S96XfGogNWVqRAexeybT7DXdyQhfcYJ1oEAgaH1RibRU0WZE0eczdxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

克隆到本地！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0PyKfGFd8UHSGIRbVLkXH5icQsgxh6K2RPibYeUER54UzuNVAYsgxXcfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)







## 7.使用码云

> github 是有墙的，比较慢，在内的话，我们一般使用 gitee ，公司中有时候会搭建自己的gitlab服务器

这个其实可以作为大家未来找工作的一个重要信息！

1、注册登录码云，完善个人信息

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0ebAqhteskG4GHwD01bX4lXYmxlmMGn8PRqn4aCXfaQdp3SnbBHdibtQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、设置本机绑定SSH公钥，实现免密码登录！（免密码登录，这一步挺重要的，码云是远程仓库，我们是平时工作在本地仓库！)

- 
- 
- 

```
# 进入 C:\Users\Administrator\.ssh 目录# 生成公钥ssh-keygen
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0YlK4ibQ0EMs3LmRmdiahpma8ssTQedkhyShNkibTyFBvaZWicicTfNicWQIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3、将公钥信息public key 添加到码云账户中即可！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0I5Zicrm4PEbnox9L5wjCPtPybCyrKI1JOkRWCYIY5zsX4FvI77LXXmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

4、使用码云创建一个自己的仓库！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0FSIwJb9g6Qbp99jY605xdPfh3N4l2rGpD44d6NCcdibankBUL60uODg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

许可证：开源是否可以随意转载，开源但是不能商业使用，不能转载，...  限制！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0S96XfGogNWVqRAexeybT7DXdyQhfcYJ1oEAgaH1RibRU0WZE0eczdxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

克隆到本地！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0PyKfGFd8UHSGIRbVLkXH5icQsgxh6K2RPibYeUER54UzuNVAYsgxXcfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



## 8.Idea中集成Git

1、新建项目，绑定git。

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0D8LPGu2SNKXD01IMqDaSkBeP8ibtvnasBYiaReyuZWAl0EjEib8IYf7cQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注意观察idea中的变化

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Cs93BiaOia1Sdk8icdH7vQzPfzIjuoTNYquKzYtrEe5mklhg2b7KOYsow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、修改文件，使用IDEA操作git。

- 添加到暂存区
- commit 提交
- push到远程仓库

3、提交测试

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0tERIszdgLVlUWamyRapfN74aR8XeGFV2OYWiaeR9CkYlfoBefRh2AIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这些都是单个人的操作！

学习的方式最重要！学会学习！我上课的更多时候都是在教大家去学习一种理念和思想（学习方式）

有道无术、术尚可求。有术无道、止于术！

真正的教学，授人以渔！

## 9.<font color="red">说明</font>>：Git分支

分支在GIT中相对较难，分支就是科幻电影里面的平行宇宙，如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，我们就需要处理一些问题了！

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0BOGzaG4QTc4JXO0hSlwcNtujNzAvxeibSrajLYLCT6otNnHDV9xYWwA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Ayn87woxfepOhSlUj4FQTFUsia4ic0j6aQy4Tz32PRuJ0HSVeGeUzURA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

git分支中常用指令：

```
# 列出所有本地分支git branch
# 列出所有远程分支git branch -r
# 新建一个分支，但依然停留在当前分支git branch [branch-name]
# 新建一个分支，并切换到该分支git checkout -b [branch]
# 合并指定分支到当前分支$ git merge [branch]
# 删除分支$ git branch -d [branch-name]
# 删除远程分支$ git push origin --delete [branch-name]$ git branch -dr [remote/branch]
```

IDEA中操作

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0wHNIYeTHC8aHGASoDyZO64QicslqiaMb1OJ1Z1LPoic3LBGyDIYBa7XXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。

作业练习：找一个小伙伴，一起搭建一个远程仓库，来练习Git！

1、不要把Git想的很难，工作中多练习使用就自然而然的会了！

2、Git的学习也十分多，看完我的Git教程之后，可以多去思考，总结到自己博客！

## 10.如何使用 GitHub Flow 给开源项目贡献代码

### 10.1 **复制（Fork）一个仓库副本**

![image-20220316150124479](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316150124479.png)

等待的时间视仓库的大小而定。

在 `fork` 完成后，你应该可以在你自己的 GitHub 仓库看到同名的一个项目。

它的 URL 应该为： `https://github.com/yourname/go`。

![image-20220316150124479](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316150124479.png)

发现了吗？这里 URL 的变化只不过是将原本的 `golang` 替换成了 `yourname`。

这个 `fork` 后的项目是你自己可以随意修改而不会影响到真正的 go 项目的。下面我们把它称之为副本仓库。

在没有示例仓库的 `push` 权限的情况下，想要做出的修改能够反映到示例仓库，也就是原始仓库，还需要做接下来的一些操作。

把你 `fork` 后的副本仓库 `clone` 到本地。

```shell
git clone https://github.com/liuhuanhuan963019/go.git
```

**使用分支 (branch)**

进入仓库目录后，可以使用如下命令创建并切换到 `test` 分支。

```
git checkout -b test     	# 创建并切换到 test 分支
```

**在本地仓库提交 (commit)**

在这个 `test` 分支下经过一些修改后，你需要提交这些修改到本地仓库。

```shell
git add .
git commit -m "add branch test"
```

先别急着 `push`，我们还有个大问题要解决。

**跟原始仓库 (upstream)合并**

前面已经说过，在副本仓库做的修改是不会影响到原始仓库的。同样，在原始仓库的更新也不会反映到副本仓库来。

在 GitHub，如果你副本仓库的进度落后于原始仓库还坚持发起 `PullRequest`，后果只会是被拒绝。

那么问题来了，我们应该如何同步原始仓库的更新呢？

答案是：区别于 `origin`，它是用来向副本仓库提交更新的远程仓库；我们添加一个 `upstream`，也被称为 上游 是专门用来同步原始仓库更新的远程仓库。

在默认情况下，在你 `clone` 后的仓库目录里，git 已经自动将 `origin` 和你的副本仓库关联在一起了，也就是 `https://github.com/yourname/go`。

```shell
git remote -v
```

然后，通过如下命令添加这个 `upstream`，使用这个名字只是约定俗成，你可以用你觉得更好的名字来替换它。 

```shell
git remote add upstream git@github.com:golang/go.git       
# 添加 upstream 远程仓库
```

现在，我们假设在做出修改后，上游（upstream）已经更新了很多提交。

此时如果对上游的变化视而不见，强行 `push` 并发起 `PullRequest` 还是会被拒绝。

可以通过如下命令拉取并合并上游的更新：

```shell
git checkout master  
# 切换到默认存在的 master 分支
git pull --rebase upstream master:master  
# 使用 rebase 模式拉取 upstream/master 上的更新
# 且与本地的 master 合并。第一个 master 是远程分支，第二个是本地分支。
git checkout test  
# 切换到前面建立的 test 分支
git rebase master  
# 使用 rebase 模式合并本地的 test 和 master 分支
```

也可以使用另外一种方式：

```shell
git checkout master  
# 切换到 master 分支

git fetch upstream master  
# 获取 upstream 上的 master 分支

git checkout test

git rebase upstream/master  
# 使用 rebase 模式合并本地的 test 和 upstream/master 分支
```

总的来说，可以把本地的 `master` 分支当作一个只负责从上游获取更新的分支，所有本地的改动都不会直接在 `master` 上面进行。

而是先将上游的 `master` 和本地的 `master` 合并，此时，本地的 `master` 是上游的最新版本；

再通过合并 `test` 和本地的 `master` 来完成本地改动的更新。整个过程在未开始合并之前，你的代码更新应该只会出现在 `test` 分支上。

> 注意：在使用 git rebase 相关的命令时，需要谨慎应用在已经提交的更新或远程仓库上

**推送 (push)到副本仓库**

现在，我们已经完成代码的修改、上游的同步更新并且完成了合并。

接下来应该将代码 push 到副本仓库。

```
git push origin test   # 将本地 test 分支的代码 push 到 origin 的 test 分支# 如果该分支不存在则会创建
```

这个 `push` 只会更新副本仓库，并不会影响到原始仓库。

要将代码贡献到原始仓库，还要发起 `PullRequest`。

**发起合并请求 (Pull Request)**

现代的 GitHub 网站已经为我们发起 `PullRequest` 做了大多数的幕后工作。下面分别说明两种方法：

- 在 `push` 代码后，直接登录到 GitHub 网站，它会智能识别并弹出按钮 `Compare&pull request`，点击后填写一些信息即可发起。 

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzr7jjwL1t19amVkYmV0b6rqia8Av6Douyju6HwWIe6woXcYQ39SBugj2lZpLgaaPibBUxveycCAtQ2w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 还有一种方式，在副本仓库的页面点击你更新的分支，再点击 `Newpull Request`。

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzr7jjwL1t19amVkYmV0b6rqyElria9WApmdc7icDTiaicD4arEXTfibUy0NDksIS7X0GoibtRO2PaaS5A3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

出现如下界面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzr7jjwL1t19amVkYmV0b6rqlfx20uInotoUhew1SH3dCWAKiaE3kxrrgmSV6mphXb7EtSJRnMKwANQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

再点击 Create pull request 后填写一些信息即可。

接下来，原始项目的相关负责人就会审查（ `review`）你的提交，并决定是通过还是拒绝。

- 当你的提交有问题时，负责人还会让你做出一些修改才给予通过。
- 当你发现想要对其贡献代码的开源项目已经很久没有更新时，需要谨慎一些。否则会发现在你发起 `PullRequest` 后无人理会，做了许多无谓的工作。发生这种情况可能是负责人已经放弃了这个项目。 

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzr7jjwL1t19amVkYmV0b6rqA4OZPf8O5Wxz7SblZED9H2RicqW0bpCMZjj3zjrqbT5nB1p2Iff9W0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此，我们已经完成使用 GitHub Flow 向开源项目贡献代码的全部步骤。



## 11.Git分支合并rebase和merge的用法

一般在我们的开发过程中，我们会新建分支，比如dev，test等环境进行开发，master分支的代码作为稳定版本，一般不做修改，在我们进行更改完dev等分支的代码后，作为一个成熟的dev。我们需要将我们dev的代码合并到我们的主分支上面，此时我们就有两种操作的方式，下面，我们来介绍第一种方式，我们先新建一个项目。然后来进行修改。我们先将我们创建的项目放入到我们的git中，上传到远程仓库，然后再进行操作。我们依次执行如下的命令

### 11.1 merge合并分支

```shell
git init    #初始化仓库
git add .   #上传我们的代码到本地缓冲区
git commit -m "first commit"   #提交缓冲区的代码到我们本地的资源库
git remote add origin https://gitee.com/liuhuanhuan963019/docker-compose-demo.git   #创建我们的remote节点
git push -u origin master    #将本地资源库中的代码的提交到远程服务器的master分支
```

此时我们在本地进行此时

```shell
git branch    #查看当前分支
```

![image-20220316160253215](/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316160253215.png)

此时我们只有一个分支，我们现在新建一个分支，并且切换到新分支上面

```shell
git checkout -b dev
git branch 
```

![image-20220316160611549](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316160611549.png)

此时我们发现，我们已经新建了一个分支，并且切换到了我们原来的分支，我们来看下日志部分

```shell
git log --oneline -5
```

![image-20220316160921009](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316160921009.png)

我们当前日志显示我们没有任何提交记录，此时我们再切换到master分支看下

![image-20220316161029982](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316161029982.png)

```shell
git checkout master
git log --oneline -5
```

此时也是没有任何提交记录的

此时我们再切换到dev分支，然后做一些改变，我们测试下

我们通过`git status`可以查看到，当前分支下我们新增了一个文件。此时我们来讲这个文件提交上去

![image-20220316161310277](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316161310277.png)

![image-20220316161554069](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316161554069.png)

此时我们的日志部分发生了一些改变，我们的刚刚提交的记录已经存在了，此时我们不着急push，我们来看下maser分支。我们切换到maste分支之后，我们来看下，我们本地的log没有发生变化，那么我们就进行最重要的一步了，将我们dev分支的代码merge到我们的主分支上

![image-20220316161808814](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316161808814.png)

```shell
#在master分支上进行merge操作
git merger dev
```

此时我们再来看下日志部分

![image-20220316161944876](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316161944876.png)

此时我们惊奇的发现，dev分支新增的代码，也已经上传到我们master分支上面了，而且我们还提交了。这时候，我们进行远程仓库的提交看看。

```shell
git push 
```

我们去远程仓库看下，最后的结果

![image-20220316162150735](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316162150735.png)

此时我们发现，我们代码已经提交成功了，那么此时我们也可以将我们的dev分支删除掉，（因为这个dev是我们创建的一个临时的分支）

通过`git branch -d dev`的，命令，我们就可以删除掉本地的分支了，具体如下图所示。以上就我们分支代码合并merge使用的全过程了。下面我们介绍另外一种方式rebase

![image-20220316162350080](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316162350080.png)

那么我们如果想要讲我们的新分支改动之后，再上传呢？，并且将我们的这个分支上传到远程仓库，我们需要怎么做呢？

![image-20220316163433688](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316163433688.png)

此时我们已经修改好我们的代码了，并且已经准备上传了，但是此时出现了问题，。在我们push的时候，提示了如下的错误。

![image-20220316163521007](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316163521007.png)

这就是提醒我们没有上游的branch，我们需要执行如下的代码，

```shell
git remote add dev xxxxxxx
```

或者直接执行如下代码

```shell
 git push --set-upstream origin dev
```

此时我们的代码成功提交了

![image-20220316163713872](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316163713872.png)

我们去远程仓库看下，是否有dev分支的提交呢

![image-20220316163744314](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316163744314.png)

此时我们发现，我们已经成功提交了，我们的代码。

当然我们也可以通过git remote的方式进行提交，这里就不演示了 我们等到rebase的时候，我们再进行讲解



### 11.2 rebase

#### 11.2.1 压缩分支

当前rebasee是不仅只有分支合并这一个作用，他也可以对我们的代码提交进行压缩提交。此时有一个场景，我们commit了三次代码，这三次修改，可能我们操作的文件都是一样，如下图所示。

<img src="/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316165347210.png" alt="image-20220316165347210" style="zoom:50%;" />

此时我们进行了3次提交，分别在test.txt文件中新增1 ，2 ，3 即是我们对test,txt的单独操作，那么我们看到我们的日志栏，出现了3个，那么我们这是对同一个文件的操作，为了使我们的git分支树看起来没那么粗糙，我们是否可以将3次提交转换为1次提交呢？这时候rebase的作用就来，我们可以在命令行输入

```shell
git rebase -i HEAD~~~~  
```

git rebaser -i 后面加上我们要提交的几个版本,几个波浪线就代表的是几次提交，当然也可以是HEAD~3这样也表示的是3次提交

然后依次进行修改即课。

输入命令后会出现如下所示：

<img src="/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316174831193.png" alt="image-20220316174831193" style="zoom:50%;" />

我们修改成如下即可：

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316174912114.png" alt="image-20220316174912114" style="zoom:50%;" />

然后:wq 后退出保存，此时页面会来到如下样子：

![image-20220316175013985](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316175013985.png)

此时我们修改下，然后保存退出后，再打开我们的git命令行看下:此时3个分支，已经压缩成一个分支了。

![image-20220316180006317](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316180006317.png)

当然我们也可以使用idea自带的工具进行提交：，我们看下此时的状态：我们又提交了一个新的记录，我们将这几个记录压缩到631这个记录上面。

![image-20220316180058617](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316180058617.png)



选中631这个分支。然后右击。<img src="/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316180154991.png" alt="image-20220316180154991" style="zoom:50%;" />

选中我们想要压缩的记录，然后会提示我们是否更改名字，此时。我们就修改成功了



![image-20220316180228270](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316180228270.png)





<img src="/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316180330254.png" alt="image-20220316180330254" style="zoom:50%;" />

此时我们就全部压缩好了。

![image-20220316180349589](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316180349589.png)



#### 11.2.2 分支合并

一般我们接收到一个项目的时候，我们都会主动的去切换分支进行编写代码。我们此时切换一个新的分支来进行操作。

```shell
git checkout -b test
```

![image-20220316180945899](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316180945899.png)

然后我们开进行开发：如果此时我们更改了文件，又需要我们切换分支的时候，一定要先讲本分支的代码commit,不然很容易引起冲突。

此时我们可有commit and push来进行操作。

![image-20220316181650661](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316181650661.png)

此时看下我们的分支是比较乱的，此时我们将dev和新建的分支进行合并看看。

![image-20220316181937894](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316181937894.png)

此时我们进行merge的时候会有一些变化，因为我们修改的是同一个文件，所以文件merge的时候会有一些冲突，我们修改玩之后，我们重新提交。

```shell
git add .
git commit -m "first commit"
git push
```

此时我们的代码又重新提交到了我们的dev分支，如下图。

<img src="/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316182139197.png" alt="image-20220316182139197" style="zoom:50%;" />

此时我们有重新新建一个分支来继续完成任务。

```shell
git checkout -b test2
```

我们编写下文件，然后push提交

然后再切换分支到我们的dev分支，再编写文档，再push.此时我们看下我们的git 分支线。

![image-20220316182729507](/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316182729507.png)

此时我们回到test2分支，继续去完成我们的工作。然后提交代码push远程分支：

现在我们未来防止我们之前合并分支的时候产生冲突的问题，我们此时可以使用rebase来进行操作。此时我们发现，我们在dev进行的操作，已经合并到我们的test2分支上了，然后我们再进行切换到dev分支，然后merge我们的代码，此时没有任何代码冲突，即使我们修改了同一个文件，这就是rebase帮助我们解决的问题

```shell
git rebase dev
```



<img src="/Users/liuhuanhuan/blog/source/_posts/C:/Users/lhh/AppData/Roaming/Typora/typora-user-images/image-20220316183053411.png" alt="image-20220316183053411" style="zoom:50%;" />

此时我们发现是没有任何冲突，所以我们此时能够正常的看到我们分支的合并。以下就是我们操作的视频链接地址。

<p align="center">
<iframe src="//player.bilibili.com/player.html?bvid=BV1Ur4y1q7xB&p=4&as_wide=1&high_quality=1&danmaku=1" allowfullscreen="true" width="100%" height="450" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>
</p>
<p align="center">
<iframe src="//player.bilibili.com/player.html?bvid=BV1cv411u7wd&p=4&as_wide=1&high_quality=1&danmaku=1" allowfullscreen="true" width="100%" height="450" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>
</p>

### 11.3 rebase和merge的区别

`Merge`和`Rebase`是合并两个分支的操作。都是checkout到某个分支上，然后把别的分支合并到该分支。

其中Merge在没有分叉的情况下，会自动使用fast-forward的方式，快速移动：

![image-20220316190729557](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316190729557.png)

merge在有分叉的情况下，会产生一个新的提交点（--no off）他就是别的分支多次commit的合并。

![image-20220316191154825](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316191154825.png)



Rebase叫做变基。也是把别的认知合到自己身上。但是效果就好像在基的基础上重新提交自己的多次commit,看起来就好像重新从基抽出来一次。

![image-20220316191818971](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316191818971.png)



异同：

- 作用大体想用，都是把别的分支合到自己身上，别的分支不会发生改变，改变的是自己。

- 效果有些不同。

  对于merge branch，它是把branch的多次提交合成一个commit.然后加在自己的分支的后面。（2-3-6） 6就是4和5合成的一个新的提交点、自己提交（45）在前面。别人的合并在后面

  ![image-20220316192139093](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316192139093.png)

  对于rebase Branch，它就好像在branch的基础上，重新提交自己的多次commit,(4-5-2-3 )看起来就好像重新从基中抽出来一次，自己的提交总是在最后面，而且不会多出一个提交点。

![image-20220316192914077](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316192914077.png)

**使用场景不同：**

1.当我们在分支future上新增了新的功能时，我们直接在主分支master上merge一下future，就把新功能加上去了（future是否继续开发无所谓）。

2.当我么会在功能分支shang future上进行开发，再次提交。这个过程中，有人动了主分支master你要要吧这个更改同步到你的future分支上，选择rebase master，这样的 话，在master上改动的commit会自动加到我们future的上面，在开发分支上rebase主分支，主要是为了让当前的分支的代码和主分支代码同步。

3.当前也可以选择在功能future上，merge别的分支。这时候别的分支的commits。就作为一个新的提交点跑到你的多次提交的后面了。

4，切记不要再公共分支master上rebase.因为rebase之后，master上的多次提交会被顶到别的分支后面，这就相当于改变了历史。

总结来说：

1.公共分支上选择Merge(将新功能整个到master上)

2，功能分支上选择rebase主分支（和公共分支同步，把自己的提交顶到最后面）

3.功能分支上选择merge(把别的分支的功能加到自己身上，如果不介意顺序的话)

4.切记不要再公共分支上rebase任何分支。

- **优缺点**：在适合的场景使用适合的方式（1.2）对于3这种情况，比如你要把future开发分支上的新功能导入到test测试分支里面去，你可以切到test，然后merge一下future因为测试分支，你没有必要把分必要把test的提交顶到最后面，你就可以选择merge。而且多出一个节点，用于记录，这是merge的小优点。当然也可以选择rebase一下future。这样的话，你test分支上的多次commit就还是在最后面的，便于你回退，这是rebase的优点





<font color="red" size="6px">特别说明：</font>

当我们从远端origin/master拉取（pull）的时候，或者在pycharm，idea里面选择uodateprojcet的时候，它总是提示你选择merge还是rebase

![image-20220316194643435](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20220316194643435.png)

我就一个分支啊，远程也是一个分支，怎么就涉及到合并分支呢。其实是：git有本地仓库的概念，本地的master是一个仓库，远程的master也是一个仓库，git pull = git fetch+git merge.也就是说，这里让你选择的是，将远程的master拉取下来之后，如何和你本地的master进行合并?

我们推荐使用rebase。站在你本地master分支上，rebase一下远程master.这样的话，你刚刚在本地master所做的多个提交，依然会被钉在你本地master分支的最后面，便于你回退。

rebase：合并后分支图谱好看，一条线，但合并过程中出现冲突的话，比较麻烦（rebase过程中，一个commit出现冲突，下一个commit也极有可能出现冲突，一次rebase可能要解决多次冲突）；
		merge：合并后分支图谱不好看，一堆线交错，但合并有冲突的话，只要解一次就行了；

参考博客：[git merge 与 git rebase的区别_Michaelliu_dev的博客-CSDN博客_merge rebase](https://blog.csdn.net/michaelshare/article/details/79108233?app_version=5.1.1)

## 12.git 进行版本回退



### 12.1 利用符号进行版本回退

1）、回退到上一个版本

```shell
git reset --hard HEAD^
```

2）、回退到上上个版本

```shell
git reset --hard HEAD^^
```

（3）、回退至上`n`个版本

```shell
git reset --hard HEAD~n
```

备注：n是代表往上几个版本，并且是具体的数字，比如往上一个版本的话n=1，往上两个版本的话n=2，以此类推，往上100个版本的话n=100

### 12.2 利用版本号进行回退版本

### 2、利用版本号进行回退版本

首先获取版本号：

```shell
git reflog
```

例如：![在这里插入图片描述](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/20200417115233640.png)



进行版本回退操作：

```java
git reset --hard 版本号
```

例如：
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/20200417115233640.png)

## 13.如何在同一台电脑上同时使用多个Git账号？

### 13.1 思路

同时管理多个SSH key。

### 13.2 解决方案

#### 13.2.1 **生成多个SSH key**

这里使用`one`、`two`两个账户进行举例。

**注意：** 在生成多个`SSH key`的时候一定要在`~/.ssh`目录下进行，否则生成的`SSH key`不会在`~/.ssh`目录下，所以以下有操作都是在`~/.ssh`目录下进行的。在生成之前尽量删除此目录下的所有文件再进行，以免出现不必要的问题。

```
ssh-keygen -t rsa -C "one@email.com"
ssh-keygen -t rsa -C "two@email.com"
```

复制代码再输入命令行的时候在第一次提示`Enter file in which to save the key`的时候对`ssh`文件进行重命名（`idrsaone`和`idrsatwo`），这样就会生成如下目录中的四个文件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrvicG1WZZmQ0R5Q8ovz7yqDxCC0yC2TicXFp8YBQNxth8f352fyQsSYMyBe57wBlhqLZoKIsiaOrSgA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

即两份包含私钥和公钥的`4`个文件。

------

#### **13.2.2获取密钥**

```
cat ~/.ssh/id_rsa_one.pub
cat ~/.ssh/id_rsa_two.pub
```

其中`idrsaone.pub`和`idrsatwo.pub`就是上面对`ssh`文件重命名的文件名。

有了这个密钥，你就可以将其添加到你所需要用的平台上去。

#### **13.2.3创建config文件**

在`~/.ssh`目录下创建一个`config`文件

```
touch config
```

这样就会在`~/.ssh`目录下生成一个空的`config`文件，然后我们在文件中添加以下内容：

```
# git server one
Host one.aliyun.com #别名
Hostname code.aliyun.com #真实域名
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_one #ssh 文件路径
User one

#git server two
Host two.aliyun.com
Hostname code.aliyun.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_two
User two
```

#### **13.2.4远程测试**

```
ssh –T one.aliyun.com
ssh –T two.aliyun.com
```

#### **13.2.5 使 用**

比如`clone`到本地

原来的写法：

```
git clone git@code.aliyun.com:项目路径.git
```

现在的写法：

```
git clone git@one.github.com:项目路径.git
git clone git@two.github.com:项目路径.git
```

给仓库设置局部用户名和邮箱

```
git config user.name "one_name"; git config user.email "one_email"
git config user.name "two_name"; git config user.email "two_email"
```

## 14.一招搞定GitHub下载加速！

### **一个痛点**

众所周知，GitHub是一个巨大的开源宝库，以及程序员和编程爱好者的聚集地，包括我之前推荐的诸多优秀的开源项目全部都是位于GitHub上。

但是每当我们看到优秀的开源项目，准备去**下（bai）载（piao）**时，会发现 `git clone`的速度异常之慢！就我个人而言，在我家里200M移动宽带的环境下，我克隆开源项目就没发现速度大于过 `20.00KiB/s`的时候，这简直太难受了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNB8qf2qvJHnkHJZsGtGOBm3W0HqBaYicQQ7DFwWfkGQGZQNdBmuVC2Yg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

小项目倒还好，我等几分钟无所谓；一旦项目庞大起来，或者项目文件数目一多， `git clone` 大概率会失败！

当然网上常见的诸如修改hosts、代理等方式实际使用效果并不一定好，而且也不稳定。

------

### **“码云”是个好东西**

接下来就介绍一种GitHub下载的加速方法：通过国内**码云平台**的转接，来完成GitHub上项目的下载加速。

> 感谢公众号小伙伴ioc提供思路

**（1）首先确保码云上有账户，可以正常使用，没有的可以自行注册一下。**

**（2）点击右上角新建仓库的加号 `+`，选择“从 `GitHub/GitLab`导入仓库”菜单**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNuxDta6zrnRY62TUCX4blM8Eaw0EiabKh9YnculvcIpujPdztzum9Ang/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**（3）然后填写位于 `GitHub`上你想 `clone`的仓库地址并导入**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicN4jkGsI7gGEDP8VxGNNxGPkLia4oNzANkia5JTZcUibeDAYib5iblOW48Fjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这一步**交给码云来做**速度是非常快的，一会儿功夫，码云就克隆出了一份和GitHub上一模一样的项目！

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNn7GaKBJP0icPH9PwdycibxUJvshX886Iyu7jJN2AbJ3m5Y9xhXdcsXBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**（4）接下来我们通过码云上的项目地址，将项目 `clone`到本地，这时候的clone速度就很快了，几 `MB/s`的速度是没问题的，很快项目就下载下来了。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNAD6nFlqorfqAw8icuZicnEhgFmOWyprlw5WJ7sicDLAoibH5rJKX88Mhug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按道理讲这时候我们的目的已经达到了，不过不要忘了，还有一件事没做。

------

### **重新关联远端地址**

要知道，这时候克隆到本地的项目关联的是码云Gitee的地址，已经和原来的GitHub项目**完全脱离了**，是另外一个**副本**。

在必要情况下（比如我们就是要给GitHub上的某个项目提 `PR`），我们还需要重新将我们本地的项目关联到原来的GitHub项目上去，做法如下：

**（1）首先找到位于本地仓库目录下的隐藏文件夹 `.git`**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNoadIe377uP8ByZMESFqn6cdFXsG1Jw7akXV0NYg4gOD5tvbNILcqdg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**（2）用文本编辑器打开 `.git`文件夹中的 `config`配置文件**

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNnmNVibavmCJRnF7vVhYMZIlfENg5CicLkGcO8MaMLPpv0EyzicranlUfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将配置文件中的 `[remote"origin"].url`字段重新关联到原来位于GitHub上的GitHub项目地址

![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzrQUnr62aOibZsG5lf4VpQicNQRick8gfWkrhSfjic8jRibK1kKkZL8y7VdEia7pL45KBoWUNIEIZfXpgIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 当然你也可以通过命令行来修改远端地址，效果一样的

至此大功告成，本地项目就相当于是 `clone`自GitHub，后续提代码，提 `PR`到GitHub上都没有问题。





## 15.Git开发分支的使用





## 16.从实践中彻底上手Git

### Git简介

`Git` 是一种分布式版本控制系统，它可以不受网络连接的限制，加上其它众多优点，目前已经成为程序开发人员做项目版本管理时的首选，非开发人员也可以用 `Git` 来做自己的文档版本管理工具。

`Git` 的api很多，但其实平时项目中90%的需求都只需要用到几个基本的功能即可，所以本文将从 `实用主义` 和 `深入探索` 2个方面去谈谈如何在项目中使用 `Git`，一般来说，看完 `实用主义` 这一节就可以开始在项目中动手用。

> “
>
> 说明：本文的操作都是基于 Mac 系统，其他平台均类似操作

### 实用主义

#### 准备阶段

进入 Git官网 下载合适你的安装包，安装好 `Git` 后，打开命令行工具，进入工作文件夹（*为了便于理解我们在系统桌面上演示*），创建一个新的demo文件夹。

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowxj20znuUX8pOw2EBB5Wvo6FbFbSgbbREAKBia8lBGqAC0DkI44wUlZA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

进入 Github网站 注册一个账号并登录，进入 我的博客，点击 `Clone or download` ，再点击 `Use HTTPS` ，复制项目地址 `https://github.com/gafish/gafish.github.com.git` 备用。

再回到命令行工具，一切就绪，接下来进入本文的重点。

#### 常用操作

所谓实用主义，就是掌握了以下知识就可以玩转 `Git`，轻松应对90%以上的需求。以下是实用主义型的Git命令列表，先大致看一下

- `git clone`
- `git config`
- `git branch`
- `git checkout`
- `git status`
- `git add`
- `git commit`
- `git push`
- `git pull`
- `git log`
- `git tag`

接下来，将通过对 我的博客 仓库进行实例操作，讲解如何使用 `Git` 拉取代码到提交代码的整个流程。

##### git clone

> “
>
> 从git服务器拉取代码

```
git clone https://github.com/gafish/gafish.github.com.git
```

代码下载完成后在当前文件夹中会有一个 `gafish.github.com` 的目录，通过 `cd gafish.github.com` 命令进入目录。

##### git config

> “
>
> 配置开发者用户名和邮箱

```
git config user.name gafish
git config user.email gafish@qqqq.com
```

每次代码提交的时候都会生成一条提交记录，其中会包含当前配置的用户名和邮箱。

##### git branch

> “
>
> 创建、重命名、查看、删除项目分支，通过 `Git` 做项目开发时，一般都是在开发分支中进行，开发完成后合并分支到主干。

```
git branch daily/0.0.0
```

创建一个名为 `daily/0.0.0` 的日常开发分支，分支名只要不包括特殊字符即可。

```
git branch -m daily/0.0.0 daily/0.0.1
```

如果觉得之前的分支名不合适，可以为新建的分支重命名，重命名分支名为 `daily/0.0.1`

```
git branch
```

通过不带参数的branch命令可以查看当前项目分支列表

```
git branch -d daily/0.0.1
```

如果分支已经完成使命则可以通过 `-d` 参数将分支删除，这里为了继续下一步操作，暂不执行删除操作

##### git checkout

> “
>
> 切换分支

```
git checkout daily/0.0.1
```

切换到 `daily/0.0.1` 分支，后续的操作将在这个分支上进行

##### git status

> “
>
> 查看文件变动状态

通过任何你喜欢的编辑器对项目中的 `README.md` 文件做一些改动，保存。

```
git status
```

通过 `git status` 命令可以看到文件当前状态 `Changes not staged for commit:` （*改动文件未提交到暂存区*）

```
On branch daily/0.0.1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   README.md
no changes added to commit (use "git add" and/or "git commit -a")
```

##### git add

> “
>
> 添加文件变动到暂存区

```
git add README.md
```

通过指定文件名 `README.md` 可以将该文件添加到暂存区，如果想添加所有文件可用 `git add .` 命令，这时候可通过 `git status` 看到文件当前状态 `Changes to be committed:`（*文件已提交到暂存区*）

```
On branch daily/0.0.1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    modified:   README.md
```

##### git commit

> “
>
> 提交文件变动到版本库

```
git commit -m '这里写提交原因'
```

通过 `-m` 参数可直接在命令行里输入提交描述文本

##### git push

> “
>
> 将本地的代码改动推送到服务器

```
git push origin daily/0.0.1
```

`origin` 指代的是当前的git服务器地址，这行命令的意思是把 `daily/0.0.1` 分支推送到服务器，当看到命令行返回如下字符表示推送成功了。

```
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 267 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/gafish/gafish.github.com.git
 * [new branch]      daily/0.0.1 -> daily/0.0.1
```

现在我们回到Github网站的项目首页，点击 `Branch:master` 下拉按钮，就会看到刚才推送的 `daily/00.1` 分支了

##### git pull

> “
>
> 将服务器上的最新代码拉取到本地

```
git pull origin daily/0.0.1
```

如果其它项目成员对项目做了改动并推送到服务器，我们需要将最新的改动更新到本地，这里我们来模拟一下这种情况。

进入Github网站的项目首页，再进入 `daily/0.0.1` 分支，在线对 `README.md` 文件做一些修改并保存，然后在命令中执行以上命令，它将把刚才在线修改的部分拉取到本地，用编辑器打开 `README.md` ，你会发现文件已经跟线上的内容同步了。

*如果线上代码做了变动，而你本地的代码也有变动，拉取的代码就有可能会跟你本地的改动冲突，一般情况下 `Git` 会自动处理这种冲突合并，但如果改动的是同一行，那就需要手动来合并代码，编辑文件，保存最新的改动，再通过 `git add .` 和 `git commit -m 'xxx'` 来提交合并。*

##### git log

> “
>
> 查看版本提交记录

```
git log
```

通过以上命令，我们可以查看整个项目的版本提交记录，它里面包含了`提交人`、`日期`、`提交原因`等信息，得到的结果如下：

```
commit c334730f8dba5096c54c8ac04fdc2b31ede7107a
Author: gafish <gafish@qqqq.com>
Date:   Wed Jan 11 09:44:13 2017 +0800
    Update README.md
commit ba6e3d21fcb1c87a718d2a73cdd11261eb672b2a
Author: gafish <gafish@qqqq.com>
Date:   Wed Jan 11 09:31:33 2017 +0800
    test
.....
```

提交记录可能会非常多，按 `J` 键往下翻，按 `K` 键往上翻，按 `Q` 键退出查看

##### git tag

> “
>
> 为项目标记里程碑

```
git tag publish/0.0.1
git push origin publish/0.0.1
```

当我们完成某个功能需求准备发布上线时，应该将此次完整的项目代码做个标记，并将这个标记好的版本发布到线上，这里我们以 `publish/0.0.1` 为标记名并发布，当看到命令行返回如下内容则表示发布成功了

```
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/gafish/gafish.github.com.git
 * [new tag]         publish/0.0.1 -> publish/0.0.1
```

##### .gitignore

> “
>
> 设置哪些内容不需要推送到服务器，这是一个配置文件

```
touch .gitignore
```

`.gitignore` 不是 `Git` 命令，而在项目中的一个文件，通过设置 `.gitignore` 的内容告诉 `Git` 哪些文件应该被忽略不需要推送到服务器，通过以上命令可以创建一个 `.gitignore`文件，并在编辑器中打开文件，每一行代表一个要忽略的文件或目录，如：

```
demo.html
build/
```

以上内容的意思是 `Git` 将忽略 `demo.html` 文件 和 `build/` 目录，这些内容不会被推送到服务器上

##### 小结

通过掌握以上这些基本命令就可以在项目中开始用起来了，如果追求实用，那关于 `Git` 的学习就可以到此结束了，偶尔遇到的问题也基本上通过 `Google` 也能找到答案，如果想深入探索 `Git` 的高阶功能，那就继续往下看 `深入探索` 部分。

### 深入探索

#### 基本概念

##### 工作区（*Working Directory*）

就是你在电脑里能看到的目录，比如上文中的 `gafish.github.com` 文件夹就是一个工作区![图片](https://mmbiz.qpic.cn/mmbiz_jpg/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowCZt4KXXvUcp7jAg660to0ogjTNbEGeOufnVajuKrGgwnDmjUiceNdaQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

##### 本地版本库（*Local Repository*）

工作区有一个隐藏目录 `.git`，这个不算工作区，而是 `Git` 的版本库。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowhpvK3eAkXrLaeUj6ACFSBbic13Ec4uMWZCG5TfjIRRfVtayMlBKfTkA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

##### 暂存区（*stage*）

本地版本库里存了很多东西，其中最重要的就是称为 `stage`（或者叫index）的暂存区，还有 `Git` 为我们自动创建的第一个分支 `master`，以及指向 `master` 的一个指针叫 `HEAD`。

##### 远程版本库（*Remote Repository*）

一般指的是 `Git` 服务器上所对应的仓库，本文的示例所在的`github`仓库就是一个远程版本库![图片](https://mmbiz.qpic.cn/mmbiz_jpg/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowzoYKlke1fkocx8gS3zFL5ibwno3gBuaJIkJlXL4ORPmo2qJF6nFex6g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

##### 以上概念之间的关系

`工作区`、`暂存区`、`本地版本库`、`远程版本库`之间几个常用的 `Git` 操作流程如下图所示：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowEN1YhichdyZx12x140WwGicznIvevNehMmJcYUjdkNYGPY7kJPFOqNnw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

##### 分支（*Branch*）

分支是为了将修改记录的整个流程分开存储，让分开的分支不受其它分支的影响，所以在同一个数据库里可以同时进行多个不同的修改

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowiby6diaQib3fKGhasTd5RbSl6qvxjibhJN2DN45ZoMIDMOseHgO1ibxfibbw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

##### 主分支（*Master*）

前面提到过 `master` 是 `Git` 为我们自动创建的第一个分支，也叫主分支，其它分支开发完成后都要合并到 `master`

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgow91IM1Bv81qSK6tYbMpS8icJiaHMuHzHTTtAOEm8DoibjmHruqlwqdWNyA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



##### 标签（*Tag*）

标签是用于标记特定的点或提交的历史，通常会用来标记发布版本的名称或版本号（如：`publish/0.0.1`），虽然标签看起来有点像分支，但打上标签的提交是固定的，不能随意的改动，参见上图中的`1.0` / `2.0` / `3.0`

##### HEAD

`HEAD` 指向的就是当前分支的最新提交

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowxN49635dB9zuiaElVicSmgcnnhZicTElUqKkKg31eMsGQSnjHhc2eH5pw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> “
>
> 以上概念了解的差不多，那就可以继续往下看，下面将以具体的操作类型来讲解 `Git`的高阶用法

#### 操作文件

##### git add

> “
>
> 添加文件到暂存区

```
git add -i
```

通过此命令将打开交互式子命令系统，你将看到如下子命令

```
***Commands***
  1: status      2: update      3: revert      4: add untracked
  5: patch      6: diff      7: quit      8: help
```

通过输入序列号或首字母可以选择相应的功能，具体的功能解释如下：

- `status`：功能上和 `git add -i` 相似，没什么鸟用
- `update`：详见下方 `git add -u`
- `revert`：把已经添加到暂存区的文件从暂存区剔除，其操作方式和 `update` 类似
- `add untracked`：可以把新增的文件添加到暂存区，其操作方式和 `update` 类似
- `patch`：详见下方 `git add -p`
- `diff`：比较暂存区文件和本地版本库的差异，其操作方式和 `update` 类似
- `quit`：退出 `git add -i` 命令系统
- `help`：查看帮助信息

```
git add -p
```

直接进入交互命令中最有用的 `patch` 模式

这是交互命令中最有用的模式，其操作方式和 `update` 类似，选择后 `Git` 会显示这些文件的当前内容与本地版本库中的差异，然后您可以自己决定是否添加这些修改到暂存区，在命令行 `Stage deletion [y,n,q,a,d,/,?]?` 后输入 `y,n,q,a,d,/,?` 其中一项选择操作方式，具体功能解释如下：

- y：接受修改
- n：忽略修改
- q：退出当前命令
- a：添加修改
- d：放弃修改
- /：通过正则表达式匹配修改内容
- ?：查看帮助信息

```
git add -u
```

直接进入交互命令中的 `update` 模式

它会先列出工作区 `修改` 或 `删除` 的文件列表，`新增` 的文件不会被显示，在命令行 `Update>>` 后输入相应的列表序列号表示选中该项，回车继续选择，如果已选好，直接回车回到命令主界面

```
git add --ignore-removal .
```

添加工作区 `修改` 或 `新增` 的文件列表， `删除` 的文件不会被添加

##### git commit

> “
>
> 把暂存区的文件提交到本地版本库

```
git commit -m '第一行提交原因'  -m '第二行提交原因'
```

不打开编辑器，直接在命令行中输入多行提交原因

```
git commit -am '提交原因'
```

将工作区 `修改` 或 `删除` 的文件提交到本地版本库， `新增` 的文件不会被提交

```
git commit --amend -m '提交原因'
```

修改最新一条提交记录的提交原因

```
git commit -C HEAD
```

将当前文件改动提交到 `HEAD` 或当前分支的历史ID

##### git mv

> “
>
> 移动或重命名文件、目录

```
git mv a.md b.md -f
```

将 `a.md` 重命名为 `b.md` ，同时添加变动到暂存区，加 `-f` 参数可以强制重命名，相比用 `mv a.md b.md` 命令省去了 `git add` 操作

##### git rm

> “
>
> 从工作区和暂存区移除文件

```
git rm b.md
```

从工作区和暂存区移除文件 `b.md` ，同时添加变动到暂存区，相比用 `rm b.md` 命令省去了 `git add` 操作

```
git rm src/ -r
```

允许从工作区和暂存区移除目录

##### git status

```
git status -s
```

以简短方式查看工作区和暂存区文件状态，示例如下：

```
 M demo.html
?? test.html
git status --ignored
```

查看工作区和暂存区文件状态，包括被忽略的文件

#### 操作分支

##### git branch

> “
>
> 查看、创建、删除分支

```
git branch -a
```

查看本地版本库和远程版本库上的分支列表

```
git branch -r
```

查看远程版本库上的分支列表，加上 `-d` 参数可以删除远程版本库上的分支

```
git branch -D
```

分支未提交到本地版本库前强制删除分支

```
git branch -vv
```

查看带有最后提交id、最近提交原因等信息的本地版本库分支列表

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowU49NhDrc0SXtGWqNUoNQ71NRCnmicZgtFQzgnunugP4pML52jChNFoA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

##### git merge

> “
>
> 将其它分支合并到当前分支

```
git merge --squash
```

将待合并分支上的 `commit` 合并成一个新的 `commit` 放入当前分支，适用于待合并分支的提交记录不需要保留的情况![图片](https://mmbiz.qpic.cn/mmbiz_gif/JdLkEI9sZfd5v84p7lS2Mr1pThtnyVebF8X289ibrNSus6ibMHfT8BviaUJuVibFvdZ8zokaCQlsrqZOKs1W7QZl5Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

```
git merge --no-ff
```

默认情况下，`Git` 执行"`快进式合并`"（fast-farward merge），会直接将 `Master` 分支指向 `Develop` 分支，使用 `--no-ff` 参数后，会执行正常合并，在 `Master` 分支上生成一个新节点，保证版本演进更清晰。

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowMRTMOI4wPj7ZZSURhODgT5QGEicfXIS3icW6LJRTwf4YdJUWOnugxQoA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

```
git merge --no-edit
```

在没有冲突的情况下合并，不想手动编辑提交原因，而是用 `Git` 自动生成的类似 `Merge branch 'test'` 的文字直接提交

##### git checkout

> “
>
> 切换分支

```
git checkout -b daily/0.0.1
```

创建 `daily/0.0.1` 分支，同时切换到这个新创建的分支

```
git checkout HEAD demo.html
```

从本地版本库的 `HEAD`（也可以是提交ID、分支名、Tag名） 历史中检出 `demo.html` 覆盖当前工作区的文件，如果省略 `HEAD` 则是从暂存区检出

```
git checkout --orphan new_branch
```

这个命令会创建一个全新的，完全没有历史记录的新分支，但当前源分支上所有的最新文件都还在，真是强迫症患者的福音，但这个新分支必须做一次 `git commit` 操作后才会真正成为一个新分支。

```
git checkout -p other_branch
```

这个命令主要用来比较两个分支间的差异内容，并提供交互式的界面来选择进一步的操作，这个命令不仅可以比较两个分支间的差异，还可以比较单个文件的差异。

##### git stash

> “
>
> 在 `Git` 的栈中保存当前修改或删除的工作进度，当你在一个分支里做某项功能开发时，接到通知把昨天已经测试完没问题的代码发布到线上，但这时你已经在这个分支里加入了其它未提交的代码，这个时候就可以把这些未提交的代码存到栈里。

```
git stash
```

将未提交的文件保存到Git栈中

```
git stash list
```

查看栈中保存的列表

```
git stash show stash@{0}
```

显示栈中其中一条记录

```
git stash drop stash@{0}
```

移除栈中其中一条记录

```
git stash pop
```

从Git栈中检出最新保存的一条记录，并将它从栈中移除

```
git stash apply stash@{0}
```

从Git栈中检出其中一条记录，但不从栈中移除

```
git stash branch new_banch
```

把当前栈中最近一次记录检出并创建一个新分支

```
git stash clear
```

清空栈里的所有记录

```
git stash create
```

为当前修改或删除的文件创建一个自定义的栈并返回一个ID，此时并未真正存储到栈里

```
git stash store xxxxxx
```

将 `create` 方法里返回的ID放到 `store` 后面，此时在栈里真正创建了一个记录，但当前修改或删除的文件并未从工作区移除

```
$ git stash create
09eb9a97ad632d0825be1ece361936d1d0bdb5c7
$ git stash store 09eb9a97ad632d0825be1ece361936d1d0bdb5c7
$ git stash list
stash@{0}: Created via "git stash store".
```

#### 操作历史

##### git log

> “
>
> 显示提交历史记录

```
git log -p
```

显示带提交差异对比的历史记录

```
git log demo.html
```

显示 `demo.html` 文件的历史记录

```
git log --since="2 weeks ago"
```

显示2周前开始到现在的历史记录，其它时间可以类推

```
git log --before="2 weeks ago"
```

显示截止到2周前的历史记录，其它时间可以类推

```
git log -10
```

显示最近10条历史记录

```
git log f5f630a..HEAD
```

显示从提交ID `f5f630a` 到 `HEAD` 之间的记录，`HEAD` 可以为空或其它提交ID

```
git log --pretty=oneline
```

在一行中输出简短的历史记录

```
git log --pretty=format:"%h"
```

格式化输出历史记录

`Git` 用各种 `placeholder` 来决定各种显示内容，我挑几个常用的显示如下：

- %H: commit hash
- %h: 缩短的commit hash
- %T: tree hash
- %t: 缩短的 tree hash
- %P: parent hashes
- %p: 缩短的 parent hashes
- %an: 作者名字
- %aN: mailmap的作者名
- %ae: 作者邮箱
- %ad: 日期 (--date= 制定的格式)
- %ar: 日期, 相对格式(1 day ago)
- %cn: 提交者名字
- %ce: 提交者 email
- %cd: 提交日期 (--date= 制定的格式)
- %cr: 提交日期, 相对格式(1 day ago)
- %d: ref名称
- %s: commit信息标题
- %b: commit信息内容
- %n: 换行

##### git cherry-pick

> “
>
> 合并分支的一条或几条提交记录到当前分支末梢

```
git cherry-pick 170a305
```

合并提交ID `170a305` 到当前分支末梢

##### git reset

> “
>
> 将当前的分支重设（reset）到指定的 `<commit>` 或者 `HEAD`

```
git reset --mixed <commit>
```

`--mixed` 是不带参数时的默认参数，它退回到某个版本，保留文件内容，回退提交历史

```
git reset --soft <commit>
```

暂存区和工作区中的内容不作任何改变，仅仅把 `HEAD` 指向 `<commit>`

```
git reset --hard <commit>
```

自从 `<commit>` 以来在工作区中的任何改变都被丢弃，并把 `HEAD` 指向 `<commit>`

##### git rebase

> ##### “
>
> 重新定义分支的版本库状态

```
git rebase branch_name
```

合并分支，这跟 `merge` 很像，但还是有本质区别，看下图：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

合并过程中可能需要先解决冲突，然后执行 `git rebase --continue`

```
git rebase -i HEAD~~
```

打开文本编辑器，将看到从 `HEAD` 到 `HEAD~~` 的提交如下

```
pick 9a54fd4 添加commit的说明
pick 0d4a808 添加pull的说明
# Rebase 326fc9f..0d4a808 onto d286baa
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
```

将第一行的 `pick` 改成 `Commands` 中所列出来的命令，然后保存并退出，所对应的修改将会生效。如果移动提交记录的顺序，将改变历史记录中的排序。

##### git revert

> “
>
> 撤销某次操作，此次操作之前和之后的 `commit` 和 `history` 都会保留，并且把这次撤销作为一次最新的提交

```
git revert HEAD
```

撤销前一次提交操作

```
git revert HEAD --no-edit
```

撤销前一次提交操作，并以默认的 `Revert "xxx"` 为提交原因

```
git revert -n HEAD
```

需要撤销多次操作的时候加 `-n` 参数，这样不会每次撤销操作都提交，而是等所有撤销都完成后一起提交

##### git diff

> “
>
> 查看工作区、暂存区、本地版本库之间的文件差异，用一张图来解释

![图片](https://mmbiz.qpic.cn/mmbiz_png/kChlCQZAfH5eBrzeP4kHVbwcqAicZkgowbTtpHas5ZBpKFGFU8FxcaR8cCeANrcGmBwtpiaHkib8SQxJBLhOxEbOA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

```
git diff --stat
```

通过 `--stat` 参数可以查看变更统计数据

```
 test.md | 1 -
 1 file changed, 1 deletion(-)
```

##### git reflog

`reflog` 可以查看所有分支的所有操作记录（包括commit和reset的操作、已经被删除的commit记录，跟 `git log` 的区别在于它不能查看已经删除了的commit记录![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 远程版本库连接

如果在GitHub项目初始化之前，文件已经存在于本地目录中，那可以在本地初始化本地版本库，再将本地版本库跟远程版本库连接起来

##### git init

> “
>
> 在本地目录内部会生成.git文件夹

##### git remote

```
git remote -v
```

不带参数，列出已经存在的远程分支，加上 `-v` 列出详细信息，在每一个名字后面列出其远程url

```
git remote add origin https://github.com/gafish/gafish.github.com.git
```

添加一个新的远程仓库，指定一个名字，以便引用后面带的URL

##### git fetch

> “
>
> 将远程版本库的更新取回到本地版本库

```
git fetch origin daily/0.0.1
```

默认情况下，`git fetch` 取回所有分支的更新。如果只想取回特定分支的更新，可以指定分支名。

#### 问题排查

##### git blame

> “
>
> 查看文件每行代码块的历史信息

```
git blame -L 1,10 demo.html
```

截取 `demo.html` 文件1-10行历史信息

##### git bisect

> “
>
> 二分查找历史记录，排查BUG

```
git bisect start
```

开始二分查找

```
git bisect bad
```

标记当前二分提交ID为有问题的点

```
git bisect good
```

标记当前二分提交ID为没问题的点

```
git bisect reset
```

查到有问题的提交ID后回到原分支

### 更多操作

#### git submodule

> “
>
> 通过 Git 子模块可以跟踪外部版本库，它允许在某一版本库中再存储另一版本库，并且能够保持2个版本库完全独立

```
git submodule add https://github.com/gafish/demo.git demo
```

将 `demo` 仓库添加为子模块

```
git submodule update demo
```

更新子模块 `demo`

### git gc

> “
>
> 运行Git的垃圾回收功能，清理冗余的历史快照

### git archive

> ##### “
>
> 将加了tag的某个版本打包提取

```
git archive -v --format=zip v0.1 > v0.1.zip
```

`--format` 表示打包的格式，如 `zip`，`-v` 表示对应的tag名，后面跟的是tag名，如 `v0.1`。



## 17.从原理上搞懂Git

Git 是程序员学习和工作都离不开发工具，也是非程序员好用的文档版本管理工具。

本文图解 Git 中的最常用命令。如果你稍微理解 Git 的工作原理，这篇文章能够让你理解的更透彻。

> 原文链接：https://marklodato.github.io/visual-git-guide/index-zh-cn.html

### 基本用法

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqusjLdmEbIVyxtkjfdtVF9qLMkEkVD69ZwzCuOHiaEFczrkAtib8ic7JznA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面的四条命令在工作目录、暂存目录(也叫做索引)和仓库之间复制文件。

- git add files 把当前文件放入暂存区域。
- git commit 给暂存区域生成快照并提交。
- git reset -- files 用来撤销最后一次git add files，你也可以用git reset 撤销所有暂存区域文件。
- git checkout -- files 把文件从暂存区域复制到工作目录，用来丢弃本地修改。

你可以用 git reset -p, git checkout -p, or git add -p进入交互模式。

也可以跳过暂存区域直接从仓库取出文件或者直接提交代码。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqud6LC2aicjNKDWT21Hia4rNsykKdUKvNLicCGEb17M3RSz3ica06iaGsJ26Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- git commit -a 相当于运行 git add 把所有当前目录下的文件加入暂存区域再运行。git commit.
- git commit files 进行一次包含最后一次提交加上工作目录中文件快照的提交。并且文件被添加到暂存区域。
- git checkout HEAD -- files 回滚到复制最后一次提交。



### 约定

后文中以下面的形式使用图片。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqu7NiaX2TCRf2LmScVxMq6Vuuu27PCD5zQARVFmicaicOTqmf58KDHjsWFA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

绿色的5位字符表示提交的ID，分别指向父节点。分支用橘色显示，分别指向特定的提交。当前分支由附在其上的HEAD标识。这张图片里显示最后5次提交，ed489是最新提交。main分支指向此次提交，另一个stable分支指向祖父提交节点。

### 命令详解

#### Diff

有许多种方法查看两次提交之间的变动。下面是一些示例。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqulXh7n4XFXW9Su6bIuaYrO1QVSG0DUx3XQV39r47DtTibzpKMWybdCaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### Commit

提交时，git用暂存区域的文件创建一个新的提交，并把此时的节点设为父节点。然后把当前分支指向新的提交节点。下图中，当前分支是main。在运行命令之前，main指向ed489，提交后，main指向新的节点f0cec并以ed489作为父节点。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquicW9XtH5x8uZYXgxTibAzI6NMHyYQicTQpx088lCjODPjyntB6fxcqEwA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

即便当前分支是某次提交的祖父节点，git会同样操作。下图中，在main分支的祖父节点stable分支进行一次提交，生成了1800b。这样，stable分支就不再是main分支的祖父节点。此时，**合并** (或者 **衍合**) 是必须的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquaQAps6sd0gF62lnMliafhlMU1JnZ0hwmroPmw3zA4mWBYSpS6JEPbAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想更改一次提交，使用 git commit --amend。git会使用与当前提交相同的父节点进行一次新提交，旧的提交会被取消。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquVBHmp05AuxQYOLNbyISvKFSpibicGXcN80BFQDGMfWeuFniaekxQw98Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

另一个例子是分离HEAD提交,后文讲。

#### Checkout

checkout命令用于从历史提交（或者暂存区域）中拷贝文件到工作目录，也可用于切换分支。

当给定某个文件名（或者打开-p选项，或者文件名和-p选项同时打开）时，git会从指定的提交中拷贝文件到暂存区域和工作目录。比如，git checkout HEAD~ foo.c会将提交节点HEAD~(即当前提交节点的父节点)中的foo.c复制到工作目录并且加到暂存区域中。（如果命令中没有指定提交节点，则会从暂存区域中拷贝内容。）注意当前分支不会发生变化。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquYRJlVeV37BX7p2RjOnhiaicKrXmVA5cET0wsFEtibEmiaicia99uvrBhicDog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当不指定文件名，而是给出一个（本地）分支时，那么HEAD标识会移动到那个分支（也就是说，我们“切换”到那个分支了），然后暂存区域和工作目录中的内容会和HEAD对应的提交节点一致。新提交节点（下图中的a47c3）中的所有文件都会被复制（到暂存区域和工作目录中）；只存在于老的提交节点（ed489）中的文件会被删除；不属于上述两者的文件会被忽略，不受影响。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquwAYoaS7XxctZHcMJRd9X2Uj0XuJJvEu97JCZE9zaicxrlv0icDxaIhAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果既没有指定文件名，也没有指定分支名，而是一个标签、远程分支、SHA-1值或者是像main~3类似的东西，就得到一个匿名分支，称作detached HEAD（被分离的HEAD标识）。这样可以很方便地在历史版本之间互相切换。比如说你想要编译1.6.6.1版本的git，你可以运行git checkout v1.6.6.1（这是一个标签，而非分支名），编译，安装，然后切换回另一个分支，比如说git checkout main。然而，当提交操作涉及到“分离的HEAD”时，其行为会略有不同，详情见在下面。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqu2YZpLEkZIPkhQt9QhMSDgZEqqKRmUfJ88OEAJ4wHR2VEm7N4icOFN7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### HEAD标识处于分离状态时的提交操作

当HEAD处于分离状态（不依附于任一分支）时，提交操作可以正常进行，但是不会更新任何已命名的分支。(你可以认为这是在更新一个匿名分支。)

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqua9280QsWR9xas8oZ5VVqTicr8mKI9Xw4uicksmSMABnDxwXn2TJicQExQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一旦此后你切换到别的分支，比如说main，那么这个提交节点（可能）再也不会被引用到，然后就会被丢弃掉了。注意这个命令之后就不会有东西引用2eecb。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqupnjPcO08ibU5I35DVVPsx6y7KpbIklBRonjWOFDibZAKQuIMOpqVDm6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但是，如果你想保存这个状态，可以用命令git checkout -b name来创建一个新的分支。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquCxouWHoFCoQH8trhDRvSYXia7qjpAskdzFgpIwmGzMretUuwwsUAvBA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### Reset

reset命令把当前分支指向另一个位置，并且有选择的变动工作目录和索引。也用来在从历史仓库中复制文件到索引，而不动工作目录。

如果不给选项，那么当前分支指向到那个提交。如果用--hard选项，那么工作目录也更新，如果用--soft选项，那么都不变。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquR2ssrwZCkzWpAicgu6ka8coVOwia46EHpmnmibVjicrbxF6bX4VXfPiaLEw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果没有给出提交点的版本号，那么默认用HEAD。这样，分支指向不变，但是索引会回滚到最后一次提交，如果用--hard选项，工作目录也同样。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqu4aYibTEhy50rlJC7foIuM354xEGwPDa5wpVRkoUkZ2l8STF4xob4hjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果给了文件名(或者 -p选项), 那么工作效果和带文件名的checkout差不多，除了索引被更新。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqul6v6bPIWC2R2Hgq5RdurdLs2AkW0aZvZJz3EqMbo3hkb2G7T78VZibg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### Merge

merge 命令把不同分支合并起来。合并前，索引必须和当前提交相同。如果另一个分支是当前提交的祖父节点，那么合并命令将什么也不做。另一种情况是如果当前提交是另一个分支的祖父节点，就导致fast-forward合并。指向只是简单的移动，并生成一个新的提交。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqufNibdMOHpQeibRTtmOmNAkW2jGcMl1UsDWeuw2N4sKjrXDckg2FR2BFA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

否则就是一次真正的合并。默认把当前提交(ed489 如下所示)和另一个提交(33104)以及他们的共同祖父节点(b325c)进行一次三方合并。结果是先保存当前目录和索引，然后和父节点33104一起做一次新提交。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqu7GCEon8ZIjiaUnX3OOwibRJJnrPmdTwibGAHDibh9sthaYCjvYAFGAr27g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### Cherry Pick

cherry-pick命令"复制"一个提交节点并在当前分支做一次完全一样的新提交。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibquoRiat32geHjtWMakEDd8Ldr65lLxb9zFN5aSR8ub2ogDeFPwibr6wFBQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### Rebase

衍合是合并命令的另一种选择。合并把两个父分支合并进行一次提交，提交历史不是线性的。衍合在当前分支上重演另一个分支的历史，提交历史是线性的。本质上，这是线性化的自动的 cherry-pick

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

上面的命令都在topic分支中进行，而不是main分支，在main分支上重演，并且把分支指向新的节点。注意旧提交没有被引用，将被回收。

要限制回滚范围，使用--onto选项。下面的命令在main分支上重演当前分支从169a6以来的最近几个提交，即2c33a。

![图片](https://mmbiz.qpic.cn/mmbiz_png/v1JN0W4OpXjuEjicbH8PQibIRkiaNHr9ibqu8oVsj0EWGa0IEXc1USnHJfl7GKJDbHkiaZj5k3XdwTSwZhfibcq4gqWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样有git rebase --interactive让你更方便的完成一些复杂操作，比如丢弃、重排、修改、合并提交。

### 技术说明

文件内容并没有真正存储在索引(.git/index)或者提交对象中，而是以blob的形式分别存储在数据库中(.git/objects)，并用SHA-1值来校验。索引文件用识别码列出相关的blob文件以及别的数据。对于提交来说，以树(tree)的形式存储，同样用对于的哈希值识别。树对应着工作目录中的文件夹，树中包含的 树或者blob对象对应着相应的子目录和文件。每次提交都存储下它的上一级树的识别码。

如果用detached HEAD提交，那么最后一次提交会被the reflog for HEAD引用。但是过一段时间就失效，最终被回收，与git commit --amend或者git rebase很像。



## 18.Git操作与常用命令

**一、创建与合并分支** 

**1、 从master分支创建dev分支并切换到dev分支**

```
git checkout mastergit checkout -b dev
```

其中，git checkout -b dev 等价于:

```
git branch devgit checkout dev
```

（1）

```
git branch
```

查看本地当前的分支，分支前面带“*”表示当前分支，剩下的分支表示本地有的分支。

（2）

```
git  branch  -a
```

查看远程全部的分支，白色的表示本地有的，红色的表示本地没有，仅在远程存在。

**2、修改代码、提交代码（当前的操作是在dev分支上进行）**

```
git add a.html
git commit -m "提交文件a.html"
```

**3、分支合并(将dev合并到master)**

```
git checkout master
git merge dev
```

**4、合并完成后，删除dev分支.(删除dev分支时，注意我们当前所在的分支不能是dev分支)**

```
git branch -d dev
```

**5、删除后，查看分支(此时看不到dev分支了)**

```
git branch
```

**6、总结 ：工作中经常从master创建新的分支，具体操作如下:**

```
master创建新分支：
git checkout master
git checkout -b  issues1234  // 从master分支创建issues1234分支
git push origin issues1234
git add ..
git commit -m "***"
git push origin issues1234
```

> 注意：将本地分支branch1推到远端的branch2操作步骤：

```
git push origin branch1:branch2
```

**7、删除分支：**

```
git branch -D   issues1234  // 本地强制删除分支issues1234
git push origin  :issues1234  // 推到远程
```

------

 **二、解决冲突** 

**1、发生冲突的文件**

```
<<<<<<< HEADCreating a new branch is quick & simple.=======Creating a new branch is quick AND simple.>>>>>>> feature1
```

其中，git使用 `<<<<<<<，=======，>>>>>>>`标记文件中自己和别人产生冲突的部分。

在 `<<<<<<<，=======`之间为自己的代码；=======，>>>>>>>之间为别人的代码。

如果保留自己的代码，将别人的代码删掉即可。

**2、冲突解决后提交**

```
git status
git add ***
git commit -m "fix conflict"
git push origin 分支名
```

------

 **三、Bug分支** 

**1、储藏更改:将当前更改的代码储藏起来，等以后恢复使用**

```
git stash
```

**2、恢复储藏的代码**

```
git stash pop // 恢复的同时把stash内容删掉
```

或者![图片](https://mmbiz.qpic.cn/mmbiz_png/xq9PqibkVAzojLzqlTxblgiaSHLoIicRgtktKaFlWibDRu1m4cmQhicv6ysibp5IUJv2yRKvUXhvxGmt5Zrlj9hJ4hvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

```
// 通过 git stash list，查看本地所有的stash,如果我要恢复第一个就执行：git stash apply stash@{0}
git stash apply  // 恢复stash，但是stash内容并不删除
git stash drop // 在上面操作的基础上，以此来删除stash
注： git stash list // 查看全部的stash列表
```

**3、将stash空间清空**

```
git stash clear
```

**4、git stash pop 和 git stash apply 区别**

```
原来git stash pop stash@{id}命令会在执行后将对应的stash id 从stash list里删除，而 git stash apply stash@{id} 命令则会继续保存stash id。
```

------

 **四、版本回退** 

**1、回退至上一个版本**

```
git reset --hard HEAD
```

**2、回退至指定版本**

```
git reset --hard  版本号
```

**3、查看以往版本号(本地的commit)**

```
git reflog
```

**4、查看各版本号及信息(所有的commit：本地commit + 其他同事的commit)**

```
git log
```

------

 **五、撤销修改** 

**1、撤销修改**

```
git  checkout -- a.html
```

> 分两种情况分析：

```
①： 还没有执行 git add 操作，执行上面的操作后，会恢复到和版本库中一模一样的版本状态。
②： 执行了git add ，还没执行 git commit ,再执行上面的操作后，会恢复到git add 结束后的状态
```

> 注：一旦执行了git commit -m "*"，就不能再使用上面的命令回退。

**2、撤销新建文件**

比如新建一个aa.html页面，并未执行git add ,即没有被git追踪，此时如果你想撤销新建动作，可执行：

```
git clean -f ../aa.html
```

**3、撤销新建文件夹**

比如新建一个文件夹"demo"，并未执行git add ,即没有被git追踪，此时如果你想撤销新建动作，可执行：

```
git clean -df ./demo
```

------

 **六、对已push版本进行回退** 

**1、第一步：**

```
git reset --hard 版本号 // 本地回退到指定的版本
```

**2、第二步：**

```
git push  -f origin dev    //将远程的也回退到指定版本
```

------

 **七、本地同步远程删除的分支** 

```
git fetch origin -p  // 用来清除已经没有远程信息的分支，这样git branch -a 就不会拉取远程已经删除的分支了
```

------

 **八、删掉未与远程分支对应的本地分支** 

从gitlab上看不到的分支在本地可以通过git branch -a 查到，删掉没有与远程分支对应的本地分支：

```
git fetch -p
```

------

 **九、查看远程库与本地分支的信息** 

```
git remote show origin
```

------

 **十、标签管理** 

**1、给当前分支最新commit打标签**

```
git tag v1.0.0
```

**2、比如现在周五，要给周一某个commit打标签，应执行以下步骤：**

（1）、查看log日志，找到相应的commit版本号

```
git log --pretty=oneline --abbrev-commit
// 显示如下commit，比如我想在 "34372b05"这个commit打标签44d2e20b fix bug34372b05 fix bug29554931 fix bug
```

（2）、给指定的commit打标签

```
git tag v1.0.0 34372b05
```

（3）、创建的标签只存在本地，推至远程

```
git push origin v1.0.0
```

（4）、一次性推送未推至远程的本地标签

```
git push origin --tags
```

（5）、查询所有标签

```
git tag
```

（6）、查询标签详细信息

```
git show v1.0.0
```

（7）、删除本地标签

```
git tag -d v1.0.0
```

（8）、删除远程标签

```
// 先从本地删除git tag -d v1.0.0
// 然后从远程删除git push origin :refs/tags/v1.0.0
// 最后可以在gitlab上查看是否真正的删除了标签
```

**3、创建带有说明的标签，用-a指定标签名，-m指定说明文字**

```
// git  tag  -a  版本号  -m  说明信息  commit版本号git tag -a v1.0.0 -m "version 1.0.0 released" 34372b05(commit版本号)     
// 查看标签详细信息git show v1.0.0    
```

