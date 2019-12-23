---
layout: post
title:  "Open atom from the terminal"
date:   2016-03-14
categories: ['editor']
tags: ['atom']
---

With the Atom editor open, in the menu bar, click Atom >> Install Shell Commands:

![image](https://user-images.githubusercontent.com/6168498/71335565-3f84db80-257e-11ea-80c5-dd5aeb97595d.png)

When Atom installs it automatically creates a symlink in your /usr/local/bin. However in case it hasn't, you can create it yourself on your Mac:

```bash
$ ln -s /Applications/Atom.app/Contents/Resources/app/atom.sh /usr/local/bin/atom
```
