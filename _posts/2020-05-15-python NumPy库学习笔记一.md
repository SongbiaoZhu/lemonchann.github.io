---
layout: post
title: "python NumPy库学习笔记一"
date:   2020-05-15
tags: [python]
toc: true
comments: true
author: Songbiao Zhu
---

Numpy 库学习笔记，第一部分。

<!-- more -->

## 引言

NumPy(Numerical Python) 是 Python 语言的一个扩展程序库，支持大量的维度数组与矩阵运算，此外也针对数组运算提供大量的数学函数库。NumPy 为开放源代码并且由许多协作者共同维护开发。

NumPy ，SciPy， Matplotlib 是python中用于替代matlab 的三剑客。

NumPy 通常与 SciPy（Scientific Python）和 Matplotlib（绘图库）一起使用， 这种组合广泛用于替代 MatLab，是一个强大的科学计算环境，有助于我们通过 Python 学习数据科学或者机器学习。

SciPy 是一个开源的 Python 算法库和数学工具包。

SciPy 包含的模块有最优化、线性代数、积分、插值、特殊函数、快速傅里叶变换、信号处理和图像处理、常微分方程求解和其他科学与工程中常用的计算。

Matplotlib 是 Python 编程语言及其数值数学扩展包 NumPy 的可视化操作界面。它为利用通用的图形用户界面工具包，如 Tkinter, wxPython, Qt 或 GTK+ 向应用程序嵌入式绘图提供了应用程序接口（API）。

