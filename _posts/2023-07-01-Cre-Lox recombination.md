---
layout: post
title: "Cre-Lox recombination"
date:   2023-07-01
tags: [biomedicine]
comments: true
author: Songbiao Zhu

---

Cre是一种重组酶，识别Lox site（最先发现的Lox site，被称为Lox P序列），进行DNA重组。Cre-Lox重组是一种位点特异性重组酶技术，用于在细胞DNA的特定位点进行删除、插入、易位和倒位。该系统无需插入任何额外的序列。 

<!-- more -->

## What is the Cre-lox system?

* Cre-Lox，发现于P1 噬菌体中。在噬菌体中的天然功能是，Cre通过识别Lox序列，进行DNA环化，利于开始下一个侵染-扩增-裂解循环。

* 工作模式：靶向特异的DNA序列（即Lox P），在Cre重组酶帮助下，对DNA序列实现splicing。

* LoxP sites 是有方向的34bp的序列，包含2个13bp的识别序列，其中由8bp space区域分隔开。LoxP序列，在除噬菌体以外的其它物种中，都没有发现。LoxP 序列也足够长，所以随机出现这样的序列几乎不可能，因此适合用于基因重组。

* 两侧加了Lox序列的DNA区域，经常被成为 floxed的DNA（Lox-flanked regions of DNA are often said to be “floxed”.）。

### Cre-containing plasmid

根据载体构建的不同，可以调控Cre的表达。通过控制Cre的表达，来调控Cre所编辑的基因重组过程。

* **Inducible Cre**: 需要添加外源配体（例如他莫昔芬）来激活 Cre。

* **Promoter-regulated Cre**: 启动子区域决定了 Cre 将表达的区域。 Cre 可以在广泛活跃的启动子（如 CAG）下全局表达，或者仅在更特定的启动子下的一部分细胞中表达（例如，Rho-Cre 在视网膜中表达）。

* **Fluorescent Cre**: Cre 与荧光报告基因的融合使得 Cre 表达可视化。

* **Optimized Cre**: 密码子优化的 Cre (iCre) 在小鼠中的表达水平高于 P1 噬菌体 Cre，促进 Cre 驱动的高重组率。

* **Split Cre**: Cre 重组酶被分成两半，分为 N 端和 C 端 Cre 片段（分别为 NCre 和 CCre），并置于不同启动子的控制下。

### loxP (floxed) Constructs

根据loxP序列的位置，以及LoxP序列的方向，Cre 可能激活或抑制基因表达。常见的构造类型包括：

* **Cre-dependent Gene Expression:** Placing a stop codon with loxP sites on either side (often called a “lox-stop-lox” or “LSL” cassette) upstream of a gene of interest will prevent gene expression in the absence of Cre. In the presence of Cre, the stop codon is excised, and gene expression proceeds.

* **Cre-dependent Gene Knockout:** Conversely, putting the loxP sites on either side of a gene (called “floxing”, for “flanked by loxP”), will permit gene expression until Cre is present, at which time the gene will be disrupted or deleted.

* **Cre-dependent shRNA Expression:** Cre-lox can be used to turn shRNA constructs on or off. In floxed-shRNA constructs, Cre can excise the shRNA to return gene expression to physiological levels. In lox-STOP-lox shRNA constructs, Cre expression promotes shRNA expression.

* **Gene Switch:** These constructs contain two genes of interest, Genes A and B. When Cre is absent, only Gene A is translated correctly. Cre expression excises Gene A and alters the reading frame to allow in-frame translation of Gene B.

* **FLEx Switch:** This system allows scientists to utilize recombination elements such as Cre to turn off the expression of one gene while simultaneously turning on another. The FLEx switch system takes advantage of the orientation specificity of Cre and the different types of target sites available, both mutant and wild type. The ability to manipulate the number, orientation, and type of target sites that flox your genes of interest makes FLEx switch a powerful experimental tool.

### Reference

[Good Cre-Lox Recombination – Introduction](https://info.abmgood.com/cre-lox-recombination-introduction)

[Conditional gene expression using the Cre Lox FLEx vector switch! - YouTube](https://www.youtube.com/watch?v=I21NmFq4F8A)


