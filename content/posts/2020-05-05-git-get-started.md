---
title: "Git 入门及连接多个远程仓库"
comment:
  enable: true
date: 2020-05-05T21:18:40+08:00
categories: ["技术","入门"]
tags: ["git"]
summary: "最近遇到了如何在电脑上的不同位置连接不同的远程仓库的问题，很多中文的 git 教程并没有涉及到这个问题，故将查阅到的办法整理为此文。"
featuredImagePreview: "https://cdn.jsdelivr.net/gh/Lucas-0/Img/img/20200505212658.jpg"

hiddenFromHomePage: true
toc:
  enable: true
  auto: true
lastmod: 
---

​    

最近遇到了如何在电脑上的不同位置连接不同的远程仓库的问题，很多中文的 git 教程并没有涉及到这个问题，故将查阅到的办法整理为此文。

&nbsp;&nbsp;

## Git初始化

### 1. 创建本地仓库及配置Git账号

```bash
git init #在当前位置初始化git仓库
git config user.name "A" #设置用户名为A
git config user.email "A@example.com" #设置邮箱为A@example.com
```
可以使用 `git config --global` 命令设置全局的账号，则除非另外声明均使用此账号。

### 2. 生成SSH密钥对

```bash
ssh-keygen -t rsa -C "A@example.com"
```

然后选择密钥对存储位置。

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/yourname/.ssh/id_rsa): [Press enter]
```

设置密码（optional）。
```bash
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:
```

---

&nbsp;&nbsp;

## 与GitHub连接

这一部分并非本文的重点，请自行查阅。可参考下面的链接：

[添加远程库 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/898732864121440)

​    

---

## 连接多个仓库

GitHub 不允许一个密钥对应用于多个仓库。所以如果我们有两个本地仓库 A 和 B 需要同步，必须生成两个密钥对，并且分别把公钥部署到 GitHub 。

### 1. 用名称区别不同仓库

在 `~/.ssh` 目录下新建 `config` 文件。

```shell
host A  #自定义别名，用于之后配置地址
    Hostname github.com #要连接的服务器
    User Lucas #用户名
    IdentityFile ~/.ssh/id_rsa  #密钥文件的地址，注意是私钥

host B #自定义别名，用于之后配置地址
    Hostname github.com
    User lucas
    IdentityFile ~/.ssh/B_id_rsa
```

通过上面的设置，对不同的本地仓库我们可以使用不同的 host 的别名来指定使用哪一对密钥，类似于 CNAME 。

### 2. 修改本地仓库的设置

修改本地仓库 A 的 `.git` 目录下， `config` 文件的内容：

```yaml
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[user]
    email = A@example.com
    name = Lucas
[remote "origin"]
    url = git@A:Yourname/example.git #使用host的别名A
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

### 3. 与远程仓库关联

```bash
git remote add origin git@server-name:path/repo-name.git
```

初始化的仓库在推送之前先拉取远程仓库的文件否则会可能会出错。

```bash
git pull origin master
```

添加当前目录下的文件。

```bash
git add <filename>
git add * #使用缺省符则将当前目录下所有文件添加到git
git commit -m "first commit" #将修改在本地保存并且注释“first commit”
```

推送到远程仓库。

```bash
git push -u origin master
```

---

&nbsp;&nbsp;

本文简单总结了 Git 的基本用法，更多的操作还需要在实践中解锁。

&nbsp;&nbsp;

&nbsp;&nbsp;