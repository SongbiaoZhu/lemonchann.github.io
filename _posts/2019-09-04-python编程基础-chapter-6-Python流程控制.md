---
layout: post
title: "chapter-6-Python流程控制"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在C语言中文网上，学习了[python编程的基础课程](http://c.biancheng.net/python/)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

Python 同样提供了现代编程语言都支持的两种基本流程控制结构，分支结构和循环结构： 

-  分支结构用于实现根据条件来选择性地执行某段代码；
-  循环结构用于实现根据循环条件重复执行某段代码；

## Python if else条件语句详解 

Python 中，选择（条件）语句可细分为  3 种形式，分别是 if 语句、if else 语句和 if elif else 语句。这 3 种形式分支语句的语法格式和执行流程，如表 1 所示。

```python
# if 语句
if 表达式：
    代码块
    
# if else 语句    
if 表达式：
    代码块 1
else：
    代码块 2
    
# if elif else
if 表达式 1：
    代码块 1
elif 表达式 2：
    代码块 2
elif 表达式 3：
    代码块 3
...//可以有零条或多条elif语句
else：
    代码块 n
    
# 以上三种形式中，第二种形式和第三种形式是相通的，如果第三种形式中的 elif 块不出现，则变成了第二种形式。
# 当要实现多重选择的功能时，只能使用 if（elif else）分支语句。
```

以上 3 种形式的分支语句中，表达式可以是一个单纯的布尔值或变量，也可以是比较表达式或逻辑表达式；代码块指的是具有相同缩进格式的多行代码。一般情况下，一个代码块会被当成一个整体来执行（除非在运行过程中遇到return、break、continue 等关键字），因此这个代码块也被称为条件执行体；

对于上面的 if 分支语句，执行过程是非常简单的，即如果 if 中的表达式为“真”，程序就会执行 if 中的代码块；否则就会依次判断 elif 中的表达式（如果有），如果为“真”，程序就会执行 elif 中的代码块……如果前面所有条件都为“假”，程序就会执行 else 后的代码块（如果有）。

除了 False 本身，各种代表“空”的 None、空字符串、空元组、空列表、空字典都会被当成 False 处理。

```
# 当下面的值作为 bool 表达式时，会被解释器当作 False 处理： 
# False、None、0、""、()、[]、{}
```

## Python if else语句用法规范（注意事项） 

1) 代码块不要忘记缩进：if 条件后的条件执行体（代码块）一定要缩进。只有缩进后的代码才能算条件执行体。Python 通常建议缩进 4 个空格。

2) if 代码块不要随意缩进：同一个代码块内的代码必须保持相同的缩进，不能一会缩进 2 个空格，一会缩进 4 个空格。对于不需要使用代码块的地方，千万不要随意缩进，否则程序也会报错。

3) if 表达式不要遗忘冒号：从 Python 语法解释器的角度来看，Python 冒号精确表示代码块的开始点这个功能不仅在条件执行体中如此，后面的循环体、方法体、类体全部遵守该规则。

如果程序遗忘了冒号，那么 Python 解释器就无法识别代码块的开始点。

## Python if语句嵌套（入门必读） 

 if、if else 和 if elif else，这 3 种条件语句之间可以相互嵌套。

判断是否为酒后驾车：如果规定，车辆驾驶员的血液酒精含量小于 20mg/100ml 不构成酒驾；酒精含量大于或等于 20mg/100ml 为酒驾；酒精含量大于或等于 80mg/100ml 为醉驾。先编写 Python 程序判断是否为酒后驾车。

```python
proof = int(input("输入驾驶员每 100ml 血液酒精的含量："))
if proof < 20:
    print("驾驶员不构成酒驾")
else:
    if proof < 80:
        print("驾驶员已构成酒驾")
    else:
        print("驾驶员已构成醉驾")
```

## Python pass语句及其作用 

Python 的 pass 语句就是空语句。

有时候程序需要占一个位、放一条语句，但又不希望这条语句做任何事情，此时就可通过 pass 语句来实现。通过使用 pass 语句，可以让程序更完整。

