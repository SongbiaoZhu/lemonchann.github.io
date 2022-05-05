---
layout: post
title: "shinydashboard系列一：标题栏"
date:   2022-05-02
tags: [R]
comments: true
author: Songbiao Zhu
---


**前言**

读研期间接触的shiny，直到18年12月份工作需要使用shiny做一些交互式的界面，才系统地整理一些shiny系列的知识点。但shiny部署较为繁琐，而shinydashboard是shiny的一个框架包，对shiny做了封装，界面比shiny更加美观，更容易上手，故这里系统介绍一下shinydashboard的知识点。分以下几部分介绍shinydashboard:
<!-- more -->

- shinydashboard三要素之一：标题栏Header
- shinydashboard三要素之一：侧边栏Siderbar
- shinydashboard三要素之一：主体Body
- 如何将shinyapp部署到服务器上
- 如何对shinyapp进行加密

**shinydashboard简介**

shiny包使得用几行R语言代码就可以轻松开发交互式web应用，不需要懂得服务器的配置，也能制作交互式网页。而shinydashboard是shiny的一个框架包，shinydashboard可以理解为对shiny的一个封装，创建一个简易的仪表板，使得shiny的外观布局更加美好。在shiny中有用户界面脚本(a user-interface)和服务器脚本(a server script）两个脚本文件，分别写在ui.R文件和server.R文件中，而在shinydashboard可以将用户界面脚本和服务器脚本封装在一个app.R脚本文件中，app.R脚本中可以通过下面标准化的代码实现：

```R
library(shinydashboard)
  shinyApp(
    ui = dashboardPage(
      dashboardHeader(),
      dashboardSidebar(),
      dashboardBody()
    ),
    server = function(input, output) { }
  )
```

从上述代码可以看出，shinydashboard由三要素组成：标题栏（Header）、侧边栏（Sidebar）和主体（Body），其实工作中用到的各种系统界面至少都包含这三要素的。下图1为Header，2为Sidebar，3为Body，是不是特别的熟悉。



![img](https://pic2.zhimg.com/80/v2-a16ea77d87639b5180ce2010fde132fd_720w.jpg)



**如何运行shinydashboard**

首先新建R脚本，命名为app.R；其次将脚本单独保存在一个文件夹中；最后点击Rstudio界面中的Run App即可发布一个app。

**步骤一：新建app.R脚本**

![img](https://pic4.zhimg.com/80/v2-c72e9f450fd099c1d4c657709ef8422f_720w.jpg)



**步骤二：脚本单独保存在一个文件夹中**

![img](https://pic1.zhimg.com/80/v2-27690dec29e3fe42903a1afd12454180_720w.jpg)



**步骤三：点击Rstudio界面上的Run App按钮**

![img](https://pic1.zhimg.com/80/v2-53cb58dea1fe48d707c482d1e9b8f1ec_720w.jpg)



**标题栏Header**

![img](https://pic3.zhimg.com/80/v2-4540e3ccc8260dead0b46dbef8dcf2ca_720w.png)

标题栏包含标题(title)和下拉菜单(dropdownMenus)，下拉菜单有三种类型：消息菜单（图中1）、通知菜单（图中2）和任务菜单（图中3），可以通过参数 type = c("messages", "notifications", "tasks")设置，都是可选的。图中红色圈圈主要用于隐藏侧边栏，如果想隐藏侧边栏点击一下即可。标题栏函数为：



```R
dashboardHeader(title = , titleWidth = , disable = ,
                dropdownMenu(),...)
参数解释：
title:设置标题
titleWidth：设置标题的宽度，例如titleWidth = 6
disable = TRUE（or FALSE），用于是否显示表头，默认为FALSE，显示表头
dropdownMenu()：用于设置一些下拉单
```

**消息下拉单**

假设我们做一个上课考勤表，学生可以登录自己的系统给班主任留言：第一条消息来自Tom，Tom生病了，向班主任请病假，并且加入了href = "[http://fontawesome.io/icons/](https://link.zhihu.com/?target=http%3A//fontawesome.io/icons/)"，点击该条消息，会自动转到Tom就诊的挂号医院，证明自己真的病啦（这里不为任何医院打广告呀，加入的链接是常用icon的网站）；第二条消息来自Marry，Marry是一名刚转来的学生，对班级比较陌生，她告诉班主任她是一名新学生，希望班主任对她多多关照；第三条消息来自Jeans，告诉班主任作业他昨天没有带的数学作业今天已经交啦。badgeStatus = "success"，可以看出消息标识的右上角数字为green颜色。代码为：

```R
dashboardHeader(
  title = "Dashboard Demo",
  ##消息下拉单
  dropdownMenu(type = "messages", badgeStatus = "success",
                 messageItem(from = "Tom",
                             message = "I'm sick. I ask for leave.",
                             time = "3 hours",
                             href = "http://fontawesome.io/icons/"
                 ),
                 messageItem(from = "Marry",
                             message = "I am a freshman.",
                             icon = icon("question"),
                             time = "2 hours"
                 ),
                 messageItem(from = "Jeans",
                             message = "I have handed in my homework.",
                             icon = icon("life-ring"),
                             time = "4 hours"
                 )
    ))
  
参数解释：
type：为messages表示这是一个消息下拉单；
badgeStatus：下拉单右上角显示数字的颜色，常用的有：primary为blue,success为green,info为auqa，warning为yellow,danger为red;
from:消息发送者
message:消息内容
icon:设置icon的tag;
time:消息发送时间
href：url链接
```



badgetStatus：参数对应的颜色为：

![img](https://pic1.zhimg.com/80/v2-ece86d7a0f6e0d63b8faba3b5c2ac3ec_720w.png)

上述代码运行结果：

![img](https://pic3.zhimg.com/80/v2-7cae4e040100c3505a0b48f2fac305ea_720w.jpg)

**通知下拉单**

班主任收到4条通知：通知一：班里转来了5名新学生；通知二：班里粉笔用完了，提醒班主任领取一些粉笔；通知三：班长买了20个笔记本，提醒班主任要给班长报销这个费用；通知四：Mrria修改了登录密码，提醒班主任问一下Mrria，是否她本人操作，账号是否被盗啦，代码为：

```R
dashboardHeader(
  title = "Dashboard Demo",
  ##通知下拉单
   dropdownMenu(type = "notifications", badgeStatus = "warning",
                 notificationItem(icon = icon("users"), status = "info",
                                 text =  "5 new members joined today",
                                 href = "https://www.r-project.org/"
                 ),
                 
                 notificationItem(icon = icon("warning"), status = "danger",
                                  text = "Chalk've run out"
                 ),
                 notificationItem(icon = icon("shopping-cart", lib = "glyphicon"),
                                  status = "success", 
                                  text = "The monitor bought 20 notebooks"
                 ),
                 notificationItem(icon = icon("user", lib = "glyphicon"),
                                  status = "danger", text = "Mrria changed her password"
                 )
    ))
  
参数解释：
type：为notifications表示这是一个通知下拉单；
badgeStatus：同消息下拉单
icon:同消息下拉单
status:表示每个通知消息的icon的颜色，参数与badgetStatus一致
text：为通知内容
href：url链接
```

上述代码运行结果：

![img](https://pic4.zhimg.com/80/v2-1979c15b0ba908802aa6e453706cd703_720w.jpg)

**任务下拉单**

今天班主任有4个任务需要完成，收语文、数学、英语和化学作业，进度条表示任务的进展程度。

```R
dashboardHeader(
  title = "Dashboard Demo",
  ##任务下拉单
      dropdownMenu(type = "tasks", badgeStatus = "danger",
                 taskItem(value = 55, color = "aqua",
                          "Today's Chinese homework has been handed in"
                 ),
                 taskItem(value = 45, color = "green",
                          "Today's math homework has been handed in"
                 ),
                 taskItem(value = 75, color = "yellow",
                          "Today's English homework has been handed in"
                 ),
                 taskItem(value = 90, color = "red",
                          "Chemistry homework has been handed in today"
                 )
    ))
  
参数解释：
type：为tasks表示这是一个任务下拉单；
badgeStatus：同消息下拉单
value:任务进度条
color:表示每个任务进度的颜色，参数见下图
text：为任务内容
href：url链接
```

color：参数可以设置为：

![img](https://pic2.zhimg.com/80/v2-f178acdd268b0bf0b5dea04e0b76cd29_720w.jpg)

上述代码运行结果：

![img](https://pic3.zhimg.com/80/v2-54d8c62a57ec62a8bd1c65265855a37a_720w.jpg)

## **总结**

标题栏包含标题和下拉菜单，标题直接用参数title设置，下拉单有三种类别：消息、通知和任务下拉单：

```R
dashboardHeader(
    title = "",
    dropdownMenu(type = , badgeStatus = ,
                 messageItem(from = ,message = , time = ,href = )),
    dropdownMenu(type = , badgeStatus = ,
                 notificationItem(icon = , status = ,
                                  text = , href = )),
    dropdownMenu(type = , badgeStatus = ,
                 taskItem(value = , color = ,
                          text = ))
  )
```

**完整代码：**

```R
library(shinydashboard)
if (interactive()) {
  library(shiny)
  
  header <- dashboardHeader(
    title = "Dashboard Demo",
    
    dropdownMenu(type = "messages", badgeStatus = "success",
                 messageItem(from = "Tom",
                             message = "I'm sick. I ask for leave.",
                             time = "3 hours",
                             href = "http://fontawesome.io/icons/"
                 ),
                 messageItem(from = "Marry",
                             message = "I am a freshman.",
                             icon = icon("question"),
                             time = "2 hours"
                 ),
                 messageItem(from = "Jeans",
                             message = "I have handed in my homework.",
                             icon = icon("life-ring"),
                             time = "4 hours"
                 )
    ),
    
    # Dropdown menu for notifications
    dropdownMenu(type = "notifications", badgeStatus = "warning",
                 notificationItem(icon = icon("users"), status = "info",
                                  text =  "5 new members joined today"
                 ),
                 
                 notificationItem(icon = icon("warning"), status = "danger",
                                  text = "Chalk've run out"
                 ),
                 notificationItem(icon = icon("shopping-cart", lib = "glyphicon"),
                                  status = "success", 
                                  text = "The monitor bought 20 notebooks"
                 ),
                 notificationItem(icon = icon("user", lib = "glyphicon"),
                                  status = "danger", text = "Mrria changed her password"
                 )
    ),
    
    
    dropdownMenu(type = "tasks", badgeStatus = "danger",
                 taskItem(value = 55, color = "aqua",
                          "Today's Chinese homework has been handed in"
                 ),
                 taskItem(value = 45, color = "green",
                          "Today's math homework has been handed in"
                 ),
                 taskItem(value = 75, color = "yellow",
```

## 转载来源

[shinydashboard系列一：标题栏](https://zhuanlan.zhihu.com/p/90018774)