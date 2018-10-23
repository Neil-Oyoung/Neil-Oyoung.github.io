---
title: Hexo搭建和部署到Github Pages
date: 2018-10-20
tags: [Hexo,Github Pages,NexT,Gitment]
---
# Hexo搭建和部署到Github Pages

## STEP 1 创建`github pages`代码库

[Create a new repository](https://github.com/new)

代码库名应为`用户名.github.io`，如Neil-Oyoung.github.io。

## STEP 2 准备本地代码库 

### 2.1 生成Hexo项目

```Bash
hexo init Neil-Oyoung.github.io
cd Neil-Oyoung.github.io
```

### 2.2 体验本地Hexo 

```Bash
hexo server
```

启动服务后就可通过浏览器到`http://localhost:4000`体验Hexo了。

### 2.3 添加Git版本管理

```Bash
git init
git add .
git commit -m "base"
git push -u origin master
git branch hexo
```

<!-- more -->

## STEP 3 部署到`Github Pages`

### 3.1 指定部署代码库与分支

```Bash
vim _config.yml
```

编辑Hexo配置文件，修改deploy项为：

```Yml
deploy:
  type: git 
  repo: https://github.com/Neil-Oyoung/Neil-Oyoung.github.io.git
  branch: master
```

#### （Optional）3.1.1 修订网站标题与作者 

编辑Hexo配置文件，修改title、subtitle和author项为：

```yml
# Site
title: Neil's MEMO
subtitle: 点滴积累，功不唐捐。
description: Neil's MEMO.
keywords:
author: Neil Oyoung
language:
timezone:
```

### 3.2 生成静态文件并部署 

```Bash
hexo g -d
```

### 3.3 体验远程Hexo 

部署成功后即可通过浏览器到`https://neil-oyoung.github.io/`体验部署后的Hexo了。

### 3.4 保存并提交修改

```Bash
git add .
git commit -m "config deploy"
git push -u origin hexo
```

## (Optional) STEP 4 添加NexT主题

### 4.1 Fork NexT代码库

前往`https://github.com/theme-next/hexo-theme-next`，fork到自己名下（此例为`https://github.com/Neil-Oyoung/hexo-theme-next.git`）。

### 4.2 添加NexT子模块

```Bash
git submodule add https://github.com/Neil-Oyoung/hexo-theme-next.git themes/next
```

### 4.3 启用NexT主题

```Bash
vim _config.yml
```

编辑Hexo配置文件，修改theme项为：

```Txt
theme: next
```

#### （Optional）4.3.1 切换为Pisces风格 

```Bash
vim themes/next/_config.yml
```
编辑主题配置文件，修改scheme项为：


```yml
# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```

### 4.4 生成静态文件并部署

```Bash
hexo g -d
```

### 4.5 体验NexT主题

部署成功后即可通过浏览器到`https://neil-oyoung.github.io/`体验NexT主题了。

### 4.6 保存并提交修改

```Bash
cd themes/next
git add .
git commit -m "config scheme"
git push -u origin master

cd ../..
git add .
git commit -m "enable NexT theme"
git push -u origin hexo
```

## (Optional) STEP 5 添加Gitment评论系统

### 5.1 注册OAuth Apps

到[这里](https://github.com/settings/developers)注册获取`Client ID`和`Client Secret`。参考：

```Txt
Application name：Gitment
Homepage URL：https://neil-oyoung.github.io/
Application description：Blog comment system
Authorization callback URL：https://neil-oyoung.github.io/
```

### 5.2 创建`gitment-comments`代码库

为了存储评论，需要创建新的代码库（此例为`https://github.com/Neil-Oyoung/gitment-comments.git`）。

### 5.3 启用Gitment

```Bash
vim themes/next/_config.yml
```

编辑主题配置文件（此例为NexT主题），根据上面两步的准备修改gitment项为：

```Txt
gitment:
  enable: true
  mint: true # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true # Show comments count in post meta area
  lazy: false # Comments lazy loading with a button
  cleanly: false # Hide 'Powered by ...' on footer, and more
  language: # Force language, or auto switch by theme
  github_user: Neil-Oyoung # MUST HAVE, Your Github Username
  github_repo: gitment-comments # MUST HAVE, The name of the repo you use to store Gitment comments
  client_id: xxxxxxxxx # MUST HAVE, Github client id for the Gitment
  client_secret: xxxxxxxxx # EITHER this or proxy_gateway, Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
```

### 5.4 生成静态文件并部署

```Bash
hexo g -d
```

### 5.5 体验Gitment

部署成功后即可通过浏览器到`https://neil-oyoung.github.io/`体验部署后的Gitment了。

### 5.6 保存并提交修改

```Bash
cd themes/next
git add .
git commit -m "config gitment"
git push -u origin master

cd ../..
git add .
git commit -m "enable gitment"
git push -u origin hexo
```

## Trouble Shooting

### Github Pages doesn't Update

1. Check `https://status.github.com` first, make sure Github is operating normally.
2. Check Github Pages's settings(e.g. https://github.com/Neil-Oyoung/Neil-Oyoung.github.io/settings), it should tell you something wrong.
3. Time zone might be different from article's date. Edit `_config.yml` to config `timezone` or make `future` as `true`.

## Reference

1. [Github Pages](https://pages.github.com/)
2. [Hexo Docs](https://hexo.io/docs/)
3. [Next](https://github.com/theme-next/hexo-theme-next)
4. [Hexo-Next 添加 Gitment 评论系统](https://ryanluoxu.github.io/2017/11/27/Hexo-Next-%E6%B7%BB%E5%8A%A0-Gitment-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/)
