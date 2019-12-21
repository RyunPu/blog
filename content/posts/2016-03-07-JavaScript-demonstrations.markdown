---
layout: post
title:  "JavaScript demonstrations"
date:   2016-03-07
categories: ['web development']
tags: ['javascript']
---

### A simple parse template function

```js
function parseTpl(tpl, obj) {
  var tpl;

  for (var property in obj) {
    if (obj.hasOwnProperty(property)) {
      tpl = tpl.replace(new RegExp('\\$' + property, 'ig'), obj[property]);
    }
  }

  return tpl;
}
```

```js
$('.js-demo-1').html(parseTpl('Hello, <strong>$name</strong>, Today is <strong>$date</strong>', {
  name: 'There',
  date: new Date().toLocaleString()
}));
```

<div class="js-demo-1"></div>

### Back to top

```js
function backToTop(selector, threshold, speed) {
  var $el = $(selector);

  $(window).on('scroll', function() {
    if ($(this).scrollTop() > (threshold ? threshold : $(this).height() / 2)) {
      $el.fadeIn();
    } else {
      $el.fadeOut();
    }
  });

  $el.on('click', function(e) {
    $('html, body').animate({
      scrollTop: 0
    }, speed ? speed : 300);

    e.preventDefault();
  });
}
```

<div class="js-demo-backtotop"><i class="icon arrow up animated slideInUp infinite"></i></div>
