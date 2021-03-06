---
layout: post
title:  "JavaScript snippets"
date:   2014-04-02
categories: ['web development']
tags: ['javascript']
---

### A simple event emitter

```js
export default {
  events: {},

  on(event, callback) {
    if (!this.events[event]) {
      this.events[event] = []
    }

    if (typeof callback === 'function') {
      this.events[event].push(callback)
    }
  },

  once(event, callback) {
    if (typeof callback === 'function') {
      const once = (...args) => {
        callback(...args)
        this.off(event, once)
      }
      this.on(event, once)
    }
  },

  emit(event, ...args) {
    if (this.events[event]) {
      this.events[event].forEach(callback => {
        callback(...args)
      })
    }
  },

  off(event, callback) {
    const callbacks = this.events[event]

    if (callbacks) {
      if (typeof callback === 'function') {
        this.events[event] = callbacks.filter(cb => cb.toString() !== callback.toString())
      } else {
        this.events[event] = null
      }
    }
  },
}
```

### Use UMD to create a jQuery plugin

```js
(function(factory) {
  if (typeof define === 'function' && define.amd) {
    // AMD. Register as an anonymous module.
    define(['jquery'], factory);
  } else if (typeof module === 'object' && module.exports) {
    // Node/CommonJS
    module.exports = function(root, jQuery) {
      if (jQuery === undefined) {
        // require('jQuery') returns a factory that requires window to
        // build a jQuery instance, we normalize how we use modules
        // that require this pattern but the window provided is a noop
        // if it's defined (how jquery works)
        if (typeof window !== 'undefined') {
          jQuery = require('jquery');
        } else {
          jQuery = require('jquery')(root);
        }
      }
      factory(jQuery);
      return jQuery;
    };
  } else {
    // Browser globals
    factory(jQuery);
  }
}(function($) {
  $.fn.jqueryPlugin = function() {
    return true;
  };
}));
```

### Lazy load images

```js
function lazyLoad(offset = 0, selector = 'img[data-src]') {
  const load = () => {
    const imgs = [...document.querySelectorAll(selector + ':not(.loaded)')]

    imgs.forEach(img => {
      if (window.innerHeight - img.getBoundingClientRect().top + offset > 0) {
        img.src = img.dataset.src
        img.onload = () => img.classList.add('loaded')
      }
    })
  }

  load()
  window.addEventListener('scroll', load, false)
  window.addEventListener('resize', load, false)
}
```

### Lazy load images with IntersectionObserver

```js
function lazyLoad(offset = 0, selector = 'img[data-src]', root = null) {
  const interactSettings = {
    root: document.querySelector(root),
    rootMargin: `0px 0px ${offset}px 0px`
  }

  const onIntersection = (entries, observer) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const img = entry.target
        observer.unobserve(img)
        img.src = img.dataset.src
        img.onload = () => img.classList.add('loaded')
      }
    })
  }

  const observer = new IntersectionObserver(onIntersection, interactSettings)
  const imgs = [...document.querySelectorAll(selector + ':not(.loaded)')]
  imgs.forEach(img => observer.observe(img))
}
```

### Throttle

```js
const throttle = (fn, wait = 17) => {
  let lastTime = 0
  return function(...args) {
    let now = Date.now()

    if (now - lastTime >= wait) {
      lastTime = now
      fn.apply(this, args)
    }
  }
}
```

### Debounce

```js
const debounce = (fn, wait = 17) => {
  let timer = null
  return function(...args) {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      fn.apply(this, args)
    }, wait)
  }
}
```

### Throttle and Debounce

```js
const throttleDebounce = (fn, wait = 17) => {
  let lastTime = 0
  let timer = null

  return function(...args) {
    let now = Date.now()

    if (now - lastTime < wait) {
      if (timer) clearTimeout(timer)
      timer = setTimeout(() => {
        lastTime = now
        fn.apply(this, args)
      }, wait)
    } else {
      lastTime = now
      fn.apply(this, args)
    }
  }
}
```

### Lodash cloneDeep

```js
function cloneDeep(obj) {
  function isObject(o) {
    return (typeof o === 'object' || typeof o === 'function') && o !== null
  }

  if (!isObject(obj)) {
    return obj
  }

  let isArray = Array.isArray(obj)
  let newObj = isArray ? [...obj] : { ...obj }

  Reflect.ownKeys(newObj).forEach(key => {
    newObj[key] = isObject(obj[key]) ? cloneDeep(obj[key]) : obj[key]
  })

  return newObj
}
```

### Format a Date

