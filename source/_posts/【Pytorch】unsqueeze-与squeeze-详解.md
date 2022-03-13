---
title: 【Pytorch】unsqueeze()与squeeze()详解
tags:
  - Pytorch
categories:
  - Pytorch
toc: true
abbrlink: 38768
date: 2021-07-25 12:56:09
---

squeeze()主要用于对数据的维度进行压缩或者解压的

[官方文档](https://pytorch.org/docs/stable/generated/torch.squeeze.html?highlight=squeeze#torch.squeeze)

<!--more-->

## torch.squeeze()

> 对数据的维度进行压缩
>
> 使用方式：torch.squeeze(input, dim=None, out=None)
>
> 将输入张量形状中的1 去除并返回。 如果输入是形如(A×1×B×1×C×1×D)，那么输出形状就为： (A×B×C×D)
>
> 当给定dim时，那么挤压操作只在给定维度上。例如，输入形状为: (A×1×B), `squeeze(input, 0)` 将会保持张量不变，只有用 `squeeze(input, 1)`，形状会变成 (A×B)。

注意：

输入的张量和返回的张量共用一段内存空间，改变了其中一个，其余的都会被改变

参数：

- `input (Tensor)` – 输入张量
- `dim (int, optional)` – 如果给定，则input只会在给定维度挤压
- `out (Tensor, optional)` – 输出张量

**多维张量本质上就是一个变换，如果维度是 1 ，那么，1 仅仅起到扩充维度的作用，而没有其他用途，因而，在进行降维操作时，为了加快计算，是可以去掉这些 1 的维度。**

~~~python
import torch


m = torch.zeros(2,1,2,1,2)
print(m.size())
# print torch.Size([2, 1, 2, 1, 2])

# 默认删除维度为1的维数
n = torch.squeeze(m)
print(n.size())
# print torch.Size([2, 2, 2])

# 当给定dim参数值的时候，那么挤压操作只会给定在指定的维度上
m = torch.zeros(2,1,2,1,2)
n = torch.squeeze(m,0)
print(n.size())
# print torch.Size([2, 1, 2, 1, 2])

n = torch.squeeze(m,1)
print(n.size())
#print torch.Size([2, 2, 1, 2])

n = torch.squeeze(m, 2)
print(n.size())
#print torch.Size([2, 1, 2, 1, 2])

n = torch.squeeze(m, 3)
print(n.size())
#print torch.Size([2, 1, 2, 2])

print('-' * 100)

p = torch.zeros(2, 1, 1)
print(p)
# tensor([[[0.]],
#         [[0.]]])
print(p.numpy())
# [[[0.]]
#  [[0.]]]

print(p.size())
# torch.Size([2, 1, 1])

q = torch.squeeze(p)
print(q)
# tensor([0., 0.])

print(q.numpy())
# [0. 0.]

print(q.size())
# torch.Size([2])
~~~

==总结：==这个函数主要对数据的维度进行压缩，去掉维数为1的的维度，比如是一行或者一列这种，一个一行三列（1,3）的数去掉第一个维数为一的维度之后就变成（3）行。squeeze(a)就是将a中所有为1的维度删掉。不为1的维度没有影响。a.squeeze(N) 就是去掉a中指定的维数为一的维度。还有一种形式就是b=torch.squeeze(a，N) a中去掉指定的定的维数为一的维度。

## torch.unsqueeze()

> torch.unsqueeze(input, dim, out=None)
>
> - **作用**：扩展维度
>
>   ​			返回一个新的张量，对输入的既定位置插入维度 1
>
> - **注意：** 返回张量与输入张量共享内存，所以改变其中一个的内容会改变另一个。
>
> > 如果dim为负，则将会被转化dim+input.dim()+1
> >
> > - **参数:**
> > - `tensor (Tensor)` – 输入张量
> > - `dim (int)` – 插入维度的索引
> > - `out (Tensor, optional)` – 结果张量

~~~python
import torch

x = torch.Tensor([1, 2, 3, 4])  # torch.Tensor是默认的tensor类型（torch.FlaotTensor）的简称。

print('-' * 50)
print(x)  # tensor([1., 2., 3., 4.])
print(x.size())  # torch.Size([4])
print(x.dim())  # 1
print(x.numpy())  # [1. 2. 3. 4.]

print('-' * 50)
print(torch.unsqueeze(x, 0))  # tensor([[1., 2., 3., 4.]])
print(torch.unsqueeze(x, 0).size())  # torch.Size([1, 4])
print(torch.unsqueeze(x, 0).dim())  # 2
print(torch.unsqueeze(x, 0).numpy())  # [[1. 2. 3. 4.]]

print('-' * 50)
print(torch.unsqueeze(x, 1))
# tensor([[1.],
#         [2.],
#         [3.],
#         [4.]])
print(torch.unsqueeze(x, 1).size())  # torch.Size([4, 1])
print(torch.unsqueeze(x, 1).dim())  # 2

print('-' * 50)
print(torch.unsqueeze(x, -1))
# tensor([[1.],
#         [2.],
#         [3.],
#         [4.]])
print(torch.unsqueeze(x, -1).size())  # torch.Size([4, 1])
print(torch.unsqueeze(x, -1).dim())  # 2

print('-' * 50)
print(torch.unsqueeze(x, -2))  # tensor([[1., 2., 3., 4.]])
print(torch.unsqueeze(x, -2).size())  # torch.Size([1, 4])
print(torch.unsqueeze(x, -2).dim())  # 2
~~~

==总结：==给指定位置加上维数为一的维度，比如原本有个三行的数据（3），在0的位置加了一维就变成一行三列（1,3）。a.unsqueeze(N) 就是在a中指定位置N加上一个维数为1的维度。



参考:https://zhuanlan.zhihu.com/p/86763381
