---
abbrlink: ''
categories:
- - windows
- - 终端
- - 命令行
cover: https://s2.loli.net/2023/01/08/tFdGpRq5Z8Wg2aI.jpg
date: '2023-01-08 01:03:43'
tags:
- windows
- 终端
- 命令行
title: 让你的windows命令行体验更佳
updated: '2023-01-16 16:10:12'
---
相信我们都被windows 糟糕的命令行体验而折磨，那么，与其等待微软的跳票，不如由我们自己堆插件提升命令行体验。

# 安装 git for windows

打开 [git官网](https://git-scm.com/downloads/win)下载 Standalone版本git并安装

安装时候一路点击`next`

## 配置git 环境变量

`win + r`，输入 `sysdm.cpl`

![image.png](https://s2.loli.net/2023/01/08/7LOIdoewrltAjzg.png)

然后点击回车

依次选择`高级` `环境变量`

![image.png](https://s2.loli.net/2023/01/08/3DObsKHEmndlJgc.png)

![image.png](https://s2.loli.net/2023/01/08/M5CO4ZgTIPwHc9X.png)

然后双击 系统变量里的 `path`

![image.png](https://s2.loli.net/2023/01/08/tpSmN94OkUwz3Gu.png)

点击 `新建`

分别输入 （p.s.默认git安装目录为C:\Program Files\Git）

（下列%git安装目录%为一个变量，并不需要添加`%`）

```
%git安装目录%\cmd
```

```
%git安装目录%\mingw64\bin
```

```
%git安装目录%\usr\bin
```

然后点击ok并关闭窗口

# 安装sudo for windows（gsudo）

[github项目地址](https://github.com/gerardog/gsudo)

`win` + `r` ，输入`powershell`

```
winget install gerardog.gsudo
```

# 安装 wget for windows （GNU WGET)

GNU Wget是一个在网络上进行下载的简单而强大的自由软件，其本身也是GNU计划的一部分。它的名字是“World Wide Web”和“Get”的结合，同时也隐含了软件的主要功能。目前它支持通过HTTP、HTTPS，以及FTP这三个最常见的TCP/IP协议协议下载。

[wget下载链接](https://nchc.dl.sourceforge.net/project/gnuwin32/wget/1.11.4-1/wget-1.11.4-1-setup.exe)

按照之前那一步，添加环境变量

```
%GNU安装路径%\bin
```

# tcping 安装

[下载链接](https://download.elifulkerson.com/files/tcping/current/tcping.exe)

将下载好的文件复制到 `C:\windows\system32`
