---
layout: post
title: "Wilcox rank-sum test"
date:   2022-06-18
tags: [Bioinformatics]
comments: true
author: Songbiao Zhu
---
t-test是参数统计检验方法，应用的前提是检测变量服从等方差的正态分布。当数据不符合此要求时，可以使用非参数检验方法是Wilcoxon rank sum test，或者叫**Mann Whitney U test**。

<!-- more -->

## wilcox.test

两个独立样本的t-test是检验两个样本的均值是否相等。而两个独立样本的wilcoxon test 则是检验两个样本的中位数，或者说两个样本的分布是否有偏移。因此，wilcoxon test在计算统计量时是先将两个样本混到一起，然后对混合后的list进行从小到大排序，根据排序把两个样本的值分别转换成排序序数，最后比较两个样本的序数的大小。如果序数大的富集在其中一个样本，表明该样本相对另一个样本的值要更大，相反亦然。


## 计算方法

* [如何计算wilcoxon test的统计量](http://sphweb.bumc.bu.edu/otlt/MPH-Modules/BS/BS704_Nonparametric/BS704_Nonparametric4.html)
* [如何计算wilcoxon test的p值](https://data.library.virginia.edu/the-wilcoxon-rank-sum-test/)

## R语言实现wilcox.test
### wilcox.test code

```R
wilcox.test(vector_A,vector_B, alternative = "two.sided") # alternative also could be "greater" or "less"

# 或者输入数据框
wilcox.test(gene_expression ~ tissue_group, alternative = "two.sided") 
# tissue_group 是名义变量，有两个水平，例如组织A和B，即比较A组织和B组织的基因表达水平
```

### wilcox.test的输出结果
> Wilcoxon rank sum test

> data: A and B
> W = 13, p-value = 0.04988
> alternative hypothesis: true location shift is not equal to 0

## R wilcox.test 报错

实际使用时，我遇到了报如下错误：
> 'cannot compute exact p-value with ties' 

搜索答案如下：
> When I execute a Wilcox u-test on two variables I receive a warning :
> 'cannot compute exact p-value with ties'
>
> - What are ties? What does this mean for my data?

If you have two identical values in your data, these are called ties.
Now the ranks are not unique anymore and hence exact p-values cannot be
calculated.
And since you do not know this, it might be worth to note that the
Wilcoxon test also assumes a non-skewed distribution.


> - Is that a problem for significance testing?

If there are just a few ties, you should not worry, but re-check how
your data looks like. It is a warning, not an error message.


> - is there a way to overcome this problem?

If you need to, use an appropriate test for your data.
## 参考
[生物学研究中常见的统计检验方法(二：Wilcoxon test)](https://www.jianshu.com/p/9df4af9249c2)
[What are ties? Wilcox u-test](https://r.789695.n4.nabble.com/What-are-ties-Wilcox-u-test-td857059.html)