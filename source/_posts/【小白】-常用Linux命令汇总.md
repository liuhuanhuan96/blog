---
title: 【小白】 常用Linux命令汇总
tags:
  - Linux
categories:
  - Linux
toc: true
abbrlink: 17450
date: 2021-07-25 14:18:48
---

##### 常用命令

~~~shell
--help    命令说明`
pwd       查看当前所在位置`
tab       补全代码（特殊情况按两次）`
曾经使用的命令可以上下按键来切换`
`输入来不像执行的命令可以使用ctrl+c取消或者ctrl+u将输入的内容删除
~~~

<!--more-->

##### l s查看目录文件

```shell
-a 显示隐藏文件。

-l 以列表的形式显示

-h 以人性化的方式显示文件的大小

-R  递归显示子目录

ls -lR | grep bcd
```



##### cd 切换工作目录

​	绝对路径和相对路径：

​		绝对路径：指的是在输入路径的时候，最前面是/或者～表示从根目录/home目录开始的具体的目录位置

​		相对路径：指的是以当前目录开始，不以/或者～开头，表示不是以根目录或者home目录开始的目录

```shell
cd  切换到指定路径

cd .  切换到当前目录

Cd ..切换到上级目录

Cd ~切换到home目录

cd -  与上一次工作目录相互换
```



##### touch新建文件命令：

```shell
	`touch 文件名称`
```

​	![image-20201006023517134](https://img-blog.csdnimg.cn/img_convert/0155a70da6bacff5b1bfb8a2a35739d2.png)

```shell
	`touch  文件名称 文件名
```

`

<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1gjf36xnubfj31uw07eacj.jpg" alt="image-20201006023905517" style="zoom:50%;" />



##### mkdir新建目录：

```shell
	`-p 递归调用`
```

```shell
`mkdir 文件名`
```

```shell
mkdir -p a/b/c
```

```shell
rmdir只能删除空目录，不能删除非空目录
```



#####   rm. 删除文件或目录

```shell
	-r   递归地删除目录下的文件，删除文件夹时必须加此参数
```

```shell
-f. 强制删除，忽略不存在的文件，无需提示
```

```shell
rm -rf filename.  删除文件名称
```



##### mv移动和重命名

```shell
-f. 覆盖前不询问
```

```shell
-i 覆盖前询问
```

```shell
-n.不覆盖已经存在的文件
```

```shell
mv 命令在同一个文件夹下移动文件，即重命名功能
```

<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1gjf36ny028j310k0dqdlx.jpg" alt="image-20201006025729725" style="zoom:50%;" />

##### Cp复制



```shell
-i  覆盖前提示
```

```shell
-r 若给出的源文件是目录文件，则cp将递归复制该目录下的所有子目录和文件，目标文件必须为以一个目录名
```

![image-20201006025650259](https://img-blog.csdnimg.cn/img_convert/d79db3a493a7704bbc2519a29f9097e3.png)



##### cat查看文件内容、合并文件

​	

```shell
-n  输出行编号
```

```shell
-s  不输出多行空行
```

```shell
	-b. 对非空行进行编号
```

```shell
	cat filename.   查看文件的内容
```

```shell
	cat. File1  file2. > file1.    将file1 和file2的文件合并写入到file1中
```

##### more  查看文件内容（分页查看）

```shell
	more filename   查看filename文件到内容	快捷键。                   功能说明	空格键   									显示下一屏	Enter键										一次滚动一行	b													回滚一屏	f													前滚一屏	q													退出
```



##### history查看历史命令

```shell
history      查看历史命令	
```

```shell
history -c   删除历史命令记录
```

##### sudo获得root权限

```shell
Linux 默认不能以root账号登陆，可以用sudo 获得权限
```



##### linux三种权限

​	![image-20201006031247263](https://img-blog.csdnimg.cn/img_convert/ffcd7d0a115605885ea3707da0ae9fc6.png)

​	

##### 创建用户：

```shell
	useradd.   【用户名】
```

```shell
	-d   指定新账户的主目录
```

```shell
	-g   指定用户的所属组
```

```shell
	-G  指定用户附加组
```

```shell
	-s. 指定用户登陆
```

```shell
	-m. 自动创建home目录	
```



##### 删除用户：

```shell
userdel. [用户组]
```

```shell
	-r 删除用户的同时删除home目录
