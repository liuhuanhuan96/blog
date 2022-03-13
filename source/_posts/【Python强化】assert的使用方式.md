---
title: 【Python强化】assert的使用方式
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 51865
date: 2021-07-25 13:53:41
---

## assert 的作用

### 一、python assert的作用：

<!--more-->

[官方文档：](https://docs.python.org/3/reference/simple_stmts.html#assert)

> assert 断言成功则继续进行，断言失败则**程序报错（类似于java中的异常捕捉，自定义异常**）
>
> 1.断言能够别人更好的理解自己的代码
>
> 2.找出程序中逻辑不对的一方面
>
> 3.断言会提示某个对象会处于何种状态
>
> 4.另一方面，如果断言为假会抛出异常，很有可能终止程序

### 二、一般用法

~~~python
assert condition
# 用来让程序测试这个condition，如果condition为false，那么raise一个AssertionError出来。逻辑上等同于：
if not condition:
    raise AssertionError()
~~~



语法：`assert expression1 [, expression2]`

> `expresssion1` 是要判断的表达式，`expression2` 是可选的，用于返回错误信息

【注意】

- 不要使用断言验证数据，因为有可能程序被禁用断言
- 不要写出永远不会失败的断言

例如：

~~~python
def foo(a):
    assert a == 2,Exception('不等于2')
    print('ok',2)
 
if  __name__ == '__main__':
    foo(3)
~~~



