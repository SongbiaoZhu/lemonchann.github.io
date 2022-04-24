---
layout: post
title: "R Not use write.csv function for writing Description column with comma"
date:   2022-04-24
tags: [R]
comments: true
author: Songbiao Zhu
---

因为蛋白质组学的数据，一般包含Description column， Description column的内容，是包含逗号的，所以一定要注意，再写出包含Description的数据时，不能使用`write.csv`函数，否则虽然不报错，但是写出的数据是错误的。并且会导致下游的基于这一步骤写出的数据的分析报错。

<!-- more -->

## Not use `write.csv()`函数导出含有逗号列的数据表

举例子，包含Description的列的数据如下：

![含有逗号列](https://raw.githubusercontent.com/SongbiaoZhu/picBed/main/%E5%90%AB%E9%80%97%E5%8F%B7%E7%9A%84%E7%A4%BA%E4%BE%8B%E6%95%B0%E6%8D%AE.png)

如上所示的数据，如果使用`write.scv()`函数，写出的表格会多出来一些列。遇到莫名多出来一些列的情况时，要分析是不是export data时用错了分隔符。