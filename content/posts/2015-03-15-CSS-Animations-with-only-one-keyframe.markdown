---
layout: post
title:  "CSS Animations with only one keyframe"
date:   2015-03-15
categories: ['web development']
tags: ['css']
---

a simple animation:

```css
@keyframes fade {
  0% { opacity: 1;}
  50% { opacity: 0;}
  100% { opacity: 1;}
}
```

more simple:

```css
@keyframes fade {
  50% { opacity: 0;}
}
```
see more: [transition-timing-function](https://easings.net/)