```



```shell
su root  切换到root账号下whoami  查看当前登陆的账号
```

![image-20201006032300031](https://img-blog.csdnimg.cn/img_convert/3ee7abb54bd11c404569589b582f3b94.png)



```shell
useradd test1   创建用户cat  /etc/passwd    /etc/passwd存放了用户的信息
```

![image-20201006032525488](https://img-blog.csdnimg.cn/img_convert/11a2993706f63e8d030a57b4838f73e1.png)

![image-20201006032633108](https://img-blog.csdnimg.cn/img_convert/84deb341acc433bbc187a8e41a1893f9.png)

此时未成功的创建好test用户

```shell
useradd -m test1   即可成功的创建用户  在/home目录下可看到该文件夹
```

修改用户的密码

```shell
passwd test1    新的下面输出新密码即可创建成功
```

<img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1gjf35snff3j31ws0cqdik.jpg" alt="image-20201006033226666" style="zoom:50%;" />

切换用户切换到对应的home目录下

![image-20201006033443851](https://img-blog.csdnimg.cn/img_convert/3c0595ecde5bf960bba6b9956cc25dab.png)

```shell
userdel test2   只会去删除用户。不会删除用户对应的home目录userdel -r test2  不仅去删除用户。也会删除用户对应的home目录
```

##### 	修改用户账号属性：

​	usermod:	

```shell
-u 用户id-g 所属家属组-a -G GID  不实用-a会覆盖之前的附加组-d -m 将home目录位置移动到新位置-s 该用户账号的新登陆-l 新的登陆名称
```

##### 用户组管理：

###### 	创建用户组：

```shell
groupadd
```

###### 删除用户组

```shell
groupdel
```

###### 	修改组属性

```shell
groupmod-g Gid
```

提示：

​	创建用户时，会默认创建一个与用户名同民的组名

​	创建成功后可在/e t c/passwd文件下查看

​	新创建的用户没有sudo权限，需要将用户加到a d m，su do这两个组中才拥有su do权限

##### 权限管理

​	

```shell
chmod + /-rwx 文件名｜目录名+增加权限,-取消权限
```

每个文件都有三组不同的权限，第一组文件所有者，第二组时文件所有组，第三组时其他用户

第一组：u文件所有者 修改所有者权限 chmod u+/-/ = rwx filename

第二组：g文件所有组 修改所有组权限 chmod g+/-/ = rwx filename

第三组：o其他用户 修改所有组权限 chmod o+/-/ = rwx filename

![image-20201006152841615](https://img-blog.csdnimg.cn/img_convert/550c24c6e9bde244b4aeafd58a2dcf27.png)

![image-20201006153342388](https://img-blog.csdnimg.cn/img_convert/54de8b3b52565338c849c254c42d6dc2.png)

![image-20201006153447514](https://img-blog.csdnimg.cn/img_convert/6c837860023f30c92e83dfa3514d72b9.png)

```shell
chmod 755 文件名｜目录名 指定权限修改chmod中第一个数字代表所有者权限，第二个数字代表所属组的权限，第三个数字代表其他人权限r   4w   2x   1
```

```shell
4 2 1    7     r w x4 2 0    6     r w -4 0 1    5     r - x4 0 0    4     r - -0 2 1    3     - w x0 2 0    2     - w -0 0 1    1     - - x0 0 0    0     - - -
```

![image-20201006154821717](https://img-blog.csdnimg.cn/img_convert/807962e7aacedb1c61f6aaa637290888.png)

##### 远程管理

###### Ifconfig

```shell
ifconfig     查看系统ip地址
```

![image-20201006155229054](https://img-blog.csdnimg.cn/img_convert/746f9acd475839015e8d252cc352d96f.png)

###### ping

```shell
ping   检查网络是否正常通信，linux下默认ping不会结束，使用c t r l+C强制结束例如:ping www.baidu.com
```

```shell
ping -c 指定几个数据包结束
```

```shell
ping -i 指定发送数据包的间隔，单位时秒
```

```shell
ping -s 指定发送数据的大小 单位时字节
```

```shell
ping -t 设置TTL的大小  TTL网络调数大小
```

![image-20201006155736975](https://img-blog.csdnimg.cn/img_convert/fc9673c68ece8028e75f52dcc1e50520.png)

###### ssh远程连接

Ssh是一种网络协议，用于计算机之间的加密登陆，Linux下默认开启sshd服务，只有开启sshd服务才能进行连接

```shell
service sshd status  查看是否开启服务 active表示已开启
```

![image-20201006160039844](https://img-blog.csdnimg.cn/img_convert/558c20a43a7e27877b75a903c812bfc8.png)

###### ssh远程连接

Window：xshell 和putty

Mac. finallshell

Linux  

```shell
ssh -p 端口 主机  -p可以指定端口ssh 一般默认使用22  看到welcome表示连接成功
```

![image-20201006160425256](https://img-blog.csdnimg.cn/img_convert/20641d3cfdcf0133083b1864e84e2d46.png)

###### scp文件复制：

scp就是se cure copy 是一个在linux下用来进行远程拷贝文件的命令

使用范例1:吧远程的e.txt文件拷贝到本地/home/python/Desktop下

```shell
scp python@192.168.254.131:/home/python/a/e.txt /home/python/Desktop
```

使用范例2:把本地的Desktop/requirements.txt 文件拷贝到远程主机的home目录下

```shell
scp Desktop/requirements.txt python@192.168.254.131:/home/python
```

使用范例3:scp -r可以复制文件夹，把当前目录下的demo文件夹复制到远程目录下的Desktop

```shell
scp -r demo user@remote:Desktop
```

使用范例4:将远程主机的a文件夹包括子文件，复制到本机的桌面

```shell
scp -r python@192.168.254.131:/home/python/a Desktop
```

scp只能在linux中使用，window中我们一般使用winscp

winscp下载地址：https://winscp.net/eng/download.php

##### 系统信息管理

###### Date 查看系统当前时间

```shell
[root@izuf6essqiicvb19gkmlb9z ~]# date2020年 10月 06日 星期二 16:17:12 CST[root@izuf6essqiicvb19gkmlb9z ~]# 
```

###### 查看磁盘空间

 d f -Th查看磁盘分区，以及挂载情况

```shell
[root@izuf6essqiicvb19gkmlb9z ~]# df -Th文件系统       类型      容量  已用  可用 已用% 挂载点/dev/vda1      ext4       40G  4.3G   34G   12% /devtmpfs       devtmpfs  911M     0  911M    0% /devtmpfs          tmpfs     920M     0  920M    0% /dev/shmtmpfs          tmpfs     920M  392K  920M    1% /runtmpfs          tmpfs     920M     0  920M    0% /sys/fs/cgrouptmpfs          tmpfs     184M     0  184M    0% /run/user/0[root@izuf6essqiicvb19gkmlb9z ~]# 
```

du -sh 【filename】 查看目录大小

```shell
[root@izuf6essqiicvb19gkmlb9z /]# du -sh liuhuanhuan0       liuhuanhuan[root@izuf6essqiicvb19gkmlb9z /]# 
```

du -h [filename] 查看文件大小

```shell
[root@izuf6essqiicvb19gkmlb9z tmp]# du -h hsperfdata_root/36K     hsperfdata_root/[root@izuf6essqiicvb19gkmlb9z tmp]# 
```

###### 查看内核/操作系统/c pu信息

```shell
uname -a 查看内核/操作系统/c pu信息
```

```shell
[root@izuf6essqiicvb19gkmlb9z tmp]# uname -aLinux izuf6essqiicvb19gkmlb9z 3.10.0-514.26.2.el7.x86_64 #1 SMP Tue Jul 4 15:04:05 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```

