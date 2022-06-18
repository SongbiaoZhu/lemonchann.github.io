---
layout: post
title: "Multiple t test with dplyr"
date:   2022-06-18
tags: [R]
comments: true
author: Songbiao Zhu
---

对于蛋白组学数据集，经常需要对所有的蛋白，使用实验分组变量，进行多重的t test。
本文介绍通过dplyr来实现的方法。

<!-- more -->

主要就是通过将一组数据，以list 的形式存储在某一列中，就可以对list 的数据进行t test.
下面参考的这篇文章代码，我已经改写后在我的代码中work了。

## 参考

[Multiple t-Tests with dplyr](https://sebastiansauer.github.io/multiple-t-tests-with-dplyr/)