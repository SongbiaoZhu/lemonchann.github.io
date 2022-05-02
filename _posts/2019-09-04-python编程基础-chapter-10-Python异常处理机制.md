---
layout: post
title: "C中文网python编程基础chapter-10-Python异常处理机制"
date:   2019-09-04
tags: [python]
comments: true
 
author: Songbiao Zhu
---

在C语言中文网上，学习了[python编程的基础课程](http://c.biancheng.net/python/)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->


## 1. 浅谈Python异常处理机制 

程序员希望有一种强大的机制来解决上面的问题，希望将上面程序改成如下伪码：

```python
if 用户输入不合法:
    alert 输入不合法
    goto retry
else :
    #业务实现代码
    ...
```

异常机制可以使程序中的异常处理代码和正常业务代间分离，保证程序代码更加优雅，并可以提高程序的健壮性。

-  try 关键字后缩进的代码块简称 try 块，它里面放置的是可能引发异常的代码；
-  在 except 后对应的是异常类型和一个代码块，用于表明该 except 块处理这种类型的代码块；
-  在多个 except 块之后可以放一个 else 块，表明程序不出现异常时还要执行 else 块；
-  最后还可以跟一个 finally 块，finally 块用于回收在 try 块里打开的物理资源，异常机制会保证 finally 块总被执行；
-  raise 用于引发一个实际的异常，raise 可以单独作为语句使用，引发一个具体的异常对象；

## 2. Python try except else（异常处理）用法详解 



## 3. Python finally：资源回收 



## 4. Python raise用法（超级详细，看了无师自通） 



## 5. Python traceback模块：获取异常信息 



## 6. Python异常机制使用细则，正确使用Python异常处理机制（入门必读 