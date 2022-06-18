---
layout: post
title: "uniprot database知识整理"
date:   2022-06-18
tags: [Bioinformatics]
comments: true
author: Songbiao Zhu
---
swiss-Prot 库和trEMBL库的关系是怎样的？

<!-- more -->

## Why is UniProtKB composed of 2 sections, UniProtKB/Swiss-Prot and UniProtKB/TrEMBL?

Swiss-Prot(创建于1986年)是一个集实验结果、计算特征和科学结论于一体的高质量的手工注释的非冗余蛋白质序列数据库。UniProtKB/Swiss-Prot现在是UniProt知识库的审查部分。

UniProtKB的TrEMBL部分是在1996年引入的，以应对基因组项目增加的数据流。当时已经认识到，作为Swiss-Prot标志的传统时间和劳力密集的人工管理过程不能扩大到包括所有可用的蛋白质序列。UniProtKB/TrEMBL包含高质量的计算分析记录，通过自动注释和分类丰富了这些记录。这些UniProtKB/TrEMBL未审查的条目与UniProtKB/Swiss-Prot手动审查的条目保持分离，以便后者的高质量数据不会以任何方式被削弱。资料的自动处理，可使市民迅速查阅有关纪录。

## swiss-Prot 库和trEMBL库的关系

以uniprot中human 物种的所有蛋白序列库为例，swissPort 和TrEMBL 两个库的数量之和，就等于uniProt中human物种的所有蛋白序列总数。所以unreviewed的TrEMBL库，和Reviewed的swissPort 库是互斥的，而不是包含关系。

## Entry status

“条目信息”部分的这一部分表明条目是否已经被UniProtKB策展人手动注释和审查，换句话说，如果条目属于UniProtKB的Swiss-Prot部分(已审查)或属于计算机注释的TrEMBL部分(未审查)。

UniProtKB/Swiss-Prot条目被标记为黄色的评审图标

UniProtKB/TrEMBL条目被标记为一个蓝色的未审核图标

This subsection of the 'Entry information' section indicates whether the entry has been manually annotated and reviewed by UniProtKB curators or not, in other words, if the entry belongs to the Swiss-Prot section of UniProtKB (reviewed) or to the computer-annotated TrEMBL section (unreviewed).

UniProtKB/Swiss-Prot entries are tagged with a yellow reviewed icon

UniProtKB/TrEMBL entries are tagged with a blue unreviewed icon 

## Automatic annotation

UniProt的自动标注管道通过自动分类和标注来丰富UniProtKB中的未审核记录，从而增强了这些记录。

* Automatic classification and domain annotation
* Automatic annotation

UniProt's Automatic Annotation pipeline enhances the unreviewed records in UniProtKB by enriching them with automatic classification and annotation.

## Entry header中包含的信息解读

以VHL蛋白为例，>sp|P40337|VHL_HUMAN von Hippel-Lindau disease tumor suppressor OS=Homo sapiens OX=9606 GN=VHL PE=1 SV=2

* sp：Swiss-Prot数据库的简称

* P40337：UniProt ID号

* VHL_HUMAN：是UniProt 的登录名

* von Hippel-Lindau disease tumor suppressor：蛋白质名称

* OS=Homo sapiens：OS是Organism简称，Homo sapiens为人的拉丁文分类命名

* OX=9606：Organism Taxonomy，即物种分类数据库Taxonomy ID

* GN=VHL：Gene name，基因名为VHL

* PE=1：Protein Existence，蛋白质可靠性，对应5个数字，数字越小越可靠：
  
  * 1：Experimental evidence at protein level
  * 2：Experimental evidence at tranlevel
  * 3：Protein inferred from homology
  * 4：Protein predicted
  * 5：Protein uncertain

* SV=2：Sequence Version，序列版本号
  
  ## 参考

[Why is UniProtKB composed of 2 sections, UniProtKB/Swiss-Prot and UniProtKB/TrEMBL?](https://www.uniprot.org/help/uniprotkb_sections)

[Entry status](https://www.uniprot.org/help/entry_status)

[Automatic annotation](https://www.uniprot.org/help/automatic%5Fannotation)