---
title: 【Python进阶】Python标准库之logging
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 63822
date: 2021-11-23 15:23:08
---

## 一、日志处理的方式

| python  | java                 |
| ------- | -------------------- |
| print() | System.out.println() |
| logging | log4j                |

一般我们在进行学习或者是简单的项目中，我们可以使用print()函数来直接输出结果，但是在一些文件比较多，更加复杂的项目中，我们需要自己重新整理一个日志库，来管理我们整个项目工程的日志管理

<!--more-->

##  二、logging库日志级别

| 级别     | 级别数值 | 使用时机                                         |
| -------- | -------- | ------------------------------------------------ |
| DEBUG    | 10       | 详细信息，常用于调试                             |
| INFO     | 20       | 程序正常运行过程中产生的一些信息                 |
| WARNING  | 30       | 警告用户，虽然程序还在正常工作，但有可能发生错误 |
| ERROR    | 40       | 由于更严重的问题，程序已经不能执行一些功能了     |
| CRITICAL | 50       | 严重错误，程序已经不能继续运行                   |

`默认的日志级别是warning`

## 三、代码实战

### **1.使用baseconfig()来指定日志输出级别**

```python
import logging

#默认的日志输出级别为warning
#使用baseconfig()来指定日志输出级别

logging.basicConfig(level=logging.DEBUG)
logging.debug("this is a debug log")
logging.info("this is a info log")
logging.warning("this is a warning log")
logging.error("this is a error log")
logging.critical("this is a criticial log")
```

修改日志输出级别后结果:

![image-20211123095331801](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123095331801.png)

我们此时做个案例，看下logging和print谁先输出：

```python
import logging

#默认的日志输出级别为warning
#使用baseconfig()来指定日志输出级别

print("this is a print data")
logging.basicConfig(level=logging.DEBUG)
logging.debug("this is a debug log")
logging.info("this is a info log")
logging.warning("this is a warning log")
logging.error("this is a error log")
logging.critical("this is a criticial log")
```

输出结果：

![image-20211123095525428](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123095525428.png)

但是实际情况是，这个输出顺序是随机的，因为`logging`这些库并不是像print一样，直接输出，他是一种`多线程的方式`，为了控制`大量日志输出`并发的问题,他只能保证所有logging输出的日志的顺序是一致，但是不能保证和其他的输出的顺序是一致的。



### 2.输出日志到文件

此种方式是通过函数`basicConfig`来指定参数`filename`来输出到文件

```python
import logging

#默认的日志输出级别为warning
#使用baseconfig()来指定日志输出级别

print("this is a print data")
logging.basicConfig(filename="demo.log",level=logging.DEBUG)
logging.debug("this is a debug log")
logging.info("this is a info log")
logging.warning("this is a warning log")
logging.error("this is a error log")
logging.critical("this is a criticial log")
```

输出到文件中：

![image-20211123100001210](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123100001210.png)

我们再重新执行一次，发现，我们的文件中，日志又新增了几行，默认的是将我们的日志追加到我们的文件当中去的。但是如果我们想要的是，每次执行程序，我们最后输出的话都是先清空文件夹，然后再输出日志到文件中，那么我们需要怎么去进行操作呢。我们只需要新增一个属性`filemode`

```python
logging.basicConfig(filename="demo.log",filemode="w",level=logging.DEBUG)
```

### 3.输出对象

```python
import logging

logging.basicConfig(level=logging.DEBUG)
name = "lhh"
age = "25"
logging.debug("name:%s,age:%s",name,age)
logging.debug("name:%s,age:%s"%(name,age))
```

输出结果

![image-20211123100837568](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123100837568.png)

### 4.输出格式添加一些重要提示信息

```python
import logging

logging.basicConfig(format="%(asctime)s|%(levelname)s|%(filename)s:%(lineno)s|%(message)s",level=logging.DEBUG)
name = "lhh"
age = "25"
logging.debug("name:%s,age:%s",name,age)
logging.debug("name:%s,age:%s"%(name,age))
```

