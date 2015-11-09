title: Git修改远程仓库地址
date: 2015-07-23
category: 教程
tags: git
keywords: git
description: git这种操作性的工具，一般情况下都是有碰到不清楚的命令，才去查询。更改远程仓库地址就是其中遇到的问题之一。

---

# git 系列教程

## 修改远程仓库地址

故事： 某天，远程系统目录有变，或者仓库服务器地址换了，本地有clone的git库，
那就得修改origin地址，以便能继续在原本地仓库继续push，pull。

**在本地仓库所在目录x执行：**

> git remote set-url origin THE-NEW-ORIGIN-ADDRESS


就这样。