```python
s = input("请输入一个整数: ")
s = int(s)
if s > 5:
    print("大于5")
elif s < 5:
    # 空语句，相当于占位符
    pass
else:
    print("等于5")
```

正如从上面程序所看到的，对于 s 小于 5 的情形，程序暂时不想处理（或不知道如何处理），此时程序就需要通过空语句来占一个位，这样即可使用 pass 语句了。

## Python assert断言函数及用法 

assert 断言语句和 if 分支有点类似，它用于对一个 bool 表达式进行断言，如果该 bool 表达式为 True，该程序可以继续向下执行；否则程序会引发 AssertionError 错误。

为什么要使用assert 断言语句呢？这是因为，与其让程序在晚些时候崩溃，不如在错误条件出现时，就直接让程序崩溃。通常，assert 语句用在检查函数参数的属性（是参数是否是按照设想的要求传入），或者作为初期测试和调试过程中的辅助工具。

```python
s_age = input("请输入您的年龄:")
age = int(s_age)
assert 20 < age < 80
print("您输入的年龄在20和80之间")
```

assert 断言的执行逻辑是：

```python
if 表达式的值为 True：
    程序继续运行；
else：     # 表示式的值为 False
    程序引发 AssertionError 错误
```

## Python while循环语句详解 

Python中，while 循环和 if 条件分支语句类似，即在条件（表达式）为真的情况下，会执行相应的代码块。不同之处在于，只要条件为真，while 就会一直重复执行那段代码块。

```python
while 条件表达式：
    代码块
```

这里的代码块，还是指的缩进格式相同的多行代码，不过在循环结构中，它又称为循环体。

while 语句执行的具体流程为：首先判断条件表达式的值，其值为真（True）时，则执行代码块中的语句，当执行完毕后，再回过头来重新判断条件表达式的值是否为真，若仍为真，则继续重新执行代码块...如此循环，直到条件表达式的值为假（False），才终止循环。

注意，在使用 while 循环时，一定要保证循环条件有变成假的时候，否则这个循环将成为一个死循环，永远无法结束这个循环。

 使用while循环遍历列表和元组

由于列表和元组的元素都是有索引的，因此程序可通过 while 循环、列表或元组的索引来遍历列表和元组中的所有元素。例如如下程序：

```
a_tuple = ('fkit', 'crazyit', 'Charli')
i = 0
# 只有i小于len(a_list)，继续执行循环体
while i < len(a_tuple):
    print(a_tuple[i]) # 根据i来访问元组的元素
    i += 1
```

```
 fkit crazyit Charli
```

下面示范一个小程序，实现对一个整数列表的元素进行分类，能整除 3 的放入一个列表中；除以 3 余 1 的放入另一个列表中；除以 3 余 2 的放入第三个列表中：

```python
src_list = [12, 45, 34,13, 100, 24, 56, 74, 109]
a_list = [] # 定义保存整除3的元素
b_list = [] # 定义保存除以3余1的元素
c_list = [] # 定义保存除以3余2的元素
# 只要src_list还有元素，继续执行循环体
while len(src_list) > 0:
    # 弹出src_list最后一个元素
    ele = src_list.pop()
    # 如果ele % 2不等于0
    if ele % 3 == 0 :
        a_list.append(ele) # 添加元素
    elif ele % 3 == 1:
        b_list.append(ele) # 添加元素
    else:
        c_list.append(ele) # 添加元素
print("整除3:", a_list)
print("除以3余1:",b_list)
print("除以3余2:",c_list)
```



## Python for循环及用法详解 

Python 中的循环语句有 2 种，分别是 while 循环和 for 循环，前面章节已经对 while 做了详细的讲解，本节给大家介绍 for 循环，它常用于遍历字符串、列表、元组、字典、集合等序列类型，逐个获取序列中的各个元素。

for 循环的语法格式如下：

```python
for 迭代变量 in 字符串|列表|元组|字典|集合：
    代码块
```