输出结果

![image-20211123101948200](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123101948200.png)

参数解读：

* asctime 表示当前时间
* levelname 表示输出日志级别
* filename 表示文件名称
* lineno 表示输出文件行号
* message 表示输出信息

当然我们也可以修改显示的时间信息:

```python
import logging

logging.basicConfig(format="%(asctime)s|%(levelname)s|%(filename)s:%(lineno)s|%(message)s",
                    datefmt="%Y%m%d",
                    level=logging.DEBUG)
name = "lhh"
age = "25"
logging.debug("name:%s,age:%s",name,age)
logging.debug("name:%s,age:%s"%(name,age))
```

此时我们发现只输出了年月日，没有时分秒的输出结果：

![image-20211123102349916](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123102349916.png)

## 四、logging的高级应用

logging模块采用了模块化设计，主要包含四种组件:

* **Loggers**：记录器，提供应用程序代码能直接使用的接口。
* **Handlers**: 处理器，将记录器产生的日志发送至目的地。
* **Filters**：过滤器，提供更好的粒度控制，决定那些日志会被输出。
* **Formatters**：格式化器，设置日志内容的组成结构和消息字段。



**logging模块的工作流程**：

### ![image-20211123102844420](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123102844420.png)4.1.loggers记录器

* 提供应用程序的调用接口

```python
logger  = logging.getLogger(__name__)
```

logger是单例的

* 决定日志记录的级别

```python
logger.setLevel()
```

* 将日志内容传递相关联的handlers中

  ```python
  logger.addHandler()和logger.removeHandler()
  ```

### 4.2 Handlers处理器

他们将日志分发到不同的目的地。可以是文件、标准输出、邮件、或者通过socke、http等协议发送到任何地方。

**SreamHandler**标准输出stdout(如显示器)分发器。

创建方法：sh = logging.StreamHandler(stream=None)

**FileHandler**将日志保存到磁盘文件的处理器

创建方法:fh=logging.FileHandler(filename,mode=“a”,encoding=Node,delay=False)

setFormatter()：设置当前handler对象使用的消息格式。

`常用的几个处理器:`

* **StreamHandler**
* **FileHandler**
* **BaseRotatingHandler**
* **RotatingFileHandler**
* **TimedRotatingFileHandler**

### 4.3 Formatters 格式

Formatter对象用来最终设置日志信息的顺序、结构和内容。

其构造方法为

```PYTHON 
ft = logging.Formatter.__init__(fmt=None,datefmt=None,style='%')
```

datefmt默认是`%Y-%m-%d %H:%M:%S`样式的

style参数默认为百分符%,这表示%（<dictionary key>）s格式的字符串

| 属性      | 格式          | 描述                                                   | 属性        | 格式            | 描述                   |
| --------- | ------------- | ------------------------------------------------------ | ----------- | --------------- | ---------------------- |
| asctime   | %(asctime)s   | 日志产生时间，默认格式为 2021-11-23 10:20:30,123       | msecs       | %(msecs)d       | 日志生成时间的毫秒部分 |
| created   | %(created)f   | time.time()生成的日志创建时间戳                        | message     | %(message)s     | 具体的日志信息         |
| filename  | %(filename)s  | 生成日志的程序名                                       | name        | %(name)s        | 日志调用者             |
| funcName  | %(funcName)s  | 调用日志的函数名                                       | pathname    | %(pathname)s    | 生成日志的完整路径     |
| levelname | %(levelname)s | 日志级别(“DEGBUG”,”INFO”,”WARNING“,”ERROR”,”CRITICAL”) | processName | %(processName)s | 进程名称               |
| levelno   | %(levelno)s   | 日志级别对应的数值                                     | thread      | %(thread)d      | 生成日志的线程id       |
| lineno    | %(lineno)d    | 日志所针对的代码行号                                   | process     | %(process)d     | 生成日志的进程id       |
| module    | %(module)s    | 生成日志的模块名                                       | threadName  | %(threadName)s  | 线程名                 |

