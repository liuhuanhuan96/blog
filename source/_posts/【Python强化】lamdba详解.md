---
title: 【Python强化】lamdba详解
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 57187
date: 2021-07-25 13:59:57
---

在Python中有两种函数，一种是def定义的函数，另一种是lambda函数，也就是大家常说的匿名函数。

与java中的lamdba类似，简化了代码，使代码看起来更加简洁流畅。 

<!--more-->

### 1.为什么使用lamdba

比如：我们需要计算两个数相加的和

传统的定义方式：

~~~python
def add(a,b):
  return a + b
~~~

lamdba表达式的形式：

~~~python
result = lamdba a,b:a+b
y = lambda a,b:a+b
#直接使用变量名作为方法名调用
print(y(1,2))  # 3
~~~



#### ==补充==map函数的使用方式：

**map()** 会根据提供的函数对指定序列做映射。

第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

map() 函数==语法==：

> ```
> map(function, iterable, ...)
> ```

- function -- 函数

- iterable -- 一个或多个序列

  ***Python 2.x 返回列表。***

  ***Python 3.x 返回迭代器。***

==demo:==

~~~python
>>>def square(x) :            # 计算平方数
...     return x ** 2
... 
>>> map(square, [1,2,3,4,5])   # 计算列表各个元素的平方
[1, 4, 9, 16, 25]
>>> map(lambda x: x ** 2, [1, 2, 3, 4, 5])  # 使用 lambda 匿名函数
[1, 4, 9, 16, 25]
 
# 提供了两个列表，对相同位置的列表数据进行相加
>>> map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
[3, 7, 11, 15, 19]

# .............python3.x
result = map(lambda x: x*x,[y for y in range(10)])
for i in result:
    print(i)
~~~

在这个简单的例子中，可以看到，lamdba使得代码看起来相对清爽，少了些代码的冗余，可以不用再去给一个函数命名，可以快速的实现一个简单的小功能，lamdba使得代码可读性更强，程序看起来更加简洁。

lamdba函数的==语法==：

> ```text
> lambda argument_list:expersion
> ```

语法中的argument_list是参数列表，它的结构与Python中函数(function)的参数列表是一样的，例如：a,b	a=1,b=2等等

lamdba虽可以简洁代码，但是对程序的执行效率无任何影响。

例如：

~~~python
import time
def add(a,b):
    return a+b



y = lambda a,b:a+b
print('def执行前：',time.time())
print(add(1,2))
print('def执行时间',time.time())
print('lamdba执行前：',time.time())
print(y(1,2))
print('lamdba执行时间',time.time())
~~~

result：

> def执行前： 1608178942.6293051
> 3
> def执行时间 1608178942.629337
> lamdba执行前： 1608178942.629343
> 3
> lamdba执行时间 1608178942.62935

可以看出两者并没有多大变化

### 2.lamdba匿名函数的优点

（1）可以直接赋一个变量，像函数一样去调用（把变量名当做函数名）

~~~python
y = lambda a,b:a+b
print(y(1,2))
~~~

​		也可以在函数后直接传入参数

~~~python
print((lambda a,b:a+b)(1,2))
~~~

(2) 将lambda函数作为参数传递给其他函数比如说结合map、filter、sorted、reduce等一些Python内置函数使用

~~~python
y = filter(lambda x:x%3==0,[1,2,3,4,5,6])for i in y:    print(i)
~~~

~~~python
result = map(lambda x: x*x,[y for y in range(10)])for i in result:    print(i)
~~~

与sorted函数结合使用，按照第一个元素排序

~~~python
sorted([('b',3),('a',2),('d',4),('c',1)],key=lambda x:x[0])print:[('a',2),('b',3),('c',1),('d',4)]
~~~

按照第二个元素排序

~~~python
sorted([('b',3),('a',2),('d',4),('c',1)],key=lambda x:x[1])print:[('c',1),('a',2),('b',3),('d',4)]
~~~

与reduce函数结合使用

~~~python
from functools import reduceprint(reduce(lambda a,b:'{},{}'.format(a,b),[1,2,3,4,5,6,7,8,9]))print:1,2,3,4,5,6,7,8,9
~~~

(3) def函数与lamdba结合使用

~~~python
def add(a):    return lambda b:a+bf = add(2)print(f(3))print: 5
~~~

(4) 字符串连接

~~~python
result = lambda x='wo',y='xiang',z='ni': x+y+zprint(result('wo shizhen d '))print: wo shizhen d xiangni
~~~

(5)判断字符串是否以某个字母开头有

~~~python
names = ['dwdw', 'Avf', 'rfegbn', 'Dqssqve ', 've n', 'Bfern', 'Zfer']result = filter(lambda x: x.startswith('r'),names)for name in result:    print(name)    print: rfegbn
~~~

(6) 求两个列表元素的和

~~~python
a = [1,2,3,4]b = [5,6,7,8]print(list(map(lambda x,y:x+y, a,b)))print: [6,8,10,12]
~~~

(7) 求字符串每个单词的长度

~~~python
sentence = "Welcome To Beijing!"words = sentence.split()lengths  = map(lambda x:len(x),words)print(list(lengths))print: [7,2,8]
~~~



参考：https://zhuanlan.zhihu.com/p/80960485?utm_source=wechat_timeline

