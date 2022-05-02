---
layout: post
title: "多重假设检验与Bonferroni校正、FDR校正"
date:   2020-10-04
tags: [R]
comments: true
 
author: Songbiao Zhu
---

高通量组学数据的统计分析，均需要进行多重假设检验。什么是多重假设检验？如何进行多重假设检验？

<!-- more -->



## 摘要

总结起来就三句话： 

1. 当同一个数据集有n次（n>=2）假设检验时，要做多重假设检验校正 
2. 对于Bonferroni校正，是将p-value的cutoff除以n做校正，这样差异基因筛选的p-value cutoff就更小了，从而使得结果更加严谨 
3. FDR校正是对每个p-value做校正，转换为q-value。q=p\*n/rank，其中rank是指p-value从小到大排序后的次序。 
举一个具体的实例： 我们测量了M个基因在A,B,C,D,E一共5个时间点的表达量，求其中的差异基因，具体做法： 
     （1）首先做ANOVA，确定这M个基因中有哪些基因至少出现过差异 
     （2）5个时间点之间两两比较，一共比较5*4/2=10次，则多重假设检验的n=10 
     （3）每个基因做完10次假设检验后都有10个p-value，做多重假设检验校正（n=10），得到q-value 

4. 根据q-value判断在哪两组之间存在差异

## 为什么要进行多重假设检验

通过T检验等统计学方法对每个蛋白进行P值的计算。T检验是差异蛋白表达检测中常用的统计学方法，通过合并样本间可变的数据，来评价某一个蛋白在两个样本中是否有差异表达。
 但是由于通常样本量较少，从而对总体方差的估计不很准确，所以T检验的检验效能会降低，并且如果多次使用T检验会显著增加假阳性的次数。
 例如，当某个蛋白的p值小于0.05（5%）时，我们通常认为这个蛋白在两个样本中的表达是有差异的。但是仍旧有5%的概率，这个蛋白并不是差异蛋白。那么我们就错误地否认了原假设（在两个样本中没有差异表达），导致了假阳性的产生（犯错的概率为5%）。
 如果检验一次，犯错的概率是5%；检测10000次，犯错的次数就是500次，即额外多出了500次差异的结论（即使实际没有差异）。为了控制假阳性的次数，于是我们需要对p值进行多重检验校正，提高阈值。

## 多重假设检验的矫正方法

### 方法一.Bonferroni，“最简单严厉的方法”

 例如，如果检验1000次，我们就将阈值设定为5%/ 1000 = 0.00005；即使检验1000次，犯错误的概率还是保持在N×1000 = 5%。最终使得预期犯错误的次数不到1次，抹杀了一切假阳性的概率。
 该方法虽然简单，但是检验过于严格，导致最后找不到显著表达的蛋白（假阴性）。

###  方法二.FalseDiscovery Rate， “比较温和的方法校正P值”

  FDR（假阳性率）错误控制法是Benjamini于1995年提出的一种方法，基本原理是通过控制FDR值来决定P值的值域。相对Bonferroni来说，FDR用比较温和的方法对p值进行了校正。其试图在假阳性和假阴性间达到平衡，将假/真阳性比例控制到一定范围之内。例如，如果检验1000次，我们设定的阈值为0.05（5%），那么无论我们得到多少个差异蛋白，这些差异蛋白出现假阳性的概率保持在5%之内，这就叫FDR＜5%。
 那么我们怎么从p value 来估算FDR呢，人们设计了几种不同的估算模型。其中使用最多的是Benjamini and Hochberg方法，简称BH法。虽然这个估算公式并不够完美，但是也能解决大部分的问题，主要还是简单好用！
 FDR的计算方法
 除了可以使用excel的BH计算方法外，对于较大的数据，我们推荐使用R命令p.adjust。

![img](https://img-blog.csdn.net/20170628101429644?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvemh1X3NpX3Rhbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
 1. 我们将一系列p值、校正方法（BH）以及所有p值的个数（length(p)）输入到p.adjust函数中。
 2. 将一系列的p值按照从大到小排序，然后利用下述公式计算每个p值所对应的FDR值。
 公式：p * (n/i)， p是这一次检验的pvalue，n是检验的次数，i是排序后的位置ID（如最大的P值的i值肯定为n，第二大则是n-1，依次至最小为1）。
 3. 将计算出来的FDR值赋予给排序后的p值，如果某一个p值所对应的FDR值大于前一位p值（排序的前一位）所对应的FDR值，则放弃公式计算出来的FDR值，选用与它前一位相同的值。因此会产生连续相同FDR值的现象；反之则保留计算的FDR值。
 4. 将FDR值按照最初始的p值的顺序进行重新排序，返回结果。
 最后我们就可以使用校正后的P值进行后续的分析了。

## Acknowledgment

[多重假设检验与Bonferroni校正、FDR校正](https://blog.csdn.net/zhu_si_tao/article/details/71077703?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param)