```shell
uname -i 查看硬件平台
```

```shell
uname -m 查看cpu
```

```shell
uname -n 查看节点名称
```

```shell
uname -o 查看操作系统
```

```shell
uname -v 查看内核版本
```

```shell
uname -r 查看发行版本号
```

###### 查看进程

to p查看进程实时运行情况，即系统资源实时使用情况，退出to p界面输入q

```shell
top - 16:27:44 up 26 days,  3:32,  3 users,  load average: 0.00, 0.06, 0.06Tasks:  79 total,   1 running,  78 sleeping,   0 stopped,   0 zombie%Cpu(s):  0.3 us,  0.2 sy,  0.0 ni, 99.5 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 stKiB Mem :  1883652 total,   104420 free,   832708 used,   946524 buff/cacheKiB Swap:        0 total,        0 free,        0 used.   847524 avail Mem   PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                                                                                              1 root      20   0   43180   3304   2100 S  0.0  0.2   0:15.42 systemd                                                                                                              2 root      20   0       0      0      0 S  0.0  0.0   0:00.02 kthreadd                                                                                                             3 root      20   0       0      0      0 S  0.0  0.0   0:08.82 ksoftirqd/0                                                                                                          5 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kworker/0:0H                                                                                                         6 root      20   0       0      0      0 S  0.0  0.0   0:10.68 kworker/u2:0                                                                                                         7 root      rt   0       0      0      0 S  0.0  0.0   0:00.00 migration/0                                                                                                          8 root      20   0       0      0      0 S  0.0  0.0   0:00.00 rcu_bh                                                                                                               9 root      20   0       0      0      0 S  0.0  0.0   1:13.69 rcu_sched                                                                                                           10 root      rt   0       0      0      0 S  0.0  0.0   0:06.55 watchdog/0                                                                                                          12 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kdevtmpfs                                                                                                           13 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 netns                                                                                                               14 root      20   0       0      0      0 S  0.0  0.0   0:00.51 khungtaskd                                                                                                          15 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 writeback                                                                                                           16 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kintegrityd                                                                                                         17 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 bioset                                                                                                              18 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kblockd                                                                                                             19 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 md                                                                                                                  25 root      20   0       0      0      0 S  0.0  0.0   0:00.91 kswapd0                                                                                                             26 root      25   5       0      0      0 S  0.0  0.0   0:00.00 ksmd                                                                                                                27 root      39  19       0      0      0 S  0.0  0.0   0:03.26 khugepaged                                                                                                          28 root      20   0       0      0      0 S  0.0  0.0   0:00.00 fsnotify_mark                                                                                                       29 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 crypto                                                                                                              37 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kthrotld 
```

