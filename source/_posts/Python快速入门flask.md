---
title: Python快速入门flask
tags:
  - Python
  - Flask
categories:
  - Flask
toc: true
abbrlink: 54258
date: 2021-08-04 01:28:00
---

## 一、介绍

Flask 是一个使用 Python 编写的轻量级 Web 应用程序框架。Armin Ronacher带领一个名为Pocco的国际Python爱好者团队开发了Flask。

<!--more-->

## 二、简单使用

```python
pip install flask
```

先安装对应的包

我们先写个简单的demo，然后来测试下：

```python
from flask import Flask

app = Flask(__name__)

@app.route("/index")
def test():
    return "hello world"

app.run()
```

然后我们右击运行，出现如下即表示运行成功

```python
 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

然后我们在浏览器中输入地址，可以看到

![image-20210804010736863](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/flask01.png)

## 三、无参传入

此时我们是传入的无参方式

```python
from flask import Flask
 
app = Flask(__name__)   #创建一个服务，赋值给APP

@app.route("/index")   # api接口 #指定接口访问的路径，支持什么请求方式get，post
#讲的是封装成一种静态的接口，无任何参数传入
def test():  #-----这里的函数名称可以任意取
    return "hello world"   # 返回数据

app.run()
```

我们可以指定固定的`host`和`port`,如下

```python
from flask import Flask
 
app = Flask(__name__)   #创建一个服务，赋值给APP

@app.route("/index")   # api接口 #指定接口访问的路径，支持什么请求方式get，post
#讲的是封装成一种静态的接口，无任何参数传入
def test():  #-----这里的函数名称可以任意取
    return "hello world"   # 返回数据

app.run(host="0.0.0.0",port=8000,debug=True)
```

## 四、有参传入

```python
from flask import Flask,request

app = Flask(__name__)   #创建一个服务，赋值给APP

@app.route("/index",methods=['post'])
def test():  #-----这里的函数名称可以任意取
    name = request.form.get('name')  #获取接口请求中form-data的username参数传入的值
    return name   # 返回数据

app.run(host="0.0.0.0",port=8000,debug=True)
```

获取传递参数的几种方式：

> request请求总体分为两类：
>
> 1.get请求 
>
> 访问时会在地址栏直接显示参数不安全，且参数大小比较小。
>
> 2.post请求 
>
> 参数不显示在地址栏，一般用户注册、登录都通过post请求完成。

request.form.get("key", type=str, default=None) 获取表单数据，

request.args.get("key")    获取get请求参数，

request.values.get("key") 获取所有参数。

**推荐使用request.values.get().**



地址栏中传递参数

```python
from flask import Flask

app = Flask(__name__)

@app.route("/index/<name>")
def test(name):
    return name

app.run()
```



![image-20210804012303699](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/flask02.png)