格式中，迭代变量用于存放从序列类型变量中读取出来的元素，所以一般不会在循环中对迭代变量手动赋值。

```
name = '张三'
#变量name，逐个输出各个字符
for ch in name:
    print(ch)
```

**for 进行数值循环**

在使用 for 循环时，最基本的应用就是进行数值循环。

```
print("计算 1+2+...+100 的结果为：")
#保存累加结果的变量
result = 0
#逐个获取从 1 到 100 这些值，并做累加操作
for i in range(101):
    result += i
print(result)
```

range() 函数，此函数是 Python 内置的函数，用于生成一系列连续的整数，多用于 for 循环中。
range() 函数的语法格式如下：

```
range(start,end,step)
# 在使用 range() 函数时，如果只有一个参数，则表示指定的是 end；如果有两个参数，则表示指定的是 start 和 end。
```

1.  start：用于指定计数的起始值，如果省略不写，则默认从 0 开始。
2.  end：用于指定计数的结束值（不包括此值），此参数不能省略。
3.  step：用于指定步长，即两个数之间的间隔，如果省略，则默认步长为 1。

**for 循环遍历列表和元组**

遍历列表。例如，下面程序要计算列表中所有数值元素的总和、平均值：

```python
src_list = [12, 45, 3.4, 13, 'a', 4, 56, 'crazyit', 109.5]
my_sum = 0
my_count = 0
for ele in src_list:
    # 如果该元素是整数或浮点数
    if isinstance(ele, int) or isinstance(ele, float):
        print(ele)
        # 累加该元素
        my_sum += ele
        # 数值元素的个数加1
        my_count += 1
print('总和:', my_sum)
print('平均数:', my_sum / my_count)
```

 Python 的 isinstance() 函数，该函数用于判断某个变量是否为指定类型的实例，其中前一个参数是要判断的变量，后一个参数是类型。

如果需要，for 循环也可根据索引来遍历列表或元组，即只要让迭代变量取 0 到列表长度的区间，就可通过该迭代变量访问列表元素。例如如下程序：

```python
a_list = [330, 1.4, 50, 'fkit', -3.5]
# 遍历0到len(a_list)的范围
for i in range(0, len(a_list)) :
    # 根据索引访问列表元素
    print("第%d个元素是 %s" % (i , a_list[i]))
```

**for 循环遍历字典**

使用 for 循环遍历字典其实也是通过遍历普通列表来实现的。前面在介绍字典时己经提到，字典包含了如下三个方法： 

1.  items()：返回字典中所有 key-value 对的列表。
2.  keys()：返回字典中所有 key 的列表。
3.  values()：返回字典中所有 value 的列表。

因此，如果要遍历字典，完全可以先调用字典的上面三个方法之一来获取字典的所有 key-value 对、所有 key、所有 value，再进行遍历。如下程序示范了使用 for 循环来遍历字典：

```python
my_dict = {'语文': 89, '数学': 92, '英语': 80}
# 通过items()方法遍历所有key-value对
# 由于items方法返回的列表元素是key-value对，因此要声明两个变量
for key, value in my_dict.items():
    print('key:', key)
    print('value:', value)
print('-------------')
# 通过keys()方法遍历所有key
for key in my_dict.keys():
    print('key:', key)
    # 在通过key获取value
    print('value:', my_dict[key])
print('-------------')
# 通过values()方法遍历所有value
for value in my_dict.values():
    print('value:', value)
```

上面程序通过三个 for 循环分别遍历了字典的所有 key-value 对、所有 key、所有 value。尤其是通过字典的 items() 遍历所有的 key-value 对时，由于 items() 方法返回的是字典中所有 key-value 对组成的列表，列表元素都是长度为 2 的元组，因此程序要声明两个变量来分别代表 key、value。

## Python循环结构中else用法（入门必读） 

Python 中，无论是 while 循环还是 for 循环，其后都可以紧跟着一个 else 代码块，它的作用是，当循环条件为 False 跳出循环时，程序会最先执行 else 代码块中的代码。

