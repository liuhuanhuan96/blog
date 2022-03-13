---
title: 【Python强化】pyecharts可视化（史上最全）
tags:
  - Python
  - PyEcharts
categories:
  - Python
toc: true
abbrlink: 16689
date: 2021-07-25 14:02:53
---

## 一、介绍

[Echarts](https://github.com/ecomfe/echarts) 是一个由百度开源的数据可视化，凭借着良好的交互性，精巧的图表设计，得到了众多开发者的认可。而 Python 是一门富有表达力的语言，很适合用于数据处理。当数据分析遇上数据可视化时，[pyecharts](https://github.com/pyecharts/pyecharts) 诞生了。

<!--more-->

* 简洁的 API 设计，使用如丝滑般流畅，支持链式调用

* 囊括了 30+ 种常见图表，应有尽有

* 支持主流 Notebook 环境，Jupyter Notebook 和 JupyterLab

* 可轻松集成至 Flask，Django 等主流 Web 框架

* 高度灵活的配置项，可轻松搭配出精美的图表

* 详细的文档和示例，帮助开发者更快的上手项目

* 多达 400+ 地图文件以及原生的百度地图，为地理数据可视化提供强有力的支持

  [官网链接](https://pyecharts.org/#/zh-cn/intro)



## 二、安装

```python
pip install pyecharts
```

查看版本：

```python
import pyecharts

print(pyecharts.__version__)
```