```shell
PID  进程idUSER  进程所有者PR  进程优先级NI   nice值，负值表示高优先级，正值表示低优先级VIRT   进程使用的虚拟机内存总量RES    进程使用的，未被换出的物理内存大小SHR    共享内存大小S      进程状态 D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程%CPU   上次更新到现在CPU时间占用百分比%MEM	进程使用的物理内存百分比TIME+ 进程使用的cpu时间统计COMMAND 进程名称
```

###### Ps 查看系用所有进程的状态

```shell
ps -ajx   一般使用ps 和-ajx一起使用D		不可中断系统进程R  	运行中的进程S		中断sleep状态T		停止Z		僵死-僵尸进程
```

###### 结束进程		

kill [参数][进程号]

``` shell
kill 9[进程号]   强制结束进程kill 15[进程号]   结束进程，等级没有-9高
```

提示：在linux中1号进程是不能被终止的

###### 练习测试

1.创建一个用户li lei,其id号未2002，基本组为s tu（id为3000）,附加组为linux

```shell
sudo groupadd -g 3000 stusudo groupadd linuxsudo useradd -u 2002 -g stu -G linux lilei
```

2.创建一个用户hanmeimei需要默认创建home目录，并指定shell为/bin/bash

```shell
sudo useradd -m -s /bin/bash hanmeimei
```

3.修改lilei 的id号为4004,所属组为linux

```shell
usermod -u 4004 -g linux lilei
```

4.添加系统用户zhao yu,其不允许其登陆系统

```shell
useradd -r -s '/bin/nologin' zhaoyu
```

5.在桌面创建一个文件a.txt，并查看其文件的权限

```shell
touch a.txtls -l
```

6.修改a,txt所在组的权限为只读

```shell
chmod g=r a.text
```

7.将a .txt的权限修改为其他人无任何权限，所有者可读可写，所属组

```shell
chmod u=rw,g=r,o=--- a.text
```

##### 文件查找

###### which命令：

查看给定命令的绝对位置，whi ch会在环境变量和$path设置的目录里查找合适的文件，也就是说which 可以查看系统某个命令是否存在，以及执行哪个位置的命令，此命令去搜索$path环境变量的目录中去，可以使用e cho $PATH查看，如：

```shell
[root@izuf6essqiicvb19gkmlb9z /]# echo $PATH/usr/local/maven/apache-maven-3.6.3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/local/java/jdk1.8.0_261/bin:/usr/local/java/jdk1.8.0_261/jre/bin:/usr/local/node/node-v12.18.4-linux-x64/bin:/root/bin
```

路径使用":"去分割，Which命令会在这些路径下去搜索

Which   [系统命令]

```shell
[root@izuf6essqiicvb19gkmlb9z /]# which java/usr/local/java/jdk1.8.0_261/bin/java[root@izuf6essqiicvb19gkmlb9z /]# which mvn/usr/local/maven/apache-maven-3.6.3/bin/mvn
```

which是根据使用者所配置的环境变量去查看，不同的环境变量所找到的内容自然也是不同的

###### whereis命令：

whereis可以查看命令的绝对位置

whic h会列出这个命令的别名的记录，而whereis只会查看该命令所在的位置

whereis

```shell
-b 只查找二进制文件
```

```shell
-B<目录> 只在设置的目录下查找二进制文件
```

```shell
-f 不显示文件民前的路径名称
```

```shell
-m 只查找说明文件
```

```shell
-M<目录>   只在设置的目录下查看说明文件
```

```shell
-s   只查找原始代码文件
```

```shell
-S<目录> 只在设置的目录下面去查看原始代码文件
```

