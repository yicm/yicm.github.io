---
layout: post
title:  Git之开始本地和远端的互动操作
key: 1010
top: false
tags: Git
category: blog
date: 2018-04-20 16:50:00 +08:00
modify_date: 2018-04-20 16:50:00 +08:00
---

## 两种方式连接远端服务器Github

方式一：

```
# 直接克隆下项目，然后就可以直接基于该项目进行版本管理操作了
$ git clone https://github.com/XiaoBaiAI/My-First-Project.git
```

方式二：

```
# 本地有一个项目，但是还未进行Git版本管理
# 第一步： 创建一个Github远端空项目(无任何文件)
# 第二步： 本地项目进行Git版本管理，并设置远端服务器项目地址
$ cd your_local_project_directory
$ git init
$ git add -A
$ git commit -m "project init"
$ git remote add origin https://github.com/XiaoBaiAI/My-First-Project.git
$ git push -u origin master
```

> ![注意](https://github.com/yicm/Images/blob/master/common/tip_32.png?raw=true) 如果`方式二`中不是空的，带有README.md，那么需要先将远端服务器(Github)上内容fetch或者pull下来，然后与本地项目合并再push到远端服务器上。

## 本地和远端的互动操作

**`git remote` **： Git是分布式管理的，可以认为Github是另外一个项目人员，你把代码交给他管理，就需要添加同一个项目他的仓库管理地址；另外，`git remote`可以添加多个这样的地址，意味着多个管理端，这中间就涉及到合并和冲突等各种处理。

**`git fetch`** ：拉取远端仓库代码，并创建一个临时的隐藏分支`FETCH_HEAD`，并将其将其记录到.git/FETCH_HEAD文件中。

**`git pull` **： `git fetch`和`git merge`的两种操作结合，即先拉取远端仓库代码到本地的临时分支`FETCH_HEAD`，然后合并该分支到当前的分支。

**`git push`** ： 将本地仓库代码推送到远端仓库，保持同步。



