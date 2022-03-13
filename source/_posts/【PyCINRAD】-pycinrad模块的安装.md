---
title: 【PyCINRAD】 pycinrad模块的安装
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 52064
date: 2021-07-25 13:51:47
---



	**PyCINRAD**模块用于读取**CINRAD**雷达数据，进行相关计算并可视化的模块，该模块支持**SA/SB/CB**三种雷达数据格式

​     **GitHub**主页：https://github.com/CyanideCN/PyCINRAD/blob/master/README_zh.md

​	**PyCINRAD源码**：https://github.com/liuhuanhuan963019/PyCINRAD.git

<!--more-->

# 安装要求

- **Python 3.6**
- **Cartopy**
- **Metpy**
- **Shapefile**
- **Pykdtree**(可选安装)

# 安装步骤

## 1. 安装Anaconda

​     在众多Python开发环境中，Anaconda3因为集成安装大量扩展库，得到了很多Python学习者和开发人员尤其是科研人员的喜爱。
​     安装教程推荐https://www.jianshu.com/p/169403f7e40c

## 2. 安装 Microsoft visual c++ 14.0

​     下载地址: https://pan.baidu.com/s/169X5Q6KMon4VCcsbP0UpAA，提取码: k7qs

> 如果出现了.Net framework版本过低，小于4.5的最低版本要求，重新安装 .Net framework 更高的版本，下载地址：https://support.microsoft.com/en-us/help/3151800/the-net-framework-4-6-2-offline-installer-for-windows，之后再安装Microsoft visual c++ 14.0

## 3. Shapefile版本修正

​     这个库本身Anaconda3就有（pyshp库），不需要再安装。在Anaconda3里有2个版本，1.2.12和2.0.1版本，但是pyshp 2.0.1版本绘图会出错，我们通过anaconda使用1.2.12版本：

### 3.1 搜索pyshape

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glpwkphg5aj30gs03yq2v.jpg)

### 3.2 选择1.2.12版本

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glpwkqku7wj30h10ae74k.jpg)

### 3.3 点击右下角apply安装，此时会有弹窗，确定即可

![img](https://tva1.sinaimg.cn/large/0081Kckwgy1glpwknzf9rj307c02gq2p.jpg)

## 4 安装Cartopy、Metpy、Pykdtree包

在anaconda中，你所创建的虚拟环境下执行下面代码：

```
conda install -c pycinrad cartopy
conda activate pycinrad
pip3 install Cartopy
pip3 install Metpy
pip3 install Pykdtree
```

## 5. 安装PyCINRAD

同样环境下执行

```
pip3 install cinrad
```
