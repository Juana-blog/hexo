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
title: Use Cloudflare Workers to build a third-party Onedrive public sharing site Oneindex
updated: Mon, 03 Apr 2023 13:58:58 GMT
---
# online experience

[Demo site built by blogger](https://od.myfw.us)

[Project GitHub address (development stopped)](https://github.com/spencerwooo/onedrive-cf-index)

## Preparation

1. A microsoft365 administrator account

2. A sub-number for storing OneDrive data

3. nodejs environment

## Configure the new application

Open [App Registration - Microsoft Azure](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and register a new application

Choose any application name

Supported account types select `Accounts in any organizational directory (any Azure AD directory - multi-tenant) and personal Microsoft accounts (e.g., Skype, Xbox)`

Redirect URI Select web type URI and fill in `http://localhost`

### Configure API permissions

Open the API permissions page

Click on `Microsoft Graph`

Select `offline_access, Files.Read, Files.Read.All`

and click on `Grant administrator consent on behalf of MSFT`

![image.png](https://s2.loli.net/2023/04/03/EoPtDbmMpfwVa1B.png)

Click `Yes`

## Get TOKEN

Click on `Overview` Copy the `Application (Client) ID` and keep it safe

Then click `Certificate and Password`, the name is arbitrary, and the period is 24mo:

Then copy the client's value and keep it safe

*Open cmd as administrator!*

```
npx @beetcb/ms-graph-cli
```

select global

Choose OneDrive

You will be asked to enter client\_id, which is the client ID you wrote down earlier. If you copy it, you can right-click and paste it directly.
client\_secret is the second one noted above

redirect\_url default http://localhost:3000

Then log in to your OneDrive data sub-account

## Configure CloudFlare

Log in to your CloudFlare, enter any domain name, there will be two IDs (zone\_id and account_id) in the right column (scroll down), copy and write down

Open the workers of the cloudflare dashboard

Create new workers with random names

### Pull the project and install it

```
git clone https://github.com/spencerwooo/onedrive-cf-index.git
cd onedrive-cf-index
npm install -g wrangler
npm install
wrangler login
```


Modify wrangler.toml in the project directory

name = "worker's name"

* account\_id: account id
* zone\_id: zone id


then save the file

```
wrangler kv:namespace create "BUCKET"
```

Paste the id it generates into `id = ""` in wrangler.toml

```
wrangler kv:namespace create "BUCKET" --preview
```

Paste the id it generates into `preview_id = ""` in wrangler.toml

Modify src/config/default.js

* client\_id: in the output of the step of getting token;
* base: The network disk folder you want to display. Start with a slash /. Default is /public

```
wrangler secret put REFRESH_TOKEN
```

Then paste your REFRESH_TOKEN

```
wrangler secret put CLIENT_SECRET
```

Then paste your CLIENT_SECRET

### Preview and modify

```
wrangler dev src/index.js
```

Edit page headers and footers
Footer: Modify src/folderView.js directly
Header of the page, modify src/render/htmlWrapper.js directly

### Deploy after modification

```
wrangler publish src/index.js --compatibility-date 2023-04-03
```
