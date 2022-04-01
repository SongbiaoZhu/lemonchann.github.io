---
layout: post
title: "C中文网python编程基础chapter-2-Python 初探"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在C语言中文网上，学习了[python编程的基础课程](http://c.biancheng.net/python/)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## Python IDE

IDE 是 Intergreated Development Environment 的缩写，中文称为集成开发环境，用来表示辅助程序员开发的应用软件。运行 C 语言（或 Java 语言）程序必须有编译器，而运行 Python 语言程序必须有解释器。在实际开发中，除了运行程序必须的工具外，我们往往还需要很多其他辅助软件，例如语言编辑器、自动建立工具、除错器等等。这些工具通常被打包在一起，统一发布和安装，例如 PythonWin、MacPython、PyCharm 等，它们统称为集成开发环境（IDE）。
PyCharm，是由 JetBrains 公司开发的一款 Python 开发工具，在 Windows、Mac OS 和 Linux 操作系统中都可以使用。

注意：Windows 系统不区分大小写，在 Windows 平台上输入源程序路径时可以不区分大小写。但是 Mac OS X 或 Linux 系统都区分大小写，因此在这两个平台上输入 Python 源程序路径时一定要注意大小写问题。

## Python注释
在 Python 中，通常包括 3 种类型的注释，分别是单行注释、多行注释和中文编码声明注释。 
```python
# 单行注释
# 这是一行简单的注释
print ("Hello World!")
print ("Hello World!") #这是一行简单的注释

# 多行注释
'''
使用 3 个单引号或者3个双引号分别作为注释的开头和结尾
可以一次性注释多行内容
这里面的内容全部是注释内容
'''

# Python中文编码声明注释
# coding:utf-8
# coding=utf-8
```

## Python缩进规则和快捷键

Python 采用代码**缩进和冒号**（ : ）来区分代码块之间的层次，行尾的冒号和下一行的缩进，表示下一个代码块的开始，而缩进的结束则表示此代码块的结束。
注意，Python 中实现对代码的缩进，可以使用空格或者 Tab 键实现。但无论是手动敲空格，还是使用 Tab 键，通常情况下都是采用 4 个空格长度作为一个缩进量（默认情况下，**一个 Tab 键就表示 4 个空格**）。
不仅如此，在使用 IDLE 开发环境编写 Python 代码时，如果想通过设置多行代码的缩进量，可以使用 Ctrl+] 和 Ctrl+[ 快捷键，此快捷键可以使所选中代码快速缩进（或反缩进）。
Python 采用 PEP 8 作为编码规范，其中 PEP 是 Python Enhancement Proposal（Python 增强建议书）的缩写，8 代表的是 Python 代码的样式指南。

* 每个 import 语句只导入一个模块，尽量避免一次导入多个模块
* **不要在行尾添加分号**，也不要用分号将两条命令放在同一行
* 使用必要的空行可以增加代码的可读性
* 通常情况下，在运算符两侧、函数参数之间以及逗号两侧，都**建议使用空格进行分隔**
* 建议每行不超过 80 个字符，如果超过，**建议使用小括号将多行内容隐式的连接起来**，而不推荐使用反斜杠 \ 进行连接
```python
#推荐
import os
import sys
#不推荐
import os,sys

#不推荐
height=float(input("输入身高：")) ; weight=fioat(input("输入体重：")) ;

#推荐
s=("C语言中文网是中国领先的C语言程序设计专业网站，"
"提供C语言入门经典教程、C语言编译器、C语言函数手册等。")
#不推荐
s="C语言中文网是中国领先的C语言程序设计专业网站，\
提供C语言入门经典教程、C语言编译器、C语言函数手册等。"

```
## Python标识符命名规范
**标识符就是一个名字**，它的主要作用就是作为变量、函数、类、模块以及其他对象的名称。
Python 中**标识符一定要遵守的命令规则**，比如说： 

* 标识符是由字符（A~Z 和 a~z）、下划线和数字组成，但第一个字符不能是数字
* 标识符不能和 Python 中的保留字相同
* Python中的标识符中，不能包含空格、@、% 以及 $ 等特殊字符
* 在 Python 中，标识符中的字母是严格区分大小写的
* 除非特定场景需要，应避免使用以下划线开头的标识符，因为Python 语言中，以下划线开头的标识符有特殊含义
* 应尽量避免使用汉字作为标识符，这会避免遇到很多奇葩的错误

标识符的**命名有一定的规范可循**，例如： 

-  当标识符用作**模块名**时，应尽量短小，并且全部使用小写字母，可以使用**下划线分割**多个字母，例如 game_mian、game_register 等。
-  当标识符用作**包的名称**时，应尽量短小，也全部使用小写字母，不推荐使用下划线，**使用.分割**，例如 com.mr、com.mr.book 等。
-  当标识符用作**类名**时，应采用**单词首字母大写**的形式。例如，定义一个图书类，可以命名为 Book。
-  模块内部的类名，可以采用 "下划线+首字母大写" 的形式，如 _Book;
-  函数名、类中的属性名和方法名，应全部使用小写字母，多个单词之间可以用下划线分割；
-  **常量**命名应全部**使用大写字母**，单词之间可以用下划线分割；

## Python关键字（保留字）一览表

保留字是 Python 语言中一些已经被赋予特定意义的单词，这就要求开发者在开发程序时，不能用这些保留字作为标识符给变量、函数、类、模板以及其他对象命名。

```python
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## Python内置函数一览表

为了提高程序员的开发效率，Python 提供了很多可以直接拿来用的函数，每个函数都可以帮助程序员实现某些具体的功能。

各个内置函数的具体功能和用法，可通过访问[内置函数](https://docs.python.org/zh-cn/3/library/functions.html) 进行查看。

| 内置函数      |             |              |              |                |
| ------------- | ----------- | ------------ | ------------ | -------------- |
| abs()         | delattr()   | hash()       | memoryview() | set()          |
| all()         | dict()      | help()       | min()        | setattr()      |
| any()         | dir()       | hex()        | next()       | slicea()       |
| ascii()       | divmod()    | id()         | object()     | sorted()       |
| bin()         | enumerate() | input()      | oct()        | staticmethod() |
| bool()        | eval()      | int()        | open()       | str()          |
| breakpoint()  | exec()      | isinstance() | ord()        | sum()          |
| bytearray()   | filter()    | issubclass() | pow()        | super()        |
| bytes()       | float()     | iter()       | print()      | tuple()        |
| callable()    | format()    | len()        | property()   | type()         |
| chr()         | frozenset() | list()       | range()      | vars()         |
| classmethod() | getattr()   | locals()     | repr()       | zip()          |
| compile()     | globals()   | map()        | reversed()   | __import__()   |
| complex()     | hasattr()   | max()        | round()      |                |