```js
Date.prototype.format = function(format) {
  var o = {
    'M+': this.getMonth() + 1, // month
    'd+': this.getDate(), // day
    'h+': this.getHours(), // hour
    'm+': this.getMinutes(), // minute
    's+': this.getSeconds(), // second
    'q+': Math.floor((this.getMonth() + 3) / 3), // quarter
    'S': this.getMilliseconds() // millisecond
  }

  if (/(y+)/.test(format)) {
    format = format.replace(RegExp.$1, (this.getFullYear() + '').substr(4 - RegExp.$1.length));
  }

  for (var k in o) {
    if (new RegExp('(' + k + ')').test(format)) {
      format = format.replace(RegExp.$1, RegExp.$1.length == 1 ?
        o[k] :
        ('00' + o[k]).substr(('' + o[k]).length));
    }
  }

  return format;
};
```

```js
new Date().format('yyyy-MM-dd hh:mm:ss'); // 2014-04-02 08:00:00
```

### Set fetch body from an object

```js
function setFetchBody(obj) {
  let str = ''
  if (!obj) return str

  let isFirstKey = true

  for (const key of Object.keys(obj)) {
    if (isFirstKey) {
      isFirstKey = false
      str += `${key}=${obj[key]}`
    } else {
      str += `&${key}=${obj[key]}`
    }
  }

  return str
}
```

### Get items filter by including any one of other items

```js
function getIncludedItems(arr1, arr2, prop) {
  return arr1.filter(function(el) {
    var included = false;

    for (var i = 0; i < arr2.length; i++) {
      var element = prop ? el[prop] : el;

      if (element.includes(arr2[i])) {
        included = true;
        break;
      }
    }

    return included;
  });
}
```

```js
getIncludedItems(['as', 'bs', 'cs'], ['a', 'b']);
// ['as', 'bs']
getIncludedItems([{ domain: 'as.com' }, { domain: 'bs.com' }, { domain: 'cs.com' }], ['as', 'bs'], 'domain');
// [{ domain: 'as.com' }, { domain: 'bs.com' }]
```

### Remove a certain item and return the rest

```js
function getRestItems(arr, value, prop) {
  var rest = arr.slice();

  for (var i = 0; i < rest.length; i++) {
    if (prop && rest[i][prop] === value || !prop && rest[i] === value) {
      rest.splice(i, 1);
      break;
    }
  }

  return rest;
}
```

```js
getRestItems([1, 2, { x: 3 }], 2); // [1, { x: 3}]
getRestItems([1, 2, { x: 3 }], 3, 'x'); // [1, 2]
```

### Stop double-scrolling propagation

```js
$('.scrollable').on('DOMMouseScroll mousewheel', function(ev) {
  var $this = $(this),
    scrollTop = this.scrollTop,
    scrollHeight = this.scrollHeight,
    height = $this.height(),
    delta = (ev.type == 'DOMMouseScroll' ?
      ev.originalEvent.detail * -40 :
      ev.originalEvent.wheelDelta),
    up = delta > 0;

  var prevent = function() {
    ev.stopPropagation();
    ev.preventDefault();
    ev.returnValue = false;
    return false;
  };

  if (!up && -delta > scrollHeight - height - scrollTop) {
    $this.scrollTop(scrollHeight);
    return prevent();
  } else if (up && delta > scrollTop) {
    $this.scrollTop(0);
    return prevent();
  }
});
```

### Update URL query string

```js
function updateQueryString(name, value) {
  var href = location.href;
  var search = location.search;
  var hash = location.hash;
  var query = getQueryString(name);
  var hasQuery = typeof query !== 'object';

  if (hasQuery) {
    return href.replace(name + '=' + query, name + '=' + value);
  } else {
    if (search) {
      return href.replace(search, search + '&' + name + '=' + value);
    } else {
      if (hash) {
        return href.replace(hash, '?' + name + '=' + value + hash);
      } else {
        return href + '?' + name + '=' + value;
      }
    }
  }
}
```

### Get URL query string

```js
function getQueryString(name, url) {
  var href = url ? url : window.location.href;
  var reg = new RegExp('[?&]' + name + '=([^&#]*)', 'i');
  var string = reg.exec(href);
  return string ? string[1] : null;
}
```

or:

```js
function getQueryString(name, url) {
  var search = url ? url : window.location.search;
  return decodeURIComponent((new RegExp('[?|&]' + name + '=' + '([^&;]+?)(&|#|;|$)').exec(search)||[,""])[1].replace(/\+/g, '%20'))||null;
}
```

get the anchor:

```js
function getAnchor(url) {
  return url ? url.split('#')[1] : window.location.hash.substring(1);
}
```

### Remove HTML tags

```js
function strip(html) {
  var tmp = document.createElement('DIV');
  tmp.innerHTML = html;
  return tmp.textContent || tmp.innerText || '';
}
```

with RegEx:

```js
function strip(html) {
  return html.replace(/(<([^>]+)>)/ig, '');
}
```

with jQuery:

```js
function strip(html) {
  return $(html).text();
}
```

### Check for animation support

