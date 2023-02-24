---
abbrlink: ''
categories:
- - cloudflare-warp
- - windows
- - wgcf
cover: https://s2.loli.net/2023/01/01/yMRSO1297k3ZjHQ.png
date: '2023-01-01 01:29:10'
tags:
- cloudflare-warp
- windows
- wgcf
title: wgcf for windows教程
updated: '2023-01-01 01:29:10'
---
校园网的IPv4收费不少高校都比较贵，而IPv6是不限速不限量的。经过2020年9月10日教育网的路由变动后，CERNET在HKIX与HE以Peer via IX的形式进行了互联。因为HE本身是IPv6的顶级之一，其在HKIX的互联还是一个开放的Public Peering，极大的降低了到达CERNET香港互联点的难度。这样修改之后虽然到HKIX那10G的链路出现了一定程度的拥塞，但是速度还是远优于以前的北美方向。


## 一、下载WGCF


WGCF是一个基于`Go`语言编写的WARP管理程序，作者一直在维护，使用起来相当方便

> 项目地址：[https://github.com/ViRb3/wgcf](https://github.com/ViRb3/wgcf)

前往release页面选择自己便于使用的平台对应的预编译程序，考虑到与CF通信的顺畅我选择的是位于境外的VPS进行操作，本地的话因为CF这项服务的特殊性很可能是不行的


```
新建一个文件夹
将下载的文件解压进这个文件夹
```

截至文章发布，releases版本为v2.2.15


## 二、修改配置文件

初次使用首先就是注册个用户并生成配置文件：

```

./wgcf_2.2.15_windows_amd64.exe register --accept-tos （注册cloudflare warp免费账户）

./wgcf_2.2.15_windows_amd64.exe generate （生成warp wireguard配置文件）


```

打开`wgcf-profile.conf`，将 `Endpoint = engage.cloudflareclient.com:2408`

改为`Endpoint = 162.159.193.1:2408`


## 三、连接

新建空隧道，将修改后的文件粘贴进去，即可使用
