---
layout: post
title:  "Install Git"
date:   2014-03-20
categories: ['web development']
tags: ['git']
---

当你想升级系统自带的 Git 的时候，可以使用下面的命令查看其所在的目录：

```bash
$ which git
```

当你看到类似 ’/user/bin‘ 的地址时，你可能需要更改用户目录下的隐藏文件 .bash_profile，添加：

    export PATH=/usr/local/bin:$PATH

然后，你就可以安装和更新 Git了，我使用的是 Homebrew：

```bash
$ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

```bash
$ brew install git
```

```bash
$ brew upgrade git
```

如果需要改变 Git 的指向:

```bash
$ brew link git --overwrite
```
