---
title: 适合macos系统中idea快捷键与设置
tags:
  - MacOS
  - Idea
categories:
  - MacOS
toc: false
abbrlink: 672
date: 2021-07-25 12:07:24
---

<u>实现ctrl+ 滚轮变大字体：</u>	

```
	setting->editor->General->勾选change font size.....
```

<!--more-->

```shell
alt = option
ctrl = control

control + enter		类初始化
command + o			打开类
command + e         打开最近打开的文件
control + table     打开上次打开的文件
command + delete	删除行
command + x			剪切行
command + d    		复制一行
control + t 		重构菜单
option + 上/下    	缩小或放大选区
command + 左/右 		移动鼠标光标到最左边和最右边
command + shift + 上/下  移动行或方法上移或下移
option + enter  	构造函数参数提取到属性，自动创建类，提示信息，错误引入修订
Command shift + o 	打开文件
command + shift + t 打开单元测试
command + option + enter 	在上面增加一行 	
COMmand + shift + enter 	在下面增加一行
control + option + 0      优化import,删除无用引入
command + shift + a		杳找action
command + option + l 	格式化代码
option + control + r 	调出运行，列出那些可以执行
Command + option + p	抽取参数
Command + option + v	抽取变量
Command + option + f	抽取字段
Command + option + c	抽取常量
Command + option + m	抽取方法

fn+shift+f6			重命名
command + option + n 	内联将调用替换成实现   将一个变量定义抽取成一个变量直接赋值

invert if condition 条件反转 内容也反转   如if大于变小于号

Live templates 内置 偏好设置E
$NAME$ 记得要 点define
目定义live tem temp lates 替换 偏好设置里有.. eg: sout Tori 1ter
向后声明 eg: "aa".var， "sdf'" . fori
智能补全

if（str == null） {
return "abc" //command +shift +enter 补分号  
double shift查找文件方
command + n弹出生 成代码(get set方法或者 构造方法之类)

```

设置自动导包：

```shell
setting->editor->general->auto import->insert imports on paste All
```

显示方法分割符号

```shell
setting->editor->general->appearance->show method separators
```


取消单行显示文件 文件多时可以一起显示

```shell
setting->editor->general->Editor Tabs->show tabs in one row
```

 修改注释的颜色

![image-20201015183930399](https://img-blog.csdnimg.cn/img_convert/a58b9ff46fcb05e7f4e2ff6a284fc6eb.png)



设置导包，超过几个包自动转为* 如5歌以上util 转为*

![image-20201015184118158](https://img-blog.csdnimg.cn/img_convert/613195d0d9477d412ad68d74fbd8e3e3.png)

设置文件新建头部标签签名：

![image-20201015184336781](https://img-blog.csdnimg.cn/img_convert/bdc9c2ee7f4c41e164a64d2f060faf8e.png)

设置当前项目编码格式的问题：

![image-20201015184540827](https://img-blog.csdnimg.cn/img_convert/b325a31c944953f98374525b4f5f0122.png)

设置自动自动编译

https://tva1.sinaimg.cn/large/007S8ZIlgy1gjq7nggkbpj31lw0t4n6n.jpg)

![image-20201015184922175](https://img-blog.csdnimg.cn/img_convert/e4111c72d9cb270af84b77cc34717d6c.png)



若出现无代码提示的显示功能时，可更改

![image-20201015185031169](https://img-blog.csdnimg.cn/img_convert/c755691474638eb535f5161ea6663813.png)



快捷输入：

```shell
Sout   输出

soutp

soutm

soutv

main 

psvm main方法

循环输出： iter. fori   itar
list.for   正对list集合的增强for循环
list.forr   倒叙遍历

ifn   判断list是不是null
inn   判断list是不是null

prsf.   p rivate static final 
```



idea添加本地tomcat运行测试

![image-20201015190525155](https://img-blog.csdnimg.cn/img_convert/d839abec792bac339117f567d431e5f2.png)



idea中添加数据库的管理

![image-20201015190722036](https://img-blog.csdnimg.cn/img_convert/ef0d13da68cb9e62a88f6eba95f15823.png)



上传当前项目到gi t



![image-20201015191142473](https://img-blog.csdnimg.cn/img_convert/79d62784078627f21154ec8e49252f19.png)