```python
count_i = 0
while count_i < 5:
    print('count_i小于5: ', count_i)
    count_i += 1
else:
    print('count_i大于或等于5: ', count_i)
```

for 循环同样可使用 else 代码块，当 for 循环把区间、元组或列表的所有元素遍历一次之后， for 循环会执行 else 代码块，在 else 代码块中，迭代变量的值依然等于最后一个元素的值。例如如下代码：

```python
a_list = [330, 1.4, 50, 'fkit', -3.5]
for ele in a_list:
    print('元素: ', ele)
else:
    # 访问循环计数器的值，依然等于最后一个元素的值
    print('else块: ', ele)
```

## Python（for和while）循环嵌套及用法 

Python 中，如果把一个循环放在另一个循环体内，那就形成循环嵌套。 for 循环和 while 循环可以相互嵌套。

```python
# 外层循环
for i in range(0, 5) :
    j = 0
    # 内层循环
    while j < 3 :
        print("i的值为: %d , j的值为: %d" % (i, j))
        j += 1
```

## Python列表推导式（for表达式）及用法 

列表推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的列表。

列表推导式的语法格式如下：

```python
 [表达式 for 迭代变量 in 可迭代对象 [if 条件表达式] ]
```

此格式中，[if 条件表达式] 不是必须的，可以使用，也可以省略。

除去 [if 条件表达式] 部分，其余各部分的含义以及执行顺序和 for 循环是完全一样的（表达式其实就是 for 循环中的循环体），即它的执行顺序如下所示：

```python
for 迭代变量 in 可迭代对象
    表达式
```

初学者可以这样认为，它只是对 for 循环语句的格式做了一下简单的变形，并用 [] 括起来而已，只不过最大的不同之处在于，列表推导式最终会将循环过程中，计算表达式得到的一系列值组成一个列表。

```python
a_range = range(10)
# 对a_range执行for表达式
a_list = [x * x for x in a_range]
# a_list集合包含10个元素
print(a_list)
```

不仅如此，我们还可以在列表推导式中添加 if 条件语句，这样列表推导式将只迭代那些符合条件的元素。例如如下代码：

```python
b_list = [x * x for x in a_range if x % 2 == 0]
# a_list集合包含5个元素
print(b_list)
```

对于包含多个循环的 for 表达式，同样可指定 if 条件。假如我们有一个需求：程序要将两个列表中的数值按“能否整除”的关系配对在一起。比如 src_a 列表中包含 30，src_b 列表中包含 5，其中 30 可以整除 5，那么就将 30 和 5 配对在一起。对于上面的需求使用 for 表达式来实现非常简单，例如如下代码：

```python
src_a = [30, 12, 66, 34, 39, 78, 36, 57, 121]
src_b = [3, 5, 7, 11]
# 只要y能整除x，就将它们配对在一起
result = [(x, y) for x in src_b for y in src_a if y % x == 0]
print(result)
```

## Python元组推导式 

元组推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的元组。

元组推导式的语法格式如下： 

```
 (表达式 for 迭代变量 in 可迭代对象 [if 条件表达式] )
```

其中，用 [] 括起来的部分，可以使用，也可以省略。

通过和列表推导式做对比，你会发现，除了元组推导式是用 () 圆括号将各部分括起来，而列表推导式用的是 []，其它完全相同。不仅如此，元组推导式和列表推导式的用法也完全相同。

不同点是，使用元组推导式生成的结果并不是一个元组，而是一个生成器对象（后续会介绍）。

如果我们想要使用元组推导式获得新元组或新元组中的元素，有以下三种方式：

```python
# 1. 使用 tuple() 函数，可以直接将生成器对象转换成元组，例如： 
a = (x for x in range(1,10))
print(tuple(a))
运行结果为：
(1, 2, 3, 4, 5, 6, 7, 8, 9)

# 2. 直接使用 for 循环遍历生成器对象，可以获得各个元素，例如： 
a = (x for x in range(1,10))
for i in a:
    print(i,end=' ')
print(tuple(a))

# 3. 使用 __next__() 方法遍历生成器对象，也可以获得各个元素，例如： 
a = (x for x in range(3))
print(a.__next__())
print(a.__next__())
print(a.__next__())
a = tuple(a)
print("转换后的元组：",a)
```

