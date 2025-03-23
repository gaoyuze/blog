---
title: "Pandas常见代码"
date: 2025-03-23T12:53:41+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["Python"]
categories: ["编程语言"]
---

pandas是一个基于Python的开源数据分析库，本文介绍其常用的代码。

## 1.引入包

```python
import pandas as pd
```

## 2.dataframe 初始化与加载数据

```python
# 初始化
df = pd.DataFrame() # 空dataframe
# 最基础
data = {
    'name': ['Alice', 'Bob', 'Charlie'],
    'age': [25, 30, 35]
}
df = pd.DataFrame(data)
# 只指定列名
df = pd.DataFrame(columns=['A', 'B'])

# 加载/保存数据
df = pd.read_csv('data.csv')
df = pd.read_excel('data.xlsx') # 可加参数指定列类型 dtype={'col1': str}
df.to_csv('data.csv', index = False) # index 是否保存行名，默认为True
df.to_excel('data.xlsx', index = False)
```

## 3.dataframe 属性

```python
df.head(8) 	       # 查看前10行
df.tail()          # 查看后5行
df.sample(5)       # 随机抽样5行
df.shape           # 查看数据形状 (行数, 列数)
df.columns         # 查看所有列名
df.info()          # 查看数据类型、缺失值等信息
df.describe()      # 快速统计汇总
```

## 4.dataframe 选择数据

```python
df['col']                  # 选择某一列
df[['col1', 'col2']]       # 选择多列

# iloc表示index选择，loc表示标签名称选择 
df.loc[0]                  # 按名称选取第0行
df.iloc[0]                 # 按index选取第0行
df.loc[0, 'col']           # 指定行列选择
df.iloc[0:5, 1:3]          # 选择第0到4行、第1到2列
df.iloc[1, 2]			  # 指定数据点
df.iloc[[0, 2], [1, 2]]    # 指定多个数据点
```

## 5.dataframe 过滤筛选

```python
df[df['col'] > 10]                      # 条件筛选
df[(df['a'] > 5) & (df['b'] < 3)]       # 多条件筛选
df[df['col'].isin([1, 2, 3])]           # 筛选多个值
df[df['col'].str.contains('abc')]       # 字符串匹配
```



## 6.dataframe 操作

```python
# 给行末尾添加一行数据
df = pd.DataFrame(columns=['name', 'age'])
df.iloc[len(df)] = ['Alice', 25]

# 列操作，复杂可使用apply函数
df['new_col'] = df['a'] + df['b']     # 新增列
df.drop('col', axis=1, inplace=True)  # 删除列

# 重命名行列 inplace=True 表示在本dataframe中操作
df.rename(columns={'old': 'new'}, inplace=True)  # 重命名列
df.reset_index(drop=True, inplace=True)          # 重置索引

# 处理缺失值
df.isnull().sum()             # 查看缺失值数量
df.dropna()                   # 删除含缺失值的行
df.fillna(0)                  # 用0填充缺失值
df['col'].fillna(df['col'].mean())  # 用均值填充

# 分组与聚合
df.groupby('col').mean().reset_index()                           # 按列分组求均值
# 多列分组多指标聚合
df.groupby(['col1', 'col2']).agg(
    new_col1 = ('col3', 'size'), 
    new_col2 = ('col3', 'nunique')).reset_index()

# 排序， 参数可以为list分别指定，默认升序
df.sort_values('col')               # 按某列升序排序
df.sort_values('col', ascending=False)  # 降序
```

## 7.dataframe 合并与拼接

```python
# 拼接，可多个共同合并
pd.concat([df1, df2], axis=0)         # 纵向行拼接
pd.concat([df1, df2], axis=1)         # 横向列拼接

# 合并 left_on, right_on 表示匹配key名称，多个可以都是list how表示匹配方式 有inner，outer，left，right
pd.merge(df1, df2, left_on='col1', right_on = 'col2', how = 'left')
```

## 8.dataframe转换

```python
# df 转 np
arr1 = df.values
arr1 = df.to_numpy() # 推荐使用，更安全
# np 转 df
df = pd.DataFrame(arr, columns=['X', 'Y'])

# 一维 list
df = pd.DataFrame(data, columns=['col1'])
# 二维 list 每个元素代表一行
data = [[1, 'Alice'], [2, 'Bob'], [3, 'Charlie']]
df = pd.DataFrame(data, columns=['id', 'name'])

# 列表字典， 每个元素是个字典
data = [
    {'id': 1, 'name': 'Alice'},
    {'id': 2, 'name': 'Bob'},
    {'id': 3, 'name': 'Charlie'}
]
df = pd.DataFrame(data)

# 字典key和value作为两列
df = pd.DataFrame(list(d.items()), columns=['key', 'value'])
d = dict(zip(df['key'], df['value']))
```
