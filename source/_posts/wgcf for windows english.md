---
abbrlink: ''
categories:
- - english
- - wgcf
- - cloudflare-warp
- - windows
cover: https://s2.loli.net/2023/01/01/yMRSO1297k3ZjHQ.png
date: '2023-01-01 01:45:08'
tags:
- english
- cloudflare-warp
- windows
- wgcf
title: wgcf for windows
updated: '2023-01-01 01:45:08'
---
# This article was translated by the Chinese version using Google Translate

Chinese version:[wgcf for windows教程](https://hexo.gw.to/wgcf/)


The IPv4 charges of the campus network are relatively expensive in many colleges and universities, while IPv6 has unlimited speed and limit. After the routing change of the education network on September 10, 2020, CERNET was interconnected with HE at HKIX in the form of Peer via IX. Because HE itself is one of the top IPv6, its interconnection in HKIX is still an open Public Peering, which greatly reduces the difficulty of reaching the CERNET Hong Kong interconnection point. After this modification, although the 10G link to HKIX has a certain degree of congestion, the speed is still much better than the previous North American direction.

## 1. Download WGCF

WGCF is a WARP management program based on `Go` language, the author has been maintaining it, it is quite convenient to use

> Project address: [https://github.com/ViRb3/wgcf](https://github.com/ViRb3/wgcf)

Go to the release page and select the precompiled program corresponding to the platform that you are easy to use. Considering the smooth communication with CF, I choose a VPS located outside the country to operate. Locally, because of the particularity of the CF service, it may not work.

```
create a new folder
Extract the downloaded file into this folder
```

As of the release of the article, the releases version is v2.2.15

## 2. Modify the configuration file

The first use is to register a user and generate a configuration file:

```

./wgcf_2.2.15_windows_amd64.exe register --accept-tos (register cloudflare warp free account)

./wgcf_2.2.15_windows_amd64.exe generate (generate warp wireguard configuration file)


```

Open `wgcf-profile.conf`, set `Endpoint = engage.cloudflareclient.com:2408`

Change to `Endpoint=162.159.193.1:2408`
