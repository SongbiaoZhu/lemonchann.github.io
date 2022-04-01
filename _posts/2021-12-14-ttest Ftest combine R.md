---
layout: post
title: "ttest Ftest combine R"
date:   2021-12-14
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

常规进行t test检验时，需要首先进行方差齐性的F test检验，根据检验结果，确定t test检验时所使用的参数，对应地设置方差齐性，或者方差非齐性。 那么在R语言中如何实现一个函数，综合这两个检验呢？

<!-- more -->

## Introduction

定义一个`super.t`函数，先做`F test`，然后再根据F test 的 p value结果，再进行做 `t test`。

## Code

```R
super.t <- function(form, data, level = 0.05) {
  vareq <- var.test(form, data)[["p.value"]] >= level
  t.test(form, data, var.equal = vareq)
}

ds <-
  structure(
    list(
      Gender = structure(
        c(2L, 2L, 2L, 2L, 2L, 2L, 1L,
          1L, 1L, 1L, 1L, 1L),
        .Label = c("F", "M"),
        class = "factor"
      ),
      Ratings = c(4L, 1L, 3L, 4L, 5L, 5L, 5L, 3L, 1L, 5L, 4L, 5L)
    ),
    .Names = c("Gender", "Ratings"),
    class = "data.frame",
    row.names = c(NA,-12L)
  )

print(ds)
# output
   Gender Ratings
1       M       4
2       M       1
3       M       3
4       M       4
5       M       5
6       M       5
7       F       5
8       F       3
9       F       1
10      F       5
11      F       4
12      F       5

typeof(ds)
# output
# list

# And then call it like:
super.t(Ratings ~ Gender, ds)

# output
	Two Sample t-test

data:  Ratings by Gender
t = 0.1857, df = 10, p-value = 0.8564
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -1.833149  2.166482
sample estimates:
mean in group F mean in group M 
       3.833333        3.666667 
```

## Reference

[Combine t.test and var.test into a function in R](https://stackoverflow.com/questions/26353279/combine-t-test-and-var-test-into-a-function-in-r)