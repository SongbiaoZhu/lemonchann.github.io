---
layout: post
title: "Regrex extract citation information in Sublime"
date:   2021-12-01
tags: [regrex]
toc: true
comments: true
author: Songbiao Zhu
---

从pubmed中下载的一堆引文列表中，如何提取出题目、年份、杂志的信息，然后将这三个信息显示在PPT文献中， 展示文献调研结果呢？可以通过使用正则表达式，在sublime text软件中即可完成。

<!-- more -->

引文列表如下：

```
[1] Arumilli M, Layer R M, Hytönen M K, et al.webGQT: A Shiny Server for Genotype Query Tools for Model-Based Variant Filtering[J].Front Genet,2020, 11: 152.
[2] Cenek L, Klindziuk L, Lopez C, et al.CIRCADA: Shiny Apps for Exploration of Experimental and Synthetic Circadian Time Series with an Educational Emphasis[J].J Biol Rhythms,2020, 35 (2): 214-222.
[3] Di Filippo L, Righelli D, Gagliardi M, et al.HiCeekR: A Novel Shiny App for Hi-C Data Analysis[J].Front Genet,2019, 10: 1079.
[4] Epifania O M, Anselmi P, Robusto E.DscoreApp: A Shiny Web Application for the Computation of the Implicit Association Test D-Score[J].Front Psychol,2019, 10: 2938.
[5] Gong T, Hayes V M, Chan E K F.Shiny-SoSV: A web-based performance calculator for somatic structural variant detection[J].PLoS One,2020, 15 (8): e0238108.
[6] Kaufman A R.Implementing novel, flexible, and powerful survey designs in R Shiny[J].PLoS One,2020, 15 (4): e0232424.
[7] Kim J, Yoon S, Nam D.netGO: R-Shiny package for network-integrated pathway enrichment analysis[J].Bioinformatics,2020, 36 (10): 3283-3285.
[8] Kraus M, Mathew Stephen M, Schapranow M P.Eatomics: Shiny Exploration of Quantitative Proteomics Data[J].J Proteome Res,2021, 20 (1): 1070-1078.
[9] Malagoli Tagliazucchi G, Taccioli C.GMIEC: a shiny application for the identification of gene-targeted drugs for precision medicine[J].BMC Genomics,2020, 21 (1): 619.
[10] Mullan K, Bramberger L, Munday P, et al.ggVolcanoR: A Shiny app for customizable visualization of differential expression datasets[J].Computational and Structural Biotechnology Journal,2021, 19: 5735-5740.
[11] Okour M.DosePredict: A Shiny Application for Generalized Pharmacokinetics-Based Dose Predictions[J].J Clin Pharmacol,2020, 60 (11): 1502-1508.
[12] Reyes A L P, Silva T C, Coetzee S G, et al.GENAVi: a shiny web application for gene expression normalization, analysis and visualization[J].BMC genomics,2019, 20 (1): 745-745.
[13] Ruppert C, Kaiser L, Jacob L J, et al.Duplex Shiny app quantification of the sepsis biomarkers C-reactive protein and interleukin-6 in a fast quantum dot labeled lateral flow assay[J].J Nanobiotechnology,2020, 18 (1): 130.
[14] Serra A, Saarimäki L A, Fratello M, et al.BMDx: a graphical Shiny application to perform Benchmark Dose analysis for transcriptomics data[J].Bioinformatics,2020, 36 (9): 2932-2933.
[15] Sundararajan Z, Knoll R, Hombach P, et al.Shiny-Seq: advanced guided transcriptome analysis[J].BMC Res Notes,2019, 12 (1): 432.
[16] Varet H, Coppée J Y.checkMyIndex: a web-based R/Shiny interface for choosing compatible sequencing indexes[J].Bioinformatics,2019, 35 (5): 901-902.
[17] Wang S, Zhang Y, Hu C, et al.Shiny-DEG: A Web Application to Analyze and Visualize Differentially Expressed Genes in RNA-seq[J].Interdiscip Sci,2020, 12 (3): 349-354.

```



## 解决方案

使用sublime， 正则表达式，类似于正则提取。

因为这些引文都是我搜索的2019-2021年关于shiny发表的文献，所以年份开头都是20.

1. 查找内容为：`^[^.]+\.(.+20\d\d),.+`
2. 替换内容为：`$1`

点击，replace all 按钮即可。