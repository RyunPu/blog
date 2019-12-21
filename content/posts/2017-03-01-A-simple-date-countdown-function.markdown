---
layout: post
title:  "A simple date countdown function"
date:   2017-03-01
categories: ['web development']
tags: ['javascript']
---

```js
function countdownDate(options) {
  var defaults = {
    selector: '.countdown-date',
    startTime: new Date(),
    endTime: new Date() - (-864000000),
    onCount: undefined,
    callback: function() {}
  };

  var cfgs = $.extend(defaults, options);
  var startTime = cfgs.startTime;
  var endTime = cfgs.endTime;
  var timer = setInterval(start, 1000);

  function start() {
    var timeDiff = endTime - startTime;
    var date = addZero(parseInt(timeDiff / 1000 / 60 / 60 / 24, 10));
    var hours = addZero(parseInt(timeDiff / 1000 / 60 / 60 % 24, 10));
    var minutes = addZero(parseInt(timeDiff / 1000 / 60 % 60, 10));
    var seconds = addZero(parseInt(timeDiff / 1000 % 60, 10));

    if (typeof cfgs.onCount === 'function') {
      cfgs.onCount({
        date: date,
        hours: hours,
        minutes: minutes,
        seconds: seconds
      });
    } else {
      showTimer(date + ' 天 ' + hours + ' 时 ' + minutes + ' 分 ' + seconds + ' 秒 ');
    }

    startTime -= -1000;

    if (timeDiff <= 0) {
      if (timer) clearInterval(timer);
      cfgs.callback();
    }
  }

  function addZero(num) {
    return num < 10 ? '0' + num : '' + num;
  }

  function showTimer(data) {
    $(cfgs.selector).html(data)
  }
}
```
