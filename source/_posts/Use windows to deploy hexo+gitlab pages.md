---
abbrlink: ''
categories:
- - gitlab-pages
- - hexo
- - windows
- - english
cover: https://s2.loli.net/2022/12/31/zO82BjGeLH4pTWg.jpg
date: '2022-12-31 23:02:03'
tags:
- gitlab-pages
- hexo
- windows
- english
title: Use windows to deploy hexo+gitlab pages
updated: '2023-01-07 21:56:37'
---
# This article was translated by the Chinese version using Google Translate

Chinese version: [使用windows部署hexo+gitlab pages环境 | ursb's blog](https://blog.ursb.eu.org/%E4%BD%BF%E7%94%A8windows%E9%83%A8%E7%BD%B2hexo+gitlab-pages%E7%8E%AF%E5%A2%83/)

# Preparation

## install Git

Go to [Git official website](https://git-scm.com/downloads) to download windows and install it.

## Install Node.js

Go to [NodeJs official website](https://nodejs.org/en/download) to download the windows version and install it.

## Register Gitlab account

Go to [Gitlab official website](https://gitlab.com/) to register.

# deploy blog

## Install Hexo

Create a new blog folder, go to the folder, right click, and select `git bash here.`

![image.png](https://s2.loli.net/2022/12/31/r3UNbQD6KMx8Ldy.png)

Enter the command to install Hexo:

```
npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive hexo-renderer-pug hexo-renderer-stylus
```

Enter the command to install Hexo: After the completion, enter the command to initialize Hexo:

```
hexo init hexo
```

Go to the hexo directory and install dependencies:

```
cd hexo
npm install
```

Enter hexo clean to test whether hexo is in normal use:

```
hexo clean
```

Not surprisingly, you will get the following:

```
INFO  Validating config
```

### Install Theme

The following uses the butterfly theme as an example

Install theme:

```
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

Change the theme used

Open `_config.yml` in the hexo root folder

Change `theme: landscape` to `theme: butterfly`

save

#### Test changing theme

```
hexo g ; hexo d
```

Open [http://localhost:4000](http://localhost:4000)

![image.png](https://s2.loli.net/2022/12/31/dlmJRy5xKHaMZVL.png)

view your blog

Then return to the git program

Press `ctrl+c`

## Gitlab create warehouse

Log in to Gitlab and click New project.

![image.png](https://s2.loli.net/2022/12/31/rqmD9aUhSlxZknC.png)

Select `Create blank project`

Project name fill in `%yourname%.gitlab.io`

Visibility Level select `Public`

Then click `Create project`

## Upload project to gitlab

Go to settings/repository

Open Protected branches

Change it to the following option

![image.png](https://s2.loli.net/2022/12/31/zEuWJjdlAeMPRkx.png)

Return to the git program in the previous step

```
hexo clean
```

Delete the themes/butterfly/.git folder

```
git init
git config user.name "your username"
git config user.email "your email"
git remote add origin the project you just created link
git config http.postBuffer 524288000 (reminder: this line is to set the cache locally, some project files are large and cannot be uploaded using http, you can set this command)
git branch -M main
git push -uf origin main

```

## Configure gitlab runner

(If you have a bank card for verification, please ignore this step)

Enter settings ci/cd

open runner

Open powershell as administrator

```
New-Item -Path 'C:\GitLab-Runner' -ItemType Directory
cd 'C:\GitLab-Runner'
```

```
Invoke-WebRequest -Uri "https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-windows-amd64.exe" -OutFile "gitlab-runner.exe"
```

and wait for it to complete

```
.\gitlab-runner.exe install
.\gitlab-runner.exe start
.\gitlab-runner.exe register
```

URL input `https://gitlab.com/`

token Fill in the registration token given in the link opened in the previous step

For the remaining three steps, press Enter three times

Enter an executor Enter `shell`

Edit C:\GitLab-Runner\config.toml

Change `shell = "pwsh"` to `shell = "powershell"`

then save and exit

Return to the powershell window opened in the previous step

Type `./gitlab-runner.exe restart`

Return to the page opened in the previous step

Set `Enable shared runners for this project`

change to gray

![image.png](https://s2.loli.net/2022/12/31/Js7nQcMeafK29FA.png)

## Configure gitlab pages

Click the plus sign to create a new file named `.gitlab-ci.yml`

Fill in the content:

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

wait 2min

Visit %yourname%.gitlab.io to view your deployed blog
