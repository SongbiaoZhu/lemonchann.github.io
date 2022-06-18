---
layout: post
title: "Students t-test"
date:   2022-06-18
tags: [Bioinformatics]
comments: true
author: Songbiao Zhu
---

Student's t-test 是由William Sealy Gosset 于1908年发表的统计检验方法，是我们通常所说的t-test，常用于检验样本的均值。

* 单样本时，检验样本均值是否等于某一数值；
* 双样本时，检验两个样本的均值是否相等。

Student's t-test的使用前提是
* 两个样本均来自正态总体，
* 两个样本的方差需相等（即方差齐性）。

 1. 对于第一个条件，可以用一些test来检验其正态性，比如Shapiro-Wilk test，Kolmogorov-Smirnov test，或者用Q-Q plot；
 2. 而方差齐性可通过F-test， Levene's test， Bartlett's test 等来检验。

<!-- more -->

## T-test的应用

* paired-sample：检验配对的样本之间的均值差异。比如对于同一组样本的两次测量结果之间的比较；又比如临床试验中两组年龄和性别上matched 样本。
* independent sample：表示随机的两个样本之间的均值检验。比如检验两个班的月考数学成绩。

## R语言实现t-test检验

> 函数：t.test(x, y = NULL, alternative = c("two.sided", "less", "greater"),
> mu = 0, paired = FALSE, var.equal = FALSE, conf.level = 0.95, ...)

部分参数说明：
x, y: 我们这里主要讲two-sample 检验，所以x和y两个向量都需要提供，表示两个不同的样本。
alternative: 选择时单侧检验还是双侧检验；
mu: 单样本检验的时候用的参数；
paired: 是否为配对样本检验；
var.equal: 这个参数选择是否样本方差一样，**默认是方差不一样**，这时候底层实现使用的**welch's t-test**；如果**方差一样**，选择TRUE，则底层实现使用的是**student's t-test**。

## 使用Student's t-test需要注意的地方 （t-test的缺点）：

使用t-test，还需要考虑 两个样本的大小，以及两个样本量是否相等的问题。

* paired-sample，两个样本量自然是相等的。
* independent sample 的检验：对于equal-size 的两个样本的t-test ，不管是方差齐或不齐，都能得到非常robust的结果；而unequal-size的两个样本就不能确定了。这表明**当样本量一样时，t-test对于方差并不敏感**；反之，当样本量大小不等时，使用t-test就不安全了。而当两个样本并非来自正态总体时，不管是sample-size相等或是不等，结果也都不太好。 这表明，**t-test对于正态性比较敏感**。

## 参考
[生物学研究中常见的统计检验方法(一：t-test)](https://www.jianshu.com/p/c4890fc4c2dd)