---
title: 【Python实战案例】基于tkinter实现简单登录注册
tags:
  - Python
categories:
  - Python
toc: false
abbrlink: 48204
date: 2021-11-01 19:37:40
---



话不多说，直接上代码

<!--more-->

```python
#encoding=utf-8
import tkinter
from tkinter import messagebox
# 初始化对象
login = tkinter.Tk()
# 定义标题名称
login.title("登录")
# 定义屏幕尺寸
login.geometry('200x200')
# 定义label标签文本  grid定义显示位置 布局管理器
tkinter.Label(login,text='登录').grid(row=0,column=0,columnspan=2)
tkinter.Label(login,text='用户名：').grid(row=1,column=0)
# 定义输入的文本框，类似于html中的text
name = tkinter.Entry(login)
name.grid(row=1,column=1)
# 定义label标签文本  grid定义显示位置
tkinter.Label(login,text='密  码：').grid(row=2,column=0,sticky=tkinter.E)
# 此种方式定义是为了避免出现‘NoneType’ object has no attribute ‘get’的错误
passwd = tkinter.Entry(login,show='*')
passwd.grid(row=2,column=1)

# 登录注册的方法
def success():
    if name.get() == 'root' and passwd.get() == '123':
        # 定义消息提示框
        messagebox.showinfo(title='successful',message='登录成功')
    else:
        messagebox.showerror(title='wrong',message='登录失败，用户名或密码错误')
# 定义登录的按钮，command绑定点击的事件
tkinter.Button(login,text='登录',command=success).grid(row=3,column=0,columnspan=2)

# 定义注册的方法
def register():
    register = tkinter.Tk()
    register.title('注册')
    register.geometry('200x200')
    tkinter.Label(register,text='用户注册').grid(row=0,column=0,columnspan=2)
    # 用户名输入框
    tkinter.Label(register,text='用户  名：').grid(row=1,column=0,sticky=tkinter.E)
    name = tkinter.Entry(register)
    name.grid(row=1,column=1)

    # 密码输入框
    tkinter.Label(register,text='密码：').grid(row=2,column=0,sticky=tkinter.E)
    password = tkinter.Entry(register,show='*')
    password.grid(row=2,column=1)

    # 密码确认
    tkinter.Label(register,text='确认密码：').grid(row=3,column=0)
    repassword = tkinter.Entry(register,show='*')
    repassword.grid(row=3,column=1)

    # 手机号码输入
    tkinter.Label(register,text='手机号：').grid(row=4,column=0,sticky=tkinter.E)
    phone = tkinter.Entry(register)
    phone.grid(row=4,column=1)

    # 身份证号输入
    tkinter.Label(register,text='身份证号：').grid(row=5,column=0)
    IDCard = tkinter.Entry(register)
    IDCard.grid(row=5,column=1)

    # 正则匹配
    def card(input_psd):
        string = "~!@#$%^&*()_+-*/<>,.[]\/"
        for i in string:
            if i in input_psd:
                return True
        return False

    # 注册的格式判断
    def registered():
        if not (any([x.isdigit() for x in name.get()]) and any([x.isalpha() for x in name.get()]) and card(name.get())):
            messagebox.showerror(title='wrong',message='注册失败，用户名格式错误，必须包括字母和数字以及特殊符号')
        elif len(password.get()) < 8:
            messagebox.showerror(title='wrong',message='注册失败，密码不应少于8位')
        elif password.get() != repassword.get():
            messagebox.showerror(title='wrong',message='注册失败，两次密码不相同')
        elif not (phone.get().isdigit() and len(phone.get()) == 11):
            messagebox.showerror(title='wrong',message='注册失败，请输入正确的11位手机号')
        elif len(IDCard.get()) != 18:
            messagebox.showerror(title='wrong',message='注册失败，请输入正确的18位身份证号')
        else:
            messagebox.showinfo(title='successful',message='注册成功！')

    tkinter.Button(register,text='注册',command=registered).grid(row=6,column=0,columnspan=2)

#定义执行按钮
tkinter.Button(login,text='还没有账号？点我开始注册！',command=register).grid(row=4,column=0,columnspan=2)
#开启窗口的主入口
login.mainloop()

```



执行效果

登录：

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/1.gif" alt="1" style="zoom: 50%;" />

