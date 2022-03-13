---
title: 【Python强化】Python之attrs和attrlib
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 52956
date: 2021-07-25 14:07:25
---

Python 是支持面向对象的，很多情况下使用面向对象编程会使得代码更加容易扩展，并且可维护性更高，但是如果你写的多了或者某一对象非常复杂了，其中的一些写法会相当相当繁琐，而且我们会经常碰到对象和 JSON 序列化及反序列化的问题，原生的 Python 转起来还是很费劲的。

<!--more-->

首先让我们定义一个对象吧，比如颜色。我们常用 RGB 三个原色来表示颜色，R、G、B 分别代表红、绿、蓝三个颜色的数值，范围是 0-255，也就是每个原色有 256 个取值。如 RGB(0, 0, 0) 就代表黑色，RGB(255, 255, 255) 就代表白色，RGB(255, 0, 0) 就代表红色，如果不太明白可以具体看看 RGB 颜色的定义哈。
好，那么我们现在如果想定义一个颜色对象，那么正常的写法就是这样了，创建这个对象的时候需要三个参数，就是 R、G、B 三个数值，定义如下：

```python
class Color(object):
    """
    Color Object of RGB
    """
    def __init__(self, r, g, b):
        self.r = r
        self.g = g
        self.b = b
```

其实对象一般就是这么定义的，初始化方法里面传入各个参数，然后定义全局变量并赋值这些值。其实挺多常用语言比如 Java、PHP 里面都是这么定义的。但其实这种写法是比较冗余的，比如 r、g、b 这三个变量一写就写了三遍。

好，那么我们初始化一下这个对象，然后打印输出下，看看什么结果：

```
color = Color(255, 255, 255)
print(color)
```

输出：

```python 
<__main__.Color object at 0x103436f60>	
```

在 Python 里面想要定义某个对象本身的打印输出结果的时候，需要实现它的`__repr__`方法，所以我们比如我们添加这么一个方法：

```python
def __repr__(self):
    return f'{self.__class__.__name__}(r={self.r}, g={self.g}, b={self.b})'
```

结果输出：

```python
Color(r=255, g=255, b=255)
```

如果我们要想实现这个对象里面的`__eq__`、`__lt__`等各种方法来实现对象之间的比较呢？

```python
def __lt__(self, other):
    if not isinstance(other, self.__class__): return NotImplemented
    return (self.r, self.g, self.b) < (other.r, other.g, other.b)
```

这里是 `__lt__`方法，有了这个方法就可以使用比较符来对两个 Color 对象进行比较了，但这里又把这几个属性写了两遍。

最后再考虑考虑，如果我要把 JSON 转成 Color 对象，难道我要读完 JSON 然后一个个属性赋值吗？如果我想把 Color 对象转化为 JSON，又得把这几个属性写几遍呢？

`attrs` 这个库，其官方的介绍如下：

> attrs 是这样的一个 Python 工具包，它能将你从繁综复杂的实现上解脱出来，享受编写 Python 类的快乐。它的目标就是在不减慢你编程速度的前提下，帮助你来编写简洁而又正确的代码。

其实意思就是用了它，定义和实现 Python 类变得更加简洁和高效。

## 一、基本用法

安装的时候是安装了`attrs`和 `cattrs` 这两个库，但是实际导入的时候是使用 `attr` 和 `cattr` 这两个包，是不带 s 的。

在`attr`这个库里面有两个比较常用的组件叫做`attrs` 和 `attr`，前者是主要用来修饰一个自定义类的，后者是定义类里面的一个字段的。有了它们，我们就可以将上文中的定义改写成下面的样子：

```python
from attr import attrs, attrib


@attrs
class Color(object):
    r = attrib(type=int, default=0)
    g = attrib(type=int, default=0)
    b = attrib(type=int, default=0)


if __name__ == "__main__":
    color = Color(255, 255, 255)
    print(color)
```

