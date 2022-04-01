---
layout: post
title: "C中文网python编程基础chapter-4.1-Python列表元组字典和集合详解"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在C语言中文网上，学习了[python编程的基础课程](http://c.biancheng.net/python/)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## **序列详解**

所谓序列，指的是一块可存放多个值的连续内存空间，这些值按一定顺序排列，可通过每个值所在位置的编号（称为索引）访问它们。

在 Python 中，序列类型包括字符串、列表、元组、集合和字典，这些**序列支持以下几种通用的操作**，但比较特殊的是，集合和字典不支持索引、切片、相加和相乘操作。

字符串也是一种常见的序列，它也可以直接通过索引访问字符串内的字符。

 Python 内置四种常用数据结构：列表（list）、元组（tuple）、字典（dict）以及集合（set）。

列表（list）和元组（tuple）比较相似，它们都按顺序保存元素，每个元素都有自己的索引，因此列表和元组都可通过索引访问元素。二者的区别在于元组是不可修改的，但列表是可修改的。

字典（dict）和集合（set）类似，它们存储的数据都是无序的，其中字典是用 `key-value` 的形式保存数据。

### **序列索引**

序列中，每个元素都有属于自己的编号（索引）。从起始元素开始，索引值从 0 开始递增

![img](http://c.biancheng.net/uploads/allimg/190705/2-1ZF5104015S0.gif)

Python 还支持索引值是负数，此类索引是从右向左计数，换句话说，从最后一个元素开始计数，从索引值 -1 开始

![img](http://c.biancheng.net/uploads/allimg/190705/2-1ZF51040251N.gif)

无论是采用正索引值，还是负索引值，都可以访问序列中的任何元素。

```python
str="C语言中文网"
print(str[0],"==",str[-6])
print(str[5],"==",str[-1])
```

输出结果为：

```python
C == C
网 == 网
```

### **序列切片**

切片操作是访问序列中元素的另一种方法，它可以**访问一定范围内的元素**，通过切片操作，可以**生成一个新的**序列。
序列实现切片操作的语法格式如下：

```python
sname[start : end : step]
```

其中，各个参数的含义分别是： 

-  sname：表示序列的名称；
-  start：表示切片的**开始索引位置（包括该位置）**，此参数也可以不指定，会**默认为 0**，也就是从序列的开头进行切片；
-  end：表示切片的**结束索引位置（不包括该位置）**，如果不指定，则**默认为序列的长度**；
-  step：表示在切片过程中，隔几个存储位置（包含当前位置）取一次元素，也就是说，如果 step 的值大于 1，则在进行切片去序列元素时，会“跳跃式”的取元素。**如果省略设置 step 的值，则最后一个冒号就可以省略**。

```python
str="C语言中文网"
#取索引区间为[0,2]之间（不包括索引2处的字符）的字符串
print(str[:2])
#隔 1 个字符取一个字符，区间是整个字符串
print(str[::2])
#取整个字符串，此时 [] 中只需一个冒号即可
print(str[:])
```

```python
C语
C言文
C语言中文网
```

### **序列相加**

Python 中，支持两种类型相同的序列使用“+”运算符做相加，它会将两个序列进行连接，但不会去除重复的元素。

“类型相同”，指的是“+”运算符的两侧序列要么都是序列类型，要么都是元组类型，要么都是字符串。

```
str="c.biancheng.net"
print("C语言"+"中文网:"+str)
```

### **序列相乘**

Python 中，使用数字 n 乘以一个序列会生成新的序列，其内容为原来序列被重复 n 次的结果。

```python
str="C语言中文网"
print(str*3)
```

比较特殊的是，列表类型在进行乘法运算时，还可以实现初始化指定长度列表的功能。例如如下的代码，将创建一个长度为 5 的列表，列表中的每个元素都是 None，表示什么都没有。

```python
#列表的创建用 []，后续讲解列表时会详细介绍
list = [None]*5
print(list)
```

```python
[None, None, None, None, None]
```

### **检查元素是否包含在序列中**

Python 中，可以使用 in 关键字检查某元素是否为序列的成员，其语法格式为：

```python
value in sequence
```

```python
str="c.biancheng.net"
print('c'in str)
```

```python
True
```

```python
str="c.biancheng.net"
print('c' not in str)
```

```python
False
```

### **和序列相关的内置函数**

| 函数        | 功能                                                         |
| ----------- | ------------------------------------------------------------ |
| len()       | 计算序列的长度，即返回序列中包含多少个元素。                 |
| max()       | 找出序列中的最大元素。注意，对序列使用 sum() 函数时，做加和操作的必须都是数字，不能是字符或字符串，否则该函数将抛出异常，因为解释器无法判定是要做连接操作（+ 运算符可以连接两个序列），还是做加和操作。 |
| min()       | 找出序列中的最小元素。                                       |
| list()      | 将序列转换为列表。                                           |
| str()       | 将序列转换为字符串。                                         |
| sum()       | 计算元素和。                                                 |
| sorted()    | 对元素进行排序。                                             |
| reversed()  | 反向序列中的元素。                                           |
| enumerate() | 将序列组合为一个索引序列，多用在 for 循环中。                |

```python
str="c.biancheng.net"
#找出最大的字符
print(max(str))
#找出最小的字符
print(min(str))
#对字符串中的元素进行排序
print(sorted(str))
```

```python
t
.
['.', '.', 'a', 'b', 'c', 'c', 'e', 'e', 'g', 'h', 'i', 'n', 'n', 'n', 't']
```

## **list列表详解**

```python
[element1,element2,element3,...,elementn]

```

格式中，element1~elementn 表示列表中的元素，个数没有限制，在同一个列表中元素的类型也可以不同。但**通常**情况下不这么做，**同一列表中只放入同一类型的数据**，这样可以提高程序的可读性。

```python
#创建列表 用等号
listname = [element1 , element2 , element3 , ... , elementn]
#创建空列表
emptylist = []

#创建列表 用list()函数
# 使用range()函数创建区间（range）对象
a_range = range(1, 5)
# 将区间转换成列表
b_list = list(a_range)
print(b_list)

# 访问列表元素，通过索引或切片
num = [1,2,3,4,5,6,7]
print(num[1])
print(num[2:4])

# 删除列表，使用 del 语句将其删除
del listname
```

### **list添加元素，用append()方法**

其中，listname 指的是要添加元素的列表；obj 表示到添加到列表末尾的数据，它可以是单个元素，也可以是列表、元组等。

```python
listname.append(obj)
```

```python
a_list = ['crazyit', 20, -2]
# 追加元素
a_list.append('fkit')
print(a_list)
a_tuple = (3.4, 5.6)
# 追加元组，元组被当成一个元素
a_list.append(a_tuple)
print(a_list)
# 追加列表，列表被当成一个元素
a_list.append(['a', 'b'])
print(a_list)
```

可以发现，即便给 append() 方法传递列表或者元组，此方法也只会将其视为一个元素，直接添加到列表中，从而形成包含列表和元组的新列表。

### **list添加元素，用extend()方法**

如果希望不将被追加的列表或元组当成一个整体，而是只追加列表中的元素，则可使用列表提供的 extend() 方法。extend()方法的语法格式如下：

```python
listname.extend(obj)
```

```python
b_list = ['a', 30]
# 追加元组中的所有元素
b_list.extend((-2, 3.1))
print(b_list)
# 追加列表中的所有元素
b_list.extend(['C', 'R', 'A'])
print(b_list)
# 追加区间中的所有元素
b_list.extend(range(97, 100))
print(b_list)
```

```python
['a', 30, -2, 3.1]
['a', 30, -2, 3.1, 'C', 'R', 'A']
['a', 30, -2, 3.1, 'C', 'R', 'A', 97, 98, 99]
```

### **list添加元素，用insert()方法**

如果希望在列表中间增加元素，则可使用列表的 insert() 方法，此方法的语法格式为：

```python
listname.insert(index , obj)
```

其中，index 参数指的是将元素插入到列表中指定位置处的索引值。

使用 insert() 方法向列表中插入元素，和 append() 方法一样，无论插入的对象是列表还是元组，都只会将其整体视为一个元素。

```python
c_list = list(range(1, 6))
print(c_list)
# 在索引3处插入字符串
c_list.insert(3, 'CRAZY' )
print(c_list)
# 在索引3处插入列表
c_list.insert(3, ["crazy"])
print(c_list)
```

```python
[1, 2, 3, 4, 5]
[1, 2, 3, 'CRAZY', 4, 5]
[1, 2, 3, ['crazy'], 'CRAZY', 4, 5]
```

### **list删除元素**

在列表中删除元素，主要分为以下 3 种应用场景： 

1.  根据目标元素所在位置的索引值进行删除，可使用 del 语句；
2.  根据元素的值进行删除，可使用列表（list类型）提供的 remove() 方法；
3.  将列表中所有元素全部删除，可使用列表（list类型）提供的 clear() 方法。

```python
# 指定删除最后一个元素
a_list=[20,2.4,(3,4)]
del a_list[-1]
print(a_list)
# [20, 2.4]

# 删除列表的中间一段
a_list = ['crazyit', 20, -2.4, (3, 4), 'fkit']
# 删除第2个到第4个（不包含）元素
del a_list[1: 3]
print(a_list)
# ['crazyit', (3, 4), 'fkit']

# 根据元素值进行删除
# remove() 方法会删除第一个和指定值相同的元素，如果找不到该元素，该方法将会引发 ValueError 错误。
c_list = [20, 'crazyit', 30, -4, 'crazyit', 3.4]
# 删除第一次找到的30
c_list.remove(30)
print(c_list)
# 删除第一次找到的'crazyit'
c_list.remove('crazyit')
print(c_list)
#再次尝试删除 30，会引发 ValueEroor 错误
c_list.remove(30)

# 删除列表所有元素
c_list = [20, 'crazyit', 30, -4, 'crazyit', 3.4]
c_list.clear()
print(c_list)
# []
```

### **list修改元素**

列表的元素相当于变量，因此程序可以对列表的元素赋值，这样即可修改列表的元素，所以有两种类型，按索引修改单个元素，或者按slice语法修改多个元素。

slice语法不要求新赋值的元素个数与原来的元素个数相等。这意味着通过这种方式既可为列表增加元素，也可为列表删除元素。

对列表使用 slice 语法赋值时，不能使用单个值；如果使用字符串赋值，[Python](http://c.biancheng.net/python/) 会自动把字符串当成序列处理，其中每个字符都是一个元素。

在使用 slice 语法赋值时，也可指定 step 参数。但如果指定了 step 参数，则要求所赋值的列表元素个数与所替换的列表元素个数相等。

```python
a_list = [2, 4, -3.4, 'crazyit', 23]
# 对第3个元素赋值
a_list[2] = 'fkit'
print(a_list) # [2, 4, 'fkit', 'crazyit', 23]
# 对倒数第2个元素赋值
a_list[-2] = 9527
print(a_list) # [2, 4, 'fkit', 9527, 23]

b_list = list(range(1, 5))
print(b_list)
# 将第2个到第4个（不包含）元素赋值为新列表的元素
b_list[1: 3] = ['a', 'b']
print(b_list) # [1, 'a', 'b', 4]

# 将第3个到第3个（不包含）元素赋值为新列表的元素，就是插入
b_list[2: 2] = ['x', 'y']
print(b_list) # [1, 'a', 'x', 'y', 'b', 4]

# 将第3个到第6个（不包含）元素赋值为空列表，就是删除
b_list[2: 5] = []
print(b_list) # [1, 'a', 4]

# Python会自动将str分解成序列
b_list[1: 3] = 'Charlie'
print(b_list) # [1, 'C', 'h', 'a', 'r', 'l', 'i', 'e']

c_list = list(range(1, 10))
# 指定step为2，被赋值的元素有4个，因此用于赋值的列表也必须有4个元素
c_list[2: 9: 2] = ['a', 'b', 'c', 'd']
print(c_list) # [1, 2, 'a', 4, 'b', 6, 'c', 8, 'd']
```

### **list常用方法速查**

在交互式解释器中输入 dir(list) 即可看到列表包含的所有方法，如下所示：

```python
>>> dir(list)
['append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

```python
# count()方法，用于统计列表中某个元素出现的次数，其格式为： listname.count(obj)
a_list = [2, 30, 'a', [5, 30], 30]
# 计算列表中30的出现次数
print(a_list.count(30))
# 计算列表中[5, 30]的出现次数
print(a_list.count([5, 30]))

# index()用法，用于定位某个元素在列表中出现的位置（也就是索引），其格式为：listname.index(obj,start,end)，可传入 start、end 参数，用于在列表的指定范围内搜索元素
a_list = [2, 30, 'a', 'b', 'crazyit', 30]
# 定位元素30的出现位置
print(a_list.index(30))
# 从索引2处开始、定位元素30的出现位置，注意给出的索引值还是基于原来的list索引序列的。
print(a_list.index(30, 2)) 
# 从索引2处到索引4处之间定位元素30的出现位置，因为找不到该元素，会引发 ValueError 错误
print(a_list.index(30, 2, 4))

# pop() 方法，用于移除列表中指定索引处的元素，如果不指定，默认会移除列表中最后一个元素。其格式为：listname.pop(index)
a_list=[1,2,3]
# 移除列表的元素 3，且该方法会返回移出的元素 3
a_list.pop()
a_list
# 移除列表中索引为 0 的元素1，且该方法会返回移出的元素 1
a_list.pop(0)
a_list

# reverse()用法，用于将列表中所有元素反向存放。listname.reverse()
a_list = list(range(1, 8))
# 将a_list列表元素反转
a_list.reverse()
print(a_list)

# sort()用法，用于对列表元素进行排序。listname.sort(key=None, reserse=False)
# key 参数用于指定从每个元素中提取一个用于比较的键。
# reverse 参数用于设置是否需要反转排序，默认 False 表示从小到大排序

a_list = [3, 4, -2, -30, 14, 9.3, 3.4]
# 对列表元素排序
a_list.sort()
print(a_list)
b_list = ['Python', 'Swift', 'Ruby', 'Go', 'Kotlin', 'Erlang']
# 对列表元素排序：默认按字符串包含的字符的编码大小比较，即字母顺序
b_list.sort()
print(b_list) # ['Erlang', 'Go', 'Kotlin', 'Python', 'Ruby', 'Swift']
# 如下代码示范了 key 和 reverse 参数的用法：
b_list = ['Python', 'Swift', 'Ruby', 'Go', 'Kotlin', 'Erlang']
# 指定key为len，指定使用len函数对集合元素生成比较的键，也就是按字符串的长度比较大小
b_list.sort(key=len)
print(b_list)
# 指定反向排序
b_list.sort(key=len, reverse=True)
print(b_list)
```

## **元组tuple**

元组可以看做是不可变的列表。通常情况下，元组用于保存不可修改的内容。

从形式上看，元组的所有元素都放在一对小括号“()”中，相邻元素之间用逗号“,”分隔，如下所示：

```
(element1, element2, ... , elementn)
```

### **创建元组**
创建元组的语法和创建列表的语法非常相似，唯一的不同在于，创建列表使用的是 []，而创建元组使用的是 ()。
在 Python 中，元组通常都是使用一对小括号将所有元素括起来的，但小括号不是必须的，只要将各元素用逗号隔开，Python 就会将其视为元组。
使用tuple()函数创建元组，tuple(data)，data 表示可以转化为元组的数据，其类型可以是字符串、元组、range 对象等。
```python
# 创建元组，用等号
num = (7,14,21,28,35)
a_tuple = ("C语言中文网","http://c.biancheng.net")
python = ("Python",19,[1,2],('c',2.0))

# 创建元组，可以省略小括号
a_tuple = "C语言中文网","http://c.biancheng.net"
print(a_tuple)

# 将列表转换成元组
a_list = ['crazyit', 20, -1.2]
a_tuple = tuple(a_list)
print(a_tuple)

# 将区间转换成元组
a_range = range(1, 5)
b_tuple = tuple(a_range)
print(b_tuple)
```

### **访问元组元素**
和列表完全一样。

### **修改元组元素**
元组也不是完全不能修改。
```python
# 可以对元组进行重新赋值
a_tuple = ('crazyit', 20, -1.2)
print(a_tuple)
#对元组进行重新赋值
a_tuple = ('c.biancheng.net',"C语言中文网")
print(a_tuple)
```
### **删除元组**
```python
a_tuple = ('crazyit', 20, -1.2)
print(a_tuple)
#删除a_tuple元组
del(a_tuple)
print(a_tuple)
```
在实际开发中，del() 语句并不常用，因为 Python 自带的垃圾回收机制会自动销毁不用的元组或列表。

## **元组和列表的区别**

元组和列表最大的区别就是，列表中的元素可以进行任意修改，而元组中的元素无法修改，除非将元组整体替换掉。

虽然看起来，元组确实没有列表那么多功能，但是元组依旧是很重要的序列类型之一，元组的不可替代性体现在以下这些场景中：

-  元组作为很多内置函数和序列类型方法的返回值存在，也就是说，在使用某些函数或者方法时，它的返回值会元组类型，因此你必须对元组进行处理。
-  元组比列表的访问和处理速度更快，因此，当需要对指定元素进行访问，且不涉及修改元素的操作时，建议使用元组。
-  元组可以在映射（和集合的成员）中当做“键”使用，而列表不行。