```js
function browserSupportsCSSProperty(propertyName) {
  var elm = document.createElement('div');
  propertyName = propertyName.toLowerCase();

  if (elm.style[propertyName] != undefined)
    return true;

  var propertyNameCapital = propertyName.charAt(0).toUpperCase() + propertyName.substr(1),
    domPrefixes = 'Webkit Moz ms O'.split(' ');

  for (var i = 0; i < domPrefixes.length; i++) {
    if (elm.style[domPrefixes[i] + propertyNameCapital] != undefined)
      return true;
  }

  return false;
}

if (!browserSupportsCSSProperty('animation')) {
  // fallback…
}
```

### Get the HTTP headers

```js
var req = new XMLHttpRequest();
var headers = req.getAllResponseHeaders().toLowerCase();
req.open('GET', document.location, false);
req.send(null);
alert(headers);
```

with jQuery：

```js
$.ajax({
  url: location.href
})
  .done(function(xhr) {
    console.log(xhr.getAllResponseHeaders(), xhr.getResponseHeader('Server'));
  });
```

### Preload sound files

```js
function preloadFiles(files, onComplete, onProgress) {
  var filesLoaded = 0,
    arr = [];

  for (var i = 0, len = files.length; i < len; i++) {
    arr[i] = new Audio();
    arr[i].addEventListener('canplaythrough', function() {
      filesLoaded++;
      if (filesLoaded === len && typeof onComplete === 'function') onComplete();
      if (typeof onProgress === 'function') onProgress(filesLoaded, len);
    }, false);
    arr[i].src = files[i];
    arr[i].load();
  };
}
```

### A imitation of the localStorage object

```js
if (!window.localStorage) {
  window.localStorage = {
    getItem: function(sKey) {
      if (!sKey || !this.hasOwnProperty(sKey)) {
        return null;
      }
      return unescape(document.cookie.replace(new RegExp("(?:^|.*;\\s*)" + escape(sKey).replace(/[\-\.\+\*]/g, "\\$&") + "\\s*\\=\\s*((?:[^;](?!;))*[^;]?).*"), "$1"));
    },
    key: function(nKeyId) {
      return unescape(document.cookie.replace(/\s*\=(?:.(?!;))*$/, "").split(/\s*\=(?:[^;](?!;))*[^;]?;\s*/)[nKeyId]);
    },
    setItem: function(sKey, sValue) {
      if (!sKey) {
        return;
      }
      document.cookie = escape(sKey) + "=" + escape(sValue) + "; expires=Tue, 19 Jan 2038 03:14:07 GMT; path=/";
      this.length = document.cookie.match(/\=/g).length;
    },
    length: 0,
    removeItem: function(sKey) {
      if (!sKey || !this.hasOwnProperty(sKey)) {
        return;
      }
      document.cookie = escape(sKey) + "=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/";
      this.length--;
    },
    hasOwnProperty: function(sKey) {
      return (new RegExp("(?:^|;\\s*)" + escape(sKey).replace(/[\-\.\+\*]/g, "\\$&") + "\\s*\\=")).test(document.cookie);
    }
  };
  window.localStorage.length = (document.cookie.match(/\=/g) || window.localStorage).length;
}
```

### Set and get cookie

set cookie:

```js
function setCookie(name, value, days, path, domain) {
  var newDate = new Date();
  var days = isNaN(days) ? 365 : days;
  var expires;
  var cookie;

  newDate.setTime(newDate.getTime() + (days * 24 * 60 * 60 * 1000));
  expires = 'expires=' + newDate.toUTCString();
  cookie = name + '=' + value + ';' + expires + ';';
  if (path) cookie += 'path=' + path + ';';
  if (domain) cookie += 'domain=' + domain + ';';
  document.cookie = cookie;
};
```

get cookie:

```js
function getCookie(name) {
  var name = name + '=';
  var cookies = document.cookie.split(';');
  var cookie;

  for (var i = 0; i < cookies.length; i++) {
    cookie = cookies[i];
    while (cookie.charAt(0) == ' ') cookie = cookie.substring(1);
    if (cookie.indexOf(name) == 0) return cookie.substring(name.length, cookie.length);
  }

  return '';
}
```

### Get a shuffled copy of an array

```js
var shuffle = function(arr) {
  var len = arr.length,
    shuffled = Array(len);

  for (var index = 0, rand; index < len; index++) {
    rand = Math.floor(Math.random() * (index + 1));
    if (rand !== index) shuffled[index] = shuffled[rand];
    shuffled[rand] = arr[index];
  }

  return shuffled;
};
```

### Create dynamic variables

with eval():

```js
eval('var variable' + i + '= arr[i]');
```

with window[]:

```js
window['variable' + i] = arr[i];
```

### Trigger click on an anchor

```js
document.getElementsByTagName('a')[0].click();
```

with [jQuery](http://jquery.com/), you can use:

```js
$('a')[0].click();
```
