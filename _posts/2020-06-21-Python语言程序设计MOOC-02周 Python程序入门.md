---
layout: post
title: "Python语言程序设计MOOC-02周 Python程序入门"
date:   2020-06-21
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在MOOC上，学习了北京理工大学嵩天老师的[Python语言程序设计](https://www.icourse163.org/course/BIT-268001#/info)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## python程序元素分析

注释：单行注释以#开头，多行注释以三个单引号开头和结尾

输入：

缩进：表示缩进关系的空格不能改变，空格不能分割命名。其余空格使用没有限制。

输出：

变量：命名名字中不能有空格，有33个保留字。赋值语言，支持同步赋值语句。

分支：

常量：

循环：

表达式：通过33个保留字与操作符号组成表达式



## 程序编写模板

initial-print模板

* 初始变量，运算需要的初始值
* 运算部分，根据算法实现
* 结果输出，print()输出结果

## 蟒蛇绘制程序实例

实现图形效果输出。共18行。

turtle库，流行的图片库。想象一只乌龟，从原点开始，在xy坐标系中爬行的轨迹即为绘制的图形。

def定义函数。定义的函数必须经过调用才会被执行。

turtle.setup():窗口的设置

turtle.pensize():小乌龟运行轨迹的宽度

turtle.pencolor():小乌龟运行轨迹的颜色

turtle.seth(-40):小乌龟开始运行的角度

调用drawSnake()函数

turtle.circle()，让小乌龟沿着圆形运行，两个参数，半径和弧度

turtle.fd(),小乌龟向前直线爬行移动，有一个参数是爬行的距离。

## 函数库的调用

两种调用方式

* import 库名：此时使用函数时，格式是 库名.函数名
* from 库名 import 函数名 或者 from 库名 import *： 使用这种方式引用时，使用函数时，不需要库名，可以直接使用函数名。

这两种调用方法的功能是一样的，是使用习惯的差别。