首先我们导入了刚才所说的两个组件，然后用 `attrs`里面修饰了 Color 这个自定义类，然后用`attrib`来定义一个个属性，同时可以指定属性的类型和默认值。最后打印输出，结果如下：

```python
Color(r=255, g=255, b=255)
```

观察一下有什么变化，是不是变得更简洁了？r、g、b 三个属性都只写了一次，同时还指定了各个字段的类型和默认值，另外也不需要再定义`__init__`方法和 `__repr__`方法了，一切都显得那么简洁。

实际上，主要是 attrs 这个修饰符起了作用，然后根据定义的 attrib 属性自动帮我们实现了`__init__`、`__repr__`、`__eq__`、`__ne__`、`__lt__`、`__le__`、`__gt__`、`__ge__`、`__hash__`这几个方法

如使用 attrs 修饰的类定义是这样子：

```python
from attr import attrs, attrib@attrsclass Color(object):    r = attrib()    g = attrib()
```

其实就相当于已经实现了这些方法：

```python
class RoughClass(object):    def __init__(self, a, b):        self.a = a        self.b = b    def __repr__(self):        return "RoughClass(a={}, b={})".format(self.a, self.b)    def __eq__(self, other):        if other.__class__ is self.__class__:            return (self.a, self.b) == (other.a, other.b)        else:            return NotImplemented    def __ne__(self, other):        result = self.__eq__(other)        if result is NotImplemented:            return NotImplemented        else:            return not result    def __lt__(self, other):        if other.__class__ is self.__class__:            return (self.a, self.b) < (other.a, other.b)        else:            return NotImplemented    def __le__(self, other):        if other.__class__ is self.__class__:            return (self.a, self.b) <= (other.a, other.b)        else:            return NotImplemented    def __gt__(self, other):        if other.__class__ is self.__class__:            return (self.a, self.b) > (other.a, other.b)        else:            return NotImplemented    def __ge__(self, other):        if other.__class__ is self.__class__:            return (self.a, self.b) >= (other.a, other.b)        else:            return NotImplemented    def __hash__(self):        return hash((self.__class__, self.a, self.b))
```

## 二、别名使用

首先是 `attrs`，它主要是用来修饰 class 类的，而 `attrib`主要是用来做属性定义的，这个就记住它们两个的用法就好了。

翻了一下源代码，发现其实它还有一些别名：

```python
s = attributes = attrsib = attr = attrib
```

也就是说，`attrs`可以用 `s`或 `attributes`来代替，`attrib` 可以用 `attr`或 `ib`来代替。

```python 
from attr import s, ib@sclass Color(object):    r = ib(type=int, default=0)    g = ib(type=int, default=0)    b = ib(type=int, default=0)if __name__ == '__main__':    color = Color(255, 255, 255)    print(color)
```

所以总结一下：

* 库名：`attrs`
* 导入包名：`attr`
* 修饰类：`s` 或 `attributes` 或 `attrs`
* 定义属性：`ib`或`attr` 或 `attrib`

## 三、声明和比较

在这里我们再声明一个简单一点的数据结构，比如叫做 Point，包含 x、y 的坐标，定义如下：

```python
@attrsclass Point(object):    x = attrib()    y = attrib()
```

其中 `attrib`里面什么参数都没有，如果我们要使用的话，参数可以顺次指定，也可以根据名字指定，如：

```python
 	p1 = Point(1, 2)    print(p1)       # Point(x=1, y=2)    p2 = Point(x=3, y=4)    print(p2)       # Point(x=3, y=4)
```

重载运算符 OK，接下来让我们再验证下类之间的比较方法，由于使用了 attrs，相当于我们定义的类已经有了` __eq__`、`__ne__`、`__lt__`、`__le__`、`__gt__`、`__ge__` 这几个方法，所以我们可以直接使用比较符来对类和类之间进行比较，下面我们用实例来感受一下：