## 五、高级用法实战

#### **5.1 生成器定义**

```python
#生成器
logger = logging.getLogger()
print(logger)
print(type(logger))
```

输出

```python
<RootLogger root (DEBUG)>
<class 'logging.RootLogger'>
```

我们也可以指定修改的显示名称，默认的话显示的是`root`

```python
#生成器
logger = logging.getLogger("log")
logger.setLevel(logging.DEBUG)
print(logger)
print(type(logger))
```

输出

```python
<Logger log (DEBUG)>
<class 'logging.Logger'>
```

#### 5.2 **处理器定义**

```python
#处理器
consoleHandler = logging.StreamHandler()
consoleHandler.setLevel(logging.DEBUG)

# 文件输出的handler
fileHandler = logging.FileHandler(filename="applog.log")
fileHandler.setLevel(logging.INFO)
```

#### 5.3 **处理器设置formatter格式**

```python
#给处理器设置formatter 格式
formatter = logging.Formatter("%(asctime)s|%(levelname)s|%(name)s:%(lineno)s|%(message)s|%(processName)s")
#设置格式
consoleHandler.setFormatter(formatter)
fileHandler.setFormatter(formatter)
```

#### 5.4 **记录器设置处理**

```python
# 记录器要设置处理器
logger.addHandler(consoleHandler)
logger.addHandler(fileHandler)
logger.debug("this is a debug data")
logger.info("this is a info data")
logger.warning("this is a warning data")
logger.error("this is a error data")
logger.critical("this is a critical data")
```

我们来看下最后的整体效果：

**控制台输出：**

![image-20211123140903040](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123140903040.png)

**文件输入:**

![image-20211123140921221](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123140921221.png)

我们发现一个问题，我们指定的`DEBUG`和`INFO`级别的日志，为啥在我们的控制台和我们的文件的格式不一样呢?

这是因为在我们定义生成器的时候：

logger = logging.getLogger()我们没有指定需要输出的日志等级，所以给我们默认输出的就是WARNING级别的日志。以至于我们最后输出结果不一样，那我们此时修改下：

此时我们想要在文件中输出INFO级别的日志，控制台输出DEBUG级别的日志，我们需要添加如下

```python
#生成器
logger = logging.getLogger()
logger.setLevel(logging.DEBUG)
print(logger)
print(type(logger))
```

此时我们看下最后的结果：

**控制台输出:**

![image-20211123141514147](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123141514147.png)

**文件输出：**

![image-20211123141535066](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123141535066.png)

#### 5.5 **定义一个过滤器**

```python
#定义过滤器   过滤开头名称为cn.cccb的文件
fit = logging.Filter("cn.cccb")

#关联过滤器
logger.addFilter(fit)
```

我们查看下效果：

此时控制台和文件都输出是空的：

![image-20211123142125199](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123142125199.png)

![image-20211123142137607](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123142137607.png)

那如果我们想要我们的输出结果显示呢，我们如何做呢，我们只需要更改我们的生成的自定义名称：

修改如下：

```python
logger = logging.getLogger("cn.cccb.log")
```

此时我们的文件和控制台均可以看到结果输出：

![image-20211123142258768](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123142258768.png)

![image-20211123142311154](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123142311154.png)

当然我们在设置过滤器的时候，我们也可以指定给我们的某个handler处理器指定过滤器来过滤，我们修改代码完整如下：

```python
import logging

#生成器
logger = logging.getLogger("log")
logger.setLevel(logging.DEBUG)

#处理器
consoleHandler = logging.StreamHandler()
consoleHandler.setLevel(logging.DEBUG)

# 文件输出的handler
fileHandler = logging.FileHandler(filename="applog.log")
fileHandler.setLevel(logging.INFO)

#给处理器设置formatter 格式
formatter = logging.Formatter("%(asctime)s|%(levelname)8s|%(name)s:%(lineno)s|%(message)s|%(processName)s")
#设置格式
consoleHandler.setFormatter(formatter)
fileHandler.setFormatter(formatter)


#定义过滤器   过滤开头名称为cn.cccb的文件
fit = logging.Filter("cn.cccb")

#关联过滤器
# logger.addFilter(fit)
fileHandler.addFilter(fit)

# 记录器要设置处理器
logger.addHandler(consoleHandler)
logger.addHandler(fileHandler)
logger.debug("this is a debug data")
logger.info("this is a info data")
logger.warning("this is a warning data")
logger.error("this is a error data")
logger.critical("this is a critical data")

```

