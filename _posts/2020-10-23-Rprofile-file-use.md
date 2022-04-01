---
layout: post
title: "如何使用Rprofile文件"
date:   2020-10-23
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

Rprofile文件的配置使用，提高R编程效率。

<!-- more -->

## RProfile

On start-up R will look for the R-Profile in the following places: (Information from https://csgillespie.github.io/efficientR/3-3-r-startup.html#rprofile)

1. R_HOME: the directory in which R is installed.  Find out where your R_HOME is with the R.home() command.
2. HOME, the user’s home directory. Can ask R where this is with, path.expand("~") 
3. R’s current working directory. This is reported by getwd().

Note although there maybe different R-Profile files R will only use one in a given session. The preference order is:

Current project>Home>R_Home

To create a project-specific start-up script  create a .Rprofile file in the project’s root directory. 

You can access and edit the different .Rprofile files via

```
file.edit(file.path("~", ".Rprofile")) # edit .Rprofile in HOME
file.edit(".Rprofile") # edit project specific .Rprofile    
```

There is information about the options you can set via

```
help("Rprofile")
```

As mentioned the link above does provide additional details but the  points outlined above should show you where the files are and how to  access them.

```R
# r code
```

## Acknowledgements

* [source_title](https://stackoverflow.com/questions/46819684/how-to-access-and-edit-rprofile)