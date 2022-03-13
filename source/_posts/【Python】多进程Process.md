---
title: 【Python】多进程Process
tags:
  - Python
categories:
  - Python
toc: true
abbrlink: 14455
date: 2021-07-25 13:56:32
---

Python中的多线程无法使用多核的优势，如果想要充分地使用多核CPU的资源（`os.cpu_count()`查看），在Python中大部分情况需要使用多进程。Python提供了multiprocessing。

<!--more-->

multiprocessing模块用来开启子进程，并在子进程中执行我们定制的任务（比如函数），该模块与多线程模块threading的编程接口类似。

`multiprocessing`模块的功能众多：支持子进程、通信和共享数据、执行不同形式的同步，提供了`Process`、`Queue`、`Pipe`、`Lock`等组件。

==注意==：**与线程不同，进程没有任何共享状态，进程修改的数据，改动仅限于该进程内**。

## 1.进程-Process

### 1.1 方法

#### 1.1.1 创建进程

~~~pythom
Process(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)
~~~

- **group**
  **参数未使用，永远为None**，故本方法应该使用关键字参数调用
- **target**
  表示调用对象，即子进程要执行的任务
- **name**
  子进程名称
- **args**
  传递给线程函数的位置参数,它必须是个tuple类型。，`args=(1,2,'egon')`
- **kwargs**
  传递给线程函数的关键字参数,它必须是个字典类型，`kwargs={'name':'egon','age':18}`
- **daemon**
  守护进程，`True` 或者 `False`，如果不传，则从父类的 `daemon` 继承

#### 1.1.2 p.run()

进程启动时运行的方法，正是它去调用 `target` 指定的函数，我们自定义类的类中一定要实现该方法。可以在子类中重写此方法。标准 `run()` 方法调用传递给对象构造函数的可调用对象作为目标参数（如果有），分别使用 `args` 和 `kwargs` 参数中的顺序和关键字参数。

### 1.1.3 p.start()

启动进程，并调用该子进程中的 `run()` 方法。

#### 1.1.4 p.join(timeout=None)

主进程等待 `p` 终止（强调：**是主进程处于等待的状态，而 `p` 是处于运行的状态**）。

> `timeout` 是可选的超时时间（**秒**），**如果可选参数 `timeout` 是 `None`（默认值），则该方法将阻塞**，直到调用 `join() `方法的进程终止。需要强调的是，`p.join()` 只能 `join` 住 `start` 开启的进程，而不能 `join` 住 `run` 开启的进程。

#### 1.1.5 p.is_alive()

返回进程是否存活。

> 从 `start()` 方法返回到子进程终止的那一刻，进程对象仍处于活动状态。

#### 1.1.6 p.terminate()

强制终止进程 `p`，不会进行任何清理操作。

> **如果 `p` 创建了子进程，该子进程就成了僵尸进程**，使用该方法需要特别小心这种情况。

> > **如果 `p` 还保存了一个锁那么也将不会被释放**，进而导致死锁

### 1.2 属性

#### 1.2.1 p.name

进程的名称。该名称是一个字符串，仅用于识别目的，它没有语义。可以为多个进程指定相同的名称。

初始名称由构造器设定。如果没有为构造器提供显式名称，则会构造一个形式为 `'Process-N' `的名称，表明是其父亲的第 N 个孩子。

#### 1.2.2 `p.pid`

返回进程的ID，在调用 `start()` 方法之前返回 `None`

#### 1.2.3 `p.daemon`

进程的守护进程标志，一个布尔值。必须在 `start()` 调用之前设置，当进程退出时，它会尝试终止其所有守护进程子进程。

> **注意，不允许守护进程创建子进程**。否则，守护进程会在子进程退出时终止其子进程。

#### 1.2.4 `p.exitcode`

进程在运行时为 `None`、如果为`–N`，表示被信号 `N` 结束(了解即可)

#### 1.2.5 `p.authkey`

进程的身份验证密钥（字节字符串）。

当 `multiprocessing` 初始化时，主进程使用 `os.urandom()` 分配一个随机字符串。