```shell
-u 查找不包含指定类型的文件
```

```shell
[root@izuf6essqiicvb19gkmlb9z /]# whereis javajava: /usr/local/java /usr/local/java/jdk1.8.0_261/bin/java /usr/local/java/jdk1.8.0_261/jre/bin/java[root@izuf6essqiicvb19gkmlb9z /]# whereis mvnmvn: /usr/local/maven/apache-maven-3.6.3/bin/mvn /usr/local/maven/apache-maven-3.6.3/bin/mvn.cmd[root@izuf6essqiicvb19gkmlb9z /]# whereis pwdpwd: /usr/bin/pwd /usr/include/pwd.h /usr/share/man/man1/pwd.1.gz
```

###### Locate命令

Locate [关键字]

1.linux特有的寻找文件和目录的命令，用于快速定位系统命令，配置文件等

2.速度虽然快，但是有时候会找不到

3.locate是在文件数据库中查找，所以是很快的

4.文件数据库没有该文件，则无法查找到

```shell
updatedb 建立整个文件系统数据库    注意，执行权限为root
```

注：

​	当在某些目录下创建文件时，然后更新数据库之后，并不能用locate命令立马查找到，原因是系统在更新数据库到配置文件中，设置了一些搜索限制，所以搜不到，输入如下命令即可看到：

locate命令安装

```shell
yun install mlocateupdatedb
```

###### find命令：

会在一个目录中去搜索文件，可以指定一些匹配条件，如文件名，文件类型和用户名等

Find [搜索路径][搜索选项] filename

path路径，表示从这个路径下开始找

```shell
-name filename  查找名为filename的文件
```

```shell
-size +/-大小 按照文件的大小来查找 +大于 -小于
```

```shell
-user username 按文件所属查找
```

```shell
通过时间查找			-ctime -atime -mtime （以天为单位）			-cmin -amin -mmin(以分为单位)
```

```shell
-type 按文件类型
```

```shell
-inum 根据i结点来查找
```

```shell
-group 组名 按所属组来查找
```

```shell
-a and 逻辑与 -O or 
```

```shell
-exec 或 -ok command {} \:将查到的文件command操作，
```

```shell
按照名称去查找[root@izuf6essqiicvb19gkmlb9z /]# find ./ -name java./usr/local/java./usr/local/java/jdk1.8.0_261/bin/java./usr/local/java/jdk1.8.0_261/jre/bin/java./usr/local/ShiJiaZhuRainAi/ShiJiaZhuangRain/src/test/java./usr/local/ShiJiaZhuRainAi/ShiJiaZhuangRain/src/main/java./etc/pki/java./etc/pki/ca-trust/extracted/java
```

发现并删除8天以前创建的文件

```shell
find ./ -mtime +8 -print|xargs rm -rf
```

Where locate whereis find的区别：

```shell
1.which用于查找直接的命令 只能查找可执行的文件，该命令只在$PATh中去查找，查重范围小，速度快 -a返回所有结果2.whereis 不只可以查看命令 棋类类型文件也可以查找。在$PATH基础上增加一些系统目录的查找，查找范围比which稍微大点，速度快，3.locat 快速查找指定的文件 他会从linux内置的文件数据库中去查找 可以使用updatedb 来更新一次索引，确保不会遗漏文件，可以通过-r正则匹配查找文件4.直接搜索整个文件目录，默认从根目录开始查找，最强大但是速度慢
```

###### Grep：

grep是强大的文本搜索工具，他能使用正则表达式搜索文本，并把匹配的行打印出来

```shell
	grep "python" filename    #在filename文件中查找python,并将结果打印出来	grep "python" filename filename2 filename3   #在多个文件中查找python,并将结果打印出来	
```

-E选项使用正则表达式：

```shell
grep -E “[a-c]+” filename 
```

在多个文件中查找

```shell
grep  "match_patter" file_1,file_2,file_3
```

输出包含匹配字符串的行数-n选项

```shell
grep "this" index -n textindex
```

###### 管道符|

将左边的输出当作右边的输入

```shell
ps -ajx | grep ssh   将ps输出的结果当作grep的输入过滤
```

