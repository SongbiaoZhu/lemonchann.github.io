---
layout: post
title: "Proteome Discoverer结果解读"
date:   2022-06-18
tags: [Bioinformatics]
comments: true
author: Songbiao Zhu
---
Proteome Discoverer结果中，这些名词的含义是什么：PSM？FPR？FDR？p-value？PEP？q-value？
<!-- more -->
## Terminology

* PSM: peptide-spectrum match, a spectrum that matches to a peptide sequence
* p-value: probability of observing an incorrect PSM with a given score or higher by
  chance, low p-value indicates a small probability of observing an incorrect PSM
* FPR: false positive rate, proportion of incorrect PSMs above a certain score threshold
  over all incorrect PSMs
* FDR: false discovery rate, expected proportion of incorrect predictions amongst a
  selected set of predictions. The fraction of incorrect PSMs within a selected set of PSMs
  above a given score threshold.
* q-value: the minimal FDR threshold at which a PSM is accepted, transforming the FDR
  into a monotone function, increasing the score threshold will always lower the FDR and
  vice versa
* PEP: posterior error probability (also called local FDR). Measures the significance of a
  single spectrum assignment with a specific PSM score. It is the probability of the PSM
  being incorrect, i.e. PEP of 0.01 means there is a 1% chance of the PSM being incorrect.