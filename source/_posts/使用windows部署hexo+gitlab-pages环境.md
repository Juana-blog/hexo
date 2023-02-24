---
abbrlink: hexo-gp-win
categories:
- - gitlab-pages
- - windows
- - hexo
cover: https://s2.loli.net/2022/12/31/zO82BjGeLH4pTWg.jpg
date: '2022-12-31 20:22:59'
tags:
- gitlab-pages
- windows
- hexo
title: 使用windows部署hexo+gitlab pages环境
updated: '2022-12-31 21:49:21'
---
# 前期准备

## 安装Git

去 [Git官网](https://git-scm.com/downloads)下载windows，进行安装即可。

## 安装Node.js

去 [NodeJs官网](https://nodejs.org/en/download) 下载windows版本，进行安装即可。

## 注册Gitlab账号

去 [Gitlab官网](https://gitlab.com/) 进行注册即可。

# 搭建博客

## 安装Hexo

在本地新建一个blog文件夹，进入文件夹，右键，选择git bash here。

![image.png](https://s2.loli.net/2022/12/31/r3UNbQD6KMx8Ldy.png)

输入指令安装Hexo：

```
npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive hexo-renderer-pug hexo-renderer-stylus
```

等到完成之后，输入指令初始化Hexo：

```
hexo init hexo
```

进入到hexo目录，安装依赖:

```
cd hexo
npm install
```

输入hexo clean 测试hexo 是否正常使用：

```
hexo clean
```

不出意外，会得到下面的内容：

```
INFO  Validating config
```

### 安装主题

以下以 butterfly 主题做示例

安装主题：

```
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

更改使用的主题

打开 hexo根文件夹中的 `_config.yml`

将其中的 `theme: landscape` 改为 `theme: butterfly`

保存

#### 测试更换主题

```
hexo g ; hexo d
```

打开 [http://localhost:4000](http://localhost:4000)

![image.png](https://s2.loli.net/2022/12/31/dlmJRy5xKHaMZVL.png)

查看你的 blog

然后返回git程序

按 `ctrl+c`

## Gitlab创建仓库

登录Gitlab，点击New project。

![image.png](https://s2.loli.net/2022/12/31/rqmD9aUhSlxZknC.png)

选择 `Create blank project`

Project name 填写 `%你的名字%.gitlab.io`

Visibility Level 选择 `Public`

然后点击 `Create project`

## 上传项目至gitlab

进入 settings/repository

打开 Protected branches

将它改为下图 选项

![image.png](https://s2.loli.net/2022/12/31/zEuWJjdlAeMPRkx.png)

返回上步中的 git 程序

```
hexo clean
```

删除 themes/butterfly/.git 文件夹

```
git init
git config user.name "你的用户名"
git config user.email "你的邮箱"
git remote add origin 你刚才建立的项目link
git config http.postBuffer 524288000 (提醒: 此行是在本地设置缓存, 有些项目文件较大, 使用http无法上传,可设置此命令) 
git branch -M main
git push -uf origin main

```

## 配置 gitlab runner

（如果你有银行卡供验证，请忽略这一步)

进入settings ci/cd

打开 runner

以管理员身份打开powershell

```
New-Item -Path 'C:\GitLab-Runner' -ItemType Directory
cd 'C:\GitLab-Runner'
```

```
Invoke-WebRequest -Uri "https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-windows-amd64.exe" -OutFile "gitlab-runner.exe"
```

等它执行完成后

```
.\gitlab-runner.exe install
.\gitlab-runner.exe start
.\gitlab-runner.exe register
```

url输入 `https://gitlab.com/`

token填写上一步打开的链接给出的registration token

剩下的三步敲三下回车

Enter an executor 输入 `shell`

编辑 C:\GitLab-Runner\config.toml

将`shell = "pwsh"`改为`shell = "powershell"`

然后保存并退出

返回上一步打开的 powershell 窗口

输入 `./gitlab-runner.exe restart`

返回上一步打开的网页

将 `Enable shared runners for this project`

改为灰色

![image.png](https://s2.loli.net/2022/12/31/Js7nQcMeafK29FA.png)

## 配置gitlab pages

点击加号 新建一个名为 `.gitlab-ci.yml`的文件

内容填写：

```
image: node:lts
cache:
  paths:
    - node_modules/

before_script:
  - npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive hexo-renderer-pug hexo-renderer-stylus
  - npm install

pages:
  script:
    - npm run build
  artifacts:
    paths:
      - public
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

```

等待2min

访问 %你的名字%.gitlab.io 查看你部署的 blog吧
