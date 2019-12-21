---
layout: post
title:  "Some commonly used UA detection"
date:   2015-04-09
categories: ['web development']
tags: ['javascript']
---

```js
var ua = navigator.userAgent.toLowerCase();
```

```js
var arr = /(chrome|firefox)[ \/]([\w.]+)/.exec(ua) || // Chrome & Firefox
  /(iphone|ipad|ipod)(?:.*version)?[ \/]([\w.]+)/.exec(ua) || // Mobile IOS
  /(android)(?:.*version)?[ \/]([\w.]+)/.exec(ua) || // Mobile Webkit
  /(webkit|opera)(?:.*version)?[ \/]([\w.]+)/.exec(ua) || // Safari & Opera
  /(msie) ([\w.]+)/.exec(ua) ||
  /(trident).+rv:(\w.)+/.exec(ua) || [];
var browser = arr[1];
var version = parseFloat(arr[2]);

switch (browser) {
  case 'msie':
  case 'trident':
    browser = 'ie';
    version = document.documentMode || version;
    break;
}
```

```js
/(msie\s|trident.*rv:)([\w.]+)/.test(ua) // IE
/micromessenger/.test(ua) // wechat
/iphone|ipad|ipod/.test(ua) // ios
/android/.test(ua) // android
/mobile|android|kindle|silk|midp|phone|(windows .+arm|touch)/.test(ua) // mobile
```

###### get IE version

```js
function getIEVersion() {
  var ua = navigator.userAgent.toLowerCase();
  var arr = /(msie) ([\w.]+)/.exec(ua) || /(trident).+rv:(\w.)+/.exec(ua) || [];
  return document.documentMode || parseFloat(arr[2]);
}
```
