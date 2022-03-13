---
title: Python标准库之json
tags:
  - Python
  - Json
categories:
  - Python
  - Json
toc: true
abbrlink: 33923
date: 2021-11-22 22:37:29
---



# Python标准库之json

## 一、什么是json

* json是一种轻量级的文本数据交换格式
* json独立于其他语言
* json具有自我描述性，更好理解
* json比xml更小、更快，更容易解析

<!--more-->

## 二、json格式

```json
{
    "name"："lhh",
   	"age":"20"
}
```

> name = lhh
>
> age = 20

## 三、json标准库的作用

* ### 使用json字符串生成python对象（load）

* ### 由python对象格式成为json字符串（dump）

## 四、数据的类型转换

将数据从python转换到json格式，在数据类型上会有什么变化呢，如下表所示：

| Python         | JSON   |
| -------------- | ------ |
| dict           | object |
| list,tuple     | array  |
| str            | string |
| int,float,int- | number |
| True           | true   |
| False          | false  |
| None           | null   |

## 五、使用方式

json模块的使用很简单，对于大多数，我们只需要使用以下4中方式：

| 方法               | 功能                                         |
| ------------------ | -------------------------------------------- |
| json.dump(obj，fp) | 将python数据类型转换并保存到json格式的文件内 |
| json.dumps(obj)    | 将python数据类型转换为json格式的字符串       |
| json.load(obj)     | 将json格式的文件中读取数据并转换为python类型 |
| json.load(s)       | 将json格式的字符串转换为python的类型         |

## 六、实战操作

### 1.python转换为json字符串

```python
#从python对象格式化一个json  string
person = {"name":"lhh","age":25}
print(person)

#转换为json字符串
jsonStr = json.dumps(person)
print(jsonStr)
```

输出：

![image-20211122220234477](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122220234477.png)

> **在python中定义json的时候，可以使用单引号，也可以使用双引号。但是最后在输出的时候，输出的是一个单引号，以字典的方式进行输出的。但是在我们进行json格式转换之后，我们就会变成一个标准的json格式的字符串，即双引号修饰的字符串**

### 2.json文件生成

```python
json.dump(person,open("data.json","w"))
```

文件输出：

![image-20211122220739657](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122220739657.png)

 此时输出到文件的时候不是json缩进的格式，此时我们只需要指定参数`indent`就可以输出执行格式

```python
#转换为json字符串
jsonStr = json.dumps(person,indent=4)
print(jsonStr)

json.dump(person,open("data.json","w"),indent=4)
```

```python
{'name': 'lhh', 'age': 25}
{
    "name": "lhh",
    "age": 25
}

```

![image-20211122220957756](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122220957756.png)

此时我们输出到文件中也是个格式化后的结果

### 3.生成文件的key进行排序

我们需要对我们的key进行排序，即按照字母的顺序进行排序的话，我们只需要指定参数`sort_keys`即可

```python
#转换为json字符串
jsonStr = json.dumps(person,indent=4,sort_keys=True)
print(jsonStr)

json.dump(person,open("data.json","w"),indent=4,sort_keys=True)
```

我们来看下最后的实际效果:

```python
{'name': 'lhh', 'age': 25}
{
    "age": 25,
    "name": "lhh"
}
```

![image-20211122221313632](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211122221313632.png)

### 4.json string 转换成python对象

第一种转换格式

```python
#json string 转换成python对象
# load loads
s = '{"name":"lhh","age":25,"home":["南京","淮安"],"only":true}'
pythonObj = json.loads(s)
print(pythonObj)
print(type(pythonObj))
```

输出：

```python
{'name': 'lhh', 'age': 25, 'home': ['南京', '淮安'], 'only': True}
<class 'dict'>
```

第二种转换格式

```python
s2 = '["name","lhh","age",25,{"home":["南京","淮安"],"only":true}]'
pythonObj2 = json.loads(s2)
print(pythonObj2)
print(type(pythonObj2))
```

输出

```python
['name', 'lhh', 'age', 25, {'home': ['南京', '淮安'], 'only': True}]
<class 'list'>
```

我们看到两种最后输出的格式是不一样的

### 5、从文件读取json并生成python对象

```python
#读取json文件
pythondata = json.load(open("data2.json","r"))
print(pythondata)
print(type(pythondata))
```

文件内容:

```json
{
    "age": 25,
    "name": "lhh",
    "home": [
      "南京",
      "淮安"
    ]
}
```

输出:

```python
{'age': 25, 'name': 'lhh', 'home': ['南京', '淮安']}
<class 'dict'>
```

