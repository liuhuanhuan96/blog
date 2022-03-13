---
title: 【Python强化】__slots__限制类实例动态添加属性和方法
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 63651
date: 2021-07-25 13:58:59
---



Python中允许动态的对类或实例对象添加属性和方法，类方法大致分为 实例方法、静态方法和类方法，在Python中允许动态的添加，但是对于实例对象，我们只允许动态的添加实例方法，不能添加类方法和静态方法

<!--more-->

`如果单纯的给实例对象添加方法，不会影响类的其他方法，如果给类添加方法的话，则会改变所有的实力对象`

**example**:

```python
class Student:
    pass

#定义了一个实例方法
def info1(self):
    print("调用实例方法1")
    
#使用注释的方式规定了这是一个类对象,约定俗称的方式规定为cls
@classmethod
def info2(cls):
    print("调用类方法1")
    
#使用注释的方式规定了这是一个静态对象,约定俗称的方式规定为cls
@staticmethod
def info3(cls):
    print("调用静态方法")

#类可以动态添加以上 3 种方法，会影响所有实例对象
Student.info1 = info1
Student.info2 = info2
Student.info3 = info3

stu = Student()
# tu 可以使用上面三种方法
stu.info1()
stu.info2()
stu.info3()

#类实例对象只能动态添加实例方法，不会影响其它实例对象
stu1 = Student()
stu1.info1 = info1
```

**print**

```python
调用实例方法1
调用类方法1
调用静态方法
```

显然，动态给类或者实例对象添加属性或方法，是非常灵活的。但与此同时，如果胡乱地使用，也会给程序带来一定的隐患，即程序中已经定义好的类，如果不做任何限制，是可以做动态的修改的。

Python 提供了 __slots__ 属性，限制了给实例对象动态地添加属性或方法。

`__slots__ 只能限制为实例对象动态添加属性和方法，而无法限制动态地为类添加属性和方法。`

__slots__ 属性值其实就是一个元组，只有其中指定的元素，才可以作为动态添加的属性或者方法的名称。如下列出：

```python
class Student:
    __slots__ = ("name","age","id")
    pass
```

可以看出， Student类中指定了 __slots__ 属性，这意味着，该类的实例对象仅限于动态添加 name、age、id这 3 个属性以及 name()、age() 和 id() 这 3 个方法。

> 对于动态添加的方法，__slots__ 限制的是其方法名，并不限制参数的个数。

比如，在 Student类的基础上，添加如下代码并运行：

```python
def age(self,name):
    print("正在调用实例方法",self.name)
stu = Student()
stu.name = "lhh"
#为 clang 对象动态添加 info 实例方法
stu.age = age
stu.info(stu,20)
```

**print**:

```python
正在调用实例方法 lhh
```

还是在Student 类的基础上，添加如下代码并运行：

```python
def id(self,name):
    print("正在调用实例方法",self.name)
stu = Student ()
stu.name = "lhh"
stu.test = id
stu.test(stu,"haha")
```

报错：

```python
Traceback (most recent call last):
  File "F:/PycharmProjects/Pytorch_frame/python/python基础代码练习/__slots.py", line 52, in <module>
    stu.test = id
AttributeError: 'Student' object has no attribute 'test'
```

根据 __slots__ 属性的设置，Student 类的实例对象是不能动态添加以 test为名称的方法的。

另外本节前面提到，__slots__ 属性限制的对象是类的实例对象，而不是类，因此下面的代码是合法的：

```python
def info(self):
    print("正在调用实例方法")
Student.test = info
stu = Student()
stu.test()
```

**可以正常执行**

此外，__slots__ 属性对由该类派生出来的子类，也是不起作用的。例如如下代码：

```python
class Student:    __slots__ = ('name','add','mul')#Student 的空子类class Boy(Student):    pass#定义的实例方法def mul(self):    print("正在调用实例方法")boy = Boy()#为子类对象动态添加 say() 方法boy.say = mulboy.say(boy)
```

print:

```python
正在调用实例方法
```



显然，__slots__ 属性只对当前所在的类起限制作用。

因此，如果子类也要限制外界为其实例对象动态地添加属性和方法，必须在子类中设置 __slots__ 属性。





参考文章：（http://c.biancheng.net/view/2291.html）