```shell
[root@izuf6essqiicvb19gkmlb9z /]# ps -ajx | grep ssh    1  2005  2005  2005 ?           -1 Ss       0   0:00 /usr/sbin/sshd -D32741  8561  8561 32741 pts/0     8561 S+       0   0:00 ssh localhost -p 22 2005  8562  8562  8562 ?           -1 Ss       0   0:00 sshd: root@pts/2 8698 14678 14677  8698 pts/2    14677 R+       0   0:00 grep --color=auto ssh 2005 27153 27153 27153 ?           -1 Ss       0   0:00 sshd: root@notty27153 27155 27155 27155 ?           -1 Ss       0   0:00 /usr/libexec/openssh/sftp-server27153 27174 27174 27174 ?           -1 Ss       0   0:00 /usr/libexec/openssh/sftp-server27153 27181 27181 27181 ?           -1 Ss       0   0:00 /usr/libexec/openssh/sftp-server27153 27188 27188 27188 ?           -1 Ss       0   0:00 /usr/libexec/openssh/sftp-server27153 27195 27195 27195 ?           -1 Ss       0   0:00 /usr/libexec/openssh/sftp-server27153 27202 27202 27202 ?           -1 Ss       0   0:00 /usr/libexec/openssh/sftp-server 2005 32739 32739 32739 ?           -1 Ss       0   0:21 sshd: root@pts/0,pts/1
```

显示/e t c目录下的文件或目录的总数量

```shell
[root@izuf6essqiicvb19gkmlb9z /]# ll /etc | grep -E ".*" -c196
```

###### 输出重定向

```shell
ls > test.txt   #将ls命令的输出重定向到test.txt文件[root@izuf6essqiicvb19gkmlb9z /]# ll > /home/TestCDX.txt[root@izuf6essqiicvb19gkmlb9z /]# lsbin  boot  dev  etc  home  lib  lib64  liuhuanhuan  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var[root@izuf6essqiicvb19gkmlb9z /]# cd /home[root@izuf6essqiicvb19gkmlb9z home]# lstemp  test  test2  TestCDX.txt  testfile[root@izuf6essqiicvb19gkmlb9z home]# cat TestCDX.txt 总用量 60lrwxrwxrwx.  1 root root     7 8月  18 2017 bin -> usr/bindr-xr-xr-x.  4 root root  4096 9月   9 21:19 bootdrwxr-xr-x  19 root root  2980 9月  11 14:00 devdrwxr-xr-x. 81 root root  4096 10月  6 17:48 etcdrwxr-xr-x.  5 root root  4096 10月  6 18:25 homelrwxrwxrwx.  1 root root     7 8月  18 2017 lib -> usr/liblrwxrwxrwx.  1 root root     9 8月  18 2017 lib64 -> usr/lib64-rw-r--r--   1 root root     0 10月  6 02:34 liuhuanhuandrwx------.  2 root root 16384 8月  18 2017 lost+founddrwxr-xr-x.  2 root root  4096 11月  5 2016 mediadrwxr-xr-x.  2 root root  4096 11月  5 2016 mntdrwxr-xr-x.  2 root root  4096 9月  27 17:35 optdr-xr-xr-x  90 root root     0 9月  10 12:55 procdr-xr-x---. 11 root root  4096 10月  6 15:25 rootdrwxr-xr-x  23 root root   660 10月  6 17:48 runlrwxrwxrwx.  1 root root     8 8月  18 2017 sbin -> usr/sbindrwxr-xr-x.  2 root root  4096 11月  5 2016 srvdr-xr-xr-x  13 root root     0 9月  10 20:55 sysdrwxrwxrwt. 13 root root  4096 10月  6 17:48 tmpdrwxr-xr-x. 13 root root  4096 8月  18 2017 usrdrwxr-xr-x. 19 root root  4096 9月  10 20:55 var
```

输出重定向：追加>>

将输出重定向追加到文件

