---
layout: post
title:  "Use the viewport meta tag"
date:   2014-04-06
categories: ['web development']
tags: ['html']
---

* 完全自适应的布局可以设置 viewport 为：

```html
<meta name="viewport" content="width=device-width,initial-scale=1">
```

* 指定具体宽度时如考虑较小分辨的设备，可按设计宽度的一半设置 viewport 如：

```html
<meta name="viewport" content="width=320">
```

* 指定具体宽度时不考虑较小分辨的设备，直接按设计宽度设置 viewport 如：

```html
<meta name="viewport" content="width=640,user-scalable=0,target-densitydpi=device-dpi">
```

* 兼容性:

```js
if (/Android (\d+\.\d+)/.test(navigator.userAgent)) {
    var version = parseFloat(RegExp.$1);
    if (version > 2.3) {
        var phoneScale = parseInt(window.screen.width) / 480;
        document.write('<meta name="viewport" content="width=480, minimum-scale = ' + phoneScale + ', maximum-scale = ' + phoneScale + ', target-densitydpi=device-dpi">');
    } else {
        document.write('<meta name="viewport" content="width=480, target-densitydpi=device-dpi">');
    }
} else {
    document.write('<meta name="viewport" content="width=480, user-scalable=no, target-densitydpi=device-dpi">');
}
```

see more: [mozilla docs](https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag)