注意，无论是使用 for 循环遍历生成器对象，还是使用 __next__() 方法遍历生成器对象，遍历后原生成器对象将不复存在，这就是遍历后转换原生成器对象却得到空元组的原因。

## Python字典推导式 

Python 中，使用字典推导式可以借助列表、元组、字典、集合以及 range 区间，快速生成符合需求的字典。

字典推导式的语法格式如下：

```python
{表达式 for 迭代变量 in 可迭代对象 [if 条件表达式]}
```

其中，用 [] 括起来的部分，可以使用，也可以省略。

可以看到，和其它推导式的语法格式相比，唯一不同在于，字典推导式用的是大括号{}。

```python
listdemo = ['C语言中文网','c.biancheng.net']
#将列表中各字符串值为键，各字符串的长度为值，组成键值对
newdict = {key:len(key) for key in listdemo}
print(newdict)

# 例2 交换现有字典中各键值对的键和值
olddict={'C语言中文网': 6, 'c.biancheng.net': 15}
newdict = {v: k for k, v in olddict.items()}
print(newdict)

# 例3 使用 if 表达式筛选符合条件的键值对
olddict={'C语言中文网': 6, 'c.biancheng.net': 15}
newdict = {v: k for k, v in olddict.items() if v>10}
print(newdict)
```

## Python集合推导式 

Python中，使用集合推导式可以借助列表、元组、字典、集合以及 range 区间，快速生成符合需求的集合。

集合推导式的语法格式和字典推导式完全相同，如下所示： 

```
 { 表达式 for 迭代变量 in 可迭代对象 [if 条件表达式] }
```

其中，用 [] 括起来的部分，可以使用，也可以省略。

有读者可能会问，集合推导式和字典推导式的格式完全相同，那么给定一个类似的推导式，如何判断是哪种推导式呢？最简单直接的方式，就是根据**表达式**进行判断，如果表达式以键值对（key：value）的形式，则证明此推导式是字典推导式；反之，则是集合推导式。

## Python zip函数及用法 

zip() 函数可以把两个列表“压缩”成一个 zip 对象（可迭代对象），这样就可以使用一个循环并行遍历两个列表。为了测试 zip() 函数的功能，我们可以先在交互式解释器中“试验”一下该函数的功能。

```python
>>> a = ['a','b','c']
>>> b = [1, 2, 3]
>>> [x for x in zip(a,b)]
[('a', 1), ('b', 2), ('c', 3)]
```

从上面的测试结果来看，zip() 函数压缩得到的可迭代对象所包含的元素是由原列表元素组成的元组。

如果 zip() 函数压缩的两个列表长度不相等，那么 zip() 函数将以长度更短的列表为准。

zip() 函数不仅可以压缩两个列表，也可以压缩多个列表。

```python
books = ['疯狂Kotlin讲义', '疯狂Swift讲义', '疯狂Python讲义']
prices = [79, 69, 89]
# 使用zip()函数压缩两个列表，从而实现并行遍历
for book, price in zip(books, prices):
    print("%s的价格是: %5.2f" % (book, price))
```

## Python reversed函数及用法 

有些时候，程序需要进行反向遍历，此时可通过 reversed() 函数，该函数可接收各种序列（元组、列表、区间等）参数，然后返回一个“反序排列”的法代器，该函数对参数本身不会产生任何影响。

