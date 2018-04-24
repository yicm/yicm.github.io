---
layout: post
title:  Git之本地和远端同步修改，开始初步冲突处理
key: 1014
top: false
tags: Git
category: blog
date: 2018-04-24 14:12:00 +08:00
modify_date: 2018-04-24 14:12:00 +08:00
---

## 1 冲突(conflict)起因

在Git中，不同分支合并到同一分支是很常见的操作，在不同的分支操作上，我们可能是修改了同一文件的不同行的地方，或者是不同的文件，这样的操作对分支的合并是影响不大的，两个分支也就比较容易合并。但是，当不同的开发者`对同一文件的同一行进行不同更改`时，或者`一个开发者编辑文件而另一个开发者却删除了这个文件`时，合并分支时就会发生冲突，这时候就必须先解决冲突s，然后才能合并分支。这同样适用于Github或者Gitlab的Merge Request(MR)操作，即开发者发起MR时，需要把所有冲突解决完时，MR才能合并成功。
{:.info}

- **冲突1：对同一文件的同一行进行不同更改:**

![冲突1](https://raw.githubusercontent.com/yicm/Images/master/blog/git_conflict1.png)
{:.shadow}
{:.rounded}

- **冲突2：一个开发者编辑文件而另一个开发者却删除了这个文件:**

![冲突2](https://raw.githubusercontent.com/yicm/Images/master/blog/git_conflict2.png)
{:.shadow}
{:.rounded}

## 2 解决冲突方式

**方式：**你必须在`命令行`或`GitHub等托管服务器`上手动选择你想要保留的代码，去掉冲突中不想要的代码，从而解决冲突。
{:.success}

- 对于上述所说的两种冲突类型均可以通过`命令行`的方式去解决。
- 对于简单的`冲突1`类型也可以直接在Github托管服务器上解决。

## 3 解决冲突具体方法和流程

### 3.1 本地命令行方式解决冲突

```bash
# 第一步：合并分支时发生了冲突(conflict)
# 第二步：查看当前冲突情况
$ git status
# On branch branch-b
# You have unmerged paths.
	#   (fix conflicts and run "git commit")
	#
	# Unmerged paths:
	#   (use "git add ..." to mark resolution)
	#
	# both modified:      test_conflict.txt
	#
no changes added to commit (use "git add" and/or "git commit -a")
# 第三步：打开冲突的文件，并进行修改，保留你想要的内容
# 通过搜索冲突标记符号<<<<<<<，可以快速定位冲突位置
# <<<<<<< HEAD  到 =======标记符号之间为一个分支修改内容
# ======= 到 >>>>>>>为另一个分支修改内容
# 保留你想要保留的内容，然后删除所有的标记符号
# 第四步：修改完冲突文件后，将修改文件添加到仓库跟踪中
$ git add -A
# 第五步：解决完冲突，提交内容
$ git commit -m "Resolved merge conflict."
# 第六步：合并分支
# 第七步：推送到远端仓库，然后在远端仓库，如Github发起Merge pull request.
```

### 3.2 Github上直接解决简单冲突

**第一步：** Github上已经存在待合并的两个分支
{:.success}

**第二步：** 点击“New pull request”
{:.success}

![点击New pull request](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_1.png)
{:.shadow}
{:.rounded}

**第三步：** 创建pull request，即点击“Create pull request”，标题和提交信息可以自定义
{:.success}

![Create pull request](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_2.png)
{:.shadow}
{:.rounded}

**第四步：** 点击“Resolve conflicts”按钮
{:.success}

![Resolve conflicts](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_3.png)
{:.shadow}
{:.rounded}

**第五步：** 开始修改冲突，保留你想要的内容
{:.success}

![修改冲突](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_4.png)
{:.shadow}
{:.rounded}

**第六步：** 解决完冲突，点击“Mark as resolved”，标记已解决该冲突
{:.success}

![Mark as resolved](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_5.png)
{:.shadow}
{:.rounded}

**第七步：** 点击“Commit merge”，提交合并
{:.success}

![Commit merge](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_6.png)
{:.shadow}
{:.rounded}

**第八步：** 重新发起Merge pull request，点击“Merge pull request”
{:.success}

![Merge pull request](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_7.png)
{:.shadow}
{:.rounded}

**第九步：** 确认合并分支，点击“Confirm merge”
{:.success}

![Confirm merge](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_8.png)
{:.shadow}
{:.rounded}

**第十步：**分支合并完成，选择是否要删除已经合并掉的分支
{:.success}

![分支合并完成](https://raw.githubusercontent.com/yicm/Images/master/blog/github_pr_9.png)