当创建 `Process` 对象时，它将继承其父进程的身份验证密钥，尽管可以通过将 `authkey` 设置为另一个字节字符串来更改。

> 需要注意的是**`start()`**，**`join()`**，**`is_alive()`**，**`terminate()`**和**`exitcode`**只能由创建进程对象的过程调用。

### 1.3 Process 的使用

**在windows中 `Process()` 必须放到 \**`if __name__ == '__main__':`\**下,
    由于Windows没有 `fork`，多处理模块启动一个新的Python进程并导入调用模块。
    如果在导入时调用 `Process()`，那么这将启动无限继承的新进程(或直到机器耗尽资源)。
    这是隐藏对 `Process()` 内部调用的源，使用 `if __name__ == “__main __”`，这个 `if`语句中的语句将不会在导入时被调用。**

#### 1.3.1 创建子进程的两种方法

- **通过`Process`类创建对象**

~~~python
import os
from multiprocessing import Process
import time
import random


def info(name):
    print(f"Process-{name} info stats....")
    time.sleep(random.randrange(1,5))
    print(f"Process-{name} info ends....")

if __name__ == "__main__":
  	# args参数传给target指向的
    p1 = Process(target=info,args=("p1",))
    p2 = Process(target=info,args=("p2",))
    p3 = Process(target=info,args=("p3",))
    p4 = Process(target=info,args=("p4",))

    p1.start()
    p2.start()
    p3.start()
    p4.start()
    print("主进程")
~~~

输出

~~~python
主进程
Process-p3 info stats....
Process-p2 info stats....
Process-p1 info stats....
Process-p4 info stats....
Process-p3 info ends....
Process-p1 info ends....
Process-p4 info ends....
Process-p2 info ends....
~~~

- **定义一个类继承 `Process`，重写 `run()` 方法，并通过自定义类创建对象**

  ~~~python
  # 方法二:
  class info(Process):
      def __init__(self,name):
          # 必须super()方法先，不然会覆盖__name
          super(info, self).__init__()
          self.__name = name
  
      def run(self) -> None:
          print(f"Process-{self.__name} info stats....")
          time.sleep(random.randrange(1, 5))
          print(f"Process-{self.__name} info ends....")
  
  
  if __name__ == "__main__":
      p1 = info("p1")
      p2 = info("p2")
      p3 = info("p3")
      p4 = info("p4")
  
      p1.start()
      p2.start()
      p3.start()
      p4.start()
  ~~~

输出：

~~~python
Process-p2 info stats....
Process-p1 info stats....
Process-p4 info stats....
Process-p3 info stats....
Process-p4 info ends....
Process-p2 info ends....
Process-p3 info ends....
Process-p1 info ends....
~~~

#### 1.3.2 进程之间的内存空间是隔离的

~~~python
# 内存隔离测试
l = [100]

def work():
    print('子进程内',id(l))

if __name__ == '__main__':
    p = Process(target=work)
    p.start()
    time.sleep(5)
    print("进程内",id(l))
~~~

输出结果:

> 子进程内 140395963531648
> 进程内 140335095201664
>
> 输出结果不同,因为进程之间的内存空间是不共享的

#### 1.3.3 Process对象的join方法：主进程等,等待子进程结束

~~~python
class info(Process):
    def __init__(self,name):
        super(info, self).__init__()
        self.__name = name

    def run(self) -> None:
        print(f"Process-{self.__name} run starts...")
        time.sleep(random.randrange(1, 3))
        print(f"Process-{self.__name} run ends...")


if __name__ == "__main__":
    p = info("p1")
    p.start()
    p.join()
    print("主进程start")
~~~

> 父进程join,就允许子进程执行完再执行父进程,如果没有join语句,执行顺序不一定，但是，创建子进程需要时间（比如分配内存等）,故总是看到父进程先执行

#### 1.3.4 守护进程

##### 1.3.4.1 守护子进程

主进程创建守护进程：

- 守护进程会在主进程代码执行结束后就终止
- 守护进程内无法再开启子进程,否则抛出异常

> 【注】进程之间是互相独立的，主进程代码运行结束，守护进程随即终止

