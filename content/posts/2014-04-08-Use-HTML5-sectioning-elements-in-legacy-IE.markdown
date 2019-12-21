---
layout: post
title:  "Use HTML5 sectioning elements in legacy IE"
date:   2014-04-08
categories: ['web development']
tags: ['html', 'javascript']
---

```js
(function() {
  if (!-[1,]) {
    var tags = ['article', 'aside', 'details', 'figcaption', 'figure', 'footer', 'header', 'hgroup', 'menu', 'nav', 'section', 'summary', 'time', 'mark', 'audio', 'video'];

    for (var i = 0, len = tags.length; i < len; i++) {
      document.createElement(tags[i]);
    }
  }
})();
```

see also: [html5shiv](https://github.com/aFarkas/html5shiv)
