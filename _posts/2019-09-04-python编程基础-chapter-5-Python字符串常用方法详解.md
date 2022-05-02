---
layout: post
title: "C中文网python编程基础chapter-5-Python字符串常用方法详解"
date:   2019-09-04
tags: [python]
comments: true
 
author: Songbiao Zhu
---

在C语言中文网上，学习了[python编程的基础课程](http://c.biancheng.net/python/)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## Python字符串拼接（包含字符串拼接数字）

```python
s2 = "Python "
s3 = "iS Funny"
#使用+拼接字符串
s4 = s2 + s3
print(s4)

# Python字符串拼接数字
# Python 不允许直接拼接数字和字符串，程序必须先将数字转换成字符串
s1 = "这是数字: "
p = 99.8
#字符串直接拼接数值，程序报错
print(s1 + p)
#使用str()将数值转换成字符串
print(s1 + str(p))
#使用repr()将数值转换成字符串
print(s1 + repr(p))
```



## Python截取字符串（字符串切片）方法详解 

```python
# string[index]
s = 'crazyit.org is very good'
# 获取s中索引2处的字符
print(s[2]) # 输出a
# 获取s中从右边开始，索引4处的字符
print(s[-4]) # 输出g

# string[start : end : step]
s = 'crazyit.org is very good'
# 获取s中从索引3处到索引5处（不包含）的子串
print(s[3: 5]) # 输出 zy
# 获取s中从索引3处到倒数第5个字符的子串
print(s[3: -5]) # 输出 zyit.org is very
# 获取s中从倒数第6个字符到倒数第3个字符的子串
print(s[-6: -3]) # 输出 y g
#每隔 1 个，取一个字符
print(s[::2]) # 输出 caytogi eygo

##  start、end 以及 step 都可以省略
# 获取s中从索引5处到结束的子串
print(s[5: ]) # 输出it.org is very good
# 获取s中从倒数第6个字符到结束的子串
print(s[-6: ]) # 输出y good
# 获取s中从开始到索引5处的子串
print(s[: 5]) # 输出crazy
# 获取s中从开始到倒数第6个字符的子串
print(s[: -6]) #输出crazyit.org is ver

# 判断s是否包含'very'子串
print('very' in s) # True
print('fkit' in s) # False

# 输出s字符串中最大的字符
print(max(s)) # z
# 输出s字符串中最大的字符
print(min(s)) # 空格
```



## Python split()方法详解：分割字符串 

分割字符串的 split() 方法

```python
str.split(sep,maxsplit)
```

此方法中各部分参数的含义分别是： 

1.  str：表示要进行分割的字符串；
2.  sep：用于指定分隔符，可以包含多个字符。此参数默认为 None，表示所有空字符，包括空格、换行符“\n”、制表符“\t”等。
3.  maxsplit：可选参数，用于指定分割的次数，最后列表中子串的个数最多为 maxsplit+1。如果不指定或者指定为 -1，则表示分割次数没有限制。

在 split 方法中，如果不指定 sep 参数，那么也不能指定 maxsplit 参数。

```python
同内建函数（如 len）的使用方式不同，字符串变量所拥有的方法，只能采用“字符串.方法名()”的方式调用。
```

```python
str = "C语言中文网 >>> c.biancheng.net"
str
'C语言中文网 >>> c.biancheng.net'
list1 = str.split() #采用默认分隔符进行分割
list1
['C语言中文网', '>>>', 'c.biancheng.net']
list2 = str.split('>>>') #采用多个字符进行分割
list2
['C语言中文网 ', ' c.biancheng.net']
list3 = str.split('.') #采用 . 号进行分割
list3
['C语言中文网 >>> c', 'biancheng', 'net']
list4 = str.split(' ',4) #采用空格进行分割，并规定最多只能分割成 4 个子串
list4
['C语言中文网', '>>>', 'c.biancheng.net']
list5 = str.split('>') #采用 > 字符进行分割
list5
['C语言中文网 ', '', '', ' c.biancheng.net']
```

需要注意的是，在未指定 sep 参数时，split() 方法默认采用空字符进行分割，但当字符串中有连续的空格或其他空字符时，都会被视为一个分隔符对字符串进行分割，例如：

```python
str = "C语言中文网   >>>   c.biancheng.net"  #包含 3 个连续的空格
list6 = str.split()
list6
['C语言中文网', '>>>', 'c.biancheng.net']
```



## Python join()方法：合并字符串 

 join()方法是 split() 方法的逆方法，用来将列表（或元组）中包含的多个字符串连接成一个字符串。

```python
newstr = str.join(iterable)
```

此方法中各参数的含义如下： 

1.  newstr：表示合并后生成的新字符串；
2.  **str**：用于指定合并时的**分隔符**；
3.  iterable：做合并操作的源字符串数据，允许以列表、元组等形式提供。

```python
# 将列表中的字符串合并成一个字符串。 
>>> list = ['c','biancheng','net']
>>> '.'.join(list)
'c.biancheng.net'

# 将元组中的字符串合并成一个字符串。
>>> dir = '','usr','bin','env'
>>> type(dir)
<class 'tuple'>
>>> '/'.join(dir)
'/usr/bin/env'
```

## Python count()方法：统计字符串出现的次数 

count 方法用于检索指定字符串在另一字符串中出现的次数，如果检索的字符串不存在，则返回 0，否则返回出现的次数。

```python
str.count(sub[,start[,end]])
```

此方法中，各参数的具体含义如下： 

1.  str：表示原字符串；
2.  sub：表示要检索的字符串；
3.  start：指定检索的起始位置，也就是从什么位置开始检测。如果不指定，默认从头开始检索；
4.  end：指定检索的终止位置，如果不指定，则表示一直检索到结尾。

```python
>>> str = "c.biancheng.net"
>>> str.count('.')
2

>>> str = "c.biancheng.net"
>>> str.count('.',1)
2
>>> str.count('.',2)
1
```

从输出结果可以分析出，从指定索引位置开始检索，其中**也包含此索引位置**。

```python
>>> str = "c.biancheng.net"
>>> str.count('.',2,-3)
1
>>> str.count('.',2,-4)
0
```



## Python find()方法：检测字符串中是否包含某子串 

find() 方法用于检索字符串中是否包含目标字符串，如果包含，则返回第一次出现该字符串的索引；反之，则返回 -1。

```python
str.find(sub[,start[,end]])
```

此格式中各参数的含义如下： 

1.  str：表示原字符串；
2.  sub：表示要检索的目标字符串；
3.  start：表示开始检索的起始位置。如果不指定，则默认从头开始检索；
4.  end：表示结束检索的结束位置。如果不指定，则默认一直检索到结尾。

```python
# “c.biancheng.net” 中首次出现 “.” 的位置索引
>>> str = "c.biancheng.net"
>>> str.find('.')
1

# 手动指定起始索引的位置
>>> str = "c.biancheng.net"
>>> str.find('.',2)
11

# 手动指定起始索引和结束索引的位置
>>> str = "c.biancheng.net"
>>> str.find('.',2,-4)
-1 # 其不包含“.”,返回值为 -1

#  rfind() 方法，与 find() 方法最大的不同在于，rfind() 是从字符串右边开始检索
>>> str = "c.biancheng.net"
>>> str.rfind('.')
11
```



## Python index()方法：检测字符串中是否包含某子串 

同 find() 方法类似，index() 方法也可以用于检索是否包含指定的字符串，不同之处在于，当指定的字符串不存在时，index() 方法会抛出异常。

```python
str.index(sub[,start[,end]])
```

此格式中各参数的含义分别是： 

1.  str：表示原字符串；
2.  sub：表示要检索的子字符串；
3.  start：表示检索开始的起始位置，如果不指定，默认从头开始检索；
4.  end：表示检索的结束位置，如果不指定，默认一直检索到结尾。

```python
# 用 index() 方法检索“c.biancheng.net”中首次出现“.”的位置索引
>>> str = "c.biancheng.net"
>>> str.index('.')
1

# 当检索失败时，index()会抛出异常
>>> str = "c.biancheng.net"
>>> str.index('z')
Traceback (most recent call last):
  File "<pyshell#49>", line 1, in <module>
    str.index('z')
ValueError: substring not found

#  rindex() 方法，其作用和 index() 方法类似，不同之处在于它是从右边开始检索
>>> str = "c.biancheng.net"
>>> str.rindex('.')
11
```



## Python startswith()和endswith()方法 

**startswith()** 方法用于检索字符串是否以指定字符串开头，如果是返回 True；反之返回 False。此方法的语法格式如下： 

```python
 str.startswith(sub[,start[,end]])
```

此格式中各个参数的具体含义如下： 

1.  str：表示原字符串；
2.  sub：要检索的子串；
3.  start：指定检索开始的起始位置索引，如果不指定，则默认从头开始检索；
4.  end：指定检索的结束位置索引，如果不指定，则默认一直检索在结束。

```python
# 判断“c.biancheng.net”是否以“c”子串开头
>>> str = "c.biancheng.net"
>>> str.startswith("c")
True

>>> str = "c.biancheng.net"
>>> str.startswith("http")
False

# 从指定位置开始检索。
>>> str = "c.biancheng.net"
>>> str.startswith("b",2)
True
```

**startswith() **方法用于检索字符串是否以指定字符串开头，如果是返回 True；反之返回 False。此方法的语法格式如下：

```python
 str.startswith(sub[,start[,end]])
```

此格式中各个参数的具体含义如下： 

1.  str：表示原字符串；
2.  sub：要检索的子串；
3.  start：指定检索开始的起始位置索引，如果不指定，则默认从头开始检索；
4.  end：指定检索的结束位置索引，如果不指定，则默认一直检索在结束。

```python
>>> str = "c.biancheng.net"
>>> str.endswith("net")
True
```



## Python字符串大小写转换（3种）函数及用法 

为了方便对字符串中的字母进行大小写转换，字符串变量提供了 3 种方法，分别是 title()、lower() 和 upper()。

**title() **方法用于将字符串中每个单词的**首字母转为大写**，其他字母全部转为小写，转换完成后，此方法会返回转换得到的字符串。如果字符串中没有需要被转换的字符，此方法会将字符串原封不动地返回。
title() 方法的语法格式如下：其中，str 表示要进行转换的字符串。

```python
 str.title()
```

**lower() **方法用于将字符串中的所有大写字母转换为**小写**字母，转换完成后，该方法会返回新得到的字符串。如果字符串中原本就都是小写字母，则该方法会返回原字符串。语法格式如下：其中，str 表示要进行转换的字符串。

```python
 str.lower()
```

**upper() **的功能和 lower() 方法恰好相反，它用于将字符串中的所有小写字母转换为**大写**字母，和以上两种方法的返回方式相同，即如果转换成功，则返回新字符串；反之，则返回原字符串。语法格式如下：str 表示要进行转换的字符串。

```python
 str.upper()
```

```python
>>> str = "c.biancheng.net"
>>> str.title()
'C.Biancheng.Net'
>>> str = "I LIKE C"
>>> str.title()
'I Like C'

>>> str = "I LIKE C"
>>> str.lower()
'i like c'

>>> str = "i like C"
>>> str.upper()
'I LIKE C'
```

## Python去除字符串中空格（删除指定字符）的3种方法 

在一些场景中，字符串前后不允许出现空格和特殊字符，此时就需要去除字符串中的空格和特殊字符。

这里的特殊字符，指的是制表符（\t）、回车符（\r）、换行符（\n）等。

Python中，字符串变量提供了 3 种方法来删除字符串中多余的空格和特殊字符，它们分别是： 

1.  strip()：删除字符串前后（左右两侧）的空格或特殊字符。
2.  lstrip()：删除字符串前面（左边）的空格或特殊字符。
3.  rstrip()：删除字符串后面（右边）的空格或特殊字符。

注意，Python 的 str 是不可变的（不可变的意思是指，字符串一旦形成，它所包含的字符序列就不能发生任何改变），因此这三个方法只是返回字符串前面或后面空白被删除之后的副本，**并不会改变字符串本身**。

```python
# str 表示原字符串，[chars] 用来指定要删除的字符，可以同时指定多个，如果不手动指定，则默认会删除空格以及制表符、回车符、换行符等特殊字符。

str.strip([chars])
 
str.lstrip([chars])
  
str.rstrip([chars])
```

```python
>>> str = "  c.biancheng.net \t\n\r"
>>> str.strip()
'c.biancheng.net'
>>> str.strip(" ,\r")
'c.biancheng.net \t\n'
>>> str
'  c.biancheng.net \t\n\r'

>>> str = "  c.biancheng.net \t\n\r"
>>> str.lstrip()
'c.biancheng.net \t\n\r'

>>> str = "  c.biancheng.net \t\n\r"
>>> str.rstrip()
'  c.biancheng.net'
```

## Python format()格式化输出方法详解 

字符串类型（str）提供了 format() 方法对字符串进行格式化,format() 方法的语法格式如下：

```python
 str.format(args)
```

此方法中，str 用于指定字符串的显示样式；args 用于指定要进行格式转换的项，如果有多项，之间有逗号进行分割。

学习 format() 方法的难点，在于搞清楚 str 显示样式的书写格式。在创建显示样式模板时，需要使用`{}`和`：`来指定占位符，其完整的语法格式为：

```python
{ [index][ : [ [fill] align] [sign] [#] [width] [.precision] [type] ] }
```

注意，格式中用 [] 括起来的参数都是可选参数，即可以使用，也可以不使用。各个参数的含义如下： 

-  index：指定：后边设置的格式要作用到 args 中第几个数据，数据的索引值从 0 开始。如果省略此选项，则会根据 args 中数据的先后顺序自动分配。
-  fill：指定空白处填充的字符。注意，当填充字符为逗号(,)且作用于整数或浮点数时，该整数（或浮点数）会以逗号分隔的形式输出，例如（1000000会输出 1,000,000）。
-  align：指定数据的对齐方式，具体的对齐方式如表 1 所示。

 **align：指定数据的对齐方式**

| align | 含义                                                         |
| ----- | ------------------------------------------------------------ |
| <     | 数据左对齐。                                                 |
| >     | 数据右对齐。                                                 |
| =     | 数据右对齐，同时将符号放置在填充内容的最左侧，该选项只对数字类型有效。 |
| ^     | 数据居中，此选项需和 width 参数一起使用。                    |

**sign：指定有无符号数**

| sign参数 | 含义                                                         |
| -------- | ------------------------------------------------------------ |
| +        | 正数前加正号，负数前加负号。                                 |
| -        | 正数前不加正号，负数前加负号。                               |
| 空格     | 正数前加空格，负数前加负号。                                 |
| #        | 对于二进制数、八进制数和十六进制数，使用此参数，各进制数前会分别显示 0b、0o、0x前缀；反之则不显示前缀。 |

* width：指定输出数据时所占的宽度。

*  .precision：指定保留的小数位数。

*  type：指定输出数据的具体类型

| type类型值 | 含义                                                  |
| ---------- | ----------------------------------------------------- |
| s          | 对字符串类型格式化。                                  |
| d          | 十进制整数。                                          |
| c          | 将十进制整数自动转换成对应的 Unicode 字符。           |
| e 或者 E   | 转换成科学计数法后，再格式化输出。                    |
| g 或 G     | 自动在 e 和 f（或 E 和 F）中切换。                    |
| b          | 将十进制数自动转换成二进制表示，再格式化输出。        |
| o          | 将十进制数自动转换成八进制表示，再格式化输出。        |
| x 或者 X   | 将十进制数自动转换成十六进制表示，再格式化输出。      |
| f 或者 F   | 转换为浮点数（默认小数点后保留 6 位），再格式化输出。 |
| %          | 显示百分比（默认显示小数点后 6 位）。                 |

```python
str="网站名称：{:>9s}\t网址：{:s}"
print(str.format("C语言中文网","c.biancheng.net"))

Traceback (most recent call last):
  File "C:\Users\mengma\Desktop\1.py", line 2, in
    print(str.format("C语言中文网","c.biancheng.net"))
ValueError: cannot switch from automatic field numbering to manual field specification

#以货币形式显示
print("货币形式：{:,d}".format(1000000))
#科学计数法表示
print("科学计数法：{:E}".format(1200.12))
#以十六进制表示
print("100的十六进制：{:#x}".format(100))
#输出百分比形式
print("0.01的百分比表示：{:.0%}".format(0.01))
```
输出结果为：

```python
货币形式：1,000,000
科学计数法：1.200120E+03
100的十六进制：0x64
0.01的百分比表示：1%
```

## Python encode()和decode()方法：字符串编码转换 

encode() 方法为字符串类型（str）提供的方法，用于将 str 类型转换成 bytes 类型，这个过程也称为“编码”。
encode() 方法的语法格式如下：

```python
 str.encode([encoding="utf-8"][,errors="strict"])
```

注意，格式中用 [] 括起来的参数为可选参数，也就是说，在使用此方法时，可以使用 [] 中的参数，也可以不使用。

注意，使用 encode() 方法对原字符串进行编码，不会直接修改原字符串，如果想修改原字符串，需要重新赋值。

| 参数               | 含义                                                         |
| ------------------ | ------------------------------------------------------------ |
| str                | 表示要进行转换的字符串。                                     |
| encoding = "utf-8" | 指定进行编码时采用的字符编码，该选项默认采用 utf-8 编码。例如，如果想使用简体中文，可以设置 gb2312。    当方法中只使用这一个参数时，可以省略前边的“encoding=”，直接写编码格式，例如 str.encode("UTF-8")。 |
| errors = "strict"  | 指定错误处理方式，其可选择值可以是：   strict：遇到非法字符就抛出异常。  ignore：忽略非法字符。  replace：用“？”替换非法字符。  xmlcharrefreplace：使用 xml 的字符引用。  该参数的默认值为 strict。 |

和 encode() 方法正好相反，decode() 方法用于将 bytes 类型的二进制数据转换为 str 类型，这个过程也称为“解码”。

decode() 方法的语法格式如下：

```python
 bytes.decode([encoding="utf-8"][,errors="strict"])
```

| 参数              | 含义                                                         |
| ----------------- | ------------------------------------------------------------ |
| bytes             | 表示要进行转换的二进制数据。                                 |
| encoding="utf-8"  | 指定解码时采用的字符编码，默认采用 utf-8 格式。当方法中只使用这一个参数时，可以省略“encoding=”，直接写编码方式即可。    注意，对 bytes 类型数据解码，要选择和当初编码时一样的格式。 |
| errors = "strict" | 指定错误处理方式，其可选择值可以是：   strict：遇到非法字符就抛出异常。  ignore：忽略非法字符。  replace：用“？”替换非法字符。  xmlcharrefreplace：使用 xml 的字符引用。  该参数的默认值为 strict。 |

## Python dir()和help()帮助函数 

只需掌握如下两个帮助函数，即可查看 Python 中的所有函数（方法）以及它们的用法和功能： 

1.  dir()：列出指定类或模块包含的全部内容（包括函数、方法、类、变量等）。
2.  help()：查看某个函数或方法的帮助文档。

```python
# 要查看字符串变量（它的类型是 str 类型）所能调用的全部内容
>>> dir(str)

# 查看某个方法的用法，则可使用 help() 函数
>>> help(str.title)
Help on method_descriptor:

title(...)
    S.title() -> str
   
    Return a titlecased version of S, i.e. words start with title case
    characters, all remaining cased characters have lower case.
```