# R语言之数据处理


## 数据处理

在进行数据分析之前，需要对数据进行处理，即根据需求对数据进行增，删，改，查。在R语言中基础包中，`subset(), which(), merge()`等函数进行数据处理。除此之外，dplyr包中的`filter(), inner_join()`等函数也可以实现相同的功能，，由于dplyr包接受`data.frame`对象，且运行速度很快，因此使用也十分广泛。具体示例如下。

## 1.单表操作

基础表格如下。

```R
id <- c(1, 2, 3, 4, 5, 6, 7)
age <- c(32, 18, 23, 57, 15, 22, 55)
score <- c(85, 70, 90, 77, 95, 85, 85)
df <- data.frame(
    id = id,
    age = age,
    score = score
)
```

### 1.1筛选

其中`filter()`速度最快，`subset()`速度最慢。

```R
# 基础包
df.1 <- subset(df,)
df.1 <- df[df$score > 80,]
df.1 <- df[which(df$score > 80),]

# dplyr
library(dplyr)
df.1 <- filter(df, score > 80)
# 多条件查询
df.1 <- filter(df, score > 80 & score < 90)
df.1 <- filter(df score > 80) %>% filter(socre < 90)
```

### 1.2group_by

dplyr包中的`group_by()`能够进行分组计算，在实际中也经常用到。示例代码如下。

```R
library(dplyr)
df.1 <- group_by(df, score)
df.2 <- summarize(df.1,
                  count = n(),
                  age.mean = round(mean(score),2),
                  age.min = min(age),
                  age.max = max(age),
                  age.sum = sum(age)
)
```



## 2.双表操作

基础表格如下：

```R
city <- c(beijing, shanghai, guangzhou, shenzhen )
province <- c(beijing, shanghai, guangdong, guangdong)
id <- c(1, 2, 3, 4)

df.1 <- data.frame(
    id = id;
    city = city
) 
df.2 <- data.frame(
    id = id;
    province = province
)
```

### 2.1拼接

表格的拼接可以认为是两个或多个表格的行\列合并，这里以行合并为例，常用的有两种方法，一种是R语言基础包中的`rbind()`，另一种是`dplyr`包中的`bind_rows()`，速度`rbind() > bind_rows()`，原因是`rbind()`在拼接时不检查元素每列的元素类型是否相同。示例代码如下。合并列也类似，函数为`cbind(), bind_cols()`。

在合并行的时候需要保证列数相同，在合并列的时候要保证行数相同。

```R
#方法1
rbind(df.1, df.2)
#方法2
library(dplyr)
bind_rows(df.1, df.2)
```

### 2.2交集，并集，差集

```R
library(dplyr)
# 交集
df.3 <- intersect(df.1, df.2)
#差集 df.1 - df2
df.3 <- setdiff(df.1, df.2)
#并集（去重复）
df.3 <- union(df.1, df.2)
#并集（不去重复）
df.3 <- union_all(df.1, df.2)
```

### 2.3连接（join）

常用的连接分为3种，分别是内连接、左连接，右连接。常用的方法有两种，分别是R语言基础包中的`merge()`函数与`dplyr`包中的`inner_join()`函数。速度后者略快于前者。

```R
library(dplyr)
# 内连接
df.3 <- inner_join(df.1, df.2, by = c("city" = "province"))
df.4 <- merge(df.1, df.2, by.x = "city"， by.y = "province", sort = FALSE)
# 左连接
df.3 <- left_join(df.1, df.2, by = "ID")
df.4 <- merge(df.1, df.2, by.x = "city"， by.y = "province", sort = FALSE, all.x = TRUE)
# 右连接
df.3 <- right_join(df.1, df.2, by = "ID")
df.4 <- merge(df.1, df.2, by.x = "city"， by.y = "province", sort = FALSE, all.y = TRUE)
# 全连接
df.3 <- full_join(df.1, df.2, by = c("city" = "province"))
df.4 <- merge(df.1, df.2, by.x = "city"， by.y = "province", sort = FALSE, all = TRUE)
```

### 2.4补充：dplyr中的管道函数

这里补充一个知识点dplyr中的管道函数`%>%`，意思是将`%>%`左边的对象传递给右边的函数，作为第一个选项的设置（或剩下唯一一个选项的设置）。使用管道函数能够精简代码，提高可读性。具体使用方法如下。

- `a %>% f(b)`等同于`f(a, b)`
- `b %>% f(a, ., c)`等同于`f(a, b, c)`



## 3.参考

1. https://zhuanlan.zhihu.com/p/31465569
2. https://blog.csdn.net/neweastsun/article/details/79435271
3. https://www.jianshu.com/p/c65dbce983dd
4. https://blog.csdn.net/wlt9037/article/details/74421916
