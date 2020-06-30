---
title: "Hugo 博客使用 LoveIt 主题"
subtitle: ""
date: 2020-06-30T18:00:00+08:00
lastmod: 
draft: false
author: ""
authorLink: ""
description: "记录使用 Hugo 搭建博客和配置 LoveIt 主题的过程, 利用 GitHub Action 实现自动部署."
expiryDate: 
publishDate: 

tags: ["Hugo","LoveIt","GitHub Pages","GitHub Action"]
categories: ["技术"]

hiddenFromHomePage: false
hiddenFromSearch: false

featuredImage: ""
featuredImagePreview: "https://cdn.jsdelivr.net/gh/Lucas-0/Img/20200406212944.jpg"

toc:
  enable: true
math:
  enable: false
lightgallery: true
license: ""
---

<!--more-->

</br>

记录使用 Hugo 搭建博客和配置 LoveIt 主题的过程, 利用 GitHub Action 实现自动部署.

{{<admonition warning>}}

使用 loveit 主题, 除了要 `new site` 以外, 还要初始化为 git 仓库, 不然本地构建不了站点.

{{</admonition>}}

---

</br>

## 初始化和管理主题 ##

```bash
hugo new site BLOG
cd  BLOG
git init
git submodule add https://github.com/dillonzq/LoveIt themes/LoveIt
```

然后把 examplesite 的文件放到博客目录下, 注意有一篇示例文章的 shortcode 引用了 :(fab fa-twitter): twitter 和 :(fab fa-instagram): Instagram 的格式, 在强国的网络环境下网站生成会失败, 要删除 post.

如果下载很慢可以考虑设置代理:surfer:或者转换链接:link:.

```bash
git config --global http.proxy 'socks5://127.0.0.1:1080'

git config --global https.proxy 'socks5://127.0.0.1:1080'

git config --global --unset http.proxy

git config --global --unset https.proxy
```

配置一下博客的 config 文件, 注意 `themesDir = "themes"` 不要添加斜杠 `/`, 否则在下一步利用 GitHub Action自动部署会报找不到主题的错误.

</br>

## GitHub Pages ##

然后添加 GitHub Pages 仓库: blog 分支管理源码, master 中为 public 文件夹.
 ```bash
git remote add origin https://github.com/Lucas-0/Lucas-0.github.io.git
# 新建 branch 分支, 也可以使用 checkout
git branch -b blog

git add .
git commit -m "init"
git push origin blog
 ```

到这一步, 已经完成了推送的步骤.

</br>

## GitHub Action ##

在博客根目录新建 `.github/workflows/main.yml` 文件, 这是 GitHub Action 读取执行的文件夹, 其中 `main.yml` 文件名字可以任取.

内容:

```yaml
name: GitHub Page Deploy

on:
  push:
    branches:
      - blog
jobs:
  build-deploy:
    runs-on: ubuntu-18.04
    steps:
      - name: Checkout master
        uses: actions/checkout@v1      
        with:
          submodules: true
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: latest
          extended: true

      - name: Build Hugo
        run: |
          hugo

      - name: Deploy Hugo to gh-pages
        uses: peaceiris/actions-gh-pages@v2
        env:
          ACTIONS_DEPLOY_KEY: ${{ secrets.ACTIONS_DEPLOY_KEY }}
          PUBLISH_BRANCH: master
          PUBLISH_DIR: ./public
```

在仓库新建 `Secrets`, 名称自定, 可以和上面给定的模板一样叫做 ACTIONS_DEPLOY_KEY, 将 SSH 私钥复制进去.这样 workflow 就有权限对 master 分支进行写操作.

例如某一次 push 的过程:

```bash
git add .
git commit -m "message"
git push origin blog
```

然后 workflow 会自动生成 public 文件夹 push 到 master 分支.

全文完.

</br>