---
layout: post
title: "read_data_with_switch_R"
date:   2022-04-19
tags: [R]
comments: true
 
author: Songbiao Zhu
---

当不确定import的数据文件的类型时，如何自动根据文件的扩展名，调用自动的import data函数呢？使用`switch`函数。

<!-- more -->

## switch的使用

I write the user defined function for read data with different file extensions.
```R
read_data <- function(file) {
  library("tools")
  ext <-  file_ext(file)
  switch(
    ext,
    txt = read.delim(
      file = file,
      header = TRUE,
      sep = "\t",
      stringsAsFactors = FALSE
    ),
    csv = read.csv(
      file = file,
      header = TRUE,
      sep = ",",
      stringsAsFactors = FALSE
    )
  )
  
}

```
## Acknowledgement

* [How to Get Extension of a File in R](https://r-lang.com/how-to-get-extension-of-a-file-in-r/#:~:text=How%20to%20Get%20Extension%20of%20a%20File%20in,method%2C%20you%20need%20to%20import%20the%20tools%20library.)