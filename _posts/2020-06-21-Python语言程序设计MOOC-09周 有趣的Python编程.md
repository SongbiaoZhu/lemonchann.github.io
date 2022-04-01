---
layout: post
title: "Python语言程序设计MOOC-09周 有趣的Python编程"
date:   2020-06-21
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在MOOC上，学习了北京理工大学嵩天老师的[Python语言程序设计](https://www.icourse163.org/course/BIT-268001#/info)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->
## Python 库纵览

Python语言解释器开源、开放。学习--实践--贡献

Python库官方索引：PyPI

## Python库通用安装方法

Python编程依赖于各种已发布的库和其中函数或对象

三种方法

1. Python库的自定义安装，根据来源提示下载安装
2. Python库的工具安装， pip在线安装
3. Python库的文件安装，.whl文件安装

### 自定义安装numpy库

自定义安装，下载.exe安装即可

### pip安装py2exe库

命令行输入 

pip install [库名称]

pip uninstall

pip list

pip show

pip search

pip help install

```shell
pip install py2exe

pip install -U [py2exe] #进行版本更新

pip uninstall py2exe

pip list #显示库列表，其中的wheel库是基于.whlwen文件进行安装的
pip list --outdated # 列出可更新的库
pip show [py2exe]
# pip search [关键字]，在Pypi中搜索名称或摘要中包含关键字的库
pip search [py2exe]

```

### 利用库的.whl文件安装库

示例安装pywin32库

根据老师示例所用的电脑系统，下载 pywin32-219-cp34-none-win_amd64.whl文件

然后安装命令是，命令行输入

```
pip install pywin32-219-cp34-none-win_amd64.whl
```

## 推荐库安装方法

优先是pip方法

部分库不成功时，不需要纠结，

找到库的主站，进行库的自定义安装。

如果扔失败，找到库的.whl文件安装。

以上三种方法的依次尝试，相信可以安装所有库。

## 目录文件的操作

自带库 os库

```
os.getcwd()
os.listdir(path)
os.remove()
os.removedir(path)
os.chdir(path)
os.mkdir(path)
os.rmdir(path)
os.rename(oldname, newname)

```

os库的子库 os.path

```
Os.path.isfile()
Os.path.isdir()
Os.path.exists()
Os.path.splitext()# 分离扩展名
Os.path.split()
Os.path.dirname()
Os.path.basename()
Os.path.getsize()
Os.path.join(path, name)

```

os.walk函数非常重要

os.walk(path)用于遍历一个目录，返回一个三元组。

root, dirs, files = os.walk(path)

其中root是字符串，dirs和files是列表类型，表示root中的所有目录和所有文件。

举例：打印一个目录下的所有文件信息

```python
import os
path = input(“请输入一个路径：”)
for root,dirs,files in os.walk(path):
for name in files:
print(os.path.join(root, name))
```

举例：将文件夹下的所有文件名字后增加一个字符串_py

```python
import os

path = input("输入一个路径：")
for root,dirs,files in os.walk(path):
    for name in files:
        fname, fext = os.path.splitext(name)
        os.rename(os.path.join(root, name),
        os.path.join(root,fname+'_py'+fext))

```



## 程序定时执行

需要sched库进行任务调度

sched.scheduler()用于创建一个调度任务。

当需要对一个任务进行时间调度时，用这个库scheduler.enter(delay,?priority,?action,?argument = ())

scheduler.run()运行调度任务中的全部调度事件

举例：定时执行函数 func_sched.py

```python
import sched, time

def print_time(msg = "default"):
    print(“当前时间”, time.time(), msg)

# 生成一个调度任务，下面有三个调度事件
s = sched.scheduler(time.time, time.sleep)
print(time.time())
s.enter(5,1,print_time, argument = ('延迟五秒，优先级1',))
s.enter(3,2,print_time, argument = ('延迟3秒，优先级2',))
s.enter(3,1,print_time, argument = ('延迟3秒，优先级1',))
s.run()
print(time.time)

```



## 可执行程序的转换

转化.py为.exe文件。使得pythonh程序在没有python安装环境的情况下运行python程序的功能。

该库使用步骤只有4步

1. 确认python程序是可执行的。这里以上述的func_sched.py为例。
2. 写一个发布脚本 setup.py。只有三行代码，只需要修改第三行中的python程序的文件名。
3. 命令行下运行   python setup.py py2exe，需要确保当前命令行的执行目录、以及setup.py 以及func_sched.py在同一个目录中。
4. 查看运行结果，生成两个结果，dist 包含发布的exe程序以及相关的依赖库，__pycache__是过程文件，可以删除。注意，目录dist需要整体拷贝到其他系统使用，因为其中包含了exe运行的依赖库，不能只拷贝exe文件。

```python
# setup.py
from distutils.core import setup
import py2exe
setup(console = ['func_sched.py'])
```



## office 文件操作函数库

Python语言可以较好的处理office文档，主要掌握以下四个函数库。

- Xlwt (pip install xlwt)
- Xlrd (pip install xlrd)
- Python-docx (需要一个lxml wheel安装，建议该库通过安装包的方式安装)
- Python-pptx ()

## excel

xlrd 和xlwt

```python
# 
import xlrd
path = input("请输入excel文件路径")
workbook = xlrd.open_workbook(path)
sheet = workbook.sheet_by_index(0)
for row in range(sheet.nrows):
    print()
    for col in range(sheet.ncols):
        print("%7s"%sheet.row(row)[col].value, '\t', end = '')
```



```python
# 
import xlwt

```

## word 

Python-docx，

先用lxml wheel的安装包安装lxml，然后再用pip安装Python-docx库。

新建文档：

添加文本：

更改项目符号：

添加标题：

添加图片：

字体设置：设置加粗、字号、颜色

创建表格：

遍历某一单元格：

对单元格操作：

```python
from docx import Document
from docx.shared import Inches
document = Document()
document.add_heading('Document Title',0)
p = document.add_paragraph('A plain paragraph having some ')
p.add_run('bold').bold = True
p.add_run(' and some ')
p.add_run('italic.').italic = True

document.add_heading('Heading, level 1', level = 1)
document.add_paragraph('first item in unordered list', style = 'ListBullet')
document.add_paragraph('first item in unordered list', style = 'ListNumber')
document.add_picture('monty-truth.png', width-Inches(1.25))

table = document.add_table(rows = 1, cols = 3)
hdr_cells - table.rows[0].cells
hdr_cells[0].text = 'Qty'
hdr_cells[1].text = 'Id'
hdr_cells[2].text = 'Desc'
for item in recordset:
    row_cells - table.add_rows().cells
    row_cells[0].text = str(item.qty)
    row_cells[1].text = str(item.id)
    row_cells[2].text = item.desc

document.add_page_break()
document.save('demo.docx')
```

## Powerpoint 编程

新建幻灯片

在幻灯片的固定位置插入某一大小的图片……

使用Presentation 表示ppt对象

```python
#生成一个简单地PPT标题页面
from pptx import Presentation

prs = Presentation()
title_slide_layout = prs.slide_layouts[0]
slide = prs.slides.add_slide(title_slide_layout)
title = slide.shapes.title
subtitle = slide.placeholders[1]

title.text = "Hello, World!"
subtitle.text = "Python-pptx was here!"

prs.save('test.pptx')
```

```python
# 生成一个简单地PPT内容页面
from pptx import Presentation

prs = Presentation()
bullet_slide_layout = prs.slide_layout[1]

slide = prs.slides.add_slide(bullet_slide_layout)
shapes = slide.shapes

title_shape = shapes.title
body_shape = shapes.placeholders[1]

title_shape.text = "Adding a Bullet Slide"
tf = body_shape.text_frame
tf.text = "Find the bullet slide layout"

p = tf.add_paragraph()
p.text = "Use _TextFrame.text for first bullet"
p.level = 1

p = tf.add_paragraph()
p.text = "Use _TextFrame.add_paragraph() for subsequent bullets"
p.level = 2

prs.save("text.pptx")

```

```python
# 生成一个带有图片、文本框和图形的PPT内容页面
from pptx import Presentation
from pptx.util import Inches

img_path = "monty-trtuth.png"

prs = Presentation()
blank_slide_layout = prs.slide_layouts[6]
slide = prs.slides.add_slide(blank_slide_layout)

left = top = Inches(1)
pic = slide.shapes.add_picture(img_path, left, top)

left = Inches(5)
height = Inches(5.5)
pic = slide.shape.add_picture(img_path, left, top, height = height)

prs.save("text.pptx")

```

