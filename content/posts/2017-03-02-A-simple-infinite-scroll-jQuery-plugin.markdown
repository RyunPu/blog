---
layout: post
title:  "A simple infinite scroll jQuery plugin"
date:   2017-03-02
categories: ['web development']
tags: ['javascript']
---

```js
;(function(factory) {
  if (typeof define === 'function' && define.amd) {
    define(['jquery'], factory);
  } else {
    factory(jQuery);
  }
}(function($) {
  function infiniteScroll(el, options) {
    this.$el = $(el);
    this.defaults = {
      offset: 100,
      callback: function() {}
    };
    this.cfgs = $.extend(this.defaults, options);
    this.bind();
  }

  infiniteScroll.prototype = {
    scroll: function() {
      var $el = this.$el;
      var offset = $el[0].scrollHeight - $(window).height() - $el.scrollTop();
      if (offset <= this.cfgs.offset) this.cfgs.callback();
    },

    bind: function(isUnbind) {
      var $el = this.$el;
      $el = $el[0].tagName && $el[0].tagName.toUpperCase() === 'BODY' ? $(document) : $el;
      $el[isUnbind ? 'off' : 'on']('scroll.infinite', $.proxy(this.scroll, this));
    },

    destroy: function() {
      this.bind(true);
    }
  };

  $.fn.infiniteScroll = function(options) {
    var args = Array.prototype.slice.call(arguments, 1);
    return this.each(function() {
      var instance = $(this).data('infiniteScroll');
      if (!instance) {
        $(this).data('infiniteScroll', new infiniteScroll(this, options));
      } else if (typeof options === 'string') {
        instance[options].apply(instance, args);
      }
    });
  };
}));
```
