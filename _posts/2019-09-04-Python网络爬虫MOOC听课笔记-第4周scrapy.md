---
layout: post
title: "Python网络爬虫MOOC听课笔记-第四周scrapy"
date:   2019-09-04
tags: [python]
comments: true
 
author: Songbiao Zhu
---

在MOOC上，学习了北京理工大学，嵩天老师的[Python网络爬虫与信息提取](https://www.icourse163.org/course/bit-1001870001)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## Scrapy爬虫框架介绍

安装

```python
pip install scrapy

scrapy -h # 测试安装是否成功
```

##  Scrapy爬虫框架解析

就是一个爬虫的半成品，帮用户更快实现网页爬取。

“5+2”结构，5个是框架的模块，还有2个中间键。

* Engine模块 不需要用户修改
* Downloader 模块 不需要用户修改
* Scheduaer 模块，对所有爬取请求进行调度，不需要用户对代码进行修改
* Downloader Middleware 实施以上三个模块之间的用户可以配置的控制，用户可以编写配置代码。如果用户不需要对request和response进行修改时，该模块也不需要修改。
* Spiders，向整个框架提供最初始的链接，是用户主要要修改编写的模块。
* Item Piplines，流水线方式处理Spider产生的爬取项，需要用户编写配置。
* Spider Middleware ，用户可以编写配置代码

重点编写的是Spider 和Item Piplines模块。

Scrapy爬虫框架三种数据流流向：

* spiders--engine--scheduler
* scheduler--engine--Downloader --engine--spiders
* spiders--engine--Item Piplines--scheduler

## scrapy vs requests

* 都很重要，都很实用，入门都简单，都没有对js和表单提交或者验证码的支持
* scrapy 是网站级，requests是网页级
* requests 并发性稍差，不如scrapy（反扒技术反而要爬的慢才行）
* requests 定制灵活；  scrapy 一般定制灵活 但是深度定制困难

小的爬取请求，用requests；不太小的爬取请求，用scrapy 。

## scrapy爬虫的常用命令

scrapy有提供命令行，cmd下运行

```
scrapy -h
```

Scrapy命令行格式：

scrapy <command> [options] [args]

scrapy爬虫的常用命令有6个

* startproject，创建工程
* genspider，创建爬虫
* setting
* crawl，运行爬虫
* list
* shell

project是最大的单元，相当于一个scrapy框架。

命令行相比于图形界面更容易编程操作，适合脚本控制。

本质上，scrapy是给程序员使用的，所以功能比界面更加重要。

## scrapy爬虫单元小结

* Scrapy的5+2结构
* 三个数据流的路径
* 和requests的比较和各自优劣
* Scrapy命令行的使用，对于命令行主要掌握如何使用命令即可，很少修改程序。

### Scrapy爬虫支持多种提取信息的方法

 beautifulsoup，lxml, re,  XPath selector，CSS selector等。

**CSS selector的使用方法**

以一个链接a标签为例

<HTML>.css('a::attr(href)').extract()

## yield关键字的使用

yield 是python3 的33个关键字中的一个。

yield就是一个生成器

生成器是一个不断产生值的函数。

生成器每次返回一个值，然后被冻结。然后再次被调用时，再从冻结的地方开始，生成下一个值。

```python
# 生成器写法
def gen(n):
    for i in range(n):
        yield i **2
for i in gen(5):
    print(i," ", end = "")
    
# 普通写法
def square(n):
    ls = [i**2 for i in range(n)]
    return ls
for i in square(5):
    print(i," ", end = "")
```

生成器相比于一次列出所有内容的优势：

* 更节省存储空间
* 响应更迅速
* 使用更灵活

## Scrapy爬虫的4个使用步骤

1. 创建一个工程和spider模板
2. 编写spider
3. 编写item Pipeline
4. 优化配置策略

## Scrapy爬虫产生的3个数据类型

- Requests类，表示一个requests对象，不过和requests库中的对象不同，但相似。Requests类包括6个属性或方法，url, .method, .headers, .body, .meta, .copy()
- Response类，表示一个http响应，包括7个属性或方法， .url, .status,  .headers,  .body,  .flags,  .request,  .copy()
- Item类，表示从一个http页面中提取的信息内容。是以类字典类型来定义的。

## Scrapy爬虫使用单元小结

* scrapy怕长的第一个例子和生成的目录结构
* yield关键字和生成器
* Request类，Response类、Item类
* CSS.selector的使用