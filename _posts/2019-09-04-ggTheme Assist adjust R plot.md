---
layout: post
title: "ggTheme Assist adjust R plot.md"
date:  2019-09-04
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

R语言中的ggplot2是最美的绘图包之一。但调整主题的细节，需要写大量代码，而且反复修改、预览，费时费力。当然你可以用Adobe Illustrator等工具进行后期编辑，但要是图重画，所有后期编辑的工作又要重来，无法实现可重复分析，每个修改都很崩溃。有没有更方便的方式调整主题细节呢？

<!-- more -->
## Introduction
ggThemeAssist横空出事，它依赖shiny  (>= 0.13), miniUI (>= 0.1.1), rstudioapi (>= 0.5), ggplot2,  formatR，可以对ggplot2图形结果直接修改，并实时预览效果，同时编辑结束返回代码。相当于一个帮你写代码的翻译官！

## Code
```R
rm(list = ls())
options(stringsAsFactors = F)
# install.packages("ggThemeAssist")
library(ggplot2)
library(ggThemeAssist)
# 使用mtcars生成一个点图示例
gg <- ggplot(mtcars, aes(x = hp, y = mpg, colour = as.factor(cyl))) + geom_point()
# 开始调整主题
#ggThemeAssistGadget(gg)
gg <- gg + theme(plot.subtitle = element_text(vjust = 1), 
    plot.caption = element_text(vjust = 1), 
    axis.line = element_line(size = 0.5, 
        linetype = "solid"), axis.title = element_text(face = "bold"), 
    axis.text = element_text(family = "sans", 
        size = 11, face = "bold"), legend.text = element_text(size = 11, 
        face = "bold"), legend.title = element_text(size = 11, 
        face = "bold"), panel.background = element_rect(fill = NA, 
        size = 0.8), plot.background = element_rect(colour = NA), 
    legend.key = element_rect(fill = "white"), 
    legend.background = element_rect(fill = NA))
ggsave('test.jpeg')

```