```shell
>>```>>ls >> text.txt   将ls命令的输出追加到test.txt>>[root@izuf6essqiicvb19gkmlb9z /]# ll > /home/TestCDX.txt>>[root@izuf6essqiicvb19gkmlb9z /]# ls>>bin  boot  dev  etc  home  lib  lib64  liuhuanhuan  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var>>[root@izuf6essqiicvb19gkmlb9z /]# cd /home>>[root@izuf6essqiicvb19gkmlb9z home]# ls>>temp  test  test2  TestCDX.txt  testfile>>[root@izuf6essqiicvb19gkmlb9z home]# cat TestCDX.txt >>总用量 60>>lrwxrwxrwx.  1 root root     7 8月  18 2017 bin -> usr/bin>>dr-xr-xr-x.  4 root root  4096 9月   9 21:19 boot>>drwxr-xr-x  19 root root  2980 9月  11 14:00 dev>>drwxr-xr-x. 81 root root  4096 10月  6 17:48 etc>>drwxr-xr-x.  5 root root  4096 10月  6 18:25 home>>lrwxrwxrwx.  1 root root     7 8月  18 2017 lib -> usr/lib>>lrwxrwxrwx.  1 root root     9 8月  18 2017 lib64 -> usr/lib64>>-rw-r--r--   1 root root     0 10月  6 02:34 liuhuanhuan>>drwx------.  2 root root 16384 8月  18 2017 lost+found>>drwxr-xr-x.  2 root root  4096 11月  5 2016 media>>drwxr-xr-x.  2 root root  4096 11月  5 2016 mnt>>drwxr-xr-x.  2 root root  4096 9月  27 17:35 opt>>dr-xr-xr-x  90 root root     0 9月  10 12:55 proc>>dr-xr-x---. 11 root root  4096 10月  6 15:25 root>>drwxr-xr-x  23 root root   660 10月  6 17:48 run>>lrwxrwxrwx.  1 root root     8 8月  18 2017 sbin -> usr/sbin>>drwxr-xr-x.  2 root root  4096 11月  5 2016 srv>>dr-xr-xr-x  13 root root     0 9月  10 20:55 sys>>drwxrwxrwt. 13 root root  4096 10月  6 17:48 tmp>>drwxr-xr-x. 13 root root  4096 8月  18 2017 usr>>drwxr-xr-x. 19 root root  4096 9月  10 20:55 var>>[root@izuf6essqiicvb19gkmlb9z home]# ls >> TestCDX.txt>>[root@izuf6essqiicvb19gkmlb9z home]# ls>>temp  test  test2  TestCDX.txt  testfile>>[root@izuf6essqiicvb19gkmlb9z home]# cat TestCDX.txt >>总用量 60>>lrwxrwxrwx.  1 root root     7 8月  18 2017 bin -> usr/bin>>dr-xr-xr-x.  4 root root  4096 9月   9 21:19 boot>>drwxr-xr-x  19 root root  2980 9月  11 14:00 dev>>drwxr-xr-x. 81 root root  4096 10月  6 17:48 etc>>drwxr-xr-x.  5 root root  4096 10月  6 18:25 home>>lrwxrwxrwx.  1 root root     7 8月  18 2017 lib -> usr/lib>>lrwxrwxrwx.  1 root root     9 8月  18 2017 lib64 -> usr/lib64>>-rw-r--r--   1 root root     0 10月  6 02:34 liuhuanhuan>>drwx------.  2 root root 16384 8月  18 2017 lost+found>>drwxr-xr-x.  2 root root  4096 11月  5 2016 media>>drwxr-xr-x.  2 root root  4096 11月  5 2016 mnt>>drwxr-xr-x.  2 root root  4096 9月  27 17:35 opt>>dr-xr-xr-x  90 root root     0 9月  10 12:55 proc>>dr-xr-x---. 11 root root  4096 10月  6 15:25 root>>drwxr-xr-x  23 root root   660 10月  6 17:48 run>>lrwxrwxrwx.  1 root root     8 8月  18 2017 sbin -> usr/sbin>>drwxr-xr-x.  2 root root  4096 11月  5 2016 srv>>dr-xr-xr-x  13 root root     0 9月  10 20:55 sys>>drwxrwxrwt. 13 root root  4096 10月  6 17:48 tmp>>drwxr-xr-x. 13 root root  4096 8月  18 2017 usr>>drwxr-xr-x. 19 root root  4096 9月  10 20:55 var>>temp>>test>>test2>>TestCDX.txt>>testfile>>>>```>>>>
```

##### 文件打包解压命令

###### 文件打包

```shell
tar -cvf 生成打包的文件名.tar 需要被打包的文件-c  	创建一个新的归档-v		详细的列出处理的文件-f    使用归档文件
```

```shell
将指定文件目录下的文件打包[root@izuf6essqiicvb19gkmlb9z home]# tar -cvf 打包测试.tar TestCDX.txt tempTestCDX.txttemp/[root@izuf6essqiicvb19gkmlb9z home]# lstemp  test  test2  TestCDX.txt  testfile  打包测试.tar
```

###### 文件解包

ta r -xvf 打包过的文件

-x 将打包过的文件解压

-f 选项必须放到最后面

```shell
解压到指定文件目录下  tar -xvf 需要解压的文件 -C 指定的文件路径[root@izuf6essqiicvb19gkmlb9z home]# tar -xvf 打包测试.tar -C /home/aTestCDX.txttemp/[root@izuf6essqiicvb19gkmlb9z home]# lsa  temp  test  test2  TestCDX.txt  testfile  打包测试.tar[root@izuf6essqiicvb19gkmlb9z home]# cd a[root@izuf6essqiicvb19gkmlb9z a]# lstemp  TestCDX.txt
```

##### 压缩解压命令

###### gzip命令

gzip一般和tar一起使用，完成打包压缩

ta r只负责打包并为做压缩，使用-z选项可以调用gzip完成压缩，完成打包压缩

使用ta r打包压缩的文件名，一般命名成x x x x x.tar.gz区别于其他文件

压缩文件

```shell
tar -zcvf py.tar.gz a.txt b.txt c.txt
```

解压缩文件

```shell
tar -zxvf py.tar.gz
```

解压缩到指定目录

```shell
tar -zxvf 打包文件.tar.gz -C 目标路径-C是指定哪里，目标文件必须存在
```

```shell
压缩指定的testfile和test2 [root@izuf6essqiicvb19gkmlb9z home]# tar -zcvf 打包测试压缩.tar.gz testfile test2testfiletest2/test2/.bash_logouttest2/.bashrctest2/.bash_profiletest2/.bash_history[root@izuf6essqiicvb19gkmlb9z home]# lsa  temp  test  test2  TestCDX.txt  testfile  打包测试.tar  打包测试压缩.tar.gz
```

```shell
解压缩压缩包到指定的文件tar -zxvf 需要解压的文件 -C 指定文件目录[root@izuf6essqiicvb19gkmlb9z home]# tar -zxvf 打包测试压缩.tar.gz -C /home/testtestfiletest2/test2/.bash_logouttest2/.bashrctest2/.bash_profiletest2/.bash_history
```

###### bzip命令

bzip和gzip的方式差不多，也是由tar去调用，使用-j选项

b zi p压缩的文件是x x x.tar.bz2

压缩文件

```shell
tar -jcvf py.tar.bz2 a.txt b.txt
```

解压缩文件

```shell
tar -jxvf py.tar.bz2
```

##### ubunt软件管理

软件安装

```shell
sudo apt install 软件包
```

如:安装s sh服务

```shell
sudo apt install ssh
```

软件更新

```shell
sudo apt update 软件包
```

如:更新s sh服务

```shell
sudo apt update ssh
```

软件卸载

```shell
sudo apt remove 软件包
```

如:卸载s sh服务

```shell
sudo apt remove ssh
```

##### vi m编辑器

###### 	1.命令模式

```shell
vim filename    打开或新建文件。 vim+n filename.  打开或新建文件。光标移至n行vim + filename.   打开文件，光标移至最后一行vim +/pattern filename   打开文件，并将光标置于第一个与pattern匹配的位置vim -r filename.  在上次使用vim编辑器崩溃时，恢复filenamevim filename---filename.  依次打开文件
```

​	移动光标命令

```shell
h			光标左移一个字符l			光标右移一个字符k或ctrl_p	光标上移一行j					光标下移一行w					光标右移一个字到字首b					光标左移一个字到字首o				光标移到当前行首$				光标移至当前行尾部ctrl+f	文件尾翻以屏ctrl+b	文件首翻以屏home	移动至行首end		移动至行末G			跳转至文档最末尾gg		跳转至文档首行nG    n是个数字，表示跳转至第几行
```

删除文档命令

```shell
dd			删除光标所在行d0			删除光标所在行光标前面的内容d$			删除光标所在行光标末尾的内容 3 dd		删除光标所在行包含当前行后面3行内容 yy		复制 2 yy	复制光标所在行开始2行内容 p	粘贴 删除的内容也可以粘贴 u   撤销 ctrl r.  反撤销
```

​	

###### 2.插入(编辑)模式

```shell
i    在光标前I.   在当前行首a. 光标后A    在当前行尾o		在当前行之下新开一行0   在当前行之上新开一行
```

退出编辑:wq 推出并保存	

###### 	3.末行模式

保存退出

```shell
:q			退出:q!			退出并不保存:w			保存:Wq			退出并保存:x  退出并保存
```

查找替换

```shell
/string  在文本中查找stringn 下一个N 上一个:n1,n2s /word1/word2/g   将n1行到n2行中word1替换成word2,g表示全部替换:1,$s /word1/word2/g  从第一行到最后一行寻找word1字符串，并将该字符串取代为word2:1,$s /word1/word2/gc 从第一行到最后一行寻找word1字符串，并将该字符串取代为word2!
```

```shell
v按字符移动选择文本V按行移动选择文本
```

​	

##### 补充：

```shell
yum install lrzsz    rz/sz命令安装
```

```shell
rm -rf + 文件名称		删除某个文件
```

```shell
mv apache-tomcat-8.5.20 tomcat8.5   更改名称
```

```shell
lsb_release -a  查看系统版本
```

