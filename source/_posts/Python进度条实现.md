---
title: Python进度条实现
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 13121
date: 2021-11-01 19:30:55
---



### 1.引言

在Python项目中，有时需要输出程序的运行进度，会print出【1/100】【50/100】等简单的字符串，殊不知Python有一些超级好用的第三方库，几行代码就可以实现进度条显示，本文介绍两个常用的进度条库：**tqdm**和**progressbar**。

<!--more-->

### 2.tqdm

安装

```shell
pip install tqdm
```

案例：

```shell
import time
from tqdm import tqdm

for i in tqdm(range(100)):
    time.sleep(0.1)

```

![img](https://tva1.sinaimg.cn/large/008i3skNgy1gvhhixyx4ng60oh016t9m02.gif)

tqdm参数设置

- desc：进度条标题
- total：迭代总次数
- ncols：进度条总长度
- ascii：使用ASCII字符串作为进度条主体
- bar_format：自定义字符串格式化输出
- mininterval：最小更新间隔，单位：秒
- maxinterval：最大更新间隔，单位：秒
- postfix：以字典形式传入

tqdm自定义参数的代码实现

```python
import time
from tqdm import tqdm

for i in tqdm(range(100), desc='Progress', ncols=100, ascii=' =', bar_format='{l_bar}{bar}|'):
    time.sleep(0.05)

```

![tqdm2](https://tva1.sinaimg.cn/large/008i3skNgy1gvhhk1x7l7g60vm016jru02.gif)

### 3.progressbar

安装

```python
pip install progressbar
```

案例：

```python
import time
from progressbar import *

progress = ProgressBar()
for i in progress(range(100)):
    time.sleep(0.05)
    print('')

```

![progressbar1](https://tva1.sinaimg.cn/large/008i3skNgy1gvhhkzolzfg60vq05gjxj02.gif)
