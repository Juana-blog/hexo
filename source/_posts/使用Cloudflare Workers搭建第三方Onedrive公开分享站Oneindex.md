---
abbrlink: ''
categories:
- - cloudflare
- - workers
- - wrangler
cover: https://s2.loli.net/2023/04/03/sT53faGbmOPFdIi.png
date: '2023-04-03 21:58:54'
tags:
- cloudflare
- workers
- wrangler
title: 使用Cloudflare Workers搭建第三方Onedrive公开分享站Oneindex
updated: Mon, 03 Apr 2023 13:58:58 GMT
---
# 在线体验

[博主搭建的demo站点](https://od.myfw.us)

[项目GitHub地址(已停止开发)](https://github.com/spencerwooo/onedrive-cf-index)

## 准备工作

1.一个microsoft365管理员账号

2.一个用于存OneDrive数据子号

3.nodejs环境

## 配置新应用

打开 [应用注册 - Microsoft Azure](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) 并新注册一个应用

应用名称随便取一个

受支持的账户类型选择 `任何组织目录(任何 Azure AD 目录 - 多租户)中的帐户和个人 Microsoft 帐户(例如,Skype、Xbox)`

重定向URI 选择web类型 URI 填写 `http://localhost`

### 配置API权限

打开API权限页面

点击 `Microsoft Graph`

选择 `offline_access, Files.Read, Files.Read.All`

并点击 `代表 MSFT 授予管理员同意`

![image.png](https://s2.loli.net/2023/04/03/EoPtDbmMpfwVa1B.png)

点击 `是`

## 获取TOKEN

点击 `概述` 复制 `应用程序(客户端) ID` 并保管好

接着点击 `证书和密码`,名字随意,期限为24mo:

然后复制客户端的值 并保管好

*以管理员身份打开cmd!*

```
npx @beetcb/ms-graph-cli
```

选择global

选择OneDrive

会要求你输入client\_id,就是前面记下的客户端ID,复制了可以右键直接粘贴进去
client\_secret就是上面记下的第二个

redirect\_url默认http://localhost:3000

然后登录你的存OneDrive数据子号

## 配置CloudFlare

登录你的CloudFlare,进入任意一域名下,右侧栏(往下翻)里头会有俩ID(zone\_id和account_id),复制并记下

打开cloudflare dashboard的workers

新建workers 取名随意

### 拉取项目,并安装

```
git clone https://github.com/spencerwooo/onedrive-cf-index.git
cd onedrive-cf-index
npm install -g wrangler
npm install
wrangler login
```


修改项目目录下的 wrangler.toml

name = "worker 的名字"

* account\_id:账户 id
* zone\_id:区域 id


然后保存文件

```
wrangler kv:namespace create "BUCKET"
```

将它生成的 id粘贴到 wrangler.toml 中的 `id = ""`里

```
wrangler kv:namespace create "BUCKET" --preview
```

将它生成的 id粘贴到 wrangler.toml 中的 `preview_id = ""`里

修改 src/config/default.js

* client\_id:获取token那一步的输出里有;
* base:你想要展示的网盘文件夹。要以斜杠 / 打头。默认为/pubic

```
wrangler secret put REFRESH_TOKEN
```

然后粘贴你的 REFRESH_TOKEN

```
wrangler secret put CLIENT_SECRET
```

然后粘贴你的 CLIENT_SECRET

### 预览并修改

```
wrangler dev src/index.js 
```

修改网页页眉和页脚
页脚:直接修改 src/folderView.js
页面的 header,直接修改 src/render/htmlWrapper.js

### 修改后部署

```
wrangler publish src/index.js --compatibility-date 2023-04-03
```
