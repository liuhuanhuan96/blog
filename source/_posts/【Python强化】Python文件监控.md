---
title: 【Python强化】Python文件监控
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 8422
date: 2021-07-25 14:04:38
---

## 一、准备工作

Windows环境下打开Cmd(开始—运行—CMD)，苹果系统环境下请打开Terminal(command+空格输入Terminal)，准备开始输入命令安装依赖。

```shell
pip install watchdog
```

<!--more-->

## 二、基本使用

主要分为以下几个关键步骤：

* 1.配置各项信息；
* 2.生成事件处理器、监控器；
* 3.注册事件处理器、配置目录、递归执行（即同时监控子文件夹）；
* 4:启动。

具体实现代码如下：

```python
#encoding=utf-8
import sys
import time
import logging
from watchdog.observers import Observer
from watchdog.events import LoggingEventHandler



if __name__ == '__main__':
    # cmd 输入 python 脚本地址  监听文件路径


    logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(message)s', datefmt='%Y-%m-%d %H:%M:%S')
    path = sys.argv[1] if len(sys.argv) > 1 else '.'

    # 生成事件处理器对象
    event_handler = LoggingEventHandler()

    # 生成监控器对象
    observer = Observer()

    # 注册事件处理器，配置监控目录
    observer.schedule(event_handler, path, recursive=True)

    # 监控器启动-创建线程
    observer.start()


    # 以下代码是为了保证主线程运行
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        observer.join()
```

**运行**

cmd 输入：

```shell
python F:\PycharmProjects\Pytorch_frame\python\python基础代码练习\文件监听\listen.py e:/test
```

结果示意图如下：

![image-20210512143252524](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/Python%E6%96%87%E4%BB%B6%E7%9B%91%E6%8E%A7.png)

对文件的操作，增加，或者删除，或者修改，都会有有日志记录

## 三、 监控文件变化

实现自动提取文件高潮部分

```python
#encoding=utf-8
import sys
import time
import logging
from watchdog.observers import Observer
from watchdog.events import LoggingEventHandler
from pychorus import find_and_output_chorus


# 自动提取音乐文件中的高潮部分
class extractor(LoggingEventHandler):

    def on_created(self, event):
        super(LoggingEventHandler, self).on_created(event)
        what = 'directory' if event.is_directory else 'file'
        logging.info('Created %s: %s', what, event.src_path)
        NameExt = event.src_path.split('.')
        if NameExt[-1] == 'mp3':
            logging.info("mp3文件，提取音乐高潮中")
            output_path = "test_high.wav"
            find_and_output_chorus(event.src_path, output_path, 30)


if __name__ == '__main__':
    # cmd 输入 python 脚本地址  监听文件路径


    logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(message)s', datefmt='%Y-%m-%d %H:%M:%S')
    path = sys.argv[1] if len(sys.argv) > 1 else '.'

    # 生成事件处理器对象
    # event_handler = LoggingEventHandler()
    event_handler = extractor()

    # 生成监控器对象
    observer = Observer()

    # 注册事件处理器，配置监控目录
    observer.schedule(event_handler, path, recursive=True)

    # 监控器启动-创建线程
    observer.start()


    # 以下代码是为了保证主线程运行
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        observer.stop()

    observer.join()
```

![img](https://mmbiz.qpic.cn/mmbiz_png/h6NqozYcCQ76YR3XHOfh21JLia7tWXZxvznKlVElicDic3aW8m1BtIHgQmTDYPex3sSBjjRiathVEjTJSJUeib3VeDQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

