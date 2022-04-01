---
layout: post
title: "Rtools4 is required for build R packages报错解决方法"
date:   2020-10-19
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

从R4.0.0(发布于2020年4月)开始，R for Windows使用了一个名为rtools40的全新工具链包。对于需要使用C/C++/Fortran code的部分R包，需要首先安装新的rtools40工具包才可以安装包。

<!-- more -->

## 报错信息

Rtools4 is required for build R packages but is not currently installed. Please download and install the appropriate version of Rtools before preceding:

## 报错处理

### 1. 检查R和RStudio版本

* R版本是R 4.0.0 或者更新版本。（R中输入`sessionInfo()` 查看R版本 ）
* RStudio 版本是 `1.2.5042`或者更新。（点击RStudio 中菜单栏Help查看RStudio版本）

### 2. 安装Rtools40

要使用rtools40，请从CRAN下载安装程序:

- On Windows 64-bit: [rtools40-x86_64.exe](https://cran.r-project.org/bin/windows/Rtools/rtools40-x86_64.exe) (recommended: includes both i386 and x64 compilers)
- On Windows 32-bit: [rtools40-i686.exe](https://cran.r-project.org/bin/windows/Rtools/rtools40-i686.exe) (i386 compilers only) 

下载后按提示安装即可。

### 3. 配置Rtools40的路径

* 打开R控制台，输入`writeLines('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', con = "~/.Renviron")`,运行。

* 重启R，输入`Sys.which("make")`，若返回你的Rtools安装路径即表示成功。例如，

    ```
    Sys.which("make")
    ## "C:\\rtools40\\usr\\bin\\make.exe"
    ```

### 4. install.packages() 安装感兴趣包即可

如，`install.packages("lubridate")`

## 参考资料

*  [Using Rtools40 on Windows](https://cran.r-project.org/bin/windows/Rtools/)