---
layout: post
title: "Python网络爬虫MOOC听课笔记-第1周requests库"
date:   2019-09-04
tags: [python]
comments: true
toc: true
author: Songbiao Zhu
---

在MOOC上，学习了北京理工大学，嵩天老师的[Python网络爬虫与信息提取](https://www.icourse163.org/course/bit-1001870001)，此为学习笔记记录，备查，备翻阅复习。

<!-- more -->

## P1.课程简介

北京理工大学 MOOC 向嵩

目的：掌握定向网络爬取和网页解析的能力

理念：the website is API

Requests 自动爬取网页，自动提交网络请求

robots.txt 网络爬虫排除标准

Beautiful Soup 解析HTML页面

Re 正则表达式库

## P2. IDE选择

选择Python IDE

文本工具类 Sublime text， IDLE

集成工具类 Pycharm， Anacoda

P3. 

P4. 第一周内容导学

* Request库入门

* Robotx协议

* 爬虫实例

Requests库安装：pip install requests

## Requests库7个主要方法

 requests.request()

 requests.get()

 requests.head()

 requests.post()

 requests.put()

 requests.patch()

 requests.delete()

其实后面6个方法都是base第一个基础方法 requests.request()

r = requests.get(url, params = None, **kwargs)

Response对象 和

```python
import requests
r = requests.get("http://www.baidu.com")
print(r.status_code)
type(r)
r.headers

r.encoding = 'utf-8'
r.text

r.encoding
r.apparent_encoding
r.encoding = 'UTF-8'
r.text
```

Response 对象的属性

* r.status_code: 200表示成功，404或其他表示异常
* r.text 字符串形式
* r.encoding 从HTTP header中charset字段猜测的response的编码方式，如果不存在charset字段则默认编码为ISO-8859-1
* r.apparent_encoding根据网页内容分析出的备选编码方式
* r.content HTTP相应内容的二进制形式

## 爬取网页的通用代码框架

异常

requests.ConnectionError

requests.HTTPError

requests.URL.Required

requests.TooManyRedirects

requests.ConnectionTimeout 与服务器连接的过程超时异常

requests.Timeout 请求URL的整个过程超时异常

r.raise_for_status()

```python
import requests

def getHTMLText(url):
   try:
       r = requests.get(url, timeout = 30)
       r.raise_for_status() #判断状态，不是200则引发Error
       r.encoding = r.apparent_encoding
       return r.text
    except:
       return "产生异常"

if __name__ =="__main__":
   url = "http://www.baidu.com"
   print(getHTMLText(url))
```

## http协议

Hypertext transfer protocol超文本传输协议

基于"请求与相应"的模式

URL 是一个通过HTTP协议存取资源的internet路径

```python
# url格式 http://host[:post][path]
# host 主机域名或IP地址
# port 端口号，缺省端口为80
# path 请求资源的路径
```

HTTP协议对网络数据资源的操作主要有6种

* GET 请求获取URL位置的资源

* HEAD 请求获取URL位置的资源时的响应消息报告，即获得该资源的头部信息

* POST 向URL资源后新增数据，不改变元数据

* PUT 向URL位置存储数据，会覆盖URL位置上的所有原数据

* PATCH 局部更新URL位置中数据资源局部更新

* DELETE 删除URL位置存储的数据资源

HTTP协议方法是与request库中的同名方法功能呢是一样的。

## requests库主要方法介绍

requests.request()方法是基础，其他的6个方法的参数都是基于这个方法的。

```python
# requests.request(method, url, **kwargs)
# method 就是GET, HEAD, POST, PUT,PATCH, DELETE, OPTIONS
# OPTIONS并不常用
```

**kwargs: 控制访问的参数，均为可选项，有13个：

params：字典或字节序列，作为参数增加到url中

data:字典或字节序列或文件数据，作为request内容

json:JSON格式数据，作为request内容

headers: 字典，HTTP定制头

cookies: 字典或CookieJar， 

auth: 元组

files: 字典类型，传输文件

timeout: 设置超时时间，second为单位

proxy： 字典，设定访问代理服务器，可以增加登录认证

allow_redirects： True/False，默认为True,重定向开关

stream:  True/False，默认为True，获取内容立即下载开关

verify:  True/False，默认为True，认证SSL证书开关

cert: 本地SSL证书路径

对于爬虫来说，其实最常用的requests库重点掌握GET和HEAD。

## 网络爬虫的道德

网络爬虫的尺寸

* 小规模  爬取网页 Requests库，绝大多数爬虫
* 中规模 爬取网站 Scrapy库
* 大规模 爬取全网 搜索引擎

网络爬虫带来的问题：

* 骚扰服务器
* 爬取有版权内容
* 爬取有个人隐私的内容

网络爬虫的限制

* 来源审查：判断User-Agent，只相应部分访问
* 发布公告：Robotx协议，告知所有爬虫的爬取要遵守

## Robots协议

网络爬虫排除标准

告知爬虫哪些可爬，哪些不可以。

在网站根目录下放robots.txt文件。

Robots协议基本语法： *代表所有， Disalow表示不允许。

User-agent: *

Disallow: /?*

不提供robots协议的网站即表示不限制爬虫访问。

## Robots协议遵守方式

网络爬虫应该可以自动或者人工识别robots.txt，然后根据规则进行爬取。不遵守robots.txt的爬取，会存在法律风险。

不过类人行为的访问（比如访问频率很低），可以酌情不遵守robots.txt，但不能用于商业用途。

## 实例1：爬取京东商品页面

常规爬取

```python
import requests
url = "https://item.jd.com/100003688077.html"
try:
    r = requests.get(url)
    r.raise_for_status() #判断状态，不是200则引发Error
    r.encoding = r.apparent_encoding
    print(r.text[:1000]) 
except:
    print("爬取失败")
```

## 实例2：亚马逊页面爬取

status 503报错.Amazon对来源进行审查。

需要修改request.get(url, header = kv)中的header字段

```python
import requests
url = "https://www.amazon.cn/gp/product/B01M8L5Z3Y"

try:
    kv = {'user-agent':'Mozilla/5.0'}
    r = requests.get(url,headers = kv)
    r.raise_for_status() #判断状态，不是200则引发Error
    r.request.headers
    r.encoding = r.apparent_encoding
    print(r.text[1000:2000]) 
except:
    print("爬取失败")


```

## 实例3：百度360搜索关键词提交搜索

向搜索引擎提交关键词的爬虫

百度的关键词接口

```python
# http://www.baidu.com/s?wd=keyword
```

360的关键词接口

```python
# http://www.so.com/s?q=keyword
```

只需要修改keyword就可以向搜索引擎提交搜索关键词。

只需要用requests库构建这样的url即可。

```python
# 逐行代码
import requests
kv = {'wd':'Python'}
r = requests.get("http://www.baidu.com/s", params = kv)
r.status_code
r.request.url
len(r.text)

```

```python
# 百度搜索全代码框架
import requests
keyword = "Python"
try:
    kv = {'wd':keyword}
    r = requests.get("http://www.baidu.com/s", params = kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text)) # 437177
except:
     print("爬取失败")
```

```python
# 360搜索的全代码，只有API接口的关键词换成了q
import requests
keyword = "Python"
try:
    kv = {'q':keyword}
    r = requests.get("http://www.so.com/s", params = kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text)) # 349167
except:
     print("爬取失败")

```

## 实例4：网络图片的爬取

网络图片链接的格式， 以.jpg结尾

```python
# 逐行代码
import requests
path = "D:/abc.jpg"
url = "http://image.nationalgeographic.com.cn/2017/0211/20170211061910157.jpg"
r = requests.get(url)
r.status_code

with open(path, 'wb') as f:
    f.write(r.content)
    f.close()    
```

图片爬取全代码

```python
import requests
import os
url = "http://image.nationalgeographic.com.cn/2017/0211/20170211061910157.jpg"
root = "F://pics//"
path = root + url.split('/')[-1]

try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r = requests.get(url)
        with open(path, 'wb') as f:
            f.write(r.content)
            f.close()
            print('文件保存成功')
    else:
        print('文件已存在')
except:
    print("爬取失败")

```

## 实例5：IP地址归属地的自动查询

www.ip138.com 查询

可以发现，提交查询时，url是http://m.ip138.com/ip.asp?ip=ipaddress

分析网站的API接口，所以就可以爬取查询信息。

```python
#逐行代码
import requests
url = "http://m.ip138.com/ip.asp?ip="
r = requests.get(url + '202.204.80.112')
r.status_code
r.text[-500]#查询返回文本的最后500个字符
```

```python
#完整代码
import requests
url = "http://m.ip138.com/ip.asp?ip="
try:
    r = requests.get(url + '202.204.80.112')
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[-500:])
except:
    print("爬取失败")
```

该实例提示，对于需要在网页中进行提交信息查询时，可以挖掘一下这个网站的API是什么，然后考虑用爬虫实现。使用网络爬虫的视角来看待网络内容，也就是网络上所有的内容都有一个url，对网络上的内容只有两个基本点，一是url，一是基于http协议的6种操作。





```python

```