```python
print('Equal:', Point(1, 2) == Point(1, 2))    # Equal: True    print('Not Equal(ne):', Point(1, 2) != Point(3, 4))    # Not Equal(ne): True    print('Less Than(lt):', Point(1, 2) < Point(3, 4))    # Less Than(lt): True    print('Less or Equal(le):', Point(1, 2) <= Point(1, 4), Point(1, 2) <= Point(1, 2))    # Less or Equal(le): True True    print('Greater Than(gt):', Point(4, 2) > Point(3, 2), Point(4, 2) > Point(3, 1))    # Greater Than(gt): True True    print('Greater or Equal(ge):', Point(4, 2) >= Point(4, 1))    # Greater or Equal(ge): True
```

## 四、属性定义

现在看来，对于这个类的定义莫过于每个属性的定义了，也就是 attrib 的定义。对于`attrib`的定义，我们可以传入各种参数，**不同的参数对于这个类的定义有非常大的影响。**

每个属性的具体参数和用法

首先让我们概览一下总共可能有多少可以控制一个属性的参数，我们用 `attrs`里面的`fields`方法可以查看一下：

```python
from attr import attrs, attrib, fields@attrsclass Point(object):    x = attrib()    y = attrib()print(fields(Point))
```

这就可以输出 Point 的所有属性和对应的参数，结果如下:

```python
(Attribute(name='x', default=NOTHING, validator=None, repr=True, 			cmp=True, hash=None, init=True,  metadata=mappingproxy({}), 		 	type=None,  converter=None, kw_only=False),   Attribute(name='y', default=NOTHING, validator=None, repr=True,  			cmp=True, hash=None, init=True, metadata=mappingproxy({}),  			 type=None, converter=None, kw_only=False) )
```

输出出来了，可以看到结果是一个元组，元组每一个元素都其实是一个 `Attribute`对象，包含了各个参数，下面详细解释下几个参数的含义：

