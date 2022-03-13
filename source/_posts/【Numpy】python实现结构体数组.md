---
title: 【Numpy】python实现结构体数组
tags:
  - Numpy
  - Python
categories:
  - Numpy
toc: true
abbrlink: 976
date: 2021-07-25 13:50:41
---

### 结构体数组

在C语言中我们可以通过struct关键字定义结构类型，结构中的字段占据连续的内存空间，每个结构体占用的内存大小都相同，因此可以很容易地定义结构数组。和C语言一样，在NumPy中也很容易对这种结构数组进行操作。只要NumPy中的结构定义和C语言中的定义相同，NumPy就可以很方便地读取C语言的结构数组的二进制数据，转换为NumPy的结构数组。假设我们需要定义一个结构数组，它的每个元素都有name, age和salary字段。在NumPy中可以如下定义：

<!--more-->

```python
import numpy as np
MyType=np.dtype({
    'names':['name','age','salary'],
    'formats':['S32','i','f']#必须加s，且S大写
})
a=np.array([("tang",23,130.2),("wang",22,100.2)],
dtype=MyType)
#或者Data=np.array([(‘zero’,0.,0.)]*10,dtype=MyType) #创建Data[2]
#Date[0]['name']="tang"

12345678910
```

我们先创建一个dtype对象persontype，通过其字典参数描述结构类型的各个字段。字典有两个关键字：names，formats。每个关键字对应的值都是一个列表。names定义结构中的每个字段名，而formats则定义每个字段*的类型：

- S32 : 32个字节的字符串类型，由于结构中的每个元素的大小必须固定，因此需要指定字符串的
  长度
- i : 32bit的整数类型，相当于np.int32
- f : 32bit的单精度浮点数类型，相当于np.float32
  然后我们调用array函数创建数组，通过关键字参数dtype=MyType， 指定所创建的数组的元素类
  型为结构MyType。运行上面程序之后，我们可以在IPython中执行如下的语句查看数组a的元素类
  型

```python
a.dtype
1
```

**结果显示：**

```
dtype([('name', 'S32'), ('age', '<i4'), ('salary', '<f4')])
1
```

这里我们看到了另外一种描述结构类型的方法： 一个包含多个组元的列表，其中形如(字段名, 类型描述) 的组元描述了结构中的每个字段。类型描述前面为我们添加了 '<'字符，这些字符用来描述字段值的字节顺序：

- <:低位字节在前
- \>:高位字节在前

结构数组的存取方式和一般数组相同，通过下标能够取得其中的元素，注意元素的值看上去像是组元，实际上它是一个结构：

```python
a[0]

12
```

**结果显示：**

```
(b'tang', 23, 130.2)
1
a[0].dtype
1
```

**结果显示：**

```
dtype([('name', 'S32'), ('age', '<i4'), ('salary', '<f4')])
1
```

a[0]是一个结构元素，它和数组a共享内存数据，因此可以通过修改它的字段，改变原始数组中的对应字段：

```python
c=a[0]
c["name"]="Lian"#修改元素属性
a[0]["name"]
123
```

**结果显示：**

```
b'Lian'
1
```

结构像字典一样可以通过字符串下标获取其对应的字段值：

```python
a[1]["name"]1
```

**结果显示：**

```
b'wang'1
```

我们不但可以获得结构元素的某个字段，还可以直接获得结构数组的字段，它返回的是原始数组的视图，因此可以通过修改b[0]改变a[0][’‘age’’]：

```python
b=a[:]["salary"]#或者a["salary"]b12
```

**结果显示：**

```
array([130.2, 100.2], dtype=float32)1
```

通过调用a.tostring或者a.tofile方法，可以直接输出数组a的二进制形式：

```python
a.tofile("test.bin")1
```

### 内存对齐

C语言的结构体为了内存寻址方便，会自动的添加一些填充用的字节，这叫做内存对齐。例如如果把下面的name[32]改为name[30]的话，由于内存对齐问题，在name和age中间会填补两个字节，最终的结构体大小不会改变。因此如果numpy中的所配置的内存大小不符合C语言的对齐规范的话，将会出现数据错位。为了解决这个问题，在创建dtype对象时，可以传递参数align=True，这样numpy的结构数组的内存对齐和C语言的结构体就一致了。

```c
#include <stdio.h>

struct person
{
	char name[32];
	int age;
	float weight;
};

struct person p[2];

void main ()
{
	FILE *fp;
	int i;
	fp=fopen("test.bin","rb");
	fread(p, sizeof(struct person), 2, fp);
	fclose(fp);
	for(i=0;i<2;i++)
		printf("%s %d %f\n", p[i].name, p[i].age, p[i].weight);
	getchar();
}
12345678910111213141516171819202122
```

用下面的字典参数也可以定义结构类型，字典的关键字为结构中字段名，值为字段的类型描述，但是由于字典的关键字是没有顺序的，因此字段的顺序需要在类型描述中给出，类型描述是一个组元，它的第二个值给出字段的字节为单位的偏移量，例如age字段的偏移量为25个字节：

```python
np.dtype({"name":('S25',0),"age":(np.uint8,25)})
1
```

**结果显示：**

```
dtype([('name', 'S25'), ('age', 'u1')])
1
1
```