我们在运行查看效果：控制台有输出结果，但是在我们的文件中是没有输出结果的

![image-20211123142606918](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123142606918.png)

![image-20211123142630670](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123142630670.png)

以上的一些方式，在我们日常使用的简单过程中，我们这样定义就可以了，但是如果我们在大型的项目过程中，如果去定义的话，那么我们就不能这样去做，我们总不能修改个日志等级的话，我们都需要去修改下代码吧？

于是我们采用了和java中日志记录相关的方式，我们将这些配置记录在我们的配置文件中，这样就很方便我们去进行修改了。

#### 5.6 配置文件方式定义

我们新建一个logger.conf文件，我们新增如下内容：

```python
[loggers]
keys=root,applog

[handlers]
keys=fileHandler,consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_applog]
level=DEBUG
handlers=fileHandler,consoleHandler
qualname=applog
propagate=0


[handler_consoleHandler]
class=StreamHandler
args=(sys.stdout,)
level=DEBUG

[handler_fileHandler]
class=handlers.TimedRotatingFileHandler
args=("logger.log","midnight",1,0)
level=DEBUG

[formatter_simpleFormatter]
format=%(asctime)s|%(levelname)8s|%(name)s:%(lineno)s|%(message)s|%(processName)s
datafm=%Y-%m-%d %H:%M:%S
```

>  **参数解读**：`[loggers]`、`[handlers`]、`[formatters]`和我们写代码定义生成器、格式化和处理器的定义是一样的，这里只是简单定义了下名称，`keys`代表的就是具体的名称，具体的属性配置在下面进行
>
> * `[logger_root`]就是对名为root的日志生成器进行属性设置
>
> * `[logger_applog]`就是对名称applog的日志生成器进行属性设置
>
>   `handlers`指定了，绑定的几个处理器对象
>
> ​		`qualname=applog` 表示在我们代码读取配置文件的时候，我们必须使用`getLogger(”applog“)`的方式才能获取到我们的这个对象
>
> ​		`propagate=0`表示0继承，这个用到 很少，就不多加赘述
>
> * `[handler_consoleHandler]`
>
>   `class=StreamHandler`表示定义的`StreaHandler`对象
>
>   `args=(sys.stdout,)` 代表的是标准输出流
>
> * `[handler_fileHandler]`
>
>   `class=handlers.TimedRotatingFileHandler`  （**这里定义的这个对象，是我们在写大工程的时候，我们经常遇到的一个，指定按时间次序生成文件）**
>
>   `args=("logger.log","midnight",1,0)`    规定文件名称，每天`凌晨12点`后备份一份数据，`1`代表的是`1`秒钟之后开始备份  `0`表示备份几份
>
> 

#### 5.7  代码异常记录日志

```python
#我们将str转换成int

a = "lhh"
int(a)
```

此时我们直接转换会出错，但是在我们的日志文件并不打印

![image-20211123151010105](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123151010105.png)

我们需要使用try catch捕捉异常处理：

```python
#我们将str转换成int
try:
    a = "lhh"
    int(a)
except Exception as e:
    applogger.exception(e)
```

我们看下效果:

![image-20211123151156075](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123151156075.png)

![image-20211123151214479](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20211123151214479.png)

我们发现不仅是在控制台上，在文件中也进行了具体的输出。此时我们全部讲完了logging标准库。还有一种我们使用dict字典的方式来定义我们的配置文件，但是这种方式我们用的并不是很多，所以我们也就不多加赘述了。

