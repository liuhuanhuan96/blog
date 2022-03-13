---
title: 【Python强化】tkinter使用教程
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 37133
date: 2021-11-01 19:36:40
---



## 一、Tkinter介绍

Tkinter 是 `Python`标准 GUI 库。Python 使用 Tkinter 可以快速的创建 GUI 应用程序。由于 Tkinter 是内置到 python 的安装包中、只要安装好 Python 之后就能 import Tkinter 库、而且 IDLE 也是用 Tkinter 编写而成。

<!--more-->

相关的还有Pyqt5

## 二、使用方式

* 导入tkinter模块
* 创建相关控件
* 指定控件所属对象
* 告诉GM产生相关对象

```python
import tkinter

top = tkinter.Tk()
top.mainloop()
```

`效果图`：

![img](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/aHR0cHM6Ly9pbWcyMDIwLmNuYmxvZ3MuY29tL2Jsb2cvMTc4MzAzMC8yMDIwMDUvMTc4MzAzMC0yMDIwMDUyMDE5MjM1NTkwMy0xNTY5ODUzMDkucG5n)

## 三、窗口主体设置

每一个 tkinter 应用的主体框架都可以包含下面这部分. 定义 `window` 窗口 和 `window`的一些属性, 然后书写窗口内容, 最后执行`window.mainloop`启动应用程序。

```python
import tkinter

top = tkinter.Tk()
top.title("my first window")
top.geometry("500x500")
top.mainloop()
```

![image-20211031174524624](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211031174524624.png)

## 四、窗口内容

### 标签设置

```python
window = tkinter.Tk()
window.title("my first window")
window.geometry("500x500")
#定义一个标签
label = tkinter.Label(window,
                      text="hello world!!!", #文本内容
                      bg="red", #背景颜色
                      font=('Arial',12),# 字体设置
                      width=15,height=2 # 标签的长宽
                      )
label.pack()   #固定窗口位置
window.mainloop()
```

![image-20211031175116582](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211031175116582.png)

我们也可以通过变量的形式控制标签的显示, 这时我们引入按钮 `tk.Button` 的概念, 没点一次按钮, 标签变化一次. 用一下内容替换上面的标签. 并把需要变化的文字存成变量 `var`:

```python
window = tkinter.Tk()
window.title("my first window")
window.geometry("500x500")
# 定义文字变量存储器
var = tkinter.StringVar()
lable = tkinter.Label(window,
                      textvariable=var, #textvariable替代text，因为这个可以进行随机改变
                      bg='green', font=('Arial', 12), width=15, height=2)
lable.pack()
window.mainloop()
```

### 按钮设置：

```python
button = tkinter.Button(window, 
    text='hit me',      # 显示在按钮上的文字
    width=15, height=2, 
    command=hit_me)     # 点击按钮式执行的命令
button.pack()    # 按钮位置
```

我们进行点击判断：	

```python
on = False  # 默认初始状态为 False
def hit_me():
    global on
    if on == False:     # 从 False 状态变成 True 状态
        on = True
        var.set('you click me')   # 设置标签的文字为 'you hit me'
    else:       # 从 True 状态变成 False 状态
        on = False
        var.set('') # 设置 文字为空
```

新增一个按钮，按钮实战，绑定点击事件

```python
import tkinter as tk
#创建窗口
window=tk.Tk()
window.title('Mywindow')#窗口的标题
window.geometry('200x100')#窗口的大小
#定义一个lable
var=tk.StringVar()#定义一个字符串变量
label = tk.Label(window,
    textvariable=var,    # 标签的文字
    bg='green',     # 标签背景颜色
    font=('Arial', 12),     # 字体和字体大小
    width=15, height=2  # 标签长宽
    )
label.pack()    # 固定窗口位置

#定义一个全局变量，
flag=False
#按钮的函数
def click_me():
    global flag#声明全局变量
    if flag==False:
        flag=True
        var.set('click me!')
    else:
        flag=False
        var.set('null')
button = tkinter.Button(window,text="点我",
                        width=15,
                        height=2,
                        command=click_me)# 绑定执行方法
button.pack()
window.mainloop()
```

![image-20211101160629239](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211101160629239.png)



### 文本框

窗口内容

创建按钮分别触发两种情况

```python
b1 = tk.Button(window,text="one",width=15,height=2,command=one)
b1.pack()

b2 = tk.Button(window,text="two",command=two)
b2.pack()
```

创建输入框entry，用户输入任何内容都显示为* 类似于html中的password

```python
#encoding=utf-8
import tkinter as tk

window = tk.Tk()
window.title("我的第一个")
window.geometry("500x500")
en = tk.Entry(window,show="*")
en.pack()
window.mainloop()
```

![image-20211101161125008](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211101161125008.png)

创建一个显示的文本框

```python
import tkinter as tk

window = tk.Tk()
window.title("我的第一个")
window.geometry("500x500")
en = tk.Text(window,height=5)
en.pack()
window.mainloop()
```

![image-20211101161245624](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211101161245624.png)

定义触发事件时的函数

`注意：因为Python的执行顺序是从上往下，所以函数一定要放在按钮的上面`

```python
def one():
    var = en.get()
    t.insert('one',var)

def two():
    var = en.get()
    t.insert('two',var)
```

实战代码：

