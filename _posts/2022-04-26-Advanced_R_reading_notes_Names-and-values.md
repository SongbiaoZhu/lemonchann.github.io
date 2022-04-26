---
layout: post
title: "Advanced R reading notes: 2-Names and values"
date:   2022-04-26
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

R语言集大成者， Hadley Wicklem的 [Advanced-R](https://adv-r.hadley.nz/introduction.html)读书笔记。阅读这本书的过程中，还会参考这本书的练习题的答案书，[Advanced-R-Solutions](https://advanced-r-solutions.rbind.io/names-and-values.html).

<!-- more -->

## 绑定的基础知识（Binding basics ）

当你创建一个对象并对该对象进行命名时，其实是首先创建一个包含数值的对象，然后将这个对象绑定到一个名字上。
换句话说，对象或值没有名称;实际上是，名称有值。

## 不符合语法规则的名称（Non-syntactic names）

有三个主要的机制来转换不符合语法规则的名称，可以 `?make.names`函数。

1. 不以字母或者一个点开头的名字，开头会强制加上 `"X"`.

    ```
    make.names("")    # prepending "x"
    #> [1] "X"
    ```

以一个点开头但是后面紧跟数字的名字，开头也会强制加上 `"X"`.

```
make.names(".1")  # prepending "X"
#> [1] "X.1"
```

2. 对于名称中不符合语法规则的字符，将自动用点代替.（non-valid characters are replaced by a dot.）

```
make.names("non-valid")  # "." replacement
#> [1] "non.valid"
make.names("@")          # prepending "X" + "." replacement 
#> [1] "X."
make.names("  R")        # prepending "X" + ".." replacement
#> [1] "X..R"
```

3. 名称中R语言保留字将会加上一个点后缀（Reserved R keywords (see `?reserved`) are suffixed by a dot.）

```
make.names("if")  # "." suffix
#> [1] "if."
```

## 修改对象时才会复制对象（Copy-on-modify）
```R
x <- c(1, 2, 3)
y <- x

y[[3]] <- 4
x
#> [1] 1 2 3
```
修改y显然不会修改x。那么共享绑定发生了什么?当与y关联的值发生变化时，原始对象没有发生变化。相反，R创建了一个新对象0xcd2，它是0x74b的副本，只更改了一个值，然后将y重新绑定到该新的对象。

![copy-on-modify](https://raw.githubusercontent.com/SongbiaoZhu/picBed/main/copy-on-modify.png)

## 数据框（Data frames）

数据框是向量的列表，因此在修改数据框时，修改即复制具有重要的后果。

* 如果你修改了一列，只需要修改那一列;其他的仍然指向它们原来的引用:
* 但是，如果修改一行，则每一列都会被修改，这意味着每一列都必须被复制:

## 字符串（Character vectors）

```R
x <- c("a", "a", "abc", "d")
```

R实际上使用了一个全局字符串池，其中字符向量的每个元素都是指向池中唯一字符串的指针.

![global-string-pool](https://raw.githubusercontent.com/SongbiaoZhu/picBed/main/global-string-pool.png)

##  就地修改（Modify-in-place）

正如我们上面看到的，修改R对象通常会创建一个副本。有两个例外:

* 如果一个对象只绑定了一个名字，R会就地修改它。

* 环境(一种特殊类型的对象)总是就地修改。因为在修改环境时，对该环境的所有现有绑定将继续具有相同的引用。