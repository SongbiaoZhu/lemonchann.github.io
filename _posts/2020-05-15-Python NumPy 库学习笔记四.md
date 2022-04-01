---
layout: post
title: "python NumPy库学习笔记四"
date:   2020-05-15
tags: [python]
toc: true
comments: true
author: Songbiao Zhu
---

Numpy 库学习笔记，第四部分。

## NumPy 字符串函数 

以下函数用于对 dtype 为 numpy.string_ 或 numpy.unicode_ 的数组执行向量化字符串操作。 它们基于 Python 内置库中的标准字符串函数。

这些函数在字符数组类（numpy.char）中定义。

| 函数           | 描述                                       |
| -------------- | ------------------------------------------ |
| `add()`        | 对两个数组的逐个字符串元素进行连接         |
| multiply()     | 返回按元素多重连接后的字符串               |
| `center()`     | 居中字符串                                 |
| `capitalize()` | 将字符串第一个字母转换为大写               |
| `title()`      | 将字符串的每个单词的第一个字母转换为大写   |
| `lower()`      | 数组元素转换为小写                         |
| `upper()`      | 数组元素转换为大写                         |
| `split()`      | 指定分隔符对字符串进行分割，并返回数组列表 |
| `splitlines()` | 返回元素中的行列表，以换行符分割           |
| `strip()`      | 移除元素开头或者结尾处的特定字符           |
| `join()`       | 通过指定分隔符来连接数组中的元素           |
| `replace()`    | 使用新字符串替换字符串中的所有子字符串     |
| `decode()`     | 数组元素依次调用`str.decode`               |
| `encode()`     | 数组元素依次调用`str.encode`               |

* numpy.char.add() 函数依次对两个数组的元素进行字符串连接。
* numpy.char.multiply() 函数执行多重连接。
* numpy.char.center() 函数用于将字符串居中，并使用指定字符在左侧和右侧进行填充。
* numpy.char.capitalize() 函数将字符串的第一个字母转换为大写：
* numpy.char.title() 函数将字符串的每个单词的第一个字母转换为大写：
* numpy.char.lower() 函数对数组的每个元素转换为小写。它对每个元素调用 str.lower。
* numpy.char.upper() 函数对数组的每个元素转换为大写。它对每个元素调用 str.upper。
* numpy.char.split() 通过指定分隔符对字符串进行分割，并返回数组。默认情况下，分隔符为空格。 
* numpy.char.splitlines() 函数以换行符作为分隔符来分割字符串，并返回数组。\n，\r，\r\n 都可用作换行符。
* numpy.char.strip() 函数用于移除开头或结尾处的特定字符。
* numpy.char.join() 函数通过指定分隔符来连接数组中的元素或字符串
* numpy.char.replace() 函数使用新字符串替换字符串中的所有子字符串。
* numpy.char.encode() 函数对数组中的每个元素调用 str.encode 函数。 默认编码是 utf-8，可以使用标准 Python 库中的编解码器。
* numpy.char.decode() 函数对编码的元素进行 str.decode() 解码。

## NumPy 数学函数 

NumPy 提供了标准的三角函数：sin()、cos()、tan()。

arcsin，arccos，和 arctan 函数返回给定角度的 sin，cos 和 tan 的反三角函数。 

numpy.around() 函数返回指定数字的四舍五入值。 

numpy.floor() 返回小于或者等于指定表达式的最大整数，即向下取整。

numpy.ceil() 返回大于或者等于指定表达式的最小整数，即向上取整。 

## NumPy 算术函数 

NumPy 算术函数包含简单的加减乘除: **add()**，**subtract()**，**multiply()** 和 **divide()**。

需要注意的是数组必须具有相同的形状或符合数组广播规则。

* numpy.reciprocal() 函数返回参数逐元素的倒数。如 **1/4** 倒数为 **4/1**。

* numpy.power() 函数将第一个输入数组中的元素作为底数，计算它与第二个输入数组中相应元素的幂。

* numpy.mod() 计算输入数组中相应元素的相除后的余数。 函数 numpy.remainder() 也产生相同的结果。

## NumPy 统计函数 

* numpy.amin() 用于计算数组中的元素沿指定轴的最小值。

* numpy.amax() 用于计算数组中的元素沿指定轴的最大值。

* numpy.ptp()函数计算数组中元素最大值与最小值的差（最大值 - 最小值）。

* numpy.percentile() 表示小于这个值的观察值的百分比。`numpy.percentile(a, q, axis)`

* numpy.median() 函数用于计算数组 a 中元素的中位数（中值）

* numpy.mean() 函数返回数组中元素的算术平均值。 如果提供了轴，则沿其计算。

* numpy.average() 函数根据在另一个数组中给出的各自的权重计算数组中元素的加权平均值。

* numpy.std() 函数 计算一个数组的标准差（标准差是方差的算术平方根）。

## NumPy 排序、条件筛选函数 

* numpy.sort() 函数返回输入数组的排序副本。函数格式如下：
* numpy.argsort() 函数返回的是数组值从小到大的索引值。
* numpy.lexsort() 用于对多个序列进行排序。把它想象成对电子表格进行排序，每一列代表一个序列，排序时优先照顾靠后的列。举一个应用场景：小升初考试，重点班录取学生按照总成绩录取。在总成绩相同时，数学成绩高的优先录取，在总成绩和数学成绩都相同时，按照英语成绩录取…… 这里，总成绩排在电子表格的最后一列，数学成绩在倒数第二列，英语成绩在倒数第三列。
* numpy.argmax() 和 numpy.argmin()函数分别沿给定轴返回最大和最小元素的索引。
* numpy.nonzero() 函数返回输入数组中非零元素的索引。
* numpy.where() 函数返回输入数组中满足给定条件的元素的索引。
* numpy.extract() 函数根据某个条件从数组中抽取元素，返回满条件的元素。

**msort、sort_complex、partition、argpartition**

| 函数                                      | 描述                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| msort(a)                                  | 数组按第一个轴排序，返回排序后的数组副本。np.msort(a) 相等于 np.sort(a, axis=0)。 |
| sort_complex(a)                           | 对复数按照先实部后虚部的顺序进行排序。                       |
| partition(a, kth[, axis, kind, order])    | 指定一个数，对数组进行分区                                   |
| argpartition(a, kth[, axis, kind, order]) | 可以通过关键字 kind 指定算法沿着指定轴对数组进行分区         |

## NumPy 线性代数 

NumPy  提供了线性代数函数库 **linalg**，该库包含了线性代数所需的所有功能，可以看看下面的说明：

| 函数          | 描述                             |
| ------------- | -------------------------------- |
| `dot`         | 两个数组的点积，即元素对应相乘。 |
| `vdot`        | 两个向量的点积                   |
| `inner`       | 两个数组的内积                   |
| `matmul`      | 两个数组的矩阵积                 |
| `determinant` | 数组的行列式                     |
| `solve`       | 求解线性矩阵方程                 |
| `inv`         | 计算矩阵的乘法逆矩阵             |

## NumPy IO 

NumPy 为 ndarray 对象引入了一个简单的文件格式：npy。

npy 文件用于存储重建 ndarray 所需的数据、图形、dtype 和其他信息。

常用的 IO 函数有：

- load() 和 save() 函数是读写文件数组数据的两个主要函数，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 .npy 的文件中。 
- savez() 函数用于将多个数组写入文件，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 .npz 的文件中。 
- loadtxt() 和 savetxt() 函数处理正常的文本文件(.txt 等)