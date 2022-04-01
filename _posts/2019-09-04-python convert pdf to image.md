---
layout: post
title: "python convert pdf to image"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

使用python，批量将pdf格式的图片文件，转为png等常见的图片格式。

<!-- more -->

# 脚本内容

pdf2png.py

已经worked.

```python
# -*- coding: utf-8 -*-
"""
1. pip install pymupdf
[https://blog.csdn.net/qq_43145035/article/details/83270501]
Created on Thu Aug 29 23:25:57 2019
@author: samsung
"""

import fitz
import os
import easygui
        
def main(path):
    items = os.listdir(path) 
    pdfs = []
    for f in items:
        if f.endswith(".pdf"):
            pdfs.append(f)
    for pdf in pdfs:
        doc = fitz.open(os.path.join(path, pdf))
        fname = pdf.split('.')[0]
        for pg in range(doc.pageCount):
            page = doc[pg]
            rotate = int(0)
            zoom_x = 2.0
            zoom_y = 2.0
            trans = fitz.Matrix(zoom_x, zoom_y).preRotate(rotate)
            pm = page.getPixmap(matrix=trans, alpha=False)
            pm.writePNG('{}\\{}_{}.png'.format(path,fname,pg))
    print('转换完成')
    input("Press Enter to exit...")

if __name__ == "__main__":
    print('请选择要转为图片的pdf存储路径')
    path = easygui.diropenbox()
    main(path)


```



## 转为可执行程序

在pdf2png.py所在的目录下，打开命令行窗口（Git bash here），输入`pyinstaller -F pdf2png.py ` 。运行结束后，会看到在工作目录下看到生成的三个新文件夹，build, dist和__pycache__文件夹。其中dist文件夹中就包含了pdf2png.exe文件。

## 致谢

* [windows下用Python把pdf文件转化为图片(png高清)](https://blog.csdn.net/qq_43145035/article/details/83270501)
* [更多图片精度及格式调整请资料参考](https://pymupdf.readthedocs.io/en/latest/faq/#how-to-increase-image-resolution)