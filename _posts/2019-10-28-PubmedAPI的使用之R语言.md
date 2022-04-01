---
layout: post
title: "PubmedAPI的使用之R语言"
date:   2019-10-28
tags: [pubmed]
comments: true
toc: true
author: Songbiao Zhu
---

使用pubmed 的API，使用R语言编程，实现自动化地获取pubmed数据。

<!-- more -->
## 实践

根据参考中的示例，我在Rstudio中实践了代码，检索 'VHL[gene]+AND+cancer'，就是在代码中写  term= 'VHL[gene]+AND+cancer'，最后运行全部代码获得txt文档，包含124篇文献的题头所有信息（期刊、作者、作者信息、年份、出版卷期信息、文章题目、摘要、PMID、PMCID）。这一数目和直接在Pubmed中检索VHL[gene]+AND+cancer 返回的结果条目数目相同。

代码如下：

 [pubmedApi.R](E:\analysis\thermoProfiling\pubmedApi.R) 

```R
rm(list = ls())
options(stringsAsFactors = F)
source("udf.R")
creDir("data")
creDir("res")
creDir("public")
dataDir = file.path(getwd(),'data')
resDir = file.path(getwd(),'res')
publicDir = file.path(getwd(),'public')
library(XML)
library(RCurl)
searchTerm = 'VHL[gene]+AND+cancer'
path='https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi'
web=getForm(path,db='pubmed',term=searchTerm,usehistory='y',RetMax='10',RetStart='1')
doc<-xmlParse(web,asText=T,encoding="UTF-8") 
webenv<-sapply(getNodeSet(doc,"//WebEnv"),xmlValue)
key<-sapply(getNodeSet(doc,"//QueryKey"),xmlValue)
path1='https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi'
res=getForm(path1,Query_key=key,db='pubmed',WebEnv=webenv,rettype='abstract',retmode='text')
write.table(res,file.path(resDir,paste0(
  unlist(strsplit(searchTerm, split = '[',fixed = T))[1], 
  '_literature.txt')),col.names=F)
```



## 参考

* [R语言网络爬虫之Pubmed API的使用](https://cloud.tencent.com/developer/article/1477089)

* [E-utilities Quick Start](https://www.ncbi.nlm.nih.gov/books/NBK25500/)

* [The E-utilities In-Depth: Parameters, Syntax and More](https://www.ncbi.nlm.nih.gov/books/NBK25499/)，这是一本详细的EUtils的备查书。

* [RISmed](https://rdrr.io/cran/RISmed/man/)， 这个是RISmed package的源代码页，其中如下三个函数正是使用本pubmed 的API EUtils进行开发的，看其源代码可以发现使用的方法。所以参考本代码中的其他函数，可以借鉴其他提取信息的方法。这个package也可以直接使用，只是直接使用时发现不能一个不漏地提取abstract信息，而使用Eutils可以一个不漏地获得abstract文档，未完成的工作是如何提取出所有的abstract信息。
    * EUtilsQuery: Construct URL to make NCBI EUtils query 
    *  EUtilsSummary: Get summary of NCBI EUtils query 
    *  EUtilsGet: Results of an NCBI EUtils query 

## 使用注意

**Note on usage: **

In order not to overload the E-utility servers, NCBI recommends that  users post no more than three URL requests per second and limit large  jobs to either weekends or between 9:00 PM and 5:00 AM Eastern time  during weekdays. Failure to comply with this policy may result in an IP  address being blocked from accessing NCBI.  