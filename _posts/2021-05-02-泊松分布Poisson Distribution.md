---
layout: post
title: "泊松分布Poisson Distribution"
date:   2021-05-02
tags: [R]
comments: true
author: Songbiao Zhu
---

## 引言

泊松分布是一个时间区间内独立事件发生的概率分布。

如果λ是每一定时间间隔平均发生的次数,那么在该时间间隔内发生x次的概率计算公式:

![poisson distribution formula](https://tse3-mm.cn.bing.net/th?id=OIP.qmfySxsxTagQmn1IikMhvQHaD0&pid=Api&rs=1)

<!-- more -->

## Problem

如果一架桥上，平均每分钟有12辆车通过，求这座桥某分钟内有17辆或更多车辆通过的概率。

## Solution

某一分钟内有16辆或更少的汽车通过这座桥的概率可以由`ppois()`函数计算得出。

```R
> ppois(q = 16, lambda=12)
[1] 0.899
```

上述概率也可以根据泊松分布的概率计算公式求得，结果数值相等，过程如下：

```R
> sum(unlist(lapply(0:16, function(x) 12^x * exp(1)^(0-12)/factorial(x))))
[1] 0.899
> 1 -  sum(unlist(lapply(0:16, function(x) 12^x * exp(1)^(0-12)/factorial(x))))
[1] 0.101
```

因此，一分钟内有17辆或17辆以上汽车通过大桥的概率是 0.101.

其实查看`help(ppois)` 可以发现，可以设置函数参数 `lower = TRUE` ，来返回一分钟内有17辆及以上车辆通过大桥的概率值。

```R
> ppois(q = 16, lambda=12, lower = FALSE)
[1] 0.101 # 注意此时依然设置q 为16，而不是17，因为已经设置了lower 的参数。
```

## Reference

* [Poisson Distribution](http://www.r-tutor.com/elementary-statistics/probability-distributions/poisson-distribution)