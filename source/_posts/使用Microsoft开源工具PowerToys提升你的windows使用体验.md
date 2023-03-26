---
abbrlink: ms-pwtys
categories:
- - Microsoft
- - windows
- - 实用工具
cover: https://s2.loli.net/2023/03/26/24m1MAwFlEsOoKg.jpg
date: '2023-03-26 17:26:52'
tags:
- Microsoft
- windows
- 实用工具
title: 使用Microsoft开源工具PowerToys提升你的windows使用体验
updated: Sun, 26 Mar 2023 09:26:59 GMT
---
相信在大家使用windows时,肯定遇到过一些windows没有自带,却十分实用的功能.😦

而近期微软的一款**免费开源**的工具引起了我的兴趣，并且让我感到非常惊艳，它就是**PowerToys**，下面就让我来介绍一下这款**小工具整合**软件.

下面我将推荐一些**PowerToys**里的个人十分需要的小功能:

# 实用功能推荐

## 文字提取工具(OCR)

![image.png](https://s2.loli.net/2023/03/26/WKZgt8FLiuc6vp9.png)

正如它的介绍所说 它的功能就是 `框选截图 一键提取文字并复制`

小编评价:这款工具的识别文字准确率十分的准确,但是识别后的文字带有空格 如下图会出现如下图情况

![原图.png](https://s2.loli.net/2023/03/26/iyOBUztMTqKPIkm.png)

(上述为识别原图)

(下述为识别到的文本)

![image.png](https://s2.loli.net/2023/03/26/HLg9zmbpCvIlxN8.png)

（识别到的文本为`文本提取器功能由系统 OCR 识别包提供 ， 可按需安装更多语言`)

## 域名(Hosts)修改器

![image.png](https://s2.loli.net/2023/03/26/HFLNfeScypYr12K.png)

正如介绍所说,这个工具的作用是图形化修改hosts

![image.png](https://s2.loli.net/2023/03/26/apxr9usYoNWzRUf.png)

## 批量重命名

![image.png](https://s2.loli.net/2023/03/26/zJFSyeW4ma8ip6j.png)

功能: **简单的文件重命名工具,可以搜索和替换文件名.**

使用方法:`选中几个文件，单击 右键 ，然后在右键菜单中选择 批量重命名`

![image.png](https://s2.loli.net/2023/03/26/GNBs7Onjb9livH5.png)

(批量重命名支持正则表达式)

## 会议助手

![image.png](https://s2.loli.net/2023/03/26/NjT7dEsl83QzxP9.png)

功能:`让用户可以在远程会议时一键静音麦克风和关闭摄像头.`

当然 这款工具肯定不止以上的这些功能

# 安装PowerToys

经过了以上的介绍 想必你想知道如何安装这款软件

## Github安装

[Github releases](https://github.com/microsoft/PowerToys/releases)

下载你所对应的.exe安装包 安装

## winget安装

打开powershell

输入

```
winget install Microsoft.PowerToys --source winget
```

## 微软商店安装

[微软商店](https://aka.ms/getPowertoys)

# 对于中文用户(安装汉化包)

[PowerToys中文非官方GH链接](https://github.com/ZetaSp/PowerToys-Chinese-TransMOD/releases)

备用下载安装包和汉化[蓝奏云][https://zeta.lanzoue.com/b01kkm1te](https://zeta.lanzoue.com/b01kkm1te) 密码：zeta

## Usage 使用方法

① 安装原版 PowerToys 软件：

　　下载 .exe 安装包，安装 PowerToys 软件

② 一键安装优化补丁包：

　　下载 PCTMODx\*\*\*.7z（带有自动安装程序），解压后运行“安装.CMD”，根据提示确定安装