```python
import tkinter as tk

window = tk.Tk()
window.title("我的第一个")
#定义窗口尺寸大小
window.geometry("500x500")
# 定义一个输入框  如果我们需要定义的是输入的密码，我们此时可以定义为show="*"
en = tk.Entry(window,show=None)
en.pack()
#这里还可以定义字符串插入的具体位置，比如tk.insert('2.2',var)，表示插入到第2行第2列
def one():
    var = en.get()
    text.insert('insert',str(var))

def two():
    var = en.get()
    text.insert('end',str(var))

# 定义两个执行函数的按钮
one_bt = tk.Button(window,text="one",width = 15,height =2,command=one)
one_bt.pack()
two_bt = tk.Button(window,text="two",width = 15,height =2,command=two)
two_bt.pack()
text = tk.Text(window,height=2)
text.pack()
window.mainloop()
```

![image-20211101162659306](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211101162659306.png)

### listbox 列表部件

创建一个label用于显示

```python
var = tk.StringVar()   
label =tk.Label(window,bg='yellow',width=4,textvariable=var1)
label.pack()
```

创建一个用于点击的事件

```python  
 def print_selection():
    value = lb.get(lb.curselection())   #获取当前选中的文本
    var1.set(value)     #为label设置值 
```

创建一个Listbox和变量var2，并将var2的值赋给Listbox

```python
var2 = tk.StringVar()
var2.set((11,22,33,44)) #为变量设置值

#创建Listbox

lb = tk.Listbox(window, listvariable=var2)  #将var2的值赋给Listbox

#创建一个list并将值循环添加到Listbox控件中
list_items = [1,2,3,4]
for item in list_items:
    lb.insert('end', item)  #从最后一个位置开始加入值
lb.insert(1, 'first')       #在第一个位置加入'first'字符
lb.insert(2, 'second')      #在第二个位置加入'second'字符
lb.delete(2)                #删除第二个位置的字符
lb.pack()
```

实战代码：

```python
import tkinter as tk
window = tk.Tk()
window.title("listbox")
window.geometry("500x500")
#创建一个label
var1 = tk.StringVar()
label = tk.Label(window,bg="red",width=4,textvariable=var1)
label.pack()
#按钮事件
def print_selection():
    value = lb.get(lb.curselection()) # 获取当前选中的文本
    var1.set(value)

#创建一个按钮
b1 = tk.Button(window,text="print selection",width=15,height=2,command=print_selection)
b1.pack()
#创建一个listBox和变量var2,并将var2的值赋给listbox
var2 = tk.StringVar()
var2 = tk.StringVar()
var2.set((11,22,33,44)) #为变量设置值

#创建Listbox

lb = tk.Listbox(window, listvariable=var2)  #将var2的值赋给Listbox

#创建一个list并将值循环添加到Listbox控件中
list_items = [1,2,3,4]
for item in list_items:
    lb.insert('end', item)  #从最后一个位置开始加入值
lb.insert(1, 'first')       #在第一个位置加入'first'字符
lb.insert(2, 'second')      #在第二个位置加入'second'字符
lb.delete(2)                #删除第二个位置的字符
lb.pack()
window.mainloop()
```

![image-20211101164022779](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211101164022779.png)

#### radiobutton选择按钮

首先我们需要定义一个 `var` 用来将 radiobutton 的值和 Label 的值联系在一起. 然后创建一个radiobutton部分:

```python
var = tk.StringVar()
l = tk.Label(window, bg='yellow', width=20, text='empty')
l.pack()

r1 = tk.Radiobutton(window, text='Option A',
                    variable=var, value='A',
                    command=print_selection)
r1.pack()
```

其中`variable=var`, `value='A'`的意思就是，当我们鼠标选中了其中一个选项，把value的值`A`放到变量var中，然后赋值给`variable`

触发事件：

我们将定义一个功能, 用来对选择的 radiobutton 进行操作. `print_selection` 功能就是选择了某个 radiobutton 后我们会在屏幕上打印的选项.

```python
def print_selection():
    l.config(text='you have selected ' + var.get())
```

当触发这个函数功能时，我们的 label 中就会显示 text 所赋值的字符串即 ‘you have selected’, 后面则是我们所选中的选项 var.get()就是获取到变量 var 的值， 举个例子就是我们一开始所做的将选项 “option A” 选中时的值以 “A” 放入 var 中， 所以获取的也就是A 即如果我们这时候选中 “option A” 选项，label显示的值则是 “you have selected A”.

代码实战：

```python
#encoding=utf-8
import tkinter as tk

window = tk.Tk()
window.title("我的第一个")
#定义窗口尺寸大小 必须是X 而不是*
window.geometry("500x500")

#创建一个label
var = tk.StringVar()
label = tk.Label(window,bg="red",width=20,height=2,text="empty")
label.pack()
#实现将选择的选项显示label
def print_selection():
    label.config(text="you have selected"+var.get())

#创建几个Radiobutton
r1 = tk.Radiobutton(window,text="Option A",variable=var,value="A",command=print_selection)
r1.pack()
r2 = tk.Radiobutton(window,text="Option B",variable=var,value="B",command=print_selection)
r2.pack()
r3 = tk.Radiobutton(window,text="Option C",variable=var,value="C",command=print_selection)
r3.pack()
r4 = tk.Radiobutton(window,text="Option D",variable=var,value="D",command=print_selection)
r4.pack()
window.mainloop()
```

![image-20211101164814878](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211101164814878.png)
