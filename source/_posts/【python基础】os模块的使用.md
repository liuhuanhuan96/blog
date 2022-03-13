---
title: 【python基础】os模块的使用
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 12524
date: 2021-07-25 13:58:06
---


## os简介

os 模块是关于操作系统操作调用的相关模块，对文件进行重命名、删除等一系列操作，在python中可以用os模块

os模块提供了一些系统级别的操作

[官网api](https://docs.python.org/3.9/whatsnew/3.9.html#os)

<!--more-->

## 相对路径与绝对路径

==绝对路径:==是指文件在硬盘上真正存在的路径。那么如果要使用绝对路径指定网页的背景图片就应该使用 以下语句：

~~~shell
/Users/liuhuanhuan/PycharmProjects/blog/os模块操作/os.md
~~~

>  注: Mac os /linux 中可直接使用pwd查看当前文件的绝对路径



==相对路径==，就是相对于自己的目标文件位置。

> 在同一个目录: <blog>  (blog为项目的主目录)
>
> 在其所在目录的子目录里: <os模块操作> （此目录为blog的二级目录）
>
> 在其所在目录的上级目录里: <../os.md>  (在相对路径里常使用“../”来表示上一级目录。如果有多个上一级目录，可以使用多个“../”.)
>
> 在其所在目录的上级目录里的os子目录里:<./os/os.md>



## 常见函数

### 1. getcwd()

>  		作用：返回当前工作目录

~~~python
import os
print(os.getcwd())
~~~

### 2. rename(old, new)

> 作用：修改文件名称
>
> 注: old 的目录必须是存在的，否则报错

~~~python
import os
os.rename('1.py','2.py')
~~~

### 3. remove(filename)

> 作用：删除指定的文件，如果 path 是目录则会抛出 OSError 

~~~python
import os
os.remove('3.py')
~~~

### 4. mkdir(name)

> 作用：创建单级目录

~~~python
import os
os.mkdir('gl')
os.mkdir("/Users/lhh/Downloads/idea")
~~~

### 5. rmdir(filename)

> 作用：删除单级目录
>
> 注：若存在子目录，则无法删除，必须为空且存在

~~~python
import os
s.rmdir('gl')
os.rmdir("/Users/lhh/Downloads/idea")  #删除失败。只能删除目录文件下面是空的
# 如果要删除非空目录的话，就需要调用shutil模块
import shutil
shutil.rmtree("/Users/lhh/Downloads/idea")  #成功删除非空的文件夹
~~~

### 6.chdir(filename)

> 作用：改变当前文件的工作目录

~~~python
import os
os.chdir('../')
~~~

### 7.listdir(filename)

> 作用：返回当前目录下所有文件和文件夹，注意 path 是目录路径

~~~python
import os# 初始写法file_list = os.listdir("dname")for name in file_list:  #打印列表的名称	print(name)     #新写法#使用with自动的去释放资源with os.scandir("/Users/liuhuanhuan/") as entries:           for entry in entries:            print(entry.name)            pass
~~~

==Demo==

~~~python
#示范:查看一个文件夹下所有的文件basePath = "/Users/liuhuanhuan/"for entry in os.listdir(basePath):      # if os.path.isfile(os.path.join(basePath,entry)):   #只显示是文件的目录文件名称#     #     print(entry)    if os.path.isdir(os.path.join(basePath,entry)):   #只显示是文件夹的目录名称        print(entry)        pass
~~~





### 8.path.join(filename1,filename2....)

> 作用：文件路径地址拼接

~~~python
import ospath = os.path.join(os.getcwd(),'gl')
~~~

### 9.makedirs(filename)

> 作用：递归创建目录,只是目录，文件无法创建
>
> filename 只有最后一层文件夹不存在，前几级必须是已存在的目录，否则创建失败

~~~python
import osos.makedirs("/Users/lhh/Downloads/idea/l/h/h/w/c/y/wo/ai/ni")  #允许创建多级目录
~~~

### 10.write(path, str)

> 作用：将 bytes 字符串 str 写入 path 所指的文件

~~~python
import osos.write('/Users/lhh/Downloads/a.txt','miss you')
~~~

### 11.chmod(filename)

> 作用：改变文件的权限

~~~python
import osos.chmod('/Users/lhh/Downloads/a.txt')
~~~

### 13.pardir

> 作用：指代上一级当前目录

~~~python
import osprint(os.pardir)
~~~

### 14.name

> 作用：指代当前使用的 操作系统（包括‘java’,'mac'等）

~~~python
import osprint(os.name)
~~~



### 15.linesep

> 作用：当前平台使用的行终止符（win下为‘\r\n’,linux下为‘\n’）

~~~python
import osprint(os.linesep)
~~~



**<u>*以上均为常使用的方法：*</u>**

## *附录：*

==***os方法大全***==

> ***os.path模块***
>
> os.path.isdir(‘name’) 判断是否为目录  返回bool
>
> os.path.isfile(‘name’) 判断是否为文件  返回bool
>
> os.path.islink(‘name’)判断是否为链接  返回bool
>
> os.path.getsize(‘name’) 返回文件大小，如果文件不存在 返回错误
>
> os.path.abspath(‘file_name’) 返回的是file_那么的绝对路径
>
> os.path.split(‘file_path’) 返回file_path分割成目录和文件名，以元组方式返回
>
> os.path.exists(‘file_path’) 如果file_path存在 返回True 反之返回False
>
> os.path.join(‘file_path’,’file_name’) 连接目录和文件名或者目录
>
> os.path.isabs() 判断是否是绝对路径
>
> os.path.exists() 检验给出的路径是否真地存
>
> os.path.splitext() 分离扩展名
>
> os.path.dirname() 获取路径名
> os.path.basename() 获取文件名
> os.system()  运行shell命令
> os.getenv() 与os.putenv() 读取和设置环境变量
> os.stat（file） 获取文件属性
> os.exit（） 终止当前进程
> os.path.getsize（filename）获取文件大小
>
> ***import time 模块***
>
> Time.ctime() 返回本地时间
>
> os.path.getatime() 文件或者目录最后访问的时间
>
> os.path.getmtime()       最后修改的时间
>
> os.path.getctime()       创建时间
>
> 



==代码综合实操：== 

~~~python
#coding=utf-8 import  reimport  osimport  time#str.split(string)分割字符串#'连接符'.join(list) 将列表组成字符串def  change_name(path):     if  not  os.path.isdir(path)  and  not  os.path.isfile(path):         return  False     if  os.path.isfile(path):         file_path  =  os.path.split(path)  #分割出目录与文件         lists  =  file_path[1].split( '.' )  #分割出文件与文件扩展名         file_ext  =  lists[ - 1 ]  #取出后缀名(列表切片操作)         img_ext  =  [ 'bmp' , 'jpeg' , 'gif' , 'psd' , 'png' , 'jpg' ]         if  file_ext  in  img_ext:             os.rename(path,file_path[ 0 ] + '/' + lists[ 0 ] + '_fc.' + file_ext)             i + = 1  #注意这里的i是一个陷阱         #或者         #img_ext = 'bmp|jpeg|gif|psd|png|jpg'         #if file_ext in img_ext:         #    print('ok---'+file_ext)     elif  os.path.isdir(path):         for  x  in  os.listdir(path):             change_name(os.path.join(path,x))  #os.path.join()在路径处理上很有用  img_dir  =  'D:\\xx\\xx\\images'img_dir  =  img_dir.replace( '\\',' / ')start  =  time.time()i  =  0change_name(img_dir)c  =  time.time()  -  startprint ( '程序运行耗时:%0.2f' % (c))print ( '总共处理了 %s 张图片' % (i))
~~~



​	

​	
