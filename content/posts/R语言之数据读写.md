---
title: "R语言之数据读写"
date: 2021-01-24T12:22:05+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["R"]
categories: ["编程语言"]
---

## 1.读数据

R语言的读写有`read.csv(), read.table(), fread()`。经过测试读写速度为`fread() > read.table() > read.csv()`。`fread()`速度快的原因是其在底层使用多核并行读取。

代码示例如下：

```R
# read.csv
mydata <- read.csv("data.csv", header = T, stringsAsFactors = FALSE, check.names = FALSE) 

# read.table
mydata <- read.table("data.csv", header = T, sep=",", quote="\"", skipNul=TRUE, 
                      stringsAsFactors=FALSE, comment.char="")

# fread
# select表示要读取的列的向量，可以是下标，也可以是列名
library(data.table)
mydata <- fread("data.csv", header = TRUE, select=c(1, 2, 3))
```

可以通过文件指针来对超大文件进行分批读取

```R
con = file("data.csv", "w")
# 读取列名
col.name <- read.table(con, header = FALSE, sep=",", quote="\"", skipNul=TRUE, 
                       stringsAsFactors=FALSE, nrows = 1)
# 分10次读取，每次读取1000000行
for i in range(10) {
    df <- read.csv(con, header = FALSE, sep=",", quote="\"", skipNul=TRUE, stringsAsFactors=FALSE, 
                   comment.char="", nrows = num)
    if(nrow(df) == 0) {
    break
  }
}
close(con)
```

读数据函数中的各项含义为：

- header：第一行是否为列名
- sep：数据的分隔符。默认情况为“`""`。
- quote：用于指定包围字符型数据的字符。
- nrows：从文件中读取的最大行数。
- skip：读取数据时忽略的行数。
- encoding：字符串的编码方式
- stringsAsFactors：是否将字符向量转换为因子。
- comment.char：逻辑值。该参数值设置为TRUE时，数据框中的变量名将会被检查。
- check.names：逻辑值。该参数值设置为TRUE时，数据框中的变量名将会被检查。
- skipNul：是否忽略空值，默认为FALSE。



## 2.写数据

RDS文件是以R本机格式存储R对象，相比于其他格式文件，二进制更紧凑，读写速度快。也可以将多个对象以 RData 格式保存到一个单一的文件。其读写如下：

```R
# RDS文件的读取与写入
df <- reasRDS(“data.rds”)
# RDS 格式中写入单个数据对象
saveRDS(df,filename)

# RData文件保存与载入
# 将多个对象以 RData 格式保存到一个单一的文件
df1 <- df 
save(df, df1, file="data.RData")
# load() 载入数据，R 会自动使用该数据原来的对象名称，在本例中，会自动载入df与df1
load("data.RData")
```

除此之外，还可以将文件写如为`csv, txt`等格式，这里以写入`csv`格式为例，进行示范。

```R
# row.names = FALSE 不显示行名
# na = "" 替代 “NA”，输出空格
write.csv(data, "data.csv", row.names = FALSE, na = "")
```



## 3.参考

1. https://openbiox.github.io/Cookbook-for-R-Chinese/section-5.html