```python
>>> a = range(10)
>>> [x for x in reversed(a)]
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

reversed() 当然也可以对列表、元组进行反转。

前面提到过，str 其实也是序列，因此也可通过该函数实现在不影响字符串本身的前提下，对字符串进行反序遍历。例如如下测试代码：

```python
>>> c = 'Hello,Charlie'
>>> [x for x in reversed(c)]
['e', 'i', 'l', 'r', 'a', 'h', 'C', ',', 'o', 'l', 'l', 'e', 'H']
```

## Python sorted函数及用法 

sorted() 函数与 reversed() 函数类似，该函数接收一个可迭代对象作为参数，返回一个对元素排序的列表。

```python
>>> a = [20, 30, -1.2, 3.5, 90, 3.6]
>>> sorted(a)
[-1.2, 3.5, 3.6, 20, 30, 90]
>>> a
[20, 30, -1.2, 3.5, 90, 3.6]
```

从上面的运行过程来看，sorted() 函数也不会改变所传入的可迭代对象，该函数只是返回一个新的、排序好的列表。

```python
# 在使用 sorted() 函数时，还可传入一个 reverse 参数，如果将该参数设置为 True，则表示反向排序。例如如下测试过程：
>>> sorted(a, reverse = True)
[90, 30, 20, 3.6, 3.5, -1.2]

# 在调用 sorted() 函数时，还可传入一个 key 参数，该参数可指定一个函数来生成排序的关键值。比如希望根据字符串长度排序，则可为 key 参数传入 len 函数。例如如下运行过程：
>>> b = ['fkit', 'crazyit', 'charlie', 'fox', 'Emily']
>>> sorted(b, key = len)
['fox', 'fkit', 'Emily', 'crazyit', 'charlie']
```

## Python break用法详解 

在某些场景中，如果需要在某种条件出现时强行中止循环，而不是等到循环条件为 False 时才退出循环，就可以使用 break 来完成这个功能。

Python 提供了 2 种强制离开当前循环体的办法：使用 continue 语句，可以跳过执行本次循环体中剩余的代码，转而执行下一次的循环。只用 break 语句，可以完全终止当前循环。

break 语句的语法非常简单，只需要在相应 while 或 for 语句中直接加入即可。

```python
# 一个简单的for循环
for i in range(0, 10) :
    print("i的值是: ", i)
    if i == 2 :
        # 执行该语句时将结束循环
        break
```

```python
i的值是:  0
i的值是:  1
i的值是:  2
```

需要注意的是，对于带 else 块的 for 循环，如果使用 break 强行中止循环，程序将不会执行 else 块。例如如下程序：

```python
# 一个简单的for循环
for i in range(0, 10) :
    print("i的值是: ", i)
    if i == 2 :
        # 执行该语句时将结束循环
        break
else:
    print('else块: ', i)
```

如果想达到 break 语句不仅跳出单前所在循环，同时跳出外层循环的目的，可先定义 bool 类型的变量来标志是否需要跳出外层循环，然后在内层循环、外层循环中分别使用两条 break 语句来实现。例如如下程序：

```python
exit_flag = False
# 外层循环
for i in range(0, 5) :
    # 内层循环
    for j in range(0, 3 ) :
        print("i的值为: %d, j的值为: %d" % (i, j))
        if j == 1 :
            exit_flag = True
            # 跳出里层循环
            break
    # 如果exit_flag为True，跳出外层循环
    if exit_flag :
        break  
```

上面程序在内层循环中判断 j 是否等于 i，当 j 等于 i 时，程序将 exit_flag 设为 True，并跳出内层循环；接下来程序开始执行外层循环的剩下语句，由于 exit_flag 为 True，因此也会执行外层循环的 break 语句来跳出外层循环。

程序从外层循环进入内层循环后，当 j 等于1 时，程序将 exit_flag 设为 True，并跳出内层循环；接下来程序又执行外层循环的 break 语句，从而跳出外层循环。

## Python continue的用法 

和 break 语句相比，continue 语句的作用则没有那么强大，它只能终止本次循环而继续执行下一次循环。

continue 语句的用法和 break 语句一样，只要 while 或 for 语句中的相应位置加入即可。例如：

```python
# 一个简单的for循环
for i in range(0, 3 ) :
    print("i的值是: ", i)
    if i == 1 :
        # 忽略本次循环的剩下语句
        continue
    print("continue后的输出语句")
```

```python
i的值是:  0
continue后的输出语句
i的值是:  1
i的值是:  2
continue后的输出语句
```

