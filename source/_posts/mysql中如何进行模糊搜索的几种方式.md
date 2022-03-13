---
title: mysql中如何进行模糊搜索的几种方式
tags:
  - MySQL
categories:
  - MySQL
toc: true
abbrlink: 27503
date: 2021-11-18 20:17:45
---



### 一、使用%代替零个或多个字符

`%`可匹配任意类型和长度的字符，有些情况下若是中文，可能需要使用两个`%%`表示

<!--more-->

#### 1.1 “%xx%”

**使用方式**： like '%XXX%'

**使用案例**：

```mysql
SELECT
	* 
FROM
	sys_menu 
WHERE
	menu_name LIKE "%用户%"
```

**结果：**

![image-20211118195705872](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211118195705872.png)

#### 1.2 “%xx%xx%”

**使用方式：**like “%xxx%”

**使用案例：**

```mysql
SELECT
	* 
FROM
	sys_menu 
WHERE
	menu_name LIKE "%用户%管理"
```

**结果**

![image-20211118195859800](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211118195859800.png)



### 二、_表示任意单个字符

#### “_管%”

**使用方式：匹配单个任意字符，它常用来限制表达式的字符长度语句**

使用案例:

```mysql
SELECT
	* 
FROM
	sys_menu 
WHERE
	menu_name LIKE "用户_理"
```

输出：

![image-20211118200449461](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211118200449461.png)

注意：有几个_就表示有几个字符，%表示的是多个字符，_表示的是单字符

比如，我们查询一张表中姓刘的名字是3位数，我们可以进行如下查询。

```mysql
select * from user where name like "刘__"
```

他的使用方式，与我们的正则使用方式类似。

### 三、[]表示

**使用方式**:表示括号内所列字符中的一个（和正则表达式的使用方式类似），指定一个字符、字符串或范围，要求所匹配对象为它们中的任一个。

**使用案例**：查询名字叫欢欢的所有姓名

```mysql
select * from user where name like "[刘张王]欢欢"
```

最后查询结果为：

```mysql
王欢欢
刘欢欢
```

`注意:我们这里使用的[]代表的是里面中的一个，不是去查询匹配“刘张王欢欢”`

#### 四、^表示

使用方式：表示不在括号所列之内的单个字符，取值和[]相同，但是是一个相反的作用

**使用案例**：查询名字叫欢欢的但是姓不是张王的所有姓名

```mysql 
select * from user where name like "[^刘张王]欢欢"
```

使用注意事项如三使用方式一致。
