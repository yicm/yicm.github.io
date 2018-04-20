---
layout: post
title: 两步走实现代码提交及Git命令的初步熟悉
key: 1008
top: false
tags: Git
category: blog
date: 2018-04-18 22:12:00 +08:00
modify_date: 2018-04-20 11:11:00 +08:00
---

## 1 两步走实现代码提交

使用`git add`和`git commit`两个命令就可以实现本地代码的提交。

```
# $ git add -A
$ git add FILENAME
$ git commit -m "your comment for this commit."
```

## 2 初步熟悉Git命令

```
$ git clone 
$ git init
$ git status
$ git log
$ git reflog
$ git checkout 
$ git reset 
$ git branch 
$ git mv
$ git rm
```
后续熟悉：

```
git checkout
git fetch
git pull
git push
git branch
git tag
git diff
```

> ![注意](https://github.com/yicm/Images/blob/master/common/tip_32.png?raw=true)`git reflog`可以查看所有分支的所有操作记录，包括`git commit`和`git reset`的操作，还包括已经被删除的commit记录，`git log`则不能查看已经删除了的commit记录。