~~~python
def task():
    # os.getpid() 获取进程pid
    print('%s is running' % os.getpid())
    time.sleep(2)
    print('%s is done' % os.getpid())
    # 注意，守护进程内无法再开启子进程,否则抛出异常

if __name__ == "__main__":
    p = Process(target=task)
    p.daemon = True   # 开启守护进程  必须是在start之前
    p.start()
    time.sleep(1)
    print("主")
~~~

输出结果:

~~~python
26433 is running主进程
~~~

> 原因是:主进程先创建子进程p,然后休眠1s,在这期间p进程创建完毕,并执行,所以先打印了第一行字符串，然后主进程苏醒（没苏醒由于 `p` 进程休眠 `2s`，也会执行它的）打印主进程的字符串，结束主进程，`p` 作为守护进程也随之毁灭，故 `p`进程的第二行字符串不会执行打印。

##### 1.3.4.2 守护子进程、非守护子进程并存

~~~python
def foo():    print(123)    time.sleep(1)    print("end123")def bar():    print(456)    time.sleep(3)    print("end456")if __name__ == "__main__":    p1 = Process(target=foo)    p2 = Process(target=bar)    p1.daemon =True    p1.start()    p2.start()    print("main.....")
~~~

输出

~~~python
main.....456end456
~~~

> 说明：由于p1.p2 都是子进程，需要开辟内存空间，需要耗费时间，所有会优先输出子进程__main__,由于守护子进程,p2是非守护子进程，当__main__进程执行完毕，p1守护进程也就退了,但是还有一个p2非守护进程成为孤儿进程，它会被程序等进程供养，所以p2会执行自己的代码任务，当p 2执行完毕，整个程序就退出了。

## 2.进程池-Pool

`Multiprocessing.Pool`可以提供指定数量的进程供用户调用，当有新的请求提交到`Pool`中时，如果池还没有满，那么就会创建一个新的进程用来执行该请求；但如果池中的进程数已经达到规定最大值，那么该请求就会等待，直到池中有进程结束，才会创建新的进程来执行它。`pool`类用于需要执行的目标很多，而手动限制进程数量又太繁琐时，如果目标少且不用控制进程数量则可以用`Process`类。

### 2.1 方法

#### 2.1.1 创建线程池

~~~python
Pool(processes=None, initializer=None, initargs=(), maxtasksperchild=None, context=None)
~~~



- **processes**
  要使用的工作进程数。如果进程是 `None`，那么使用返回的数字 `os.cpu_count()`，也就是说根据本地的CPU个数决定
- **initializer**
  如果 `initializer` 是 `None`，那么每一个工作进程在开始的时候会调用 `initializer(*initargs)`
- **initargs**
  调用 `initializer` 的参数
- **maxtasksperchild**
  工作进程退出之前可以完成的任务数，完成后用一个新的工作进程来替代原进程，来让闲置的资源被释放。`maxtasksperchild` 默认是 `None`，意味着只要 `Pool`存在工作进程就会一直存活
- **context**
  用在制定工作进程启动时的上下文，一般使用 `multiprocessing.Pool()` 或者一个 `context` 对象的 `Pool()` 方法来创建一个池，两种方法都适当的设置了 `context`。

#### 2.1.2 p.apply(func,args=(),kwds={})

**Equivalent of func(\*args, \**kwds), Pool must be running**。它会阻塞其他进程(包括线程池中的其他进程和 `main` 进程)，直到结果准备就绪。

~~~python
from multiprocessing import Pooldef test(p):    print(p)if __name__ == "__main__":    pool = Pool(3)    for i in range(4):        pool.apply(test,args=(i,))    print("test")
~~~

输出

~~~python
0123test
~~~

> test 最后打印是因为前面执行了apply()函数阻塞了，等apply 执行完才会继续执行下面

#### 2.1.3 p.apply_async()

~~~python
apply_async(func, args=(), kwds={}, callback=None,error_callback=None)
~~~

在一个池工作进程中执行 `func(*args,**kwds)`，然后返回结果。此方法的结果是 `AsyncResult` 类的实例，`callback` 是可调用对象，接收一个参数，当结果变为 `ready` 时，将回调函数应用于它。回调应该立即完成，否则处理结果的线程将被阻塞。

