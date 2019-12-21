---
layout: post
title:  "Center Anything with CSS"
date:   2015-04-06
categories: ['web development']
tags: ['css']
---

```css
.centered { position: absolute; left: 0; right: 0; top: 0; bottom: 0; margin: auto;}
```

```css
.centered { position: absolute; left: 50%; top: 50%; transform: translate(-50%,-50%);}
```

```css
.center-container { display: table;}
.center-container > div { display: table-cell; text-align: center; vertical-align: middle;}
.center-container > div .centered { margin: auto;}
```

```css
.center-container { display: flex; -webkit-justify-content: center; justify-content: center; -webkit-align-items: center; align-items: center;}
```
