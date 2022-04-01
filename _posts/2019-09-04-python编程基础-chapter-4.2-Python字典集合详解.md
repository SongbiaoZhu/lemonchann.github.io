---
layout: post
title: "C中文网python编程基础chapter-4.2-Python字典集合详解"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在C语言中文网上，学习了[python编程的基础课程](http://c.biancheng.net/python/)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## 字典(dict)

和列表相同，字典也是许多数据的集合，属于可变序列类型。不同之处在于，它是无序的可变序列，其保存的内容是以“键值对”的形式存放的。

字典类型是 Python 中唯一的映射类型。即通过一个元素，可以唯一找到另一个元素。

字典中，习惯将各元素对应的索引称为键（key），各个键对应的元素称为值（value），键及其关联的值称为“键值对”。

| 主要特征                       | 解释                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| 通过键而不是通过索引来读取元素 | 字典类型有时也称为关联数组或者散列表（hash）。它是通过键将一系列的值联系起来的，这样就可以通过键从字典中获取指定项，但不能通过索引来获取。 |
| 字典是任意数据类型的无序集合   | 和列表、元组不同，通常会将索引值 0 对应的元素称为第一个元素。而字典中的元素是无序的。 |
| 字典是可变的，并且可以任意嵌套 | 字典可以在原处增长或者缩短（无需生成一个副本），并且它支持任意深度的嵌套，即字典存储的值也可以是列表或其它的字典。 |
| 字典中的键必须唯一             | 字典中，不支持同一个键出现多次，否则，只会保留最后一个键值对。 |
| 字典中的键必须不可变           | 字典中的键是不可变的，只能使用数字、字符串或者元组，不能使用列表。 |

## 创建字典

### 1) 花括号语法创建字典

```python
dictname = {'key':'value1','key2':'value2',...,'keyn':valuen}
```

```python
scores = {'语文': 89, '数学': 92, '英语': 93}
print(scores)
# 空的花括号代表空的dict
empty_dict = {}
print(empty_dict)
# 使用元组作为dict的key
dict2 = {(20, 30):'good', 30:[1,2,3]}
print(dict2)
```

可以看到，同一字典中，键值可以是整数、字符串或者元组，只要符合唯一和不可变的特性；对应的值可以是 Python 支持的任意数据类型。

### 2) 通过 fromkeys() 方法创建字典

使用 dict 字典类型提供的 fromkeys() 方法创建所有键值为空的字典，使用此方法的语法格式为：

```python
 dictname = dict.fromkeys(list，value=None)
```

其中，list 参数表示字典中所有键的列表，value 参数默认为 None，表示所有键对应的值。

```python
knowledge = {'语文', '数学', '英语'}
scores = dict.fromkeys(knowledge)
print(scores)
```

###  3) 通过 dict() 映射函数创建字典

通过 dict() 函数创建字典的写法有多种，表 2 罗列出了常用的几种方式，它们创建的都是同一个字典 a。

| 创建格式                                                     | 注意事项                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| a = dict(one=1,two=2,three=3)                                | 注意，其中的 one、two、three 都是字符串，但使用此方式创建字典时，字符串不能带引号。 |
| demo = [('two',2),('one',1),('three',3)] #方式1<br/>demo = [['two',2],['one',1],['three',3]] #方式2<br/>demo = (('two',2),('one',1),('three',3)) #方式3<br/>demo = (['two',2],['one',1],['three',3]) #方式4<br/>a = dict(demo) | 向 dict() 函数传入列表或元组，而它们中的元素又各自是包含 2 个元素的列表或元组，其中第一个元素作为键，第二个元素作为值。（左侧示例表示元组的列表、或者列表的元组都可以经dict转为字典） |
| demokeys = ['one','two','three'] #还可以是字符串或元组<br/>demovalues = [1,2,3] #还可以是字符串或元组<br/>a = dict(zip(demokeys,demovalues)) | 通过应用 dict() 函数和 zip() 函数，可将前两个列表转换为对应的字典。 |

```python
# 创建空的字典
dict5 = dict()
print(dict5)
```

注意，无论采用以上哪种方式创建字典，字典中各元素的键都只能是字符串、元组或数字，不能是列表。

## 访问字典

和列表、元组不同，它们访问元素都是通过下标，而字典不同，它是通过键来访问对应的元素值。

因为字典中元素是无序的，所以不能像列表、元组那样，采用切片的方式一次性访问多个元素。

```python
a = dict(one=1,two=2,three=3)
# 获取指定键的值
>>> a['one']
1

# 更推荐使用 dict 类型提供的 get() 方法获取指定键的值。
# dict.get(key[,default])
# 其中，dict 指的是所创建的字典名称；key 表示指定的键；default 用于指定要查询的键不存在时，此方法返回的默认值，如果不手动指定，会返回 None。
>>>a.get('two')
2
# 在使用 get() 方法时，可以为其设置默认值，这样，即便指定的键不存在，也不回报错。
>>> a.get('four','字典中无此键')
'字典中无此键'
```

## 删除字典

和删除列表、元组一样，手动删除字典也可以使用 del 语句。例如：

```python
a = dict(one=1,two=2,three=3)
del(a)
```

## 字典基本操作（添加、修改、删除）

key 是字典的关键数据，字典的基本操作都是围绕 key 值实现的。

常见的字典操作有以下几种：

1.  向现有字典中添加新的键值对。
2.  修改现有字典中的键值对。
3.  从现有字典中删除指定的键值对。
4.  判断现有字典中是否存在指定的键值对。

### 添加键值对

为 dict 添加键值对，只需为不存在的 key 赋值即可。实现此操作的语法格式如下：

```python
 dict[key] = value
```

### 修改键值对

修改键值对”并不是同时修改某一键值对的键和值，而只是修改某一键值对中的值。

由于在字典中，各元素的键必须是唯一的，因此，如果新添加元素的键与已存在元素的键相同，原来键所对应的值就会被新的值替换掉，就是修改的效果。例如：

```
a = {'数学': 95, '语文': 89, '英语': 90}
a['语文']=100
print(a)
```

### 删除键值对

要删除字典中的键值对，还是可以使用 del 语句。例如：

```
# 使用del语句删除键值对
a = {'数学': 95, '语文': 89, '英语': 90}
del a['语文']
del a['数学']
print(a)
```

### 判断字典中是否存在指定键值对

判断字典是否包含指定键值对的**键**，可以使用 in 或 not in 运算符。

对于 dict 而言，in 或 not in 运算符都是**基于 key **来判断的。

```
a = {'数学': 95, '语文': 89, '英语': 90}
# 判断 a 中是否包含名为'数学'的key
print('数学' in a) # True
# 判断 a 是否包含名为'物理'的key
print('物理' in a) # False
```

通过 in（或 not in）运算符，我们可以很轻易地判断出现有字典中是否包含某个键，如果存在，由于通过键可以很轻易的获取对应的值，因此很容易就能判断出字典中是否有指定的键值对。

## dict字典方法速查

字典的数据类型为 dict，我们可使用 `dir(dict)` 来查看该类包含哪些方法。在交互式解释器中输入 `dir(dict)` 命令，将看到如下输出结果：

```
>>> dir(dict)
['clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']
```

### keys()、values() 和 items()方法

这 3 个方法都是用来获取字典中的特定数据。

keys() 方法用于返回字典中的所有键；values() 方法用于返回字典中所有键对应的值；items() 用于返回字典中所有的键值对。

```
a = {'数学': 95, '语文': 89, '英语': 90}
print(a.keys())
print(a.values())
print(a.items())
```

输出为

```
dict_keys(['数学', '语文', '英语'])
dict_values([95, 89, 90])
dict_items([('数学', 95), ('语文', 89), ('英语', 90)])
```

然后如果想操作返回的查询值，

```
# 使用 list() 函数，将它们返回的数据转换成列表，例如： 
a = {'数学': 95, '语文': 89, '英语': 90}
b = list(a.keys())
print(b)

# 利用多重赋值的技巧，利用循环结构将键或值分别赋给不同的变量，比如说： 
a = {'数学': 95, '语文': 89, '英语': 90}
for k in a.keys():
    print(k,end=' ')
print("\n---------------")
for v in a.values():
    print(v,end=' ')
print("\n---------------")
for k,v in a.items():
    print("key:",k," value:",v)
```

输出为

```
['数学', '语文', '英语']

数学 语文 英语
---------------
95 89 90
---------------
key: 数学  value: 95
key: 语文  value: 89
key: 英语  value: 90
```

### copy()方法

copy() 方法用于返回一个具有相同键值对的新字典，例如：

```
a = {'one': 1, 'two': 2, 'three': [1,2,3]}
b = a.copy()
print(b)
```

### update()方法

update() 方法可使用一个字典所包含的键值对来更新己有的字典。

在执行 update() 方法时，如果被更新的字典中己包含对应的键值对，那么原 value 会被覆盖；如果被更新的字典中不包含对应的键值对，则该键值对被添加进去。

```
a = {'one': 1, 'two': 2, 'three': 3}
a.update({'one':4.5, 'four': 9.3})
print(a)
# 运行结果为：
{'one': 4.5, 'two': 2, 'three': 3, 'four': 9.3}
```

### pop方法

pop() 方法用于获取指定 key 对应的 value，并删除这个键值对。

```
a = {'one': 1, 'two': 2, 'three': 3}
print(a.pop('one'))
print(a)
# 运行结果为： 
1
{'two': 2, 'three': 3}
```

### popitem()方法

popitem() 方法用于随机弹出字典中的一个键值对。

注意，此处的**随机其实是假的**，它和 list.pop() 方法一样，也是弹出字典中最后一个键值对。但由于字典存储键值对的顺序是不可知的，因此 popitem() 方法总是弹出**底层存储的最后一个键值对**。

```
a = {'one': 1, 'two': 2, 'three': 3}
print(a)
# 弹出字典底层存储的最后一个键值对
print(a.popitem())
print(a)
# 运行结果为： 
{'one': 1, 'two': 2, 'three': 3}
('three', 3)
{'one': 1, 'two': 2}
```

实际上，由于 popitem 弹出的是一个元组，因此我们也可以通过序列解包的方式，用两个变量分别接收 key 和 value。

```
a = {'one': 1, 'two': 2, 'three': 3}
# 将弹出项的key赋值给k、value赋值给v
k, v = a.popitem()
print(k, v)
# 运行结果为： 
three 3
```

### setdefault()方法

setdefault() 方法总能返回指定 key 对应的 value；如果该键值对存在，则直接返回该 key 对应的 value；如果该键值对不存在，则先为该 key 设置默认的 value，然后再返回该 key 对应的 value。

```
a = {'one': 1, 'two': 2, 'three': 3}
# 设置默认值，该key在dict中不存在，新增键值对
print(a.setdefault('four', 9.2))
print(a)
# 设置默认值，该key在dict中存在，不会修改dict内容
print(a.setdefault('one', 3.4))
print(a)
# 运行结果为： 
9.2
{'one': 1, 'two': 2, 'three': 3, 'four': 9.2}
1
{'one': 1, 'two': 2, 'three': 3, 'four': 9.2}
```

## 使用字典格式化字符串

可以使用字典对字符串进行格式化输出，具体方法是：在字符串模板中按 key 指定变量，然后通过字典为字符串模板中的 key 设置值。

```
# 字符串模板中使用key
temp = '教程是:%(name)s, 价格是:%(price)010.2f, 出版社是:%(publish)s'
book = {'name':'Python基础教程', 'price': 99, 'publish': 'C语言中文网'}
# 使用字典为字符串模板中的key传入值
print(temp % book)
book = {'name':'C语言小白变怪兽', 'price':159, 'publish': 'C语言中文网'}
# 使用字典为字符串模板中的key传入值
print(temp % book)
```

运行上面程序，可以看到如下输出结果：

```
教程是:Python基础教程, 价格是:0000099.00, 出版社是:C语言中文网
教程是:C语言小白变怪兽, 价格是:0000159.00, 出版社是:C语言中文网
```

## set集合详解

Python 中的集合，和数学中的集合概念一样，用来保存不重复的元素，即集合中的元素都是唯一的，互不相同。

从形式上看，和字典类似，Python 集合会将所有元素放在一对大括号 {} 中，相邻元素之间用“,”分隔，如下所示：

```
{element1,element2,...,elementn}
```

其中，elementn 表示集合中的元素，个数没有限制。
从内容上看，同一集合中，只能存储不可变的数据类型，包括整形、浮点型、字符串、元组。

无法存储列表、字典、集合这些可变的数据类型。

并且需要注意的是，数据必须保证是唯一的，因为集合对于每种数据元素，只会保留一份。

Python 中的 set 集合是无序的，所以每次输出时元素的排序顺序可能都不相同。

Python 中有两种集合类型，一种是 set 类型的集合，另一种是 frozenset 类型的集合，它们唯一的区别是，set 类型集合可以修改，而 forzenset 类型集合不能修改。

## 创建set集合

### 1) 使用 {} 创建

```
a = {1,'c',1,(1,2,3),'c'}
print(a)
```

### 2) set()函数创建集合

set() 函数为 Python 的内置函数，其功能是将字符串、列表、元组、range 对象等可迭代对象转换成集合。

```
# 语法 setname = set(iteration)
# 其中，iteration 就表示字符串、列表、元组、range 对象等数据。
set1 = set("c.biancheng.net")
set2 = set([1,2,3,4,5])
set3 = set((1,2,3,4,5))
print("set1:",set1)
print("set2:",set2)
print("set3:",set3)
# 运行结果为： 
set1: {'a', 'g', 'b', 'c', 'n', 'h', '.', 't', 'i', 'e'}
set2: {1, 2, 3, 4, 5}
set3: {1, 2, 3, 4, 5}
```

## 访问set集合元素

由于集合中的元素是无序的，因此无法向列表那样使用下标访问元素。Python 中，访问集合元素最常用的方法是使用循环结构，将集合中的数据逐一读取出来。

```
a = {1,'c',1,(1,2,3),'c'}
for ele in a:
    print(ele,end=' ')
# 运行结果为:
1 c (1, 2, 3)
```

## 删除set集合

和其他序列类型一样，手动函数集合类型，也可以使用 del() 语句。

## set集合基本操作

### 向 set 集合中添加元素

set 集合中添加元素，可以使用 set 类型提供的 add() 方法实现，该方法的语法格式为：

```
setname.add(element)
```

其中，setname 表示要添加元素的集合，element 表示要添加的元素内容。
需要注意的是，使用 add() 方法添加的元素，只能是数字、字符串、元组或者布尔类型（True 和 False）值，不能添加列表、字典、集合这类可变的数据，否则 Python 解释器会报 TypeError 错误。

### 从set集合中删除元素

删除现有 set 集合中的指定元素，可以使用 remove() 方法，该方法的语法格式如下：

```
setname.remove(element)
```

使用此方法删除集合中元素，需要注意的是，如果被删除元素本就不包含在集合中，则此方法会抛出 KeyError 错误。

如果我们不想在删除失败时令解释器提示 KeyError 错误，还可以使用 discard() 方法，此方法和 remove() 方法的用法完全相同，唯一的区别就是，当删除集合中元素失败时，此方法不会抛出任何错误。

```
a = {1,2,3}
a.remove(1)
print(a)
a.remove(1)
print(a)
a.discard(1)
print(a)
```

### set集合做交集、并集、差集运算

有 2 个集合，分别为 set1={1,2,3} 和 set2={3,4,5}

| 运算操作 | Python运算符 | 含义                              | 例子                                           |
| -------- | ------------ | --------------------------------- | ---------------------------------------------- |
| 交集     | &            | 取两集合公共的元素                | >>> set1 & set2  {3}                           |
| 并集     | \|           | 取两集合全部的元素                | >>> set1 \| set2  {1,2,3,4,5}                  |
| 差集     | -            | 取一个集合中另一集合没有的元素    | >>> set1 - set2  {1,2}  >>> set2 - set1  {4,5} |
| 对称差集 | ^            | 取集合 A 和 B 中不属于 A&B 的元素 | >>> set1 ^ set2  {1,2,4,5}                     |

### set集合方法速查

```
>>> dir(set)
['add', 'clear', 'copy', 'difference', 'difference_update', 'discard', 'intersection', 'intersection_update', 'isdisjoint', 'issubset', 'issuperset', 'pop', 'remove', 'symmetric_difference', 'symmetric_difference_update', 'union', 'update']
```

| 方法名                | 语法格式                       | 功能                                                         | 实例                                                         |
| --------------------- | ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| add()                 | set1.add()                     | 向 set1 集合中添加数字、字符串、元组或者布尔类型             | >>> set1 = {1,2,3}  >>> set1.add((1,2))  >>> set1  {(1, 2), 1, 2, 3} |
| clear()               | set1.clear()                   | 清空 set1 集合中所有元素                                     | >>> set1 = {1,2,3}  >>> set1.clear()  >>> set1  set()    set()才表示空集合，{}表示的是空字典 |
| copy()                | set2 = set1.copy()             | 拷贝 set1 集合给 set2                                        | >>> set1 = {1,2,3}  >>> set2 = set1.copy()  >>> set1.add(4)  >>> set1  {1, 2, 3, 4}  >>> set1  {1, 2, 3} |
| difference()          | set3 = set1.difference(set2)   | 将 set1 中有而 set2 没有的元素给 set3                        | >>> set1 = {1,2,3}  >>> set2 = {3,4}  >>> set3 = set1.difference(set2)  >>> set3  {1, 2} |
| difference_update()   | set1.difference_update(set2)   | 从 set1 中删除与 set2 相同的元素                             | >>> set1 = {1,2,3}  >>> set2 = {3,4}  >>> set1.difference_update(set2)  >>> set1  {1, 2} |
| discard()             | set1.discard(elem)             | 删除 set1 中的 elem 元素                                     | >>> set1 = {1,2,3}  >>> set1.discard(2)  >>> set1  {1, 3}  >>> set1.discard(4)  {1, 3} |
| intersection()        | set3 = set1.intersection(set2) | 取 set1 和 set2 的交集给 set3                                | >>> set1 = {1,2,3}  >>> set2 = {3,4}  >>> set3 = set1.intersection(set2)  >>> set3  {3} |
| intersection_update() | set1.intersection_update(set2) | 取 set1和 set2 的交集，并更新给 set1                         | >>> set1 = {1,2,3}  >>> set2 = {3,4}  >>> set1.intersection_update(set2)  >>> set1  {3} |
| isdisjoint()          | set1.isdisjoint(set2)          | 判断 set1 和 set2 是否没有交集，有交集返回 False；没有交集返回 True | >>> set1 = {1,2,3}  >>> set2 = {3,4}  >>> set1.isdisjoint(set2)  False |
| issubset()            | set1.issubset(set2)            | 判断 set1 是否是 set2 的子集                                 | >>> set1 = {1,2,3}  >>> set2 = {1,2}  >>> set1.issubset(set2)  False |
| issuperset()          | set1.issuperset(set2)          | 判断 set2 是否是 set1 的子集                                 | >>> set1 = {1,2,3}  >>> set2 = {1,2}  >>> set1.issuperset(set2)  True |
| pop()                 | a = set1.pop()                 | 取 set1 中一个元素，并赋值给 a                               | >>> set1 = {1,2,3}  >>> a = set1.pop()  >>> set1  {2,3}  >>> a  1 |
| remove()              | set1.remove(elem)              | 移除 set1 中的 elem 元素                                     | >>> set1 = {1,2,3}  >>> set1.remove(2)  >>> set1  {1, 3}  >>> set1.remove(4)  Traceback (most recent call last):    File "<pyshell#90>", line 1, in <module>      set1.remove(4)  KeyError: 4 |

所有函数功能介绍请查看详细[detail](http://c.biancheng.net/view/4402.html)

## frozenset集合

frozenset 是 set 的不可变版本，因此 set 集合中所有能改变集合本身的方法（如 add、remove、discard、xxx_update 等），frozenset 都不支持；set 集合中不改变集合本身的方法，fronzenset 都支持。

```
>>> dir(frozenset)
['copy', 'difference', 'intersection', 'isdisjoint', 'issubset', 'issuperset', 'symmetric_difference', 'union']
```

frozenset 的作用主要有两点： 

1.  当集合元素不需要改变时，使用 frozenset 代替 set 更安全。
2.  当某些 API 需要不可变对象时，必须用 frozenset 代替set。比如 dict 的 key 必须是不可变对象，因此只能用  frozenset；再比如 set 本身的集合元素必须是不可变的，因此 set 不能包含 set，set 只能包含 frozenset。

如下程序示范了在 set 中添加 frozenset：

```
s = set()
#创建 frozenset 不可变集合，使用 frozenset() 函数
frozen_s = frozenset('Kotlin')
# 为set集合添加frozenset
s.add(frozen_s)
print('s集合的元素：', s)
sub_s = {'Python'}
# 为set集合添加普通set集合，程序报错
s.add(sub_s)
```

