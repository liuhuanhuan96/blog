---
title: 【小白】 git本地代码上传到github
tags:
  - GitHub
categories:
  - GitHub
toc: true
abbrlink: 37038
date: 2021-07-25 13:03:49
---



[下载git](https://git-scm.com/download/win)

[注册github账户](https://github.com/join?source=header-home)

<!--more-->

### 1.在github上创建项⽬

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6vxki6zj30ms0csgzt.jpg" alt="image-20201208090803623" style="zoom:50%;" />

> 填好后点 Create repository 按钮提交

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6w275wgj30ky0g2thz.jpg" alt="image-20201208090839504" style="zoom:50%;" />

提交成功如下图：

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6wfzzi4j30mw0dw74w.jpg" alt="image-20201208090908481" style="zoom:50%;" />

### 2.把本地代码提交到git

> **进⼊到：本地⽬录代码⽂件⽬录**
>
> 单击 右键 打开git bush 类似于Win的cmd

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6wiuqckj30ju0gewmt.jpg" alt="image-20201208091412803" style="zoom:50%;" />

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6wn03q6j30mo0gcjvp.jpg" alt="image-20201208091425553" style="zoom:50%;" />

下边操作之前需要设置⽤户

⾸先,你需要执⾏下⾯两条命令,作为git的基础配置,作⽤是告诉git你是谁,你输⼊的信息将出现在你创建的提 交中.

 ~~~shel
git config --GLOBAL user.NAME "你的名字或昵称"
git config --GLOBAL user.EMAIL "你的邮箱"
 ~~~

然后执⾏:

~~~shell
git init
git ADD .
git commit -m "first commit"	（first commit 本次提交的内容）
git remote ADD origin https://github.com/852172891/test3.git （地址换成你
git push -u origin MASTER	（这⼀句执⾏的时候 可能需要输⼊你的 git 账号 和密码
~~~

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6wqji2sj30mo0m21kx.jpg" alt="image-20201208091640521" style="zoom:50%;" />


输⼊密码后，提交成功，到github上刷新⼀下，本地的⽂件已经上传到github上了

### 3.项目地址

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6wsmstij30k40i67ek.jpg" alt="image-20201208091730178" style="zoom:50%;" />

### 4.常见问题

#### 4.1Permanently added the RSA host key for IP address '13.250.177.223' to t he list of known hosts?

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6ww10i2j30mq05y11w.jpg" alt="image-20201208091813211" style="zoom:50%;" />

步骤:1 可以⽤ ssh -T [git@github.com去测试⼀下](mailto:git@github.com去测试)

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6wypyuvj30mq05sn52.jpg" alt="image-20201208091841090" style="zoom:50%;" />

图上可以明显看出缺少了公钥

 2. 在下载好的Git中的bin⽬录下打开bash.exe输⼊命令ssh-keygen -t rsa-C "username" (注：username为你git上的⽤户名)，如果执⾏成	功。返回：

    Generating public/private rsa key pair.

    Enter file in which to save the key

(/Users/username/.ssh/id_rsa):    //这⾥的username是电脑上的⽤户名 这个地址也是⽂件的存储地址，然后我们按回⻋.

如果你以前有存储地址会返回/Users/yourusername/.ssh/id_rsa already exists.Overwrite (y/n)? 直接输⼊y回⻋。如果以前没有储存地址就会出现

​		Enter passphrase(empty for no passphrase);也直接回⻋，两种情况回⻋后都会出现 Enter same passphrase again 然后接着回⻋会显示⼀⻓串内容其中

​	还有⼀些..o.. o oo .oS. 之类的代码，这说明SSH key就已经⽣成了。⽂件⽬录就是：username/.ssh/id_rsa.pub.

​	<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6x21r25j30mu086q3i.jpg" alt="image-20201208092240295" style="zoom:50%;" />

3. 然后找到系统⾃动在.ssh⽂件夹下⽣成两个⽂件，id_rsa和id_rsa.pub，⽤记事本打开id_rsa.pub将全部的内容复制。

4. 打开https://github.com/，登陆你的账户，进⼊设置（Settings）找到

   <img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6x4do8bj30jg0e648f.jpg" alt="image-20201208092336801" style="zoom:50%;" />

5. 然后将你复制的内容粘贴到key中

   <img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg6x785wjj30mc0aatdo.jpg" alt="image-20201208092353244" style="zoom:50%;" />

6. 再点击Add SSH Key            

7. 仍然在bash.exe中输⼊[ssh -T git@github.com然后会跳出⼀堆内容你](mailto:ssh-Tgit@github.com然后会跳出)只需输⼊yes回⻋就完事了，然后他会提示你成功了

   #### 4.2 ! [rejected] master -> master (fetch first)

   ~~~shel
   git push -f origin master 暴⼒解决
   https://blog.csdn.net/weixin_44118318/article/details/85030461(转载)
   ~~~

   