* `name`：属性的名字，是一个字符串类型。
* `default`：属性的默认值，如果没有传入初始化数据，那么就会使用默认值。如果没有默认值定义，那么就是 NOTHING，即没有默认值。
* `validator`：验证器，检查传入的参数是否合法。
* `init`：是否参与初始化，如果为 False，那么这个参数不能当做类的初始化参数，默认是 True。
* `metadata：元数据，只读性的附加数据。
* `type`：类型，比如 int、str 等各种类型，默认为 None。
* `converter`：转换器，进行一些值的处理和转换器，增加容错性。
* `kw_only`：是否为强制关键字参数，默认为 False。

**属性名**

对于属性名，非常清楚了，我们定义什么属性，属性名就是什么，例如上面的例子，定义了：

```python
x = attrib()
```

那么其属性名就是 x。

**默认值**

对于默认值，如果在初始化的时候没有指定，那么就会默认使用默认值进行初始化，我们看下面的一个实例：

```python
from attr import attrs, attrib, s,fields@attrsclass Point(object):    x = attrib()    y = attrib(default=100)if __name__ == '__main__':    point3 = Point(1)    print(point3)
```

**初始化**

如果一个类的某些属性不想参与初始化，比如想直接设置一个初始值，一直固定不变，我们可以将属性的 init 参数设置为 False，看一个实例：

```python
from attr import attrs, attrib@attrsclass Point(object):    x = attrib(init=False, default=10)    y = attrib()if __name__ == '__main__':    print(Point(3))
```

比如 x 我们只想在初始化的时候设置固定值，不想初始化的时候被改变和设定，我们将其设置了 init 参数为 False，同时设置了一个默认值，如果不设置默认值，默认为 NOTHING。然后初始化的时候我们只传入了一个值，其实也就是为 y 这个属性赋值。

```python
Point(x=10, y=3)
```

没什么问题，y 被赋值为了我们设置的值 3。

那假如我们非要设置 x 呢？会发生什么，比如改写成这样子：

```python
Point(1, 2)
```

报错了，

**强制关键字**

强制关键字是 Python 里面的一个特性，在传入的时候必须使用关键字的名字来传入，如果不太理解可以再了解下 Python 的基础。

设置了强制关键字参数的属性必须要放在后面，其后面不能再有非强制关键字参数的属性，否则会报这样的错误：

```python
ValueError: Non keyword-only attributes are not allowed after a keyword-only attribute (unless they are init=False)
```

将最后一个属性设置`kw_only 参数`为`True`：

```python
from attr import attrs, attrib, s,fields@attrsclass Point(object):    x = attrib(default=0)    y = attrib(kw_only=True)if __name__ == '__main__':    point4 = Point(y = 12)    print(point4)    # point4 = Point(12)  报错，必须指定y变量名称
```

> 注意，如果我们将一个属性设置了`init` 为`False`，那么`kw_only`这个参数会被忽略。

**验证器**

有时候在设置一个属性的时候必须要满足某个条件，比如性别必须要是男或者女，否则就不合法。对于这种情况，我们就需要有条件来控制某些属性不能为非法值。

````python
#encoding=utf-8from attr import attrs, attrib, s,fieldsdef is_valid_gender(instance,attribute,value):    if value not in ['male','female']:        raise ValueError(f'gender {value} is not valid')@attrsclass Person(object):    name = attrib()    gender = attrib(validator=is_valid_gender)if __name__ == '__main__':    print(Person(name="lhh",gender="male"))  #正确显示    print(Person(name="lhh",gender="mlea"))   # 报错
````

在这里我们定义了一个验证器 `Validator 方法`，叫做 is_valid_gender。
然后定义了一个类 Person 还有它的两个属性 name 和 gender，其中 gender 定义的时候传入了一个参数`validator`，其值就是我们定义的 Validator 方法。

这个`Validator`定义的时候有几个固定的参数：

* `instance`：类对象
* `attribute`：属性名
* `value`：属性值

这是三个参数是固定的，在类初始化的时候，其内部会将这三个参数传递给这个 Validator，因此 Validator 里面就可以接受到这三个值，然后进行判断即可。在 Validator 里面，我们判断如果不是男性或女性，那么就直接抛出错误。

OK，结果显而易见了，第二个报错了，因为其值不是正常的性别，所以程序直接报错终止。

注意在 Validator 里面返回 True 或 False 是没用的，错误的值还会被照常复制。所以，一定要在 Validator 里面 raise 某个错误

另外 attrs 库里面还给我们内置了好多 Validator，比如判断类型，这里我们再增加一个属性 age，必须为 int 类型：

```python
age = attrib(validator=validators.instance_of(int))
```

这时候初始化的时候就必须传入 int 类型，如果为其他类型，则直接抛错：

```python
TypeError: ("'age' must be <class 'int'> (got 'x' that is a <class 'str'>).
```

其它的一些验证器：

```python
#encoding=utf-8import attrfrom attr import attrs, attrib, s,fields,validatorsimport enumclass State(enum.Enum):    on = "on"    off = "off"@sclass C(object):    state = attr.ib(validator=attr.validators.in_(State))    val = attr.ib(validator=attr.validators.in_([1, 2, 3]))c = C(State.on,1)print(c)# C(state=<State.on: 'on'>, val=1)c = C(State.off,4)print(c)#   File "<attrs generated init __main__.C>", line 6, in __init__#  File "D:\Anaconda\envs\gui\lib\site-packages\attr\validators.py", line 229, in __call__#   raise ValueError(#ValueError: 'val' must be in [1, 2, 3] (got 4)
```

**转换器**

其实很多时候我们会不小心传入一些形式不太标准的结果，比如本来是 int 类型的 100，我们传入了字符串类型的 100，那这时候直接抛错应该不好吧，所以我们可以设置一些转换器来增强容错机制，比如将字符串自动转为数字等等，看一个实例：

```python
from attr import attrs, attribdef to_int(value):    if isinstance(value,str):        return int(value)@attrsclass Point(object):    x = attrib(converter=to_int)    y = attrib()if __name__ == '__main__':    print(Point("10",10))  # Point(x=10, y=10)
```

**类型**

```python
from attr import attrs, attrib@attrsclass Point(object):    x = attrib(type=int)    y = attrib()if __name__ == '__main__':    print(Point(100, 3))    print(Point('100', 3))
```

这里我们将 x 属性定义为 int 类型了，初始化的时候传入了数值型 100 和字符串型 100，结果如下：

```python
Point(x=100, y=3)Point(x='100', y=3)
```

但我们发现，虽然定义了，但是不会被自动转类型的。

另外我们还可以自定义 typing 里面的类型，比如 List，另外 attrs 里面也提供了类型的定义：

```python
from attr import attrs, attrib, Factoryimport typing@attrsclass Point(object):    x = attrib(type=int)    y = attrib(type=typing.List[int])    z = attrib(type=Factory(list))
```

这里我们引入了 typing 这个包，定义了 y 为 int 数字组成的列表，z 使用了 attrs 里面定义的 Factory 定义了同样为列表类型。

## 五、序列转换

在很多情况下，我们经常会遇到 JSON 等字符串序列和对象互相转换的需求，尤其是在写 REST API、数据库交互的时候。

attrs 库的存在让我们可以非常方便地定义 Python 类，但是它对于序列字符串的转换功能还是比较薄弱的，`cattrs` 这个库就是用来弥补这个缺陷的，下面我们再来看看 `cattrs 库`。

cattrs 导入的时候名字也不太一样，叫做 cattr，它里面提供了两个主要的方法，叫做 `structure`和 `unstructure`，两个方法是相反的，对于类的序列化和反序列化支持非常好。

## 六、基本转换

首先我们来看看基本的转换方法的用法，看一个基本的转换实例：

```python
from cattr import structure,unstructurefrom attr import attrib, attrs@attrsclass Point(object):    x = attrib(type=int,default=0)    y = attrib(type=int,default=0)if __name__ == '__main__':    point = Point(1,2)    print("point",point)    json = unstructure(point)    print('json:', json)    obj = structure(json, Point)    print('obj:', obj)
```

在这里我们定义了一个 Point 对象，然后`调用 unstructure 方法`即可直接转换为 JSON 字符串。如果我们再想把它转回来，那就需要调用 `structure 方法`，这样就成功转回了一个 Point 对象。

```python
point Point(x=1, y=2)json: {'x': 1, 'y': 2}obj: Point(x=1, y=2)
```



## 七、多类型转

另外 structure 也支持一些其他的类型转换，看下实例：

````python
    print(structure(1,str))    print(structure("1", float))    print(structure([1.0, 2, "3"], Tuple[int, int, int]))    print(structure((1, 2, 3), MutableSequence[int]))    print(structure((1, None, 3), List[Optional[str]]))    print(structure([1, 2, 3, 4], Set))    print(structure([[1, 2], [3, 4]], Set[FrozenSet[str]]))    print(structure(OrderedDict[(1, 2), (3, 4)], Dict))    print(structure([1, 2, 3], Tuple[int, str, float]))
````

输出

```python
11.0(1, 2, 3)[1, 2, 3]['1', None, '3']{1, 2, 3, 4}{frozenset({'1', '2'}), frozenset({'4', '3'})}
```

不过总的来说，大部分情况下，JSON 和对象的互转是用的最多的。

## 八、属性处理

上面的例子都是理想情况下使用的，但在实际情况下，很容易遇到 JSON 和对象不对应的情况，比如 JSON 多个字段，或者对象多个字段。

```python
from attr import attrs, attribfrom cattr import structure@attrsclass Point(object):    x = attrib(type=int, default=0)    y = attrib(type=int, default=0)json = {'x':1,'y':2,'z':3}json2 = {'x':1,'y':2}print(structure(json,Point))print(structure(json2,Point))
```

输出

```python
Point(x=1, y=2)Point(x=1, y=2)
```





