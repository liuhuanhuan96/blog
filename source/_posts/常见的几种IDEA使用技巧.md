---
title: 常见的几种IDEA使用技巧
tags:
  - Idea
categories:
  - Idea
toc: false
abbrlink: 20585
date: 2021-07-25 13:40:40
---



1、在 IDEA 中，当我们编辑代码时，点击查看了调用类实现逻辑，然后可以使用后退快捷键，快速回到刚才待编辑的代码处。

<!--more-->

**前进/后退快捷键如下：**

* **Windows:Ctrl + Alt + Left/Right（方向键）**
* **Mac: ⌘ + ⌥ + ← / →(方向键)**
* ![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuLiaxAlaJichVebmZDqlLROsuwQ4D1T0j1oSibicic8tHBpHJrUyl8PknqWQ/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

2、IDEA 也提供类似的功能查看历史文件,并且在弹出窗口内可以使用关键键快速查找。

快捷键如下：

* **Windows：ctrl + E**
* **Mac：⌘ +E**

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuCnbOzFs3NIDIFsmJrqlltib7dtL2N1DJXOtic0lJX9SoK5g80iaSAn64Q/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

另外 IDEA 中还有可以查看最近修改代码的位置，直接点击快速跳转。

快捷键如下：

* **Windows：ctrl + shift + E**
* **Mac：⌘ + ⇧  +E**

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuor9jqnMEuiaLFgNWNjl3KDVCNemefhfccc2OxaD5LftibSGMTNcOME3Q/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

小技巧：设置一个选项，限制标签页（Edit Tabs）数量。

![image-20210523164525810](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/idea%E4%BD%BF%E7%94%A8%E6%8A%80%E5%B7%A71.png)

3、**自动补全代码**

使用这个快捷键，可以自动补全代码末尾的分号，括号对等等，可以让我们少打很多字符。另外这个快捷键还会自动格式化完成的代码。

快捷键：

* **Windows：ctrl + shift + Enter（回车键）**
* **Mac：⌘ + ⇧  +⏎** 

**自动补全分号**

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuYQmGQSupqCXDb4VY9I131KuLsgUEZWricMCUicWEic41bedDlvZpIxeAg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

**自动补全括号对**

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuYQmGQSupqCXDb4VY9I131KuLsgUEZWricMCUicWEic41bedDlvZpIxeAg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

4、**快速抽取变量**

有时候新建了一个对象，忘记了创建了变量，就很麻烦，需要移动光标到前面，然后声明。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/LEFcpfxrbq6GN932uicD7rU53aSNMjWtutibaGCdiaXWSJLJicNL0N27EJLYcjn2Zc9e6nbYn0VphVfGusBPxvAC8g/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这种情况下，我们可以使用 IDEA 的重构功能-**Introduce Variable**。

快捷键如下：

* **Windows：ctrl + alt + V**
* **Mac：⌥ + ⌘  + V**

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuySPrLev3Pzo5mgJibvbZqWib2gjrqGocN5siaeRUznJoXMlzcZ4r0BSVw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

除了这种方式之外，最近还学到另外一种方式，使用 IDEA 后缀补全（**Postfix Completion**）。

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtuuSVAYGeicp6FAzFXVvXN7bph0m8BqcibhwCZrYjzNsKBHLQSBy6H2exg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

5、**重命名**

有时候手误会把边变量名拼写错误，等到自己发现时，这个变量已经被引用了多次，这时再修改，需要把所有引用的地方都修改一遍，这就很麻烦。

IDEA 重构功能-重命名（**Rename**）,可以修改命名，并且一键替换所有的引用的地方。

另外函数名，类名修改都可以使用这个快捷键。

快捷键如下：

* **Windows：shift + F6**
* **Mac： ⇧  + F6**

![img](https://mmbiz.qpic.cn/mmbiz_gif/LEFcpfxrbq6GN932uicD7rU53aSNMjWtunTWLPs6Ho1ZqhO5vWOmChkqFyZC4oeGV2tibPcmOULNbnib3eoXXttYQ/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

