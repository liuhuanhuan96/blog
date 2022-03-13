---
title: SpringBoot多模块打包常见问题
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: true
abbrlink: 32735
date: 2021-11-01 19:20:25
---



### 1.The project com.nuist:x x x:xxx has 1 error  'dependencies.dependency.version' for com.nuist:xxx:jar is missing. @ line 31, column 21

因为在多模块项目，我们打包需要子模块依赖于父模块，所以我们需要在我们的父模块中导入相应的子模块

<!--more-->

在`modules`中加入我们提示的模块，然后在我们的`dependencies.dependency`标签中引入我们对应的模块,重新加载即可。

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gv9hw0he47j60lo03gjrk02.jpg" alt="image-20211009234850147" style="zoom:50%;" />

![image-20211009235022617](https://tva1.sinaimg.cn/large/008i3skNgy1gv9hw4n105j60wk08gjsd02.jpg)





### 2.No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?

这个错误的话比较好解决，是由于你项目所需jdk版本和你当前使用的jdk版本不一致导致的，因为我项目的pom.xml中定义了java版本为1.8，但是我实际idea中run这个项目却是1.7

更换当前jdk版本为项目所需jdk版本即可

操作步骤：![image-20211009235603878](https://tva1.sinaimg.cn/large/008i3skNgy1gv9i0ffbjlj61j00tktee02.jpg)

选中项目右击 ->F4键设置项目属性进入

![image-20211009235659674](https://tva1.sinaimg.cn/large/008i3skNgy1gv9i18f1qkj61b20emdiq02.jpg)

![image-20211009235709950](https://tva1.sinaimg.cn/large/008i3skNgy1gv9i1eeaowj61920ekad702.jpg)

版本均需要一致。此时我们确认之后，还是会出现这个样的问题，我们检查发现，父pom中没有问题，子pom也没有问题，此时我们会看到第三个错误

### 3. After correcting the problems, you can resume the build with the command

  mvn <args> -rf :framework

遇到这个错误，代表我们的版本定义重复啦，我们父pom中已经定义了j d k 版本，但是在我们子模块中又重新定义，所以提示我们mvn -rf：framework.我们只需要删除对应子模块中的指定的java版本即可，删除之后，打包成功。

![image-20211010000143777](https://tva1.sinaimg.cn/large/008i3skNly1gv9i65ffflj61ba0a476d02.jpg)
