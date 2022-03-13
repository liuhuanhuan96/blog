---
title: 【Python强化】对字典分别按照key值、value值进行排序
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 19241
date: 2021-11-01 19:27:49
---



### 1.sorted介绍

sorted(iterable,key,reverse)，sorted一共有iterable，key，reverse这三个参数。

其中iterable表示可以迭代的对象，例如可以是dict.items()、dict.keys()等，key是一个函数，用来选取参与比较的元素，reverse则是用来指定排序是倒序还是顺序，reverse=true则是倒序（从大到小），reverse=false则是顺序（从小到大），默认是reverse=false。

<!--more-->

### 2.按照ke y进行排序

直接使用sorted函数

```python
 my_dict = {'money': 250, 'age': 24, 'number': 12}
    print(sorted(my_dict.keys()))  
```

输出结果

```python
['age', 'money', 'number']
```

如果想要反向排序的话，那我们只需要加上一个参数`reverse=True`

```python
 my_dict = {'money': 250, 'age': 24, 'number': 12}
print(sorted(my_dict.keys(),reverse=True))  
```

输出结果

```python
['number', 'money', 'age']
```

### 3.按照value 进行排序

#### 3.1 	key使用lambda匿名函数取value进行排序

```python
d = {'lhh': 25, 'yl': 21, 'wcy': 32, 'yq': 19}
print(sorted(d.items(), key=lambda item: item[1]))
```

输出结果：

```python
[('yq', 19), ('yl', 21), ('lhh', 25), ('wcy', 32)]
```

如果我们需要倒序进行排序的话，我们只需要加上一个参数`reverse=True`

```python
d = {'lhh': 25, 'yl': 21, 'wcy': 32, 'yq': 19}
print(sorted(d.items(), key=lambda item: item[1]),reverse=True)
```

输出结果：

```python
[('wcy', 32), ('lhh', 25), ('yl', 21), ('yq', 19)]
```

#### 3.2 使用operator的itemgetter进行排序

```python
import operator
    print(sorted(d.items(), key=operator.itemgetter(1)))   
```

输出结果：

```python
#[('yq', 19), ('yl', 21), ('lhh', 25), ('wcy', 32)]
```

#### 3.3 使用zip函数将map分成2个元祖再进行排序

```python
f = zip(my_dict.keys(),my_dict.values())
    c = sorted(f)
    print(c)
```

输出结果

```python
[('number', 12), ('money', 250), ('age', 24)]
```

### 4.取出排序的前n个value值和key值

```python
# 排序
    test_sort = dict(sorted(test.items(), key=lambda e: e[1]))
    print(test_sort)
    # 取出前几个， 也可以在sorted返回的list中取前几个
    required_cnt = 3
    cnt = 0
    for key, value in test_sort.items():
        cnt += 1
        if cnt > required_cnt:
            break
        print("{}:{}".format(key, value))
```

输出结果

```python
{'key2': 10, 'key3': 15, 'key1': 20, 'key4': 21}
key2:10
key3:15
key1:20
```

