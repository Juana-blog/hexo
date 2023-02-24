---
abbrlink: better-windows-cmd
categories:
- - windows
- - cmd
cover: https://s2.loli.net/2023/01/08/tFdGpRq5Z8Wg2aI.jpg
date: '2023-01-08 01:55:50'
tags:
- windows
- cmd
title: Make your windows command line experience better
updated: '2023-01-08 01:59:55'
---
# This article was translated by the Chinese version using Google Translate

Chinese version:[让你的windows命令行体验更佳 | ursb's blog](https://blog.ursb.eu.org/让你的windows终端更好用/)

I believe that we are all tortured by the poor command line experience of windows, so, instead of waiting for Microsoft's bounced ticket, it is better for us to pile up plug-ins to improve the command line experience.

# install git for windows

Open [git official website] (https://git-scm.com/downloads/win) to download the Standalone version git and install it

Click `next` all the way during installation

## Configure git environment variables

`win + r`, enter `sysdm.cpl`

![image.png](https://s2.loli.net/2023/01/08/7LOIdoewrltAjzg.png)

then hit enter

Select `Advanced` `Environment Variables`

![image.png](https://s2.loli.net/2023/01/08/3DObsKHEmndlJgc.png)

![image.png](https://s2.loli.net/2023/01/08/M5CO4ZgTIPwHc9X.png)

Then double-click `path` in the system variable

![image.png](https://s2.loli.net/2023/01/08/tpSmN94OkUwz3Gu.png)

Click on `New`

Enter respectively (p.s. The default git installation directory is C:\Program Files\Git)

(The following %git installation directory% is a variable and does not need to add `%`)

```
%git installation directory%\cmd
```

```
%git installation directory%\mingw64\bin
```

```
%git installation directory%\usr\bin
```

Then click ok and close the window

# Install sudo for windows (gsudo)

[github project address](https://github.com/gerardog/gsudo)

`win` + `r`, enter `powershell`

```
winget install gerardog.gsudo
```

# Install wget for windows (GNU WGET)

GNU Wget is a simple and powerful free software download on the Internet, which is itself part of the GNU project. Its name is a combination of "World Wide Web" and "Get", which also implies the main function of the software. Currently it supports downloading via HTTP, HTTPS, and FTP, the three most common TCP/IP protocols.

[wget download link](https://nchc.dl.sourceforge.net/project/gnuwin32/wget/1.11.4-1/wget-1.11.4-1-setup.exe)

Follow the previous step to add environment variables

```
%GNU installation path%\bin
```

# install tcping

[Download link](https://download.elifulkerson.com/files/tcping/current/tcping.exe)

Copy the downloaded file to `C:\windows\system32`
