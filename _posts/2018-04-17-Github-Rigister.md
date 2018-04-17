---
layout: post
title: Github账号注册及HTTPS/SSH连接方式介绍
key: 1006
tags: Git Study
category: blog
date: 2018-04-17 19:12:00 +08:00
modify_date: 2018-04-17 19:12:00 +08:00
---
# 注册Github账号

[https://github.com/join](https://github.com/join)

# 使用SSH/HTTPS方式连接Github

## 两者区别和HTTPS连接方式

&emsp;&emsp;有两种方式可以去连接Github，比如使用`git clone`、`git fetch`、`git pull`、`git push`到一个远端(Github)仓库的时候：

- 使用HTTPS的方式（推荐）: 每当使用上述命令的时候，系统需要你输入Github的用户名和密码来确认操作。
- 使用SSH的方式: 使用SSH协议，你可以连接并验证远程服务器和服务；使用SSH密钥，你可以连接到GitHub，而无需在每次访问时提供用户名或密码。

&emsp;&emsp;另外如果你设置了[双因素身份验证](https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/)，不仅需要用户名和密码，还需要使用辅助方式来验证，即下面两种方式：
    - 使用手机APP获取双因素认证码来验证
    - GitHub发送带双因素认证码的短信来验证


**建议：**可以通过设置来实现用户名和密码的缓存（Linux系统下）:

```
# 设置git以使用凭证内存缓存
$ git config --global credential.helper cache
# 将缓存设置为1小时后超时（秒为单位）
$ git config --global credential.helper 'cache --timeout=3600'

```
## SSH连接方式

&emsp;&emsp;创建一个SSH key:

(1) 打开Cygwin或者类UNIX系统终端
(2) 创建ssh key,并以your_email@example.com作为标签

`$ ssh-keygen -t rsa -C "your_email@example.com"`

(3) 一路回车，创建成功。
(4) 查看SSH key公钥

`$ cat ~/.ssh/id_rsa.pub`

(5) [将公钥复制到Github配置项](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

![](https://github.com/yicm/Images/blob/master/blog/git_register_1.png?raw=true)

# 建立第一个Github项目(仓库)

1) 登陆Github

[https://github.com/login](https://github.com/login)

2) 点击**“New repository”**，并设置待创建项目信息

![](https://github.com/yicm/Images/blob/master/blog/git_register_2.png?raw=true)

3) 填写项目信息，点击提交。
