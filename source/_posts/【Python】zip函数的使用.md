---
title: 【Python】zip函数的使用
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 1937
date: 2021-07-25 13:55:44
---

## 描述

**zip()** 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。

我们可以使用 list() 转换来输出列表。

<!--more-->

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 ***** 号操作符，可以将元组解压为列表。

## 语法

zip 语法：

```python
zip([iterable, ...])
```

参数说明：

* iterabl -- 一个或多个迭代器;

## 返回值

返回一个对象。

## 实例demo

 **`返回一个对象`**

```python
#encoding=utf-8
import numpy as np
a = [1,2,3]
b = [4,5,6]
c = [4,5,6,7,8]
d = zip(a,b)
print(d)
# 转换为list的形式,返回的是一个元组的形式
d_list = list(d)
for i in d_list:
    print(i)
```

print:

```python
# print    <zip object at 0x7f94a3699140>
# print(1, 4)
#      (2, 5)
#      (3, 6)
```

**`当只有一个参数的时候`**

```python
a=[1,2,3]
zz=list(zip(a))
print(zz)
```

print:

```python
# print [(1,), (2,), (3,)]
```

**`当没有参数的时候`**

```python
zz=list(zip())
print(zz)
```

print:

```python
[]
```

**`压缩长度不一致的数组，元素的个数与长度最短的数组相关`**

```python
a = [1,2,3]
b = [4,5,6]
c = [4,5,6,7,8]
e_list =  list(zip(a,c))
print(e_list)
```

print:

```python
# print [(1, 4), (2, 5), (3, 6)]
```

**`与 zip 相反，zip(*) 可理解为解压，返回二维矩阵式`**

```python
a = [1,2,3]b = [4,5,6]a1,a2 = zip(*zip(a,b))print(a1,a2)
```

print:

```python
# print (1, 2, 3) (4, 5, 6)
```

**`通过解压操作之后，输出的是元组类型，而并不是原来的类型，但是值并不会发生改变，除非原来的参数列表长度不一样，看下面的代码`**

```python
import numpy as npa = [1,2,3]b = [3,4,5,6,7]# zz = list(zip(a,b))a,b = zip(*zip(a,b))print(a,b)
```

print

```python
(1, 2, 3) (3, 4, 5)
```

unzip后的列表b的值都少了，但是里面的值还是不变的。



`扩展`：

机器学习模型训练中，经常需要打乱数据集，用 zip() 函数可以实现如下：

```python
#encoding=utf-8
import random
import numpy as np

# 设置随机种子,保证每次生成随机相同，方便重现
random.seed(1)

x = [1, 2, 3, 4, 5, 6]
y = [0, 1, 0, 0, 1, 1]

zipped_data = list(zip(x,y))
# 打乱样本的数据 打乱样本的数据 random使用的是原地操作的方式，没有任何 返回值
random.shuffle(zipped_data)
# print(zipped_data)
# 打乱后[(1, 0), (4, 0), (2, 1), (5, 1), (3, 0), (6, 1)]
# 原始 [(1, 0), (2, 1), (3, 0), (4, 0), (5, 1), (6, 1)]

# zip(*)反向解压，map()逐项转换类型，list()做最后转换
zipped_data2 = list(map(list,zip(*zipped_data)))
print(zipped_data2)

print(zipped_data2[0])
print(zipped_data2[1])
```

print:

```python
[[3, 4, 6, 1, 5, 2], [0, 0, 1, 0, 1, 1]]
[3, 4, 6, 1, 5, 2]
[0, 0, 1, 0, 1, 1]
```
