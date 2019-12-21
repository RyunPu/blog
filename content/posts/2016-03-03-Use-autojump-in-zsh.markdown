---
layout: post
title:  "Use autojump in zsh"
date:   2016-03-03
categories: ['web development']
tags: ['tool']
---

### Install

##### use homebrew:

```bash
$ brew install autojump
```

##### load the plugin in ```~/.zshrc``` file:

plugins=(git autojump)

##### add the following line to your ```~/.zshrc``` file:

[[ -s `brew --prefix`/etc/autojump.sh ]] && . `brew --prefix`/etc/autojump.sh

##### source the file to update your current session:

```bash
$ source ~/.zshrc
```

### Usage

##### Jump To A Directory That Contains foo:

```bash
$ j foo
```

##### Jump To A Child Directory:

```bash
$ jc bar
```

##### Open File Manager To Directories (instead of jumping):

```bash
$ jo music
```

##### Opening a file manager to a child directory is also supported:

```bash
$ jco images
```

see more: [autojump](https://github.com/wting/autojump)
