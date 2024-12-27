---
title: "R语言之基础"
date: 2021-01-22T17:55:24+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["R"]
categories: ["编程语言"]

---

R语言是Ross Ihaka和Robert Gentlemanat在新西兰奥克兰大学于1996年发起的一个项目，并且由1976年贝尔实验室的S语言发展而来。目前于R语言常用于统计分析，绘图，数据挖掘。

获取R的地址：http://cran.r-project.org/，国内镜像为：https://mirrors.tuna.tsinghua.edu.cn/CRAN/。

R语言常用IDE为RStudio，下载地址为：https://rstudio.com/products/rstudio/。

## 1.基础

这里首先列举一些常用语法，之后解释了遇到的一些问题。

推荐的变量命名：`China.City`, `ThisIsAFunction`, `i`。

### 1.1基本运算

- 整除：`%/%`
- 整除取余：`%%`
- 索引：`[],$`
- 判断元素是否在向量中，返回布尔值`%in%`
- 矩阵乘法：`%*%`
- 数学函数：`exp(), log(), log10(), sqrt()`
- 取整函数：四舍五入取整`round(n)`，向上取整`ceiling(n)`，向下取整`floor(n)`。`round(n,m)`表示对n保留m位小数进行四舍五入。

常用语句如下：

```R
a <- 1
b <- "aaa"
#输出
print(a)       # 1
#拼接
paste(a, b)    # "1 aaa"
paste(a, b, collapse=",")    # "1,aaa"
paste0(a, b)   # "1aaa"
```

### 1.2常见疑惑

`<-`，`<<-`与`=`的区别

- 在大多数语言中`=`作用有两个赋值和传参，但在R语言中`<-`的作用只有赋值并且创建对象，且该箭头方向为双向（可向右赋值`->`）。如果同时存在，优先据`<-`高于`=`。由于`<-`的可读性好，故R语言中一般使用`<-`。
- `<<-`表示全局赋值，可在函数中向全局变量赋值，与`<-`类似，也可向右进行赋值



## 2.数据结构

基本常用数据类型有：数值型（numeric）、逻辑性（logical）、字符型（character）、复数型（complex）、原味型（raw）、缺省型（missing value）。

数据对象有：向量（vector）、矩阵（matrix）、数组（array）、列表（list）、数据框（data.frame）、因子（factor）。

下文是常用的代码示例：

```R
# charactor
a <- "study"
# 分割
substr(a, 1, 2)    # "st"
# 长度
nchar(a)    # 5

# vector
#常用函数：length()
x <- c(1,2,3,4,5)
x <- 1:5        # 1 2 3 4 5 与 x <- seq(1,5) 等价
x <- rep(1, 5)  # 1 1 1 1 1
x <- seq(1, 10, 2)    # 1 3 5 7 9

# list 列表
# 创建一个列表，包含了字符串、向量和数字
list_data <- list("runoob", "google", c(11,22,33), 123, 51.23, 119.1)
# 给列表元素设置名字
names(list_data) <- c("Sites", "Numbers", "Lists")

# matrix
#常用函数：行数与列数dim(), 逆矩阵solve(), 转置矩阵t()
M <- matrix(c(3:14), nrow = 4, byrow = TRUE)  #元素按行排列
N <- matrix(c(3:14), nrow = 4, byrow = FALSE) #元素按列排列
P <- matrix(c(3:14), nrow = 4, byrow = TRUE, dimnames = list(rownames, colnames))  # dimnames可以定义列名与行名

# array, matrix其实就是一个二维数组
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)
# 创建3行3列的2维数组
result <- array(c(vector1,vector2),dim = c(3,3,2), dimnames = list(row.names,column.names,matrix.names))

# data.frame (初始化，v1与v2为其中的列)
df <- data.frame{
    col1 = v1,
    col2 = v2
}
#选取第一列
df[1,]
#选取第一行
df[,1]
```



## 3.基本语法

R语言与Python不同，需要通过`{}`来进行代码块的分割，在R语言中`next`类似与其他语言中的`continue`。

代码示例如下：

```R
# switch 
# expression是一个常量表达式，可以是整数或字符串，如果是整数则返回对应的 case 位置值，如果整数不在位置的范围内则返回 NULL
# 如果是字符串，则对应的是 case 中的变量名对应的值，没有匹配则没有返回值。
# 如果匹配到多个值则返回第一个。
switch(
    expression, 
    case1, 
    case2, 
    case3....)

#循环
for (i in 1:10) {
  print(i)
}

#函数
function_name <- function(arg.1, arg.2, ...) {
    expressions;
}
```



## 4.高效原则

随着数据的海量增加，对于数据的处理效率能够市数据。在编程过程中通过一些简单技巧，就可以使程序的执行效率有显著的提高，

1. R语言能够直接对向量进行运算，所以尽量避免使用`for`循环，可以通过`apply(), foreach()`来等价替换。
2. 在使用向量时最高能够提前分配好大小，而不是动态添加。
4. 使用R语言中并行包`parallel, foreach, doParallel`来处理数据。
5. 通过 `rm()` 将对象从内存中及时释放。



## 5.参考

1. https://zh.wikipedia.org/wiki/R%E8%AF%AD%E8%A8%80
2. https://zhuanlan.zhihu.com/p/27339301
3. https://www.runoob.com/r/r-tutorial.html