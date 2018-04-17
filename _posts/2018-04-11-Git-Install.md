---
layout: post
title: Git安装
key: 1004
tags: Git
category: blog
date: 2018-04-11 19:01:00 +08:00
modify_date: 2018-04-11 19:02:00 +08:00
---

# Windows系统

在Windows系统下，可以选择几种方式去安装git：

- 通过安装[https://cygwin.com/install.html](https://cygwin.com/install.html)(Cygwin是一个在windows平台上运行的类UNIX模拟环境)，然后再Cygwin中安装git
- Win10中安装Ubuntu应用，然后在应用中安装git
- https://gitforwindows.org/ 下载gitfor windows
- 通过其他虚拟化技术，可以是Virtual Box虚拟机或者是Boot2Docker容器等，然后在虚拟机中的系统中安装git

以上四种方式中，第三种方式支持带界面的git操作，这里推荐第一种，第二种方式，这两种方式是纯命令去操作的，因为纯命令操作对于技术开发者而言在很多方面是更方便的，比如更换了操作系统，我们就很容易去适应新的环境。这里只具体的对Cygwin方式做具体的说明，即第一种方式：

**Cygwin方式安装git:**

1. http://www.cygwin.com/下载安装程序setup-x86_64.exe
2. 选择从Internet安装

![Install from Internet](https://github.com/yicm/Images/blob/master/blog/git_install_1.png?raw=true)

3. 选择安装目录

![选择安装目录](https://github.com/yicm/Images/blob/master/blog/git_install_2.png?raw=true)

4. 选择软件包下载缓存目录:当想安装其他工具时，有了缓存包，不必从头安装已经安装过的软件包

![选择软件包下载缓存目录](https://github.com/yicm/Images/blob/master/blog/git_install_3.png?raw=true)

5. 设置网络连接方式是否使用代理等，默认。

![](https://github.com/yicm/Images/blob/master/blog/git_install_4.png?raw=true)

6. 选择软件包下载源，注意，不同的软件源可能网络下载速度不一样。

![](https://github.com/yicm/Images/blob/master/blog/git_install_5.png?raw=true)

7. 然后在软件包管理器界面选择安装Git相关的软件包：
- git: git工具
- git-completion：Git 命令的自动补齐功能包

![](https://github.com/yicm/Images/blob/master/blog/git_install_6.png?raw=true)

8. 下一步，等待安装完成。
9. 打开Cygwin，测试是否安装成功：

![](https://github.com/yicm/Images/blob/master/blog/git_install_7.png?raw=true)

# Linux系统

Fedora或者Centos系统使用如下命令进行安装：

```
$ sudo yum install git-core
```

而Ubuntu 这类 Debian 体系的系统上，可以用 apt-get 安装：

```
$ sudo apt-get install git
```


