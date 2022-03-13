---
title: 【Numpy】 meshgrid()函数
tags:
  - Numpy
  - Python
categories:
  - Numpy
toc: false
abbrlink: 46758
date: 2021-07-25 13:45:09
---

np.mesharid()函数通常用来生成二维数据网格，例如一张灰度图片中长为x轴，宽为y轴，图中每一个像素点。

可以接受两个一维数组生成两个二维矩阵。

<!--more-->

~~~python
np.mesharid(np.arange(4),np.arange(4)) 
~~~

> 根据传入的两个一维数组参数生成两个数组元素的列表。
>
> 如果第一个参数是xarray，维度是xdimesion，
>
> 第二个参数是yarray，维度是ydimesion。
>
> 那么生成的第一个二维数组是以xarray为行，共ydimesion行的向量；而第二个二维数组是以yarray的转置为列，共xdimesion列的向量。



直观的感受：x-y坐标系中，x可取（1，2，3） y可取（4，5）

共有6个点	（1，4）（1，5）（2，4）（2，5）（3，4）（3，5）

np.mesharid()函数就是生成类似的数据网格

![image-20201209180432323](https://tva1.sinaimg.cn/large/0081Kckwgy1glhrguqrl1j31fg08ewfd.jpg)

![](https://tva1.sinaimg.cn/large/0081Kckwgy1glhrjzdsrej31f80d8dh5.jpg)



==测试代码：==

~~~python
import numpy as np
import matplotlib.pyplot as plt
# np建立一个等差数列
x = np.linspace(0,30,3)
print(f"x的维度:{x.ndim},shape:{x.shape}")
print(x)
y = np.linspace(0,20,2)
print(f"y的维度:{y.ndim},shape:{y.shape}")
print(y)

xx,yy = np.meshgrid(x, y)
print(f"xv的维度:{xx.ndim},shape:{xx.shape}")
print(f"yv的维度:{yy.ndim},shape:{yy.shape}")

plt.plot(xx, yy,'.')
plt.grid(True)
plt.show()
~~~

result:

![image-20201209181329819](https://tva1.sinaimg.cn/large/0081Kckwgy1glhrq4qr4wj31fk0podio.jpg)

