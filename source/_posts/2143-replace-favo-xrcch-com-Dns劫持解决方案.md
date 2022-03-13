---
title: 2143.replace.favo.xrcch.com  Dns劫持解决方案
tags:
  - Windows
categories:
  - Windows
toc: false
abbrlink: 5846
date: 2021-07-25 12:41:14
---

**DNS劫持具体过程：**

<!--more-->

> ```
> 当你访问 http://[2143.replace.favo.xrcch.com](https://link.zhihu.com/?target=http%3A//2143.replace.favo.xrcch.com) 时，浏览器会自动去尝试http://[2143.replace.favo.xrcch.com](https://link.zhihu.com/?target=http%3A//2143.replace.favo.xrcch.com)/index.html这个URL。返回了一个页面，页面是空白的，并包含了一段代码，这段代码会将页面跳转到另一个地址：[http://baidu.scj.xrcch.com/th.](https://link.zhihu.com/?target=http%3A//baidu.scj.xrcch.com/th.html)
> 
> 这个页面也是空白的，同样包含一段代码，这段代码从如下地址中随机挑选一个，并把页面跳转过去。
> 
> 最后看起来的结果就是，你访问到了百度。
> 
> 其实tn后面的东西标记了这个请求的来源，百度会把一部分广告费分给tn后面对应的账号，因为你是被tn拉过来访问百度的。
> ```
>
> 

**DNS劫持具体原因：**

> ```
> 被DNS劫持了。
> 
> 这样就可以通过访问一个特定的网站，给对方增加流量。他们就可以赚钱了。
> 
> 请检查多种浏览器是否都出现这种情况？如果是，那就说明要么您的路由器把黑了，要么就是宽带运营商动了手脚。如果只是谷歌浏览器出现这个情况，那么先考虑您的浏览器是官方的，还是别人修改过的。如果是修改过的，那么就有可能把修改者植入了相关劫持功能。
> 如果是官方的，那么请关闭所有扩展工具，并一个一个测试它们，这样就知道哪个扩展工具在进行劫持操作。
> ```

**解决方案**：

**方法一：**

1、同时按住“win+i”打开设置页面，选择“网络和Internet”；

2、在设置页面中，切换至“以太网”选项卡，并点击右侧页面的“更改适配器选项”；

3、在网络页面中，右键正在使用中的网络接口，选择“属性”；

4、在属性页面中，选择“Internet协议版本4(TCP/IPv4)”并点击“属性”；

![image-20210301195143744](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/dns%E5%9F%9F%E5%90%8D%E5%8A%AB%E6%8C%81.png)

5、在属性页面中，可以看到设置是自动获取IP地址，选择使用下面的IP地址，输入地址，最后点击确定即可；

首选DNS服务器：114.114.114.114；

备用 DNS 服务器：114.114.115.115点击确认

（有时需要关闭dns首选，开启自动获取）

6、这时再刷新一下DNS缓存，同时按下“Win+R”打开运行窗口，输入“cmd”；

7、在命令窗口中，输入“ipconfig /flushdns”并回车运行即可。

8、ipconfig /flushdns 即可

**方法二：**

打开[腾讯电脑管家](http://www.xitongtiandi.net/zhuanti/48200.html)或者360管家，或者火绒安全

打开DNS选优进行检测

受到DNS攻击或威胁，选择一键修复或者还原最初DNS

以上就是全部内容，记得开启防火墙哦!!!

