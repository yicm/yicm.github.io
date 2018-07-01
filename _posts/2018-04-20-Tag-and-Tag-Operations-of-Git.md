---
layout: post
title:  Git之tag及tag操作
key: 1012
top: false
tags: Git
category: blog
date: 2018-04-23 15:42:00 +08:00
modify_date: 2018-04-23 15:42:00 +08:00
---

## 1 什么是Tag？

Tag可以认为是一个标签，某个版本的标签，如某个分支在不同时期发布版本的标签，可以打上tag。

![分支示意图](https://raw.githubusercontent.com/yicm/Images/master/blog/git_tag.png)


## 2 Tag和[分支](https://yicm.github.io/blog/2018/04/20/Branch-and-Branch-Operations-of-Git.html)的区别

Tag代表某个特定分支的版本，而分支代表一个独立的开发线程，可以与同一代码库上的其他开发线程同时运行。分支更多的是提供对特定版本代码的持续更新，同时继续对其进行开发，并有可能在某一天合并到其他分支，从而该分支也可能会删除。
{:.info}

## 3 Tag的作用和特点

- 对分支中特定版本进行打标签，如V.0之类
- 标签是永久作用的，无法更改的，除非删除了这个标签
- tag可以认为是某个commit的重命名

## 4 Tag操作

**查看：**
```bash
# 查看所有标签
$ git tag
# 查看标签的版本信息，并连同显示打标签时的提交对象
$ git show tag_name
# 按相关信息查看标签，只显示1.1 系列的版本
# -nN 每个标签信息打印N行出来，N为数字
$ git tag -l "v1.1.*"
$ git tag -ln2 "v1.1.*"
# 查看标签和分支树状简图
$ git log --oneline --decorate --graph
```
**创建：**Git标签有两种，一种是轻量级的，一种是包含附加信息的。轻量级其实就是指向特定提交对象的引用，而附加型实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，电子邮件地址和日期，以及标签说明，标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证。

建议使用附加型的打标签方式。
{:.info}

```bash
# 轻量级标签创建
$ git tag new_tag_name

# 附加型标签创建
# -a 附加型标签创建选项
# -m 选项则指定了对应的标签说明
$ git tag -a new_tag_name -m 'The comment of your new tag.'

# 对某个提交打标签，c1820a9为某个提交对象的校验和(哈希码，唯一标识)
$ git tag -a new_tag_name c1820a9
```

**删除标签：**

```bash
# 删除本地标签
$ git tag -d your_tag_name
# 删除远程标签
$ git push origin --delete tag tag_name

```

**与远端仓库共享标签：**

```bash
# 单个标签共享
$ git push origin your_tag_name
# 所有标签一次性共享
$ git push origin --tags
```

**采用GPG签署验证：**

GPG是加密软件，可以使用GPG生成的公钥在网上安全的传播你的文件、代码，防止别人篡改。比如在你建立的标签v1.0处你想要做代码修改，修改完后将这个tag删除，然后又创建同名tag指向刚刚修改过的提交对象，正常的附加型和轻量级标签都是没问题的。但是，采用了GPG签署过的v1.0，即使你修改了代码，删除tag，重新创建同名tag，在你再次clone你修改后的项目时，你会发现，你对此tag的改变不被认可，验证失败，导致你的修改在这里无法正常实现。这也保证了最高权限的项目负责人不允许其他开发人员去修改这个tag代码。
{:.success}

```bash
# 创建GPG Key
# 根据提示选择并创建key
$ gpg --gen-key

# 验证是否创建key成功，显示公钥
$ gpg --list-keys
# 显示私钥
$ gpg --list-secret-keys

# 使用GPG加密tag
$ git tag -s new_tag_name -m "The comment of your new tag.e"

# 验证GPG加密的tag，注意验证前签署者的公钥需存放在 keyring 中
$ git tag -v your_tag_name
```



