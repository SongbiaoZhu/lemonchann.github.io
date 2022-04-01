---
layout: post
title: "STRING API使用方法"
date:   2019-10-08
tags: [bioinformatics]
comments: true
toc: true
author: Songbiao Zhu
---

STRING 网站数据分析的API使用方法介绍。

<!-- more -->

## 简介

STRING has an application programming interface (API) which enables you to get the data without using the graphical user interface of the web page. The API is convenient if you need to programmatically access some information but still do not want to download the entire dataset. There are several scenarios when it is practical to use it. For example, you might need to access some interaction from your own scripts or want to incorporate STRING network in your web page.

We currently provide an implementation using HTTP, where the database information is accessed by HTTP requests. Due to implementation reasons, similarly to the web site, some API methods will allow only a limited number of proteins in each query. If you need access to the bulk data, you can download the entire dataset from the [download page](https://string-db.org/cgi/download.pl).

## 主要功能

1. Mapping identifiers
2. Getting STRING network image
3. Getting the STRING network interactions
4. Getting all the STRING interaction
5. partners of the protein set
6. Retrieving similarity scores of the protein set
7. Retrieving best similarity hits between species
8. Getting functional enrichment
9. Retrieving functional annotation
10. Getting protein-protein interaction enrichment
11. Getting current STRING version
