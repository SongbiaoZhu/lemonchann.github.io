---
layout: post
title: "Pyinstaller 转python脚本为可执行程序"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

python程序的运行，往往依赖于python语言的解释器，比如spyder, pycharm, python IDLE。那么如何将python脚本打包成不依赖于python解释器的可执行程序呢？



<!-- more -->

## 简介

目的：编写一个可执行的、可跨电脑的、不依赖于python安装的程序，该程序可以统计某一个路径下的子文件夹和子文件的数目。

* 借助Pyinstaller进行python脚本和可执行程序.exe文件的转换
* 借助easygui进行弹出选择要统计的文件夹路径的窗口
* 借助os模块进行遍历路径统计数目

## 模块安装

以上模块中，Pyinstaller和easygui需要事先安装，os不需要安装，因为是标准内置库。

```python
# pip install PyInstaller

# pip install easygui
```



## 步骤

* 首先，编写python 脚本，countFilesNum.py
* 在countFilesNum.py所在的目录下，打开命令行窗口（Git bash here），输入`pyinstaller -F countFilesNum.py ` 。运行结束后，会看到在工作目录下看到生成的三个新文件夹，build, dist和__pycache__文件夹。其中dist文件夹中就包含了countFilesNum.exe文件。
* 双击dist文件夹中的countFilesNum.exe，即打开程序运行窗口。提示请选择路径，然后鼠标点击选择路径，即输出统计结果。
* 程序运行结束后，窗口提示"Press Enter to exit..." ，所以点击回车键即结束并关闭窗口。
* 最后，拷贝dist文件夹中的countFilesNum.exe 到其他位置或者其他电脑，双击即可运行。

## Code

countFilesNum.py如下

```python
# -*- coding: utf-8 -*-
"""
Created on Wed Aug 21 11:40:35 2019

@author: samsung
"""

import os
import easygui

def main(path):
    file_count = 0
    dir_count = 0
    for root, dirs, files in os.walk(path):
        for file in files:
            file_count += 1
        for folder in dirs:
            dir_count += 1
    print('统计完成！')
    print('该路径下共有{}个文件，{}个子文件夹'.format(file_count, dir_count))
    input("Press Enter to exit...")

if __name__ == "__main__":
    print('请选择要统计文件数目的路径')
    path = easygui.diropenbox()
    main(path)
```

## code知识点总结

* `os.walk(path)` 函数遍历路径十分方便
* main()函数结束的一句，`input("Press Enter to exit...")` 可以实现运行结束后，不马上关闭窗口，而是等键入回车键以后再关闭窗口。
* 执行代码中的一句`path = easygui.diropenbox()` 即是为了实现调出路径的选择窗口，很方便。还有函数`file = easygui.fileopenbox()` 以后可以为实现调出文件选择窗口使用。
* `pyinstaller -F countFilesNum.py ` 是pyinstaller的示例用法，可以查看其更多的help参数设置。此处的参数 -F是指打包成一个exe文件。

## 致谢

* [ PyInstaller 3.5 ](https://pypi.org/project/PyInstaller/)

* [pyinstaller转exe](https://blog.csdn.net/solarnanocar/article/details/82077484)

* [Quick and easy file dialog in Python?](https://stackoverflow.com/questions/9319317/quick-and-easy-file-dialog-in-python)

* [Python -- 让程序运行后不立即关闭窗口](https://www.cnblogs.com/Joseph-AMI/p/4712988.html)