本学习笔记的学习内容为[numpy 菜鸟教程](https://www.runoob.com/numpy/numpy-tutorial.html)，菜鸟教程对于我的编程语言学习帮助很大。

## NumPy Ndarray 对象 

NumPy 最重要的对象就是其 N 维数组对象 ndarray，它是一系列同类型数据的集合，以 0 下标为开始进行元素的索引。

创建一个 ndarray 只需调用 NumPy 的 array 函数即可：

```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```

| 名称   | 描述                                                      |
| :----- | :-------------------------------------------------------- |
| object | 数组或嵌套的数列                                          |
| dtype  | 数组元素的数据类型，可选                                  |
| copy   | 对象是否需要复制，可选                                    |
| order  | 创建数组的样式，C为行方向，F为列方向，A为任意方向（默认） |
| subok  | 默认返回一个与基类类型一致的数组                          |
| ndmin  | 指定生成数组的最小维度                                    |

举例

```python

import numpy as np 
a = np.array([1,2,3])  
print (a)
# [1, 2, 3]

a = np.array([[1,  2],  [3,  4]])  
print (a)
#[[1, 2] 
# [3, 4]]

import numpy as np 
a = np.array([1,  2,  3], dtype = complex)  
print (a)
# [ 1.+0.j,  2.+0.j,  3.+0.j]
```

## NumPy 数据类型

numpy 支持的数据类型比 Python 内置的类型要多很多，基本上可以和 C 语言的数据类型对应上，其中部分类型对应为 Python 内置的类型。[详表](https://www.runoob.com/numpy/numpy-dtype.html)列举了常用 NumPy 基本类型。

数据类型对象 (dtype)

## NumPy 数组属性 

NumPy 数组的维数称为秩（rank），即数组的维度，一维数组的秩为 1，二维数组的秩为 2，以此类推。

NumPy 的数组中比较重要 ndarray 对象属性有：

| 属性             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| ndarray.ndim     | 秩，即轴的数量或维度的数量                                   |
| ndarray.shape    | 数组的维度，对于矩阵，n 行 m 列                              |
| ndarray.size     | 数组元素的总个数，相当于 .shape 中 n*m 的值                  |
| ndarray.dtype    | ndarray 对象的元素类型                                       |
| ndarray.itemsize | ndarray 对象中每个元素的大小，以字节为单位                   |
| ndarray.flags    | ndarray 对象的内存信息                                       |
| ndarray.real     | ndarray元素的实部                                            |
| ndarray.imag     | ndarray 元素的虚部                                           |
| ndarray.data     | 包含实际数组元素的缓冲区，由于一般通过数组的索引获取元素，所以通常不需要使用这个属性。 |

## NumPy 创建数组

ndarray 数组除了可以使用底层 ndarray 构造器来创建外，也可以通过以下几种方式来创建。

### numpy.empty

用来创建一个指定形状（shape）、数据类型（dtype）且未初始化的数组

`numpy.empty(shape, dtype = float, order = 'C')`

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| shape | 数组形状                                                     |
| dtype | 数据类型，可选                                               |
| order | 有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |

```python
import numpy as np 
x = np.empty([3,2], dtype = int) 
print (x)

# out
[[ 6917529027641081856  5764616291768666155]
 [ 6917529027641081859 -5764598754299804209]
 [          4497473538      844429428932120]]
```

注意 − 数组元素为随机值，因为它们未初始化。

### numpy.zeros

创建指定大小的数组，数组元素以 0 来填充：

`numpy.zeros(shape, dtype = float, order = 'C')`

| 参数  | 描述                                                |
| :---- | :-------------------------------------------------- |
| shape | 数组形状                                            |
| dtype | 数据类型，可选                                      |
| order | 'C' 用于 C 的行数组，或者 'F' 用于 FORTRAN 的列数组 |

```python

import numpy as np
 
# 默认为浮点数
x = np.zeros(5) 
print(x)
 
# 设置类型为整数
y = np.zeros((5,), dtype = np.int) 
print(y)
 
# 自定义类型
z = np.zeros((2,2), dtype = [('x', 'i4'), ('y', 'i4')])  
print(z)

```

输出结果为

```
[0. 0. 0. 0. 0.]
[0 0 0 0 0]
[[(0, 0) (0, 0)]
 [(0, 0) (0, 0)]]
```

### numpy.ones

创建指定形状的数组，数组元素以 1 来填充：

`numpy.ones(shape, dtype = None, order = 'C')`

## NumPy 从已有的数组创建数组 

主要有三个方法，分别如下：

### numpy.asarray

numpy.asarray 类似 numpy.array，但 numpy.asarray  只有三个参数。可以从列表、列表的元组、多维数组等等生成n维数组。

`numpy.asarray(a, dtype = None, order = None)`

| 参数  | 描述                                                         |
| ----- | ------------------------------------------------------------ |
| a     | 任意形式的输入参数，可以是，列表, 列表的元组, 元组, 元组的元组, 元组的列表，多维数组 |
| dtype | 数据类型，可选                                               |
| order | 可选，有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |

```python
# 将列表转换为 ndarray:
import numpy as np 
x =  [1,2,3] 
a = np.asarray(x)  
print (a)
# out
[1  2  3]

# 将元组转换为 ndarray:
x =  (1,2,3) 
a = np.asarray(x)  
print (a)
# out
[1  2  3]

# 将元组列表转换为 ndarray:
x =  [(1,2,3),(4,5)] 
a = np.asarray(x)  
print (a)
# out
[(1, 2, 3) (4, 5)]
```

### numpy.frombuffer

numpy.frombuffer 用于实现动态数组。numpy.frombuffer 接受 buffer 输入参数，以流的形式读入转化成 ndarray 对象。

`numpy.frombuffer(buffer, dtype = float, count = -1, offset = 0)`

| 参数   | 描述                                     |
| ------ | ---------------------------------------- |
| buffer | 可以是任意对象，会以流的形式读入。       |
| dtype  | 返回数组的数据类型，可选                 |
| count  | 读取的数据数量，默认为-1，读取所有数据。 |
| offset | 读取的起始位置，默认为0。                |

> **注意：**buffer 是字符串的时候，Python3 默认 str 是 Unicode 类型，所以要转成 bytestring 在原 str 前加上 b。

```python
import numpy as np 
 
s =  b'Hello World' 
a = np.frombuffer(s, dtype =  'S1')  
print (a)

# out
[b'H' b'e' b'l' b'l' b'o' b' ' b'W' b'o' b'r' b'l' b'd']
```


### numpy.fromiter

numpy.fromiter 方法从可迭代对象中建立 ndarray 对象，返回一维数组。

`numpy.fromiter(iterable, dtype, count=-1)`

| 参数     | 描述                                   |
| -------- | -------------------------------------- |
| iterable | 可迭代对象                             |
| dtype    | 返回数组的数据类型                     |
| count    | 读取的数据数量，默认为-1，读取所有数据 |

```python

import numpy as np 
 
# 使用 range 函数创建列表对象  
list=range(5)
it=iter(list)
 
# 使用迭代器创建 ndarray 
x=np.fromiter(it, dtype=float)
print(x)

# out
[0. 1. 2. 3. 4.]
```

## NumPy 从数值范围创建数组

### numpy.arange

使用 arange 函数创建数值范围并返回 ndarray 对象，函数格式如下：

`numpy.arange(start, stop, step, dtype)`

| 参数    | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| `start` | 起始值，默认为`0`                                            |
| `stop`  | 终止值（不包含）                                             |
| `step`  | 步长，默认为`1`                                              |
| `dtype` | 返回`ndarray`的数据类型，如果没有提供，则会使用输入数据的类型。 |

```python
import numpy as np
x = np.arange(10,20,2, dtype =  float)  
print (x)
#out
[10.  12.  14.  16.  18.]
```

### numpy.linspace

用于创建一个一维数组，数组是一个等差数列构成的，格式如下：

`np.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)`

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `start`    | 序列的起始值                                                 |
| `stop`     | 序列的终止值，如果`endpoint`为`true`，该值包含于数列中       |
| `num`      | 要生成的等步长的样本数量，默认为`50`                         |
| `endpoint` | 该值为 `true` 时，数列中中包含`stop`值，反之不包含，默认是True。 |
| `retstep`  | 如果为 True 时，生成的数组中会显示间距，反之不显示。         |
| `dtype`    | `ndarray` 的数据类型                                         |

```python
import numpy as np
# 将 endpoint 设为 false，不包含终止值20
a = np.linspace(10, 20,  5, endpoint =  False)
print(a)
[10. 12. 14. 16. 18.]

# 将 endpoint 设为 true，则会包含 20。
a = np.linspace(10, 20,  5, endpoint =  True)
print(a)
[10.  12.5 15.  17.5 20. ]
```

所以从上面的参数含义和例子，可以发现最后生成的等差数列的公差，受endpoint参数的影响。

首先，确定生成的数列的第一个元素，就是 `a1 = start`。然后根据endpoint参数，

* 当endpoint = False时，数列公差为 `d = (stop - start) / (num)`
* 当endpoint = True时，数列公差为 `d = (stop - start) / (num - 1)`

最后计算通项的公式都是，第n （n 从1开始）个数为 `an = start + (n - 1) * d`

### numpy.logspace

用于创建一个于等比数列。格式如下：

`np.logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None)`

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `start`    | 序列的起始值为：base ** start                                |
| `stop`     | 序列的终止值为：base ** stop。如果`endpoint`为`true`，该值包含于数列中 |
| `num`      | 要生成的等步长的样本数量，默认为`50`                         |
| `endpoint` | 该值为 `True` 时，数列中中包含`stop`值，反之不包含，默认是True。 |
| `base`     | 对数 log 的底数。                                            |
| `dtype`    | `ndarray` 的数据类型                                         |

```python
import numpy as np
# 将 endpoint 设为 false
a = np.logspace(0, 9, num = 10, base = 2, endpoint =  False)
print(a)
[  1.           1.86606598   3.48220225   6.49801917  12.12573253
  22.627417    42.22425314  78.79324245 147.03338944 274.37400641]

# 将 endpoint 设为 true
a = np.logspace(0, 9, num = 10, base = 2, endpoint =  True)
print(a)
[  1.   2.   4.   8.  16.  32.  64. 128. 256. 512.]
```

所以从上面的参数含义和例子，可以发现最后生成的等比数列的公比 `q`，受endpoint参数的影响。

以下内容中，**表示次方运算。

首先，确定生成的数列的第一个元素，就是`a1 = base ** start`。然后根据endpoint参数，

- 当endpoint = False时，数列公比为 `q = base ** ((stop - start) / (num))`
- 当endpoint = True时，数列公比为 `q = base ** ((stop - start) / (num - 1))`

最后计算通项的公式都是，第n （n 从1开始）个数为 `an = a1 * (q**(n - 1))`
