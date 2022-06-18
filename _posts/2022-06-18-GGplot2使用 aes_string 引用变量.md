---
layout: post
title: "GGplot2使用 aes_string 引用变量"
date:   2022-06-18
tags: [R]
comments: true
author: Songbiao Zhu
---
## 引言

ggplot的绘图代码中，`aes()`函数中映射数据的时候，是直接写名字。但是当需要对多个变量进行循环绘图的时候，就需要使用`aes_string()` 函数了。

推荐参考链接中的文章，我已经实践work。

## 参考

[GGplot2 - 参数化与aes_string](https://n3xtchen.github.io/n3xtchen/r/2016/12/12/r-ggplot-aes_string)