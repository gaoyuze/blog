---
title: "NumPy常见代码"
date: 2025-03-22T16:00:40+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["Python"]
categories: ["编程语言"]
---

numpy是Python中常用的科学计算和数据处理的最常用的库之一，本文梳理了常用的代码。

## 1.基础配置

```python
# 包引入
import numpy as np
# 设置随机种子
np.random.seed(42)
```

## 2.数组创建

```python
# 直接创建
ar = np.array([1, 2, 3])
ar = np.array([[1, 2, 3], [4, 5, 6]])

# 随机创建数组指定大小
ar = np.random.random(10) # 范围0-1, 指定大小：将10替换为（w,h）
ar = np.random.uniform(low, high, (2,3))  # 均匀分布
ar = np.random.randn((2, 3)) # 生成标准正态分布随机数
ar = np.random.randint(low, high, (2, 3))  # 整数，范围区间为[low,high)

# 创建全为0的数组
ar = np.zeros((2, 5))
# 创建全为1的数组
ar = np.ones((2, 5))
# 创建单位矩阵
ar = np.eye(10)

# 指定数组元素类型
ar = np.array(np.random.rand(224,224,3)*255, dtype=np.uint8)
```

## 3.数组属性

```python
# 数组维度
ar.ndim
# 数组维度形状
ar.shape
# 数组元素个数
ar.size
# 数据元素类型
ar.dtype

```

## 4.数组操作

```python
# 数组转置
ar2 = ar1.T
# 改变数组形状 ar1 = np.ones(10)
ar2 = ar1.reshape(5, 2)
# 数组拉平成1维
ar2 = ar1.flatten()
# 合并数组
ar3 = np.append(ar1, ar2, axis=0) # axis = 0 按行合并 axis = 1 按列合并
# 交换维度 将维度从[w,h,c] 换为 [c,w,h] 数字为维度重新排列
img_np = np.transpose(img_np, (2, 0, 1)) 
# 转变数据类型
ar2 = ar1.astype(np.float32)

a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])
# 列拼接
# [[1 2 5 6]
# [3 4 7 8]]
result = np.hstack((a, b))
# 行拼接
#[[1 2]
# [3 4]
# [5 6]
# [7 8]]
result = np.vstack((a, b))


# 数组比较，比较有NaN的两个数组是否完全一样， 由于 np.nan == np.nan 会返回 False，需要用array_equal方法
np.array_equal(a, b, equal_nan=True)
```



## 5.数组计算

```python
# 对应元素相乘
ar3 = np.multiply(ar1, ar2)
# 点积运算
ar3 = np.dot(ar1,ar2)
ar3 = ar1 @ ar2\
# 其他数学运算
ar2 = exp(ar1)
ar2 = sqrt(ar1)
ar2 = log(ar1)


```

## 6.数组统计与排序

```python
# 常见统计 ，可接axis参数，axis = 0 每一列 axis = 1 每一行
np.mean(ar1)
np.var(ar1)
np.std(ar1)
np.sum(ar1)
np.max(ar1)
# 数组展平（一维）后，最大值的索引位置，想得到具体位置 np.unravel_index(np.argmax(ar1), ar1.shape)
np.argmin(ar1)
# 每列最大值的索引
np.argmax(ar1, axis=0)
# 每行最大值的索引
np.argmax(ar1, axis=1) 

# 排序
# 每一行排序
np.sort(ar1, axis=1)
# 返回排序后索引
np.argsort(ar1)
# 去重， 返回1维数组
np.unique(ar1)
# 统计每个唯一值出现次数， 两个数组，第一个是元素，第二个是个数
np.unique(ar1, return_counts=True)
```

## 6.条件筛选

```python
# 筛选元素大于x的元素， 变成1维数组
ar1[ar1 > x]
# 是否存在大于x的元素
np.any(ar1 > x)
# 是否全部大于0
np.all(ar1 > x)
# 偶数变1，奇数变0
np.where(a % 2 == 0, 1, 0)  

```

## 7.类型转换

```python
# dataframe 互相转换
df = pd.DataFrame(arr, columns=['A', 'B', 'C'])
arr = df.to_numpy()
# tensor 互相转换, 转换后 tensor 与 NumPy 共享内存，更改其中一个会影响另一个！
tensor = torch.from_numpy(arr)
# cpu中的tensor
arr = tensor.numpy()
# gpu中的tensor
arr = tensor.cpu().numpy()
```



