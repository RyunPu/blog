---
layout: post
title:  "Insert the Mac command symbol"
date:   2018-07-04
categories: ['mac']
tags: ['mac']
---

### Copy and Paste

⌘

### Use Emoji and Symbols `⌃ + ⌘ + Space`

You'll find it under Edit -> Emoji and Symbols in any program that takes text input. The Command key symbol can be found by searching for it's name "place of interest".

![image](https://user-images.githubusercontent.com/6168498/71318008-56b3c280-24c5-11ea-9701-82a88d412d37.png)

### Use Unicode Hex Input `⌥ + 2318`

![image](https://user-images.githubusercontent.com/6168498/71318093-e5750f00-24c6-11ea-8080-5161c1efac45.png)

### Use text replacements

![image](https://user-images.githubusercontent.com/6168498/71318130-b01cf100-24c7-11ea-8213-5e7752c992c6.png)


### Use Atom snippets

```cson
'.text.plain, .source.gfm':
  'command symbol':
    'prefix': 'cmds'
    'body': '⌘'
  'ctrl symbol':
    'prefix': 'cs'
    'body': '⌃'
  'alt symbol':
    'prefix': 'as'
    'body': '⌥'
  'shift symbol':
    'prefix': 'ss'
    'body': '⇧'
```
