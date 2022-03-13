---
title: 【Pytorch】pytorch安装
tags:
  - Pytorch
categories:
  - Pytorch
toc: true
abbrlink: 41412
date: 2021-07-25 12:52:57
sticky: 2
---

## 一、安装anaconda

网址：https://www.anaconda.com/products/individual

<!--more-->

网页翻到最下面，选择下载Windows 32位/64位版本，傻瓜式安装，记得勾选【Add to Path】 可以将anaconda的环境安装到系统中去

![image-20210226184530041](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91Pytorch%E5%AE%89%E8%A3%8501.png)

## 二、Anaconda创建虚拟环境

**1 、**从开始菜单中打开Anaconda Navigator，单机进入Environments选项卡，如下图所示

![image-20210226185001846](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8502.png)

**2、**在Environments选项卡中，单击左下方的Create按钮，创建虚拟环境，如下图所示

![image-20210226185132837](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20210226185132837.png)

![image-20210226185258488](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8504.png)`此时在Environments选项卡中，已经出现刚刚创建的虚拟环境
【注】才创建的虚拟环境只包含最基本的库`

![image-20210226185650716](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8505.png)

## 三、安装Pycharm,创建工程

网址：https://www.jetbrains.com/pycharm/

1、单击download进入下载页面

![image-20210226185905498](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8506.png)

此时，有两种版本选择，嫌麻烦就用社区版，但是功能较少，专业版需要自己找破解，或者用校园邮箱申请一年免费，一年后再次审查通过还可以继续用

![image-20210226185939074](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8507.png)

**2、打开PyCharm，单击New project**

![image-20210226190033081](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8508.png)

**3、PyCharm创建Conda工程**

![image-20210226190145258](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8509.png)

![image-20210226190227936](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8510.png)

4、在Anaconda安装文件夹下找到envs文件夹，里面存储的都是你创建的虚拟环境，然后选择刚刚创建的虚拟环境文件下的python.exe，点击OK

![image-20210226190301076](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8511.png)

![image-20210226190328238](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8512.png)

![image-20210226190350296](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8546.png)

5、创建完成后自动进入如下界面：

![image-20210226190429918](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8513.png)

## 四、CUDA安装

**1、查看CUDA支持版本**

打开NVIDIA控制面板，按照图示顺序查看CUDA所支持的最高版本

![image-20210226200016567](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8514.png)

**2、下载CUDA**

打开网址：https://developer.nvidia.com/cuda-toolkit-archive，选择适合自己电脑的cuda版本，比刚才查看的所支持的CUDA 版本低都行

![image-20210226233838107](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8515.png)

此时要根据自己的系统进行选择

![image-20210226235343901](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8516.png)

![image-20210226235440600](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8517.png)

**3、下载cuDNN**

打开网址：https://developer.nvidia.com/cudnn，点击Download cuDNN

![image-20210227000358285](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8518.png)

注意，cuDNN下载需要NVIDIA账户，没有则先注册，此步需要耐心，贼卡

![image-20210227000437102](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8519.png)

4、登陆之后，点击Download cuDNN进入的应该是如下界面，先把问卷填了，才能进入下载界面

![image-20210227000708677](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8520.png)

此时终于进入下载界面了，勾选I agree…，然后按照下图操作

![image-20210227000739017](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8521.png)

5、选择适合自己的操作系统版本下载

![image-20210227000848436](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8522.png)

**6、安装CUDA**

双击安装包开始安装，此时让你选择的路径并不是安装路径，而是暂时解压出来的文件所需要存放的地方，安装完成后会删除，只要保证选择空间足够大的地方即可，安装路径是默认C盘里，不能修改，此处可以不更改，点击OK即可

![image-20210227000933389](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8523.png)

![image-20210227001012795](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8524.png)

![image-20210227001038878](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8525.png)

![image-20210227001105715](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8526.png)

![image-20210227001140064](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8527.png)

 `验证CUDA是否安装成功，打开cmd，输入 nvcc –V，如下返回则说明安装成功 `

![image-20210227001226296](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8528.png)

解压压缩包，压缩包内文件如下：

![image-20210227001333119](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8529.png)

**7、安装cuDNN**

打开cuda安装文件夹，默认的强制安装路径为：

C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\版本号

打开安装路径如下：

![image-20210227001422354](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8530.png)

将解压的cuDNN压缩包内的三个文件夹复制到CUDA安装目录下：

![image-20210227001503720](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8531.png)

![image-20210227001527682](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8532.png)

验证cuDNN是否安装完成，打开cmd，输入

   `cd C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.0\extras\demo_suite   `

然后执行命令：

   `bandwidthTest.exe   `

![image-20210227001624983](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8533.png)

然后再执行命令：

 `deviceQuery.exe `

![image-20210227001657605](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8534.png)

**8、下载PyTorch安装文件**

打开网址：https://download.pytorch.org/whl/torch_stable.html，界面如下：

![image-20210227001753290](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8535.png)

每个文件命名都是有规律的：

![image-20210227001822167](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8536.png)

使用快捷键Ctrl+F，搜索我们需要安装的版本文件下载

![image-20210227001851897](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8540.png)

![image-20210227001909013](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8539.png)

## 五、安装pytorch

1、打开PyCharm，进入刚刚创建的工程里，打开Terminal窗口：

![image-20210227002109768](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8541.png)

2、在PyCharm的Terminal窗口中键入cd 命令，切换目录到PyTorch安装包所在的地址，然后分别执行pip install命令安装两个文件，先安装torch，再安装torchvision，期间会一起下载所需要的依赖包

![image-20210227002141655](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8542.png)

![image-20210227002200869](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8543.png)

3、现在验证是否安装成功，在main.py里写入以下代码并运行：

![image-20210227002226122](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8544.png)

![image-20210227002303019](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E3%80%90Pytorch%E3%80%91pytorch%E5%AE%89%E8%A3%8545.png)



> 以上方式针对的是windows10操作系统，大家可以根据大家各自的操作系统选择，安装cuda或者不安装cuda
