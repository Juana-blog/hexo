---
abbrlink: ms-pwtys
categories:
- - Microsoft
- - windows
- - Utilities
cover: https://s2.loli.net/2023/03/26/24m1MAwFlEsOoKg.jpg
date: '2023-03-26 17:26:52'
tags:
- Microsoft
- windows
- Utilities
title: Use Microsoft open source tools PowerToys to enhance your windows experience
updated: Sun, 26 Mar 2023 09:26:59 GMT
---
# This article was translated by the Chinese version using Google Translate

Chinese version:[使用Microsoft开源工具PowerToys提升你的windows使用体验](https://hexo.myfw.us/%E4%BD%BF%E7%94%A8Microsoft%E5%BC%80%E6%BA%90%E5%B7%A5%E5%85%B7PowerToys%E6%8F%90%E5%8D%87%E4%BD%A0%E7%9A%84windows%E4%BD%BF%E7%94%A8%E4%BD%93%E9%AA%8C/)

I believe that when you use windows, you must have encountered some useful functions that windows does not come with.😦

Recently, a **free open source** tool from Microsoft has aroused my interest and made me feel very amazing. It is **PowerToys**, let me introduce this **gadget integration* *software.

Below I will recommend some small functions in **PowerToys** that I really need:

# Practical function recommendation

## Text extraction tool (OCR)

![image.png](https://s2.loli.net/2023/03/26/WKZgt8FLiuc6vp9.png)

As its introduction says, its function is to "frame select screenshots, extract text and copy with one click"

Editor's evaluation: The recognition rate of this tool is very accurate, but the recognized text has spaces, as shown in the figure below.

![Original Picture.png](https://s2.loli.net/2023/03/26/iyOBUztMTqKPIkm.png)

(The above is the original image for identification)

(The following is the recognized text)

![image.png](https://s2.loli.net/2023/03/26/HLg9zmbpCvIlxN8.png)

(The recognized text is `文本提取器功能由系统 OCR 识别包提供 ， 可按需安装更多语言`)

## Domain name (Hosts) modifier

![image.png](https://s2.loli.net/2023/03/26/HFLNfeScypYr12K.png)

As the introduction said, the function of this tool is to graphically modify hosts

![image.png](https://s2.loli.net/2023/03/26/apxr9usYoNWzRUf.png)

## batch rename

![image.png](https://s2.loli.net/2023/03/26/zJFSyeW4ma8ip6j.png)

Function: **Simple file renaming tool, can search and replace file names.**

How to use: `Select several files, right-click , and select Batch Rename in the right-click menu`

![image.png](https://s2.loli.net/2023/03/26/GNBs7Onjb9livH5.png)

(Batch renaming supports regular expressions)

## Meeting Assistant

![image.png](https://s2.loli.net/2023/03/26/NjT7dEsl83QzxP9.png)

Function: `Allow users to mute the microphone and turn off the camera with one click during a remote meeting.`

Of course, this tool is definitely more than the above functions

# Install PowerToys

After the above introduction, you must want to know how to install this software

## Github installation

[Github releases](https://github.com/microsoft/PowerToys/releases)

Download your corresponding .exe installation package and install

## winget install

open powershell

enter

```
winget install Microsoft.PowerToys --source winget
```

## Microsoft store installation

[Microsoft Store](https://aka.ms/getPowertoys)

# For Chinese users (install Chinese package)

[PowerToys Chinese unofficial GH link](https://github.com/ZetaSp/PowerToys-Chinese-TransMOD/releases)

Alternate download installation package and Sinicization [Blue Cloud][https://zeta.lanzoue.com/b01kkm1te](https://zeta.lanzoue.com/b01kkm1te) Password: zeta

## Usage Usage

① Install the original PowerToys software:

Download the .exe installation package and install the PowerToys software

② One-click installation optimization patch package:

Download PCTMODx\*\*\*.7z (with automatic installation program), run "Install.CMD" after decompression, and confirm the installation according to the prompt