~~~python
def test(p):    time.sleep(random.randrange(2))    return p*pif __name__ == "__main__":    pool = Pool(processes=2)    for i in range(1,5):        pool.apply_async(test,args=(i,),callback=print)    print("test")    # 必须要先close,禁止向池中添加任务，不然join会出错    pool.close()    # 没有这个代码，直接输出test后，程序将会停止    pool.join()
~~~

输出：

~~~python
test14169
~~~

> 上面的程序是，多进程执行 `test()`函数，如果执行没问题返回`ready`，就对 `test` 的结果执行`callback` 指定的回调函数
>
> `apply_async()` 不阻塞主进程，`callback` 的入参是 `func()` 的返回值

总结一下，`apply_async`方法是异步方法，可以不等先添加到进程池的方法执行完，就异步地继续添加方法到进程池中；而 `apply` 方法是同步方法，必须等上一个函数执行完再添加。打个比方，执行的函数要休眠3 s，显然异步 `apply_async` 几乎3 s就结束，而 `apply` 方法随子进程增加，耗时也是线性增加。`apply_async` 也是Python官方推荐的方法。

#### 2.1.4 p.map()

~~~python
map(func, iterable, chunksize=None)
~~~

`map()`内置函数的并行等价物（尽管它只支持一个可迭代的参数）。它会阻塞 `main`，直到结果准备就绪。可以把传入的 `Iterable` 对象分成多个块，通过将 `chunksize`设置块的大小，将这些块作为单独的任务提交给进程池，不传值时，会自动根据 `Iterable` 对象和进程池的大小自动确定。返回值是 `list`。

~~~python
def int2str(n):    return str(n)if __name__ == "__main__":    pool = Pool(processes=2)    l = [6,4,4,4,7,6,1,1,4]    # map的结果可以迭代    for n in pool.map(int2str,l):        print(n,end="")    print("\n test")
~~~

输出：

~~~python
644476114 test
~~~

> Main 进程被阻塞，test 是最后打印的

#### 2.1.5 p.map_async()

~~~python
map_async(self, func, iterable, chunksize=None, callback=None,error_callback=None)
~~~

`map()`返回结果对象的方法的变体，异步执行，不阻塞`main`进程。返回值是`ApplyResult`。

~~~python
def show(x):    print(x)    time.sleep(0.5) if __name__ == "__main__":		pool = Pool(processes=2)    pool.map_async(show, range(50))	    time.sleep(1)    print('test')
~~~

输出：

~~~python
0718test
~~~

> `map_async()`在`main`进程停止后会跟着停止

#### 2.1.6 p.imap()

~~~python
imap(func, iterable, chunksize=1)
~~~

①大体功能上和内置的map()方法的功能是一样的

②返回的是一个`Generator`，是一种**lazier**版本的`map()`方法

③该方法不会阻塞`main`进程，`main`进程结束，程序就结束

#### 2.1.7 p.close()

防止向池提交任何其他任务。一旦所有任务完成，工作进程将退出

#### 2.1.8 p.terminate()

立即停止工作进程而不完成未完成的工作。当池对象被垃圾收集时，`terminate()`将立即调用

#### 2.1.9 p.join()

必须在`close()`之后执行。

必须等待进程池任务都结束，程序才能结束（相当于**join**住`main`进程）

### 2.2 ApplyResult（AsyncResult它的是别名）

`Pool` 中 `apply_async()` 和 `map_async()` 的方法返回值是 `AsyncResult` 的实例（或者是它子类的实例）obj。实例具有以下方法：

- `obj.get(timeout=None)`
  返回结果的值，如果设置`timeout`，则要在规定时间内返回结果，否则报错
- `obj.ready()`
  如果 `Pool` 的方法调用完成，则返回 `True`
- `obj.successful()`
  如果调用完成且没有引发异常，返回 `True`，如果在 `obj.ready()` 为 `True` 之前调用此方法，将引发异常
- `obj.wait(timeout=None)`
  等待结果可用或超时秒过去

