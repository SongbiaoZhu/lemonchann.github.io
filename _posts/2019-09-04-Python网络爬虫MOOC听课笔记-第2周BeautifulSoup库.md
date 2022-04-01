---
layout: post
title: "Python网络爬虫MOOC听课笔记-BeautifulSoup库"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在MOOC上，学习了北京理工大学，嵩天老师的[Python网络爬虫与信息提取](https://www.icourse163.org/course/bit-1001870001)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## 目的

掌握解析HTML页面的信息标记和提取方法

Beautiful soup库的使用：该库可以树形解析html页面

## Beautiful soup库的安装

```python
pip install beautifulSoup4
```

测试：

打开浏览器，打开http://python123.io/ws/demo.html，

ctrl + U查看源代码。

```python
import requests
r = requests.get("http://python123.io/ws/demo.html")
r.text
demo = r.text

from bs4 import BeautifulSoup # bs4 is short for BeautifulSoup4，也可以直接import bs4
soup = BeautifulSoup(demo, "html.parser")# 两个参数，html格式data，以及html.parser作为解析器参数
print(soup.prettify())

```

## Beautiful Soup库的基本元素

理解Beautiful Soup库：html页面有标签，只要你的文件时标签类型，那么该库就可以解析。将HTML转化为标签树再转化为BeautifulSoup类。BeautifulSoup类对应一个HTML或XML文档的全部内容。

![1564969462679](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564969462679.png)

可以看到属性是由键值对构成的。

### BeautifulSoup库的4种解析器

| 解析器           | 使用方法                        | 条件                 |
| ---------------- | ------------------------------- | -------------------- |
| bs4的HTML解析器  | BeautifulSoup(mk,'html.parser') | 安装bs4库            |
| lxml的HTML解析器 | BeautifulSoup(mk,'lxml')        | pip install lxml     |
| lxml的XML解析器  | BeautifulSoup(mk,'xml')         | pip install lxml     |
| html5lib的解析器 | BeautifulSoup(mk,'html5lib')    | pip install html5lib |

事实上，四种解析器都是可以处理html文档的，只是速度和强项有差别。

### BeautifulSoup类的5种基本元素

| 基本元素        | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| Tag             | 标签，分别用尖括号对和内有反斜线的尖括号对作为开头和结尾     |
| Name            | 标签名字，格式是 标签.name                                   |
| Attributes      | 标签属性，格式是 标签.attrs                                  |
| NavigableString | 标签内非属性字符串，两对尖括号中的字符串，格式是 标签.string |
| Comment         | 标签内字符串的注释部分，一种特殊的comment类型                |

示例以上的基本元素用法：

```python
import requests
r = requests.get("http://python123.io/ws/demo.html")
r.text
demo = r.text

from bs4 import BeautifulSoup # bs4 is short for BeautifulSoup4
soup = BeautifulSoup(demo, "html.parser")# html.parser作为解析器参数
print(soup.prettify())

soup.title # 查看 标签的题目
tag = soup.a # 获取a 标签的内容，只能返回html中的第一个a标签
tag

soup.a.name # 获取a 标签的名字
soup.a.parent.name
soup.a.parent.parent.name

tag.attrs # 查看 标签的属性
tag.attrs['class'] # 查看 标签属性中class的内容
tag.attrs['href'] # 查看 标签属性中href的内容
type(tag.attrs)# 查看 标签属性的类型
type(tag)

soup.a
soup.a.string# 查看 标签的非属性字符串
soup.p
soup.p.string
type(soup.p.string)

newsoup = BeautifulSoup("<b><!--This is a comment--></b><p>This is not a comment</p>","html.parser")
# html中用尖括号感叹号表示comment
newsoup.b.string
type(newsoup.b.string)

newsoup.p.string
type(newsoup.p.string)
# 通过上面的例子可以看到，.string对标签都可以返回一个字符串，但是不能告诉你是否是comment，可以通过type进行判断
```

## 基于bs4库的HTML内容遍历方法

任何的HTML页面都是树形结构

对树形结构有三种遍历方法

* 下行遍历

* 上行遍历

* 平行遍历

### 下行遍历介绍

| 属性         | 说明                                                   |
| ------------ | ------------------------------------------------------ |
| .contents    | 获取子节点的列表                                       |
| .children    | 返回子节点的迭代类型，用于循环遍历儿子节点             |
| .descendants | 返回子孙节点的遍历类型，包含所有子孙节点，用于循环遍历 |

### 上行遍历介绍

| 属性     | 说明                   |
| -------- | ---------------------- |
| .parent  | 父亲节点               |
| .parents | 返回迭代类型，父祖标签 |

### 平行遍历介绍

注意所有的平行遍历发生在同一个父亲节点下的各节点之间。

| 属性               | 说明                                   |
| ------------------ | -------------------------------------- |
| .next_sibling      | 返回下一个平行节点标签                 |
| .previous_sibling  | 返回上一个平行节点标签                 |
| .next_siblings     | 返回迭代类型，返回所有后续平行节点标签 |
| .previous_siblings | 返回迭代类型，返回所有前续平行节点标签 |

返回的迭代类型只能用在for in 语句中。

示例介绍

```python
import requests
r = requests.get("http://python123.io/ws/demo.html")
r.text
demo = r.text
from bs4 import BeautifulSoup # bs4 is short for BeautifulSoup4
soup = BeautifulSoup(demo, "html.parser")
soup.head
soup.head.contents
soup.body.contents
len(soup.body.contents)
soup.body.contents[1]

for child in soup.body.children:
    print(child) #遍历儿子节点
for child in soup.body.descendants:
    print(chid) #遍历子孙节点
    
soup.title.parent
soup.html.parent #最高级的parent就是自身
soup.parent #是空的
for parent in soup.a.parents:
    if parent is None:
        print(parent)
    else:
        print(parent.name)
        
soup.a.next_sibling # 发现获得了NavigableString，也就是说遍历时获得的不一定都是标签，NavigableString也被认为是一个节点
soup.a.next_sibling.next_sibling
soup.a.previous_sibling
soup.a.previous_sibling.previous_sibling
soup.a.parent
for sibling in soup.a.next_siblings:
    print(sibling) #遍历后续节点
for sibling in soup.a.previous_siblings:
    print(sibling) #遍历前续节点

```

## 基于bs4库的HTML内容的输出

### bs4库的prettify()方法

```python
from bs4 import BeautifulSoup # bs4 is short for BeautifulSoup4
soup = BeautifulSoup(demo, 'html.parser')
soup.prettify() #发现将每一个标签尖括号后加了一个换行符
print(soup.prettify()) # 内容变得有结构，更易读
print(soup.a.prettify())# 可以对一个标签内容使用

soup = BeautifulSoup("<p>中文</p>", 'html.parser')
print(soup.p.prettify())
```

## 信息标记的三种形式

标记后的信息可以形成信息组织结构，可用于以通信存储。HTML的信息标记是预定义的尖括号开头和结尾的标签。

信息标记的三种形式：

* XML  eXensible markup language，基本和HTML的格式一样
* JSON JavaScript Object Notation，键值对组合，键值都有双引号
* YAML YAML Ain't Markup Language，采用无类型的键值对组织信息，键值没有有双引号，YAML中键值对之间可以嵌套并使用缩进表示所属关系，用减号表达并列关系，用竖线表示整块数据，用#表示注释。



![1564990270754](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564990270754.png)



![1564990304055](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564990304055.png)



![1564990338812](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564990338812.png)



![1564990375404](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564990375404.png)



![1564990411940](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564990411940.png)



![1564990443558](C:\Users\samsung\AppData\Roaming\Typora\typora-user-images\1564990443558.png)

以上三种标记语言的比较：

* XML最早，扩展性好，但繁琐；Tnternet上信息的传递
* JSON 信息有类型，适合程序处理（JS），较简洁，但，无注释；移动应用云端和节点之间的信息通信
* YAML 信息无类型，文本信息比例最高，可读性好；用于各类系统的配置文件，有注释易读。

## 信息提取的一般方法

从标记的信息中提取所关注的内容。

* 方法1，完整解析信息的标记形式，再提取关键信息，比如bs4库的标签树遍历，需要标记解析器
* 方法2，无视标记形式，直接搜索关键信息，需要文本查找函数
* 融合方法，需要标记解析器以及文本查找函数

soup.find_all(name, attrs, recursive,string)

返回一个列表类型，存储查找的结果

name:对标签名称的检索字符串

attrs:对标签属性值的检索字符串，可标注属性检索

recursive:是否对子孙节点全部搜索，默认为True,如果为False，就是只搜索当前节点的儿子节点。

string: 标签中字符串区域的检索字符串

因为find_all函数非常常用，所以.find_all(..)可以简写为(..)使用。

find_all还有7个扩展方法，其参数是一样的，区别在与搜索区域和返回的结果数量不同。

<>.find()

<>.find_parents()

<>.find_parent()

<>.find_next_siblings()

<>.find_next_sibling()

<>.find_previous_siblings()

<>.find_previous_sibling()

## 实例：中国大学排名定向爬虫

爬取“最好大学网”的大学排名信息

定向爬虫，指只针对给定的url爬取，不爬取其他url 的信息

首先确认是否可以爬取，就是看要爬取的信息是存在静态的html中的，而不是动态js生成的。再看一下robots.txt，如果不存在就是不限制爬虫。

### 程序的结构设计：

* 步骤1，从网络上获取大学排名的网页内容，getHTMLText()
* 步骤2，提取网页内容中信息到合适的数据结构，fillUnivList()
* 步骤3，利用数据结构展示并输出结果，printUnivList()



```python


```

