---
layout: post
title:  "Show hidden files on mac"
date:   2018-07-06
categories: ['mac']
tags: ['mac']
---

### The quickest way

Since the release of macOS Sierra, when in Finder, it is now possible to use the shortcut:

```
⌘ + ⇧ + .
```

### Use terminal

Show files:

```bash
$ defaults write com.apple.finder AppleShowAllFiles YES; killall Finder
```

Hide files:

```bash
$ defaults write com.apple.finder AppleShowAllFiles NO; killall Finder
```
