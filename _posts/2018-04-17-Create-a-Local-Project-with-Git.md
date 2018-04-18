---
layout: post
title: 使用Git建立本地仓库及gitignore文件介绍
key: 1007
tags: Git
category: blog
date: 2018-04-18 19:12:00 +08:00
modify_date: 2018-04-18 19:12:00 +08:00
---

## 1 初步认识Git命令

```
$ git --help
用法：git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

这些是各种场合常见的 Git 命令：

开始一个工作区（参见：git help tutorial）
   clone      克隆一个仓库到一个新目录
   init       创建一个空的 Git 仓库或重新初始化一个已存在的仓库

在当前变更上工作（参见：git help everyday）
   add        添加文件内容至索引
   mv         移动或重命名一个文件、目录或符号链接
   reset      重置当前 HEAD 到指定状态
   rm         从工作区和索引中删除文件

检查历史和状态（参见：git help revisions）
   bisect     通过二分查找定位引入 bug 的提交
   grep       输出和模式匹配的行
   log        显示提交日志
   show       显示各种类型的对象
   status     显示工作区状态

扩展、标记和调校您的历史记录
   branch     列出、创建或删除分支
   checkout   切换分支或恢复工作区文件
   commit     记录变更到仓库
   diff       显示提交之间、提交和工作区之间等的差异
   merge      合并两个或更多开发历史
   rebase     在另一个分支上重新应用提交
   tag        创建、列出、删除或校验一个 GPG 签名的标签对象

协同（参见：git help workflows）
   fetch      从另外一个仓库下载对象和引用
   pull       获取并整合另外的仓库或一个本地分支
   push       更新远程引用和相关的对象

命令 'git help -a' 和 'git help -g' 显示可用的子命令和一些概念帮助。
查看 'git help <命令>' 或 'git help <概念>' 以获取给定子命令或概念的
帮助。

```

## 2 建立本地Git版本管理项目

```
$ mkdir project_name
$ cd project_name
$ git init
```

## 3 仓库之.gitignore文件

### 3.1 .gitignore作用

过滤一些我们不想提交(commit)文件或目录，比如临时文件(*.bak/*.swp等)，二进制文件(*.exe/*.bin/*.so/*.a等)，比如编译输出目录(./build)等等;


### 3.2 什么时候用.gitignore？

- IDE产生的文件，如Virtual studio编译产生的输出文件
- 编辑器时产生的临时备份文件，如Vim编辑时会产生*.swp等临时文件
- 不想上传的文件，比如测试图片之类的

### 3.3 如何写.gitignore？

- .gitignore文件每一行代表一个过滤模式
- .gitignore可以设置成全局的，即对有所的项目生效；可以是只针对项目，即放入项目所在目录；
- 可以只编写对本地项目有效的gitignore文件，无需另外写.gitignore文件，即编辑.git/info/exclude
```bash
# 1 编辑配置文件~/.gitconfig，指定全局gitignore文件
[core]
excludesfile = /home/username/.gitignore
# 2 编写~/.gitignore过滤模式
```
- 项目的每个文件夹都可以放一个.gitignore文件，只作用于当前文件夹和子文件夹；

.gitignore具体编写规则：

- 每一行代表一个过滤规则
- 空白行无过滤性质，可以作为分隔符
- 以`#`符号作为注释符号
- `*.txt`，即过滤掉所有以txt结尾的文件或`文件夹`
- `?.txt`，即将问号(?)替换成任何一个字符(除斜杠'/'外)所得到的文件将会被过滤掉
- `[01234].txt`匹配中括号内的任一个`字符`，即0.txt、1.txt...。
- `/dir`，过滤掉当前目录的dir文件夹，而不过滤子目录中含有dir的文件夹
- 每一行的过滤规则的最后空格是不计入的，除非使用转义符号`\`
- 以`!`符号作为规则前缀，则表示取反，不过滤该模式下的内容
- 过滤文件夹的时候，如果只写了文件夹的名称，那么则会将所有同名的文件夹或者文件都会过滤掉，只想过滤文件夹，那么需要加上斜杠`Directory/`
- `build/*`，过滤掉build目录下所有的文件和文件夹，等同于`build/**`
- `build/*.txt`，仅过滤掉build目录下的txt文件，不过滤其子文件夹里面的txt文件
- 斜杠后(/)跟两个连续的星号(\*\*)，则斜线匹配零个或多个目录。例如，"a/\*\*/b"与"a/b"，"a/x/b"，"a/x/y/b"等匹配
示例：

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

### 3.4 .gitignore的作用优先级

- `项目.gitignore`优先级大于`只对本地有效的.git/info/exclude文件`优先级大于`全局.gitignore`
- `子文件夹的.gitignore`优先级大于`父级.gitignore文件`，如父级过滤规则中过滤掉了`*.txt`文件，但是子文件夹不想过滤掉，则可以使用`!*.txt`规则不过滤掉txt文件，当然子文件夹的.gitignore起作用的前提是父级的.gitignore没有过滤这个子文件夹。

> ![注意](https://github.com/yicm/Images/blob/master/common/tip_32.png?raw=true) 根据优先级，因此推荐项目开发时采用项目.gitignore的方式，这样所有的开发人员都能够共享过滤规则。

### 3.5 .gitignore注意事项和操作小细节

![注意](https://github.com/yicm/Images/blob/master/common/tip_32.png?raw=true).gitignore文件是无法对已经跟踪(tracked,即git add操作了)了的文件起作用的

解决办法： 

```
# 对所有文件和文件夹操作，删除跟踪缓存
git rm -r --cached .
# 针对具体的文件操作，删除跟踪缓存
git rm --cached FILENAME
# gitignore已生效，可以继续操作
git add -A
git commit -m "update .gitignore to remove tracked files"
```

![注意](https://github.com/yicm/Images/blob/master/common/tip_32.png?raw=true)如果你没有权限修改或者不能修改全局.gitignore，但是你想过滤掉某些文件下的文件，怎么办？

解决办法：
```
在待过滤的文件夹下建立你自己的.gitignore文件即可
```
### 3.6 常见.gitignore文件大全

[https://github.com/github/gitignore](https://github.com/github/gitignore)
