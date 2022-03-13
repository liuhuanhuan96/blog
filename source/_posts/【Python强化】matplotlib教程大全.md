---
title: 【Python强化】matplotlib教程大全
tags:
  - Python
  - Matplotlib
categories:
  - Python
toc: true
abbrlink: 16690
date: 2021-07-25 14:00:56
---



## 一、初识matplotlib

### 1.1 核心原理

使用`matplotlib`绘图的原理，主要就是理解`figure`(**画布**)、`axes`(**坐标系**)、`axis`(**坐标轴**)三者之间的关系。

<!--more-->

![img](http://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDIwLmNuYmxvZ3MuY29tL2Jsb2cvMTQ5NzAzOC8yMDIwMDUvMTQ5NzAzOC0yMDIwMDUxMTEzNTMyNDY1Ni00NDM5MjY3OTcuanBn?x-oss-process=image/format,png)

下面这幅图更详细：

![img](http://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDIwLmNuYmxvZ3MuY29tL2Jsb2cvMTQ5NzAzOC8yMDIwMDUvMTQ5NzAzOC0yMDIwMDUxMTEzNTMzNTYzNi04Mjk4OTY1NDYuanBn?x-oss-process=image/format,png)

`matplotlib`中，就是需要指定`axes`(**坐标系**)，每一个`axes`(**坐标系**)相当于一张画布上的一块区域。一张画布上，可以分配不同区域，也就是说，一张画布，可以指定多个`axes`(**坐标系**)。

>  一个`figure`(画布)上，可以有多个区域`axes`(**坐标系**)，我们在每个坐标系上绘图，也就是说每个`axes`(**坐标系**)中，都有一个`axis`(**坐标轴**)。

> 特别注意：在`matplotlib`中，`figure`**画布**和`axes`**坐标轴**并不能显示的看见，我们能够看到的就是一个`axis`**坐标轴**的各种图形。

### 1.2 基本使用

#### 1.2.1 创建figure(画布)的两种方式

##### 1.2.1.1 隐式创建figure对象

当第一次执行`plt.xxx()`画图代码时，系统会去判断是否已经有了`figure`对象，如果没有，系统会自动创建一个`figure`对象，并且在这个`figure`之上，自动创建一个`axes`坐标系。

【注意】默认创建一个`figure`对象，一个`axes`坐标系

也就是说，如果我们不设置`figure`**对象**，那么一个`figure`**对象**上，只能有一个`axes`**坐标系**，即我们只能绘制一个图形。

隐式创建figure对象存在的问题

优势：如果只是绘制一个小图形，那么直接使用plt.xxx()的方式，会自动帮我们创建一个figure对象和一个axes坐标系，这个图形最终就是绘制在这个axes坐标系之上的。

劣势：如果我们想要在一个figure对象上，绘制多个图形，那么我们就必须拿到每个个axes对象，然后调用每个位置上的axes对象，就可以在每个对应位置的坐标系上，进行绘图，如下图所示。注意：如果figure对象是被默认创建的，那么我们根本拿不到axes对象。因此，需要我们显示创建figure对象。

##### 1.2.1.2  显示创建figure对象

```python
import matplotlib.pyplot as plt

fig = plt.figure()

axes1 = fig.add_subplot(2,1,1)
axes2 = fig.add_subplot(2,1,2)
plt.show()
```

![image-20210602211338614](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib01.png)

案例：

```python
figure = plt.figure()
axes1 = figure.add_subplot(2, 1, 1)
axes2 = figure.add_subplot(2, 1, 2)
axes1.plot([1, 3, 5, 7], [4, 9, 6, 8])
axes2.plot([1, 2, 4, 5], [8, 4, 6, 2])
figure.show()
```

![image-20210602211530337](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib02.png)

#### 1.2.2 完整的绘图步骤

1.**导库**

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
```

2.创建figure画布对象
如果绘制一个简单的小图形，我们可以不设置figure对象，使用默认创建的figure对象，当然我们也可以显示创建figure对象。如果一张figure画布上，需要绘制多个图形。那么就必须显示的创建figure对象，然后得到每个位置上的axes对象，进行对应位置上的图形绘制。

3.**根据`figure`对象进行布局设置**

4.**获取对应位置子图的`axes`坐标系对象**

```python
figure = plt.figure()
axes1 = figure.add_subplot(2,1,1)
axes2 = figure.add_subplot(2,1,2)
```

5.**调用`axes`对象，进行对应位置的图形绘制**

这一步，是我们传入数据，进行绘图的一步。对于图形的一些细节设置，都可以在这一步进行。

6.**显示图形**

`plt.show()`或`figure.show()`如果在**PyCharm**中绘图的话，必须要加这句代码，才能显示。如果在notebook中进行绘图，可以不用加这句代码，而是自动显示。

## 二、matplotlib常用函数

### 2.1  绘制图表组成元素的主要函数

#### 2.1.1  plot()——展现量的变化趋势

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(1,10,1000)
y = np.cos(x)

# ls 曲线类型  lw曲线粗细  lable 图例名称
plt.plot(x,y,ls="--",lw=5,label="plot figure")
plt.legend()
plt.show()
```

![image-20210602212357519](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib03.png)

#### 2.1.2 scatter()——寻找变量之间的关系

```python
#encoding=utf-8
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(1,10,1000)

y = np.random.rand(1000)

# ls 曲线类型  lw曲线粗细  lable 图例名称
plt.scatter(x,y,label="scatter figure")
plt.legend()
plt.show()
```

![image-20210602212736467](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib04.png)

#### 2.1.3 xlim()——设置x轴的数值显示范围

```python
#encoding=utf-8
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(1,10,1000)

y = np.random.rand(1000)

# ls 曲线类型  lw曲线粗细  lable 图例名称
plt.scatter(x,y,label="scatter figure")
plt.xlim(0.01,10)
plt.ylim(0,1)
plt.legend()
plt.show()
```

![image-20210602212950451](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib05.png)

#### 2.1.4 xlabel()——设置x轴的标签文本

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib


x = np.linspace(0.05, 10, 1000)
y = np.sin(x)

plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")
plt.legend()
plt.xlabel("x-axis")
plt.ylabel("y-axis")
plt.show()
```

![image-20210602221218562](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib06.png)

#### 2.1.5 grid()——绘制刻度线的网格线

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.linspace(0.05, 10, 1000)y = np.sin(x)plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")plt.legend()plt.grid(linestyle="-",color="r")plt.show()
```

![image-20210602221531887](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib07.png)

> grid()函数的主要参数为grid(b, which, axis, color, linestyle, linewidth， **kwargs)：
>
> b：布尔值。就是是否显示网格线的意思。官网说如果b设置为None， 且kwargs长度为0，则切换网格状态
> which：取值为major, minor， both。 默认为major
> axis：取值为both， x，y。就是想绘制哪个方向的网格线
> color：这就不用多说了，就是设置网格线的颜色。或者直接用c来代替color也可以
> linestyle：也可以用ls来代替linestyle， 设置网格线的风格，是连续实线，虚线或者其它不同的线条

#### 2.1.6 axhline()——绘制平行于x轴的水平参考线

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.linspace(0.05, 10, 1000)y = np.sin(x)plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")plt.legend()plt.axhline(y=0.0,c="r",ls=":",lw=2)plt.axvline(x=4.0,c="r",ls=":",lw=2)plt.show()
```

![image-20210602221923757](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib08.png)

#### 2.1.7  axvspan()——绘制垂直于x轴的参考区域

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.linspace(0.05, 10, 1000)y = np.sin(x)plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")plt.legend()plt.axhspan(ymin=0.0,ymax=0.5,facecolor="y",alpha=0.3)plt.axvspan(xmin=4.0,xmax=6.0,facecolor="y",alpha=0.3)plt.show()
```

![image-20210602222200923](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib09.png)

#### 2.1.8 annotate()——添加图形内容细节的指向型注释文本

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.linspace(0.05, 10, 1000)y = np.sin(x)plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")plt.legend()plt.annotate(    # 文字描述    s = "maximum",    # 设置xy坐标点    xy=(np.pi / 2 ,1.0),    xytext=((np.pi / 2) + 1.0, 0.8),    weight="bold",    c="b",    arrowprops=dict(arrowstyle="->", connectionstyle="arc3", color="b"))plt.show()
```

> `xy`：被注释图形内容的位置坐标
>
> `xytext`：注释文本的位置坐标
>
> `weight`：注释文本的字体粗细风格
>
> `color`：注释文本的字体颜色
>
> `arrowprops`：指示被注释内容的箭头的属性字典

![image-20210602223828150](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib10.png)

#### 2.1.9 text()——添加图形内容细节的无指向型注释文本

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.linspace(0.05, 10, 1000)y = np.sin(x)plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")plt.legend()plt.annotate(    # 文字描述    s = "maximum",    # 设置xy坐标点    xy=(np.pi/2,1.0),    xytext=((np.pi / 2) + 1.0, 0.8),    weight="bold",    c="b",    arrowprops=dict(arrowstyle="->", connectionstyle="arc3", color="b"))plt.text(x=3.10,y=0.09,s="y=sin(x)",weight="bold", c="b")plt.show()
```

![image-20210602224045180](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib11.png)

#### 2.1.10 title()——添加图形内容的标题

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.linspace(0.05, 10, 1000)y = np.sin(x)plt.plot(x, y, ls="--", lw=2, c="c", label="plot figure")plt.legend()plt.title("center")plt.title("left",loc="left",fontdict={"size": "xx-large",                    "color": "r",                    "family": "Times New Roman"})plt.title("right",loc="right",family="Comic Sans MS", size=20,          style="oblique", color="c")plt.show()
```

![image-20210602224241314](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib12.png)

#### 2.1.11 legend()——表示不同图形的文本标签图例

```python
import numpy as npimport matplotlib.pyplot as pltimport matplotlibx = np.arange(0,3,0.1)y1 = np.power(x,3)y2 = np.power(x,2)y3 = np.power(x,1)plt.plot(x,y1,c="r",ls="-", lw=2, label="$x^3$")plt.plot(x,y2,c="b",ls="-", lw=2, label="$x^2$")plt.plot(x,y3,c="y",ls="-", lw=2, label="$x^1$")plt.legend(loc="upper left",fontsize="x-large",bbox_to_anchor=(0.05, 0.95), ncol=3,           title="power function", shadow=True, fancybox=True)plt.show()
```

> * `loc`参数控制图例的位置，可选值为
>
>   ：
>
>   * `best`
>   * `upper right`
>   * `upper left`
>   * `lower left`
>   * `lower right`
>   * `right`
>   * `center left`
>   * `center right`
>   * `lower center`
>   * `upper center`
>   * `center`

> * `fontsize`控制图例字体大小，可选值为
>
>   ：
>
>   * `int`
>   * `float`
>   * `xx-small`
>   * `x-small`
>   * `small`
>   * `medium`
>   * `large`
>   * `x-large`
>   * `xx-large`

> * `frameon`：`True`或`False`，是否显示图例边框
> * `edgecolor`：图例边框颜色
> * `facecolor`：图例背景颜色,若无边框,参数无效
> * `title`：设置图例标题
> * `fancybox`：`True`表示线框直角，`False`表示线框圆角
> * `shadow`：`True`或`False`，是否显示阴影



### 2.2  常用配置参数

#### 2.2.1 线型

```
linestyle`或`ls
```

* `-`：实线
* `--`：虚线
* `-.`：点划线
* `:`：点线

#### 2.2.2 线宽

```
linewidth`或`lw
```

* 浮点数

#### 2.2.3 线条颜色

```
color`或`c
```

* `b`：blue，蓝色
* `g`：green，绿色
* `r`：red，红色
* `c`：cyan，蓝绿
* `m`：magenta，洋红
* `y`：yellow，黄色
* `k`：black，黑色
* `w`：white，白色

> 也可以对关键字参数color赋十六进制的RGB字符串如 color='#900302'

#### 2.2.4 点标记类型

`marker`，只能用以下简写符号表示

* `.`：point marker
* `,`：pixel marker
* `o`：circle marker
* `v`：triangle_down marker
* `^`：triangle_up marker
* `<`：triangle_left marker
* `>`：triangle_right marker
* `1`：tri_down marker
* `2`：tri_up marker
* `3`：tri_left marker
* `4`：tri_right marker
* `s`：square marker
* `p`：pentagon marker
* `*`：star marker
* `h`：hexagon1 marker
* `H`：hexagon2 marker
* `+`：plus marker
* `x`：x marker
* `D`：diamond marker
* `d`：thin_diamond marker
* `|`：vline marker
* `_`：hline marker

特别地，标记还有mathtext模式

```python
#encoding=utf-8import numpy as npimport matplotlib.pyplot as pltimport matplotlib as mplmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.arange(1,13,1)y = np.array([12, 34, 22, 30, 18, 13, 15, 19, 24, 28, 23, 27])# 将画布分为2行2列fig,ax = plt.subplots(2,2)ax[0, 0].scatter(x, y * 1.5, marker=r"$\clubsuit$", c="#fb8072", s=500)ax[0, 0].locator_params(axis="x", tight=True, nbins=11)ax[0, 0].set_xlim(0, 13)ax[0, 0].set_xticks(x)ax[0, 0].set_title('显示样式{}的散点图'.format(r"$\clubsuit$"))ax[0, 1].scatter(x, y - 2, marker=r"$\heartsuit$", c="#fb8072", s=500)ax[0, 1].locator_params(axis="x", tight=True, nbins=11)ax[0, 1].set_xlim(0, 13)ax[0, 1].set_xticks(x)ax[0, 1].set_title('显示样式{}的散点图'.format(r"$\heartsuit$"))ax[1, 0].scatter(x, y + 7, marker=r"$\diamondsuit$", c="#fb8072", s=500)ax[1, 0].locator_params(axis="x", tight=True, nbins=11)ax[1, 0].set_xlim(0, 13)ax[1, 0].set_xticks(x)ax[1, 0].set_title('显示样式{}的散点图'.format(r"$\diamondsuit$"))ax[1, 1].scatter(x, y - 9, marker=r"$\spadesuit$", c="#fb8072", s=500)ax[1, 1].locator_params(axis="x", tight=True, nbins=11)ax[1, 1].set_xlim(0, 13)ax[1, 1].set_xticks(x)ax[1, 1].set_title('显示样式{}的散点图'.format(r"$\spadesuit"))plt.suptitle("不同原始字符串作为标记类型的展示效果", fontsize=16, weight="black")plt.show()
```

官网有一张属性表，先贴在这，以后有空会再补充内容的

![img](http://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDIwLmNuYmxvZ3MuY29tL2Jsb2cvMTQ5NzAzOC8yMDIwMDUvMTQ5NzAzOC0yMDIwMDUxMTE2MDUxNDg2My0xMjY1MDAwODcucG5n?x-oss-process=image/format,png)

## 三、matplotlib常用图表

### 3.1 柱状图

柱状图主要是应用在**定性数据的可视化**场景中，或是离散数据类型的分布展示。例如，一个本科班级的学生籍贯分布，出国旅游人士的职业分布以及下载一款App产品的操作系统的分布。

```python
import matplotlib.pyplot as pltimport matplotlib as mplmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = [1,2,3,4,5]y = [6,10,2,1,1]plt.bar(x,y,align="center",color="b",tick_label=["语文","数学","英语","物理","化学"],alpha=0.6)plt.xlabel("学科")plt.ylabel("分数")plt.show()
```

![image-20210606090150432](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib13.png)

> 

* `x`：柱状图中的柱体标签值
* `y`：柱状图中的柱体高度
* `align`：柱体对齐方式，可选`center`或`edge`
* `color`：柱体颜色
* `tick_label`：刻度标签值
* `alpha`：柱体透明度

### 3.2 条形图

其实就是把柱状图转置过来

```python
import matplotlib.pyplot as pltimport matplotlib as mplmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = [1,2,3,4,5]y = [6,10,2,1,1]plt.barh(x,y,align="center",color="b",tick_label=["语文","数学","英语","物理","化学"],alpha=0.6)plt.xlabel("学科")plt.ylabel("分数")plt.show()
```

![image-20210606090426320](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib14.png)

### 3.3  多数据并列柱状图

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.arange(1,6,1)y = [0,4,3,5,6]y1 = [1,3,4,2,7]y2 = [3,4,1,6,5]labels = ["BluePlanet", "BrownPlanet", "GreenPlanet"]colors = ["#8da0cb", "#fc8d62", "#66c2a5"]x = np.arange(5)y = [6,10,4,5,1]y1 = [2,6,3,8,5]bar_width = 0.35tick_label = ["A", "B", "C", "D", "E"]plt.bar(x,y,bar_width,color="r", align="center",label="班级A",alpha=0.5)plt.bar(x+bar_width, y1,bar_width,color="b", align="center", label="班级B", alpha=0.5)plt.xlabel("测试难度")plt.ylabel("试卷份数")plt.xticks(x + bar_width / 2, tick_label)plt.legend()plt.show()
```

![image-20210606100340193](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib20.png)



### 3.4 多数据平行条形图

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.arange(1,6,1)y = [0,4,3,5,6]y1 = [1,3,4,2,7]y2 = [3,4,1,6,5]labels = ["BluePlanet", "BrownPlanet", "GreenPlanet"]colors = ["#8da0cb", "#fc8d62", "#66c2a5"]x = np.arange(5)y = [6,10,4,5,1]y1 = [2,6,3,8,5]bar_width = 0.35tick_label = ["A", "B", "C", "D", "E"]plt.barh(x,y,bar_width,color="r", align="center",label="班级A",alpha=0.5)plt.barh(x+bar_width, y1,bar_width,color="b", align="center", label="班级B", alpha=0.5)plt.xlabel("测试难度")plt.ylabel("试卷份数")plt.xticks(x + bar_width / 2, tick_label)plt.legend()plt.show()
```



![image-20210606100419966](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib21.png)

### 3.5 参数探讨

如果想在柱体上绘制装饰线或装饰图，也就是说，设置柱体填充样式，我们可以用关键字参数`hatch`，其可能取值为：`/ `,`\` ,` |` ,` -` , `+` , `x` , `o` , `O` , `.` , `*`

> 每种符号数量越多，填充样式越密集，如`///`

柱状图还有其他关键字参数，如描边

* 边缘颜色（包括填充样式颜色，会一起变）：`edgecolor`(`ec`)
* 边缘样式：`linestyle`(`ls`)
* 边缘粗细：`linwwidth`(`lw`)

### 3.6 堆积折线图

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.arange(1,6,1)y = [0,4,3,5,6]y1 = [1,3,4,2,7]y2 = [3,4,1,6,5]labels = ["BluePlanet", "BrownPlanet", "GreenPlanet"]colors = ["#8da0cb", "#fc8d62", "#66c2a5"]plt.stackplot(x,y,y1,y2,labels=labels,colors=colors)plt.legend(loc="upper right")plt.show()
```

![image-20210606095849915](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib19.png)



### 3.7 间断条形图

主要用来可视化定性数据的相同指标在时间维度上的指标值的变化情况，实现定性数据的相同指标的变化情况的有效直观比较

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串plt.broken_barh([(30,100),(180,50),(260,70)],(20,8),facecolors="#1f78b4")plt.broken_barh([(60, 90), (190, 20), (230, 30), (280, 60)], (10, 8),                facecolors=("#7fc97f", "#beaed4", "#fdc086", "#ffff99"))plt.xlim(0, 360)plt.ylim(5, 35)plt.xlabel("演出时间")plt.xticks(np.arange(0, 361, 60))plt.yticks([15, 25], ["歌剧院A", "歌剧院B"])plt.grid(ls="-", lw=1, color="gray")plt.title("不同地区的歌剧院的演出时间比较")plt.show()
```

![image-20210606095248591](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib18.png)

> 针对plt.broken_barh([(60, 90), (190, 20), (230, 30), (280, 60)], (10, 8),facecolors=("#7fc97f", "#beaed4", "#fdc086", "#ffff99"))来讲解使用方法：
>
> 列表[(60, 90), (190, 20), (230, 30), (280, 60)]的元组表示从起点是x轴的数值为60的位置起，沿x轴正方向移动90个单位。其他元组类似。
>
> 参数(10, 8)表示从起点是y轴的数值为10的位置起，沿y轴正方向移动8个单位，这就是每个柱体的高度和垂直起始位置。
>
> 关键字参数facecolors表示每个柱体的填充颜色，这里使用HEX模式的颜色表示方法

### 3.8 阶梯图

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.linspace(1,10,10)y = np.sin(x)plt.step(x,y, color="#8dd3c7", where="pre", lw=2)plt.xlim(0,11)plt.ylim(-1.2,1.2)plt.xticks(np.arange(1,11,1))plt.show()
```

![image-20210606094726215](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib17.png)

> `step()`方法参数和`plot()`类似，主要是关键字参数`where`，默认值是`pre`，表示数据点向右对齐，，还可以设为`post`，表示数据点向左对齐，如下图。

### 3.9 饼图

```python

```

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串# 标记每份饼片的文本标签内容labels = "A","B","C","D"# 饼片代表的百分比students = [0.35,0.15,0.20,0.30]colors = ['#377eb8', '#4daf4a', '#984ea3', '#ff7f00']# 饼片边缘偏离半径的百分比explode = (0.1,0.1,0.1,0.1)# autopct 饼片文本标签内容对应的数值百分比样式# startangle 从x轴作为起始位置，第一个饼片的起始位置（逆时针），单位度# shadow 是否绘制饼片的阴影# colors：饼片的颜色wedges,texts,autotexts = plt.pie(students, explode=explode,                                 autopct="%3.1f%%",startangle=45,                                 shadow=True, colors=colors)plt.legend(wedges, labels, fontsize=12, title="难度等级",loc="right",           bbox_to_anchor=(0.95,0,0.3,1))plt.setp(autotexts, size=15, weight="bold")plt.setp(texts, size=12)plt.title("选择不同难度测试试卷的学生占比")colLables = ["A", "B", "C", "D"]rowLables = ["学生选择试卷人数"]studentValues = [[350, 150, 200, 300]]colColors = ["#377eb8", "#e41a1c", "#4daf4a", "#984ea3"]plt.table(cellText=studentValues,          cellLoc="center",          colWidths=[0.1] * 4,          colLabels=colLables,          colColours=colColors,          rowLabels=rowLables,          rowLoc="center",          loc="bottom")plt.show()
```

![image-20210606094204188](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib16.png)

### 3.10 箱线图

关于箱线图的组成部分有：箱体、箱须和离群值，其中，箱体主要由第一四分位数、中位数和第三四分位数，箱须又分为上箱须和下箱须。上箱须和下箱须长度的确定方法是绘制箱线图的原始数据集Data中分贝寻找不大于Q3+whis×IQRQ3+whis×IQR的最大值valuemaxvaluemax和不小于Q1−whis×IQRQ1−whis×IQR的最小值valueminvaluemin，其中Q1Q1和Q3Q3分别是第一四分位数和第三四分位数，whis是关键字参数whis的值，IQR是四分位差，计算方法是IQR=Q3−Q1IQR=Q3−Q1。离群值OutlierOutlier的判断标准是 value<(Q1−whis×IQR)value<(Q1−whis×IQR)或者value>(Q3+whis×IQR)value>(Q3+whis×IQR)，其中valuevalue是Data中的数据点。

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串testA = np.random.randn(5000)testB = np.random.randn(5000)# 绘制图片输入数据testList = [testA,testB]labels = ["随机数生成器AlphaRM","随机数生成器BetaRM"]colors = ["#1b9e77", "#d95f02"]# 四分卫间距的倍数，用来确定箱须包含数据范围的大小whis = 1.6# 设置箱体的宽度，可以统一设为一个值，或者分别赋值宽度width = 0.35# sym  离群值的标记样式bplot = plt.boxplot(testList, whis=whis, widths=width, sym="o",labels=labels, patch_artist=True)for patch,color in zip(bplot["boxes"],colors):    patch.set_facecolor(color)plt.ylabel("随机数值")plt.title("生成器抗干扰能力的稳定性比较")plt.show()
```



![image-20210606091516310](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib15.png)

## 四、matplotlib划分画布的主要函数

### 4.1 subplot()

* 绘制网格区域中几何形状相同的子区布局

函数签名有：

* `subplot(numRows, numCols, plotNum)`
* `subplot(CRN)`

> 都是整数，意思是将画布划分为C行R列个子区，此时定位到第N个子区上，子区编号按照行优先排序。

Example

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.linspace(-2 * np.pi, 2*np.pi, 200)y = np.sin(x)y1 = np.cos(x)plt.subplot(121)plt.plot(x,y)plt.subplot(122)plt.plot(x,y1)plt.show()
```

```python
import matplotlib.pyplot as pltimport matplotlib as mplimport numpy as npmpl.rcParams['font.sans-serif'] = ['SimHei']mpl.rcParams['font.serif'] = ['SimHei']mpl.rcParams['axes.unicode_minus'] = False  # 解决保存图像是负号'-'显示为方块的问题,或者转换负号为字符串x = np.linspace(0.0, 2*np.pi)y = np.cos(x)*np.sin(x)fig = plt.figure()ax1 = fig.add_subplot(121)# 设置自动缩放ax1.margins(0.03)ax1.plot(x,y,ls="-",lw=2,color="b")ax2 = fig.add_subplot(222)ax2.margins(0.1)ax2.plot(x,y,ls="-",lw=2,color="r")ax2 = fig.add_subplot(224)ax2.margins(0.1)ax2.plot(x,y,ls="-",lw=2,color="y")plt.show()
```

![image-20210606101908004](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/matplotlib22.png)

> 非等分画布可以多次使用等分画布来实现

### 4.2 subplot2grid()

* 让子区跨越固定的网格布局

```python

```

