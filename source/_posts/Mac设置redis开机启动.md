---
title: Mac设置redis开机启动
tags:
  - Redis
  - MacOS
categories:
  - Redis
  - MacOS
toc: true
abbrlink: 32806
date: 2021-07-25 12:50:43
---

### 1.创建.plist配置文件

```shell
sudo vim /Library/LaunchDaemons/io.redis.redis-server.plist
```

<!--more-->

按 `i `进入编辑模式

拷贝如下内容：

```shell
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>io.redis.redis-server</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/redis-server</string>
        <string>/usr/local/redis-5.0.5/redis.conf</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
</dict>
</plist>
```

其中`redis-server`路径与`redis.conf`路径根据实际情况修改

```shell 
which redis-server   # 查看redis-server路径
```

 建议使用brew安装redis，便于管理

保存并退出：`esc`+`:+wq`

### 2.使用launchctl将配置加入launchd

```shell
sudo launchctl load /Library/LaunchDaemons/io.redis.redis-server.plist
```

此时Mac开机或重启都会自动启动redis

### 3.使用launchctl手动启动/关闭redis

启动redis

```shell
sudo launchctl start io.redis.redis-server
```

关闭redis

```shell
sudo launchctl stop io.redis.redis-server
```

可对上述命令进行简化（通过设置别名的方式）
切换到用户目录`cd`
编辑环境变量配置`vim .bash_profile`
将别名设置粘贴到配置文件

```shell
alias redisstart='sudo launchctl start io.redis.redis-server'
alias redisstop='sudo launchctl stop io.redis.redis-server'
```

退出并保存`esc` - `:` - `wq`
最后使用source命令使别名生效`source .bash_profile`，如果提示无此文件可使用下面几种方式：

```shell
source ~/.bash_profile
source ./.bash_profile
```





参考文档：https://www.jianshu.com/p/afb1b1796cc6
