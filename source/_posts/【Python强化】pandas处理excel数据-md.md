---
title: 【Python强化】pandas处理excel数据.md
tags:
  - Pandas
  - Python
categories:
  - Python
  - Pandas
toc: true
abbrlink: 62546
date: 2021-11-04 03:01:05
---



### 一、安装环境

[python](https://so.csdn.net/so/search?from=pc_blog_highlight&q=python)操作excel表格文件的增删读写，一般需要用到的[第三方库](https://so.csdn.net/so/search?from=pc_blog_highlight&q=第三方库)有xlwt,xlrd。xlrd负责读取excel,xlwt负责写入excel文件。这种操作方法比较繁琐，效率还不错，通俗易懂。

Pandas是xlwt,xlrd库的封装库，拥有更全面的操作对象，csv,excel,dataframe等等。在xlwt等读写库的基础上可以实现一个库操作不同格式的文件。

`pandas`依赖处理Excel的`xlrd`模块，所以我们需要提前安装这个，安装命令是：

<!--more-->

```PYTHON 
pip install xlrd
```

### 二、读写excel

表格内容：

| number | name | age  | score | sex  |      |
| ------ | ---- | ---- | ----- | ---- | ---- |
| 1      | lhh  | 24   | 100   | 男   |      |
| 2      | wcy  | 28   | 99    | 女   |      |
| 3      | lfg  | 56   | 98    | 男   |      |
| 4      | zzy  | 52   | 97    | 女   |      |

### 1.读取文件

```python
#encoding=utf-8
import pandas as pd

# 读取文本内容
data= pd.read_excel("demo.xlsx")
print(data)
#解决数据显示不完全的问题
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
#获取指定单元格的值
one = data.iloc[3,3]
two = data.iloc[0,2]
print(one,two)
```

输出：

```shell
   number name  age  score sex
0       1  lhh   24    100   男
1       2  wcy   28     99   女
2       3  lfg   56     98   男
3       4  zzy   52     97   女
97 24
```

* **获取前几条数据**

```python
# 获取数据
data = data.head()
print(data)

# sheet_name 代表是第几个工作簿，可以用名称组成列表输入
data = pd.read_excel("demo.xlsx",sheet_name=0)
print(data)
```

输出：

```shell
   number name  age  score sex
0       1  lhh   24    100   男
1       2  wcy   28     99   女
2       3  lfg   56     98   男
3       4  zzy   52     97   女
   number name  age  score sex
0       1  lhh   24    100   男
1       2  wcy   28     99   女
2       3  lfg   56     98   男
3       4  zzy   52     97   女
```

* 获取所有的表中数据，返回一个list

```python
# 获取所有的数据，返回的是一个list
value = data.values
print(value)
```

输出：

```shell
[[1 'lhh' 24 100 '男']
 [2 'wcy' 28 99 '女']
 [3 'lfg' 56 98 '男']
 [4 'zzy' 52 97 '女']]
```

* 输出指定行的数据

```python
df = pd.read_excel("demo.xlsx")
#表示第一行,不包含表头
data = df.iloc[0].values
print(data)
```

输出：

```shell
[1 'lhh' 24 100 '男']
```

### 2.loc 和iloc详解

* `loc[row,cloumn]`  先行后列 : 是全部行或列,一般多行可以用中括号,连续的可以用a:c等
* `iloc[index,columns]` 行索引,列索引,索引都是从0开始,用法是一样的

### 3.多行多列读取

```python
# 多行输出
df = pd.read_excel("demo.xlsx")
#读取指定多行的话,就要在ix[]里面嵌套列表指定行数
data = df.loc[1:2]
print(data)
```

输出：

```python
   number name  age  score sex
1       2  wcy   28     99   女
2       3  lfg   56     98   男
```

* 读取第一行第二列的值

```python
df = pd.read_excel("demo.xlsx")
data = df.iloc[1,2]
print(data)
```

输出:

```python
28
```

* 读取第二行第三行和第3列第4列的值

```python
#读取第一行第二行的第三列和第四列的数据，这里需要嵌套列表
df = pd.read_excel("demo.xlsx")
data = df.iloc[[1,2],[2,3]].values
print(data)
```

输出:

```python
[[28 99]
 [56 98]]
```

* 读取第二行和第三行指定“score”和“age”列的数据

```python
df = pd.read_excel("demo.xlsx")
data = df.loc[[1,2],["score","age"]].values
print(data)
```

输出：

```python
[[99 28]
 [98 56]]
```

* 读取指定列的数据

```python
#读取指定列的数据
df = pd.read_excel("demo.xlsx")
data = df.loc[:,["score","age"]].values
print(data)
```

输出:

```python
[[100  24]
 [ 99  28]
 [ 98  56]
 [ 97  52]]
```

### 4.输出行号和列号

```python
#输出行号和列号
df=pd.read_excel('demo.xlsx')
print("输出行号列表",df.index.values)
print("输出列好列表",df.columns.values)
# df.sample方法类似于df.head()和df.values方法数据  这个数据选取是随机选取3行
print("输出:",df.sample(3).values)
```

输出

```shell
输出行号列表 [0 1 2 3]
输出列好列表 ['number' 'name' 'age' 'score' 'sex']
输出: [[3 'lfg' 56 98 '男']
 [4 'zzy' 52 97 '女']
 [2 'wcy' 28 99 '女']]
```

### 5.获取指定值

```python
#获取指定列的指定值
df=pd.read_excel('demo.xlsx')
print("输出值",df['score'].values)
```

输出:

```shell
输出值 [100  99  98  97]
```

* excel数据转字典

```python
#excel数据转字典
df=pd.read_excel('demo.xlsx')
test_data=[]
for i in df.index.values：
    #注意loc不要写成iloc
    row_data=df.loc[i,['number','name','score','age','sex']].to_dict()
    test_data.append(row_data)
print("输出".format(test_data))
```

输出:

```python
输出: [{'number': 1, 'name': 'lhh', 'score': 100, 'age': 24, 'sex': '男'}, {'number': 2, 'name': 'wcy', 'score': 99, 'age': 28, 'sex': '女'}, {'number': 3, 'name': 'lfg', 'score': 98, 'age': 56, 'sex': '男'}, {'number': 4, 'name': 'zzy', 'score': 97, 'age': 52, 'sex': '女'}]
```

### 6.数据清洗操作

* 去除全部带空值 的行

```python
df = pd.read_excel('demo.xlsx')
print(df)
data = df.dropna()
print(data)
```

输出:

```python
   number name   age  score   sex
0       1  lhh  24.0  100.0     男
1       2  wcy  28.0   99.0     女
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   NaN    NaN  dwdw
   number name   age  score sex
0       1  lhh  24.0  100.0   男
1       2  wcy  28.0   99.0   女
2       3  lfg  56.0   98.0   男
3       4  zzy  52.0   97.0   女
```

* 对空值进行填充

```python
#对空值进行填充
df = pd.read_excel('demo.xlsx')
print(df)
df["age"].fillna(0,inplace=True)
print(df)
```

输出:

```python
   number name   age  score   sex
0       1  lhh  24.0  100.0     男
1       2  wcy  28.0   99.0     女
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   NaN    NaN  dwdw
   number name   age  score   sex
0       1  lhh  24.0  100.0     男
1       2  wcy  28.0   99.0     女
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   0.0    NaN  dwdw
```

* 去除字符串的空格

```python
df['name'] = df['name'].map(str.strip)
print(df)
```

* 字符串大小写转换

```python
df['name'] = df['name'].map(str.lower)
print(df)
```

* 更改数据格式

```python
df['name'].fillna(0).astype("int")
```

* 更改列的名称

```python
df.rename(columns={"name":"username"},inplace=True)
print(df)
```

* 删除重复数据

```python
df['age'].drop_duplicates(inplace=True)
df['age'].drop_duplicates(inplace=True,kepp="last")
print(df)
```

* 列举前几条数据

```python
# 修改和替换
data = df.tail(3)
print(data)
```

* 打印第几行的数据

```python
# 打印第几行的数据
print(data.loc[3])
```

* 打印第几行的数据第几列的数据

```python
#打印出第八行[column_1]的列
print(data.loc[3,column_1])
```

```python
# 打印第几行的数据名为。。。的数据
print(data.loc[2:4,"name":"sex"])
```

* 统计出现的次数

```python
# 统计出现的次数  name是列的名称
data = df.name.value_counts()
print(data)
```

* 给每个列应用一个函数 apply()用法

```python
# 给每个列应用一个函数
f = lambda x : x-20
df["age"] = df["age"].apply(f)
print(df)
```

* 给每个元素应用一个函数applymap()函数

```python
# 给每个元素应用一个函数
df = pd.read_excel("dw.xlsx")
f = lambda x:x+100
df = df.applymap(f)
print(df)
```

* 遍历行和列的数据

```python
# 遍历行和列
for i,row in df.iterrows():
    print(i,row)
```

* map函数用法

```python
df["name"] = df["name"].map(lambda name:name+"wo")
print(df)
```

* 选择指定的列重新输出

```python
df = pd.read_excel("demo.xlsx")
df.loc[:,"name":"score"].to_excel("3列输出.xlsx")
```

* 添加行头

```python
df = pd.read_excel("demo.xlsx",header=None,names=["序号","姓名","年龄","分数","性别"])
df.to_excel("title.xlsx",index=False)
print(df)
```

### 7.多表合并

#### concat参数详解：

* objs(必须参数):参与连接的pandas对象的列表或字典
* axis:指明连接的轴向,默认为0
* join:选中inner或outer(默认),其它轴向上索引是按交集(inner)还是并集(outer)进行合并
* join_axes:指明用于其他N-1条轴的索引,不执行并集/交集运算
* keys:与连接对象有关的值,用于形成连接轴向上的层次化索引
* verify_integrity:是否去重
* ignore_index:是否忽略索引

```python
frames = [df1,df2,df3]
result = pd.concat(frames)
result = pd.concat(frames,keys=["x","y","z"])  #把每张表来个定义
```

```python
df = pd.read_excel("demo.xlsx")
df.iloc[2:4,:].to_excel("demo01.xlsx")
data = pd.read_excel("demo01.xlsx")
frames = [df,data]
content = pd.concat(frames,keys=["one","two"],ignore_index=True,verify_integrity=True)
print(content)
```

输出：

```python
   number name   age  score   sex  Unnamed: 0
0       1  lhh  24.0  100.0     男         NaN
1       2  wcy  28.0   99.0     女         NaN
2       3  lfg  56.0   98.0     男         NaN
3       4  zzy  52.0   97.0     女         NaN
4       5   dw   NaN    NaN  dwdw         NaN
5       3  lfg  56.0   98.0     男         2.0
6       4  zzy  52.0   97.0     女         3.0
```

`新增一行表进行连接`：

```python
# 新建一个数据按行进行合并
df2 = pd.DataFrame({"number":10,"name":"www","age":30,"score":1000},index=[1])
print(df2)
result = pd.concat([df,df2],axis=0,ignore_index=True)
print(result)
```

输出：

```python
   number name   age  score   sex
0       1  lhh  24.0  100.0     男
1       2  wcy  28.0   99.0     女
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   NaN    NaN  dwdw
   number name  age  score
1      10  www   30   1000
   number name   age   score   sex
0       1  lhh  24.0   100.0     男
1       2  wcy  28.0    99.0     女
2       3  lfg  56.0    98.0     男
3       4  zzy  52.0    97.0     女
4       5   dw   NaN     NaN  dwdw
5      10  www  30.0  1000.0   NaN
```

`新增一列数据进行连接`

```python
\#新建一列进行合并
df3 = pd.DataFrame({"index":[2,3,4,5,6]})
result = pd.concat([df,df3],axis=1)
print(result)
```

输出:

```python
   number name   age  score   sex
0       1  lhh  24.0  100.0     男
1       2  wcy  28.0   99.0     女
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   NaN    NaN  dwdw
   number name   age  score   sex  index
0       1  lhh  24.0  100.0     男      2
1       2  wcy  28.0   99.0     女      3
2       3  lfg  56.0   98.0     男      4
3       4  zzy  52.0   97.0     女      5
4       5   dw   NaN    NaN  dwdw      6
```

常见的集中用法

```python
#将df1和df4横向进行交集合并
result = pd.concat([df1,df4],axis=1,join="inner")   列是增加,行是交集`
```

```python
#按照df1的索引进行df1表和df4表的横向索引
pd.concat([df1,df4],axis=1,join_axes=[df1.index])  列是增加,行以df1为准,空的为NaN
```

```python
#通过append()方法连接表格
result = df.append(result,ignore_index=True)
print(result)
```

```python
#新增一列s1表,并且跟df进行横向合并
s1 = pd.Series(["a","a","a","a","a"],name="x")
result = pd.concat([df,s1],axis=1)
print(result)
```

输出：

```python
   number name   age  score   sex
0       1  lhh  24.0  100.0     男
1       2  wcy  28.0   99.0     女
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   NaN    NaN  dwdw
   number name   age  score   sex  x
0       1  lhh  24.0  100.0     男  a
1       2  wcy  28.0   99.0     女  a
2       3  lfg  56.0   98.0     男  a
3       4  zzy  52.0   97.0     女  a
4       5   dw   NaN    NaN  dwdw  a
```

#### 数据过滤

```python
#只显示年龄为24和28的数据
print(df)
df = df[df["age"].isin([24,28])]
print(df)
```

```python
   number name   age  score sex
0       1  lhh  24.0  100.0   男
1       2  wcy  28.0   99.0   女
```

```python
#只显示年龄除了24和28的数据
print(df)
df = df[df["age"].isin([24,28])]
print(df)
```

```python
   number name   age  score   sex
2       3  lfg  56.0   98.0     男
3       4  zzy  52.0   97.0     女
4       5   dw   NaN    NaN  dwdw
```

```python
# 删除不需要的列
result = df.iloc[:, :len(df.columns) - 1]
print(result)
```

```python
# 取出包含的数据并保存
one = result[result["age"].isin([24])]
two = result[result["age"].isin([28])]
three = result[result["age"].isin([52])]
four = result[result["age"].isin([50])]
writer = pd.ExcelWriter("数据筛选.xlsx")
result.to_excel(writer, sheet_name="all", index=False)
one.to_excel(writer, sheet_name="one", index=False)
two.to_excel(writer, sheet_name="two", index=False)
three.to_excel(writer, sheet_name="three", index=False)
four.to_excel(writer, sheet_name="four", index=False)
writer.save()
```





