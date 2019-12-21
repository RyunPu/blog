---
layout: post
title:  "Prevent touch event click underneath layer"
date:   2015-03-13
categories: ['web development']
tags: ['mobile', 'javascript']
---

* 延迟事件处理(>300ms)：

```js
$('#mask').on('tap', function() {
  setTimeout(function() { $('#mask').hide(); }, 400);
});
```

* 使用 touchstart 或 touchend：

```js
$('#mask').on('touchend', function(e) {
  setTimeout(function() { $('#mask').hide(); }, 300);
  e.preventDefault();
});
```

* 使用 [fastclick](https://github.com/ftlabs/fastclick)

```js
$(function() {
  FastClick.attach(document.body);
});
```
