---
layout: post
title: "R 中环境文件.Renviron说明"
date:   2020-09-11
tags: [R]
comments: true
toc: true
author: Songbiao Zhu
---

R 中环境文件.Renviron的配置，可以提高R编程效率。

<!-- more -->

## Introduction

Once you start working with APIs, you will find yourself working with keys and tokens and shared secrets (shhhhh!!!) and the like. To the  extent possible, you should *avoid putting those sorts of things directly in your code*. The reason is quite simple: depending on the platform and its API,  those alphanumeric identifiers may very well unlock access to your data  for anyone who comes into possession of them. Or, if not unlocking  access to your data, they can enable others to use cloud-based resources (like the Google Cloud platform) that can cost you money!

R has a good way to drastically reduce the risk of this occurring. It’s up to you to take advantage of that mechanism, though.

## R Startup Files

R has a couple of “startup” files:

- `.Rprofile` gets executed every time R starts up, so, if you always want to run some specific script, you can put it in the `.Rprofile` file.
- `.Renviron` also gets evaluated every time an R session starts, but its sole purpose is to set *environment variables*.

We’re not going to go into detail on `.Rprofile` here, as it’s not used for the API key protection that we’re covering.

So, there’s a `.Renviron` file. File that away for now.

## A Hierarchy of Locations

These startup files can be located in three different locations, but only *one* version of any file will be read and used for any given R session. So,  which one gets used? The file that gets used is the one that exists at  the *lowest* level of the hierarchy. We’ll start from the top of the hierarchy.

### R_HOME

`R_HOME` is the directory in which R is installed. Enter `R.home()` to find out that location.

There may be cases where you want to put the `.Renviron` file here…but generally not. It’s just cleaner to keep “the program itself” separate from “the configuration of the program.”

### HOME

`HOME` is actually the user’s home directory. You can find out what your `HOME` directory is with `Sys.getenv("HOME")`. This *can* be a good place to locate your `.Renviron` file. It’s a good place *if* you are not setting any variables that you want to change from project to project.

### The Working Directory

We touched on this earlier, and it’s generally set as the current  project’s directory. You can find the current working directory with `getwd()`. If you have different credentials that you use with different projects, then you probably want to place your `.Renviron` file in the project directory.

## .Renviron File Structure

The structure of the `.Renviron` file is quite simple. It’s just a text file with one row for each variable you want to define. As an example, the following `.Renviron` file establishes two environment variables: `ADOBE_KEY` and `ADOBE_SECRET`. There is no magic to the naming – just make them clear (and ALL CAPS is a nice convention to use):

```
ADOBE_KEY="a7xxxxx639-iih-nordic-r"
ADOBE_SECRET="2eadxxxxx1495ea49"
```

## Accessing the Variables

Environment variables are accessed using the `Sys.getenv()` command.

Consider the above example. Let’s say that we’re writing a script that uses `RSiteCatalyst` and needs to use the API username and secret. In the script, we could  create two new objects, and then set them to be the values from the  environment variables:

```
adobe_key <- Sys.getenv("ADOBE_KEY")
adobe_secret <- Sys.getenv("ADOBE SECRET")
```

From that point onward, I can use `adobe_key` and `adobe_secret`. In this case, the objects created in the script were just lowercase forms of the actual environment variable. *This is not a requirement*. But, if what you’re storing is something where that sort of consistency makes sense, then it’s one approach for making things clear and  consistent.

## Avoiding Sharing .Renviron

We’ll cover Github later, but, if you’re using Github to manage your  projects (and there are lots of reasons to do that), you do *not* want to include your `.Renviron` file when you commit code to the repository. The way to bake this into  your process is to add a couple of lines (one line, really, but comments are nice to use):

```
# Environment file
.Renviron
```

The `.gitignore` file specifies which files to *not* include when checking updates into a repository. You may also want to include data files in the `.gitignore` file…but that’s a topic for another page.

## Acknowledgements

[.Renviron](http://www.dartistics.com/renviron.html)