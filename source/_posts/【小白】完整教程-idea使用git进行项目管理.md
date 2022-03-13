---
title: 【小白】完整教程-idea使用git进行项目管理
tags:
  - GitHub
  - Idea
categories:
  - GitHub
toc: true
abbrlink: 23807
date: 2021-07-25 13:01:36
---

## Github如何删除项目

[https://jingyan.baidu.com/article/86112f13aba9c7273797871a.html](https://jingyan.baidu.com/article/86112f13aba9c7273797871a.html)

<!--more-->

## 上传本地项目到gitHub上：

1. 详细见：[https://www.cnblogs.com/gougouyangzi/articles/9429280.html](https://www.cnblogs.com/gougouyangzi/articles/9429280.html)

2. idea本地创建一个项目后

3. 下载安装git

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg8887dqmj30cw03it8q.jpg)

4. 

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg8cq1tfzj30d706djrl.jpg)

5. 在IDEA中设置Git:

在File-->Setting->Version Control-->Git-->Path to Git executable选择你的git安装后的git.exe文件，然后点击Test，测试是否设置成功

 

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg8861u78j30d707f0te.jpg)

要是在bin目录下没找到此exe，不妨看看cmd目录下面有没有，也就是c://~install/cmd/git.exe;

 

6. 在IDEA中设置GitHub，File-->Setting->Version Control-->GibHub

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg885dts2j30d707c3yv.jpg)

登录后：

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg884kwwhj30d707lglx.jpg)

login后会自动发送一封邮件过来

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg887auh9j307v03k3ym.jpg)

点击邮件中的第一个链接

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88953oij30d701ngll.jpg)

会根据用户名和密码生成一个token

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg888os3xj30d702x0sp.jpg)

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg8d8x064j30d703wdg0.jpg)

可以根据这个token去登录idea中的gitHub

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8iagaquj30qe0feth4.jpg" alt="image-20201208101859609" style="zoom:50%;" />

 

7. 创建本地仓库，VCS-->Import into Version Control-->Create Git Repository...

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88kk3a0j30ci06raas.jpg)

在弹框中选中项目所在的位置，点击OK，若选中其他位置，则git-->add不可点选，不知为何）

 

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg8e9vz98j30c60cdgmc.jpg)

效果：

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg8ecrl70j308b08kmxo.jpg)

此时项目文件全部变成红色

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8esj1b4j30qe0b47jv.jpg" alt="image-20201208101931988" style="zoom:50%;" />

8. 上传项目到本地仓库，项目右键选择Git-->add，此时项目文件变成绿色，此时文件只是处于暂存区，并没有真正进入到版本库中

 (本步骤是接着第6步骤的，把代码add到暂存区当中)

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8iyil3uj30qe0oi4qp.jpg" alt="image-20201208101958599" style="zoom:50%;" />

效果：

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88jjjr0j30ad0agwew.jpg)

8.项目右键Git--> Commit Directory，在弹窗中输入Commit Message，点击commit，此时项目文件从暂存区真正进入版本库中，项目文件变成白色

commit会报错，是创建项目的时候多了一个文件，删除再次提交就不会有error了

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8ja1751j30qe0lqttl.jpg" alt="image-20201208102031248" style="zoom:50%;" />

在idea中删除不掉，就要到项目所在的地方去删除了

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg886ea2wj30cv03pq35.jpg)

9.上传项目到GitHub中，VCS-->Import into Version Control-->Share Project on GitHub，在弹框中输入仓库名和描述，点击Share，即可是上传，中间会弹窗输入GitHub的用户名和密码（已输入过用户名和密码并记住的不会再次弹框输入），上传成功后IDEA右下角会给出提示

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88il8scj30b0094t9a.jpg)

出现下面情况是登录失效导致的，重新登录就行了

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8gb4k3xj30eg0i4aj9.jpg" alt="image-20201208102106821" style="zoom:50%;" />

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg889l5b3j30d705ugls.jpg" alt="img" style="zoom:50%;" />

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88a27nbj309b07gt8v.jpg)

好像并没有share成功，只是在gitHub上完成可创建项目名，实际上并么有内容

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88aokwxj3081036gln.jpg)

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88bluv7j30d706mjrr.jpg)

解决方法：[https://blog.csdn.net/guyuealian/article/details/51558560](https://blog.csdn.net/guyuealian/article/details/51558560)

就是第5步骤链接账号的时候，不应该选

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88lgd81j30d707j0sz.jpg)

再次share,由于刚才已经创建了一个同名的文件，所以可以将github上的那个删除掉，或者这个重新命名即可

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88cezxhj3099098q36.jpg)

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8opcy4dj30ia0g4gpi.jpg" alt="image-20201208102556448" style="zoom:50%;" />

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8otm4i5j30fu05o78l.jpg" alt="image-20201208102608959" style="zoom:50%;" />

<img src="https://tva1.sinaimg.cn/large/0081Kckwgy1glg8ovz46bj30qe0fcjze.jpg" alt="image-20201208102618274" style="zoom:50%;" />

10，push到远程：

新增文件（红色），右键-->Git-->add，将新增的文件加入本地仓库，此时文件变绿色

　　修改文件（蓝色）

　　在项目右键-->Git-->Commit Directory，查看有变动的文件并输入Commit Message，点击Commit and Push...

　　提交后会进行语法检查，若存在错误或警告会给出确认提示，点击Commit，弹出Push框，点击Push，上传GitHub成功（因为此时是你自己的项目，

所以有权限提交，一般git到别人的项目，应当叫别人给与权限你才能提交）

**注意：中间可能会出现这个问题**

push faildsrc: Could not read from remote repository.

解决方法：[https://www.jianshu.com/p/8f80878925fd](https://www.jianshu.com/p/8f80878925fd)

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88k0cz0j30d70600t8.jpg)

选择要上传的git仓库：

**![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88cx74mj30d705z74j.jpg)**

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glg88ddtofj307t023a9y.jpg)
