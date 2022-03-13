---
title: mysql 优化浅析
tags:
  - MySQL
categories:
  - MySQL
toc: false
abbrlink: 45590
date: 2021-07-25 13:14:12
---

数据库优化从4个方向去优化
1、sql和索引，写出健壮的sql，索引不是越多越好
2、数据表结构（存储引擎，字段大小，字段类型，索引，第三规范）
3、系统配置（打开文件系统次数，文件安全性）
4、硬件（更合适的cup,更大的内存，更快的io，cup并不是越大越好）

<!--more-->

> show variables like 'slow_query_log'  查询慢查询日志
> set globel slow_query_log_file = '/home/mysql/sql_log/mysql-slow.log'  设置慢查询日志的路径
> set global log_queries_not_using_indexes = on;    设置慢查询日志是否记录未添加索引的字段
> set global long_query_time = 1    设置记录慢查询日志时间
> mysqldumpslow -t 3 url | more



