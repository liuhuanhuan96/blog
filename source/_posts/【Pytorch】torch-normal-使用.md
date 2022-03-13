---
title: 【Pytorch】torch.normal()使用
tags:
  - Pytorch
categories:
  - Pytorch
toc: true
abbrlink: 17735
date: 2021-07-25 12:54:08
---

### torch.normal()

```
torch.normal(means, std, out=None)
```

<!--more-->

返回一个张量，包含从给定参数`means`,`std`的离散正态分布中抽取随机数。 均值`means`是一个张量，包含每个输出元素相关的正态分布的均值。 `std`是一个张量，包含每个输出元素相关的正态分布的标准差。 均值和标准差的形状不须匹配，但每个张量的元素个数须相同。

参数:

- means (Tensor) – 均值
- std (Tensor) – 标准差
- out (Tensor) – 可选的输出张量

~~~python
torch.normal(means=torch.arange(1, 11), std=torch.arange(1, 0, -0.1))
 
1.5104
1.6955
2.4895
4.9185
4.9895
6.9155
7.3683
8.1836
8.7164
9.8916
[torch.FloatTensor of size 10]


~~~

~~~python
torch.normal(mean=0.0, std, out=None)
~~~

与上面函数类似，所有抽取的样本共享均值。

参数:

- means (Tensor,optional) – 所有分布均值
- std (Tensor) – 每个元素的标准差
- out (Tensor) – 可选的输出张量

例子:

```python
torch.normal(mean=0.5, std=torch.arange(1, 6))
  0.5723
  0.0871
	-0.3783
	-2.5689
	10.7893
[torch.FloatTensor of size 5]
```

~~~python
torch.normal(means, std=1.0, out=None)
~~~

与上面函数类似，所有抽取的样本共享标准差。

参数:

- means (Tensor) – 每个元素的均值
- std (float, optional) – 所有分布的标准差
- out (Tensor) – 可选的输出张量

例子:

~~~python
>>> torch.normal(means=torch.arange(1, 6))
 
 1.1681
 2.8884
 3.7718
 2.5616
 4.2500
[torch.FloatTensor of size 5]
~~~



