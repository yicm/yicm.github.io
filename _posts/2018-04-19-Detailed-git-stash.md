---
layout: post
title:  Git之git stash详解
key: 1012
top: false
tags: Git
category: blog
date: 2018-04-19 10:12:00 +08:00
modify_date: 2018-04-19 10:12:00 +08:00
---

## 1 为什么要用git stash？

**场景：**当你在某一个分支上工作时，突然因为某个原因想要切换到其他分支上看看或者操作，但是你又不想提交当前分支只改了部分代码的半成品，因此，你就可以使用`git stash`来缓存当前分支的操作工作，然后再切换到其他分支操作，等操作完了，你就可以切回来将缓存的操作弹出来继续操作。当然这个缓存的操作内容不仅仅可以弹出到原来的操作分支，还可以弹出到你想要的任意分支。
{:.info}

## 2 git stash操作步骤

**一般的操作步骤：**

```bash
# step0: 查看当前工作分支状态，存在未跟踪的文件file_name
$ git status
# step1： 将操作了一半的文件进行缓存，只需要git add，不需要commit
$ git add file_name
$ git stash
# step2: 再查看状态，此时提示工作分支很干净，无需任何操作，然后就可以切换到其他分支做你想做的事了
$ git status
$ git checkout other_branch_name

# ......

# step3: 其他分支操作完了，然后切回到原来分支后，重新把file_name弹出来继续操作
$ git stash pop
```

## 3 与git stash操作的一些常用命令

```bash
# 查看当前所有缓存操作的堆栈记录
$ git stash list
	stash@{0}: WIP on master: c1820a9 xxx information.
	stash@{1}: WIP on master: c1820a9 yyy information.

# 查看当前某个缓存的具体缓存内容
# x为缓存列表中的数字
$ git stash show -p stash@{x}
	
# 弹出缓存操作方式一
$ git stash pop

# 弹出缓存操作方式二
$ git stash apply

# 弹出指定的缓存操作，上述两种方式默认弹出缓存列表中最新的缓存记录
# 两种方式： apply & pop
$ git stash apply stash@{x}
$ git stash pop stash@{x}

# 删除某个缓存(不是弹出)
$ git stash drop stash@{x}

# 删除所有缓存
$ git stash clear
```

**注意：**`git stash apply`和`git stash pop`的区别就是前者将缓存的内容弹出来之后，缓存还存在一个副本在缓存列表中，后者是弹出来之后缓存堆栈中就没有这个记录了。
{:.warning}
