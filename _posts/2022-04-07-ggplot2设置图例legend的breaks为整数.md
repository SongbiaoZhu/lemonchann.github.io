---
layout: post
title: "ggplot2设置图例legend的breaks为整数"
date:   2022-04-07
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

在用ggplot绘制，KEGG富集结果的bubble plot时，以每个KEGG通路中，包含的list 中的基因数目来表示bubble的大小，但是默认的语法出来的结果，在gene number比较小的时候，比如区间是[1, 3]时，size 图例中就会出现小数。但基因数目不可能是小数，所以需要解决这个问题。
解决办法是，在`scale_size_continuous()` 中，在 `breaks` 函数中使用 `round` 函数。

<!-- more -->

## 解决办法

在`scale_size_continuous()` 中，在 `breaks` 函数中使用 `round` 函数。

下图是我的，对富集结果列表中的上调蛋白 和下调蛋白的基因列表分别进行作图的代码：

```R
# KEGG bubble plot

invisible(
  lapply(seq_along(enrichKEGG_res_sig), function(x)
    enrichKEGG_res_sig[[x]] %>%
      dplyr::mutate(across(
        .cols = starts_with("num"),
        .fns = as.numeric
      )) %>%
      dplyr::mutate(gene_ratio = num_in_KEGG / num_in_list) %>%
      ggplot(aes(x = gene_ratio,
                 y = Description)) +
      geom_point(aes(
        size = num_in_KEGG, color = -1 * log10(qvalue)
      )) +
      scale_size_continuous(name = "Gene number",
                            breaks = round) +
      scale_color_gradient(
        name = expression(paste("\u2013 Log " * italic("P"))),
        low = "blue",
        high = "red"
      ) +
      labs(x = "Gene ratio",
           y = NULL) +
      theme_bw() +
      ggsave(
        filename = file.path(res_dir,
                             paste0(
                               names(enrichKEGG_res_sig)[x], "_KEGG_bubble.jpeg"
                             )),
        width = 15,
        height = 10,
        units = "cm"
      ))
)
```



## 致谢

* [ggplot2 geom_count set legend breaks to integers](https://stackoverflow.com/questions/45921746/ggplot2-geom-count-set-legend-breaks-to-integers)