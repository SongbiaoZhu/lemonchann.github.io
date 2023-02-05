---

layout: post
title: "Activity-Based Protein Profiling (ABPP)"
date:   2023-02-05
tags: [ABPP, MS]
comments: true
author: Songbiao Zhu

---

ABPP

 ABPP is a chemical proteomics approach that utilizes small-molecule probes to determine the functional state of enzymes directly in native systems.

<!-- more -->

 An ABPP probe contains at least two key features: 1) a reactive group that binds and covalently modifies the active sites of a large number of enzymes that share conserved mechanistic and/or structural features, and 2) a reporter tag, such as a fluorophore or biotin, to enable detection, enrichment, and identification of probe-labeled enzymes by gel electrophoresis and in-gel fluorescence scanning.

 ABPP probes have been generated for more than a dozen enzyme classes, including probes that react specifically with serine hydrolases, cysteine proteases, and glycosidases. These probes selectively label active enzymes, but not their inactive forms, facilitating the characterization of changes in enzyme activity that occur without alterations in protein levels.


 ![Basics of Activity-Based Protein Profiling](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4138146/bin/nihms613584f1.jpg) 

(a) Schematic of ABPP probes. (b) Gel-based ABPP. (c) ABPP-MudPIT. 

## What's the difference between ABPP-MS and Affinity-IP-MS?
我个人总结了二者的三点差别如下：
1. ABPP方法中，使用的探针是化学反应性的探针，并且化学反应的发生基于酶催化反应的发生。而Affinity-IP-MS中所使用的亲和基团，是通过空间相互作用实现的结合。ABPP中的探针的分子结构，可能与酶空间的binding pocket没有任何类似之处，见下表中的ABPP探针举例：

![ABPP probes are available for a variety of enzyme classes](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4138146/bin/nihms613584f2.jpg)
2. ABPP方法，测定的有活性的酶的水平。而Affinity-IP-MS测定的是有binding的酶的水平。
3. 当target没有酶活方面的性质时，不适合ABPP分析。而Affinity-IP-MS不受这一限制。所以ABPP主要用于分析某一分子对哪些类酶的抑制作用，关注的酶活性的研究；而Affinity-IP-MS主要关注的是相互作用蛋白（binding partner）的研究。

## What is the application of ABPP in industrial?

1. ABPP 用于靶点发现
Two or more proteomes are analyzed by ABPP in parallel to identify enzymes with different levels of activity. If the samples analyzed reflect different biological conditions (e.g., physiological vs. pathological), then the enzyme(s) showing differential activity can be hypothesized to be involved in the phenotype in question. 
2. ABPP 用于酶的抑制剂的发现
When performed in a competitive mode, ABPP can also be used to screen for enzyme inhibitors or to identify the target(s) to which a small-molecule inhibitor binds.

In competitive ABPP, proteomes are first incubated with the small molecule of interest (e.g., a phenotypic hit that targets an unknown enzyme), and then labeled with a broad ABPP probe that reacts with most enzymes in the class under study. Enzyme activities present in the vehicle, but not the inhibitor-treated sample, represent the molecular target of the compound in question.

![Competitive ABPP for enzyme and inhibitor discovery](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4138146/bin/nihms613584f3.jpg)


## Reference
1. [Application of Activity-Based Protein Profiling to Study Enzyme Function in Adipocytes](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4138146/)
