---
layout: post
title:  "Show the current path in the finder"
date:   2018-07-05
categories: ['mac']
tags: ['mac']
---

### Enable the finder path bar `⌥ + ⌘ + P`

![image](https://user-images.githubusercontent.com/6168498/71318386-240cc880-24cb-11ea-81db-ed56ccfe2522.png)

### Show the path in the finder title bar

```bash
$ defaults write com.apple.finder _FXShowPosixPathInTitle -bool true; killall Finder
```

![image](https://user-images.githubusercontent.com/6168498/71318404-66cea080-24cb-11ea-870a-58d73b923638.png)


Use this command to turn it off

```bash
$ defaults write com.apple.finder _FXShowPosixPathInTitle -bool false; killall Finder
```
