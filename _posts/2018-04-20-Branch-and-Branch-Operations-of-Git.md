---
layout: post
title:  Git之分支及分支操作
key: 1011
top: false
tags: Git
category: blog
date: 2018-04-20 18:50:00 +08:00
modify_date: 2018-04-21 16:50:00 +08:00
---

## 1 什么是分支？

**粗暴型解释：** 即项目的一个副本，备份，但是Git相比这个粗暴型更加灵活，存储各分支并不是简单粗暴，不然就影响开发工作了，因为粗暴型的只会让仓库越来越重，而Git是通过文件快照和一系列指针和操作信息的保存，可以无缝切换分支(不同副本)工作，是轻量级的操作，能够快速的操作。

![分支示意图](https://raw.githubusercontent.com/yicm/Images/master/blog/git_branch.png)

一般创建好Git仓库的时候，默认属于Master分支。Git提供了强大的分支管理功能，分支也是Git的一大利器，因此我们要充分发挥分支的作用。
{:.info}

## 2 分支的作用

使用分支可以很好的管理我们的开发工作，比如在主体的开发分支上，我们可以开辟出bug修复分支，而从不影响主分支的开发，可以开辟出临时功能开发分支，还可以开辟出针对不同用户或者平台产品的分支，等等等等。通过一定的开发模型，配合分支，形成Git工作流，提高团队开发效率以及规范化开发。
{:.info}

## 3 分支操作

```bash
# 查看分支
$ git branch branch_name
# 切换分支
$ git checkout branch_name
$ 基于当前分支新建一个分支
$ git branch new_branch_name
$ 基于当前分支新建一个分支，并切换到新建的分支
$ git checkout -b new_branch_name
# 删除一个分支（需处于另一个分支）
$ git branch -d branch_name
# 强制删除一个分支(需处于另一个分支)
$ git branch -D branch_name
$ git branch --delete --force branch_name
# 重命名一个分支
$ git branch -m old_branch_name new_branch_name
# 查看所有分支结构图，包括git stash操作缓存分支
$ git log --graph --decorate --all
# 分支合并
$ git merge 
$ git rebase 
```