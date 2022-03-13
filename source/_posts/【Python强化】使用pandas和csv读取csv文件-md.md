---
title: 【Python强化】使用pandas和csv读取csv文件.md
tags:
  - Python
  - Pandas
categories:
  - Python
  - Pandas
toc: true
abbrlink: 15248
date: 2021-11-03 20:57:18
---





### 一、pandas读取方式

#### 1、csv介绍

csv文件是一种以逗号分割字符的文件形式

我们创建一个简单的文件demo.csv，如下格式的形式进行存储，以，进行分割

<!--more-->

```python
name,score,age,sex
lhh,100,24,男
wcy,99,28,女
```

#### 2.读文件

* 直接读取

```python
import pandas as pd
# 读取csv文件  全文件读取
data = pd.read_csv('demo.csv',encoding="gbk")  # 中文显示需要指定编码格式
df = pd.DataFrame(data)   # 当然这一步也可以不要，因为读出来的结果就是这种格式的，但是习惯性的写上这种方式
print(df)
```

输出：

```she
  name  score  age sex
0  lhh    100   24   男
1  wcy     99   28   女
```

* 按行读取

```python
# 读取csv文件，一行一行的进行读取
file = pd.read_csv('demo.csv',encoding="gbk")
df = pd.DataFrame(file)

for i in range(len(df)):
    row  = df[i:i+1]
    print(row ,'\n')
```

输出：

```shell
  name  score  age sex
0  lhh    100   24   男 

  name  score  age sex
1  wcy     99   28   女
```

* 获取文本标题中的每个值

```python
# row
print("获取row 中的每个值")
for i in range(len(df)):
    row  = df[i:i+1]
    name = row ['name'][i]
    score = row ['score'][i]
    print(name,score,'\n')
```

#### 3.写入csv

```python
# 写  使用pd将数据写入到csv文件当中，按列写入
file = pd.read_csv('demo.csv',encoding="gbk")
df = pd.DataFrame(file)

dict = {}

for i in range(len(df)):
    row = df[i:i + 1]
    name = row['name'][i]
    sex = row['sex'][i]
    dict[name] = sex

new_df = pd.DataFrame.from_dict(dict,orient='index')
new_df.to_csv('demo_new.csv')
```

文件内容：

```shell
,0
lhh,男
wcy,女
```

### 二、csv读取方式

#### 1.读取操作

```python
#encoding=utf-8
import csv


# 读取csv文件
with open("demo.csv","r",encoding="gbk") as csvfile:
    spamreader = csv.reader(csvfile)
    for row in spamreader:
        print(row)
```

输出：

```shell
['name', 'score', 'age', 'sex']
['lhh', '100', '24', '男']
['wcy', '99', '28', '女']
```

#### 2.以字典形式进行读取

```python
# 以字典的形式读取
with open("demo.csv","r",encoding="gbk") as file:
    reader = csv.DictReader(file)
    items = list(reader)
    print(items)
```

输出

```shell
[{'name': 'lhh', 'score': '100', 'age': '24', 'sex': '男'}, {'name': 'wcy', 'score': '99', 'age': '28', 'sex': '女'}]
```

```python
#指定列读取
filename = ['name','sex']
with open("demo.csv","r",encoding="gbk") as file:
    reader = csv.DictReader(file,filename)
    items = list(reader)
    print(items)
```

输出：

```python
[{'name': 'name', 'sex': 'score', None: ['age', 'sex']}, {'name': 'lhh', 'sex': '100', None: ['24', '男']}, {'name': 'wcy', 'sex': '99', None: ['28', '女']}]
```

#### 3.写入操作

```python
# 写入csv文件
with open("demo_new_csv.csv","w") as file:
    writer = csv.writer(file)
    writer.writerow(['name','score'])  # 此时的标题需要以list形式写入，writer会在新建的csv文件中，一行一行写入
```

文本内容

```python
name,score
```

以字典方式写入

```python
with open('demo_new_csv.csv', 'w',newline="",encoding="gbk") as f:
    writer = csv.DictWriter(f,fieldnames=["name","score","age","sex"])
    writer.writeheader()
    writer.writerows(items)
    writer.writerow({'name': 'lhh', 'score': '100', 'age': '24', 'sex': '男'})
```

文本内容

```python
name,score,age,sex
lhh,100,24,男
wcy,99,28,女
lhh,100,24,男
```

