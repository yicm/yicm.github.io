---
layout: post
title:  本地Git仓库操作实战演练
key: 1009
top: false
tags: Git
category: blog
date: 2018-04-19 9:12:00 +08:00
modify_date: 2018-04-19 9:12:00 +08:00
---

&emsp;&emsp;这一篇主要为实操演练，具体内容要结合视频来学习。

## Git

```
$ git clone 
$ git init
$ git status
$ git log
$ git checkout 
$ git remote 
$ git branch 
$ git diff
$ git reset
$ git mv
$ git rm
```

## Git gitignore

```bash
# 过滤掉txt结尾文件和文件夹
*.txt
# 重新去除过滤掉txt结尾文件或文件夹
!*.txt

# 过滤掉当前目录的foo文件夹，而不过滤子目录中含有foo的文件夹
/foo
# 过滤掉build目录下所有的文件和文件夹
build/*
# 过滤掉所有test目录
test/
# 过滤掉所有test目录和test文件
test
```