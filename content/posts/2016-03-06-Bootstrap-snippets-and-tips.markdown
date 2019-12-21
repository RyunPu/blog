---
layout: post
title:  "Bootstrap snippets and tips"
date:   2016-03-06
categories: ['web development']
tags: ['javascript', 'css']
---

### Update popover text:

```js
$('[data-toggle="popover"]').popover({
  html: true,
  trigger: 'focus',
  content: '',
  placement: 'bottom'
});

$('[data-toggle="popover"]').data('bs.popover').options.content = 'new content';
$('[data-toggle="popover"]').popover('show');
```

to dismiss the popover on iOS, you may use ```body { cursor: pointer; }```

> Specific markup required for dismiss-on-next-click
For proper cross-browser and cross-platform behavior, you must use the ```<a>``` tag, not the ```<button>``` tag, and you also must include the **role="button"** and **tabindex** attributes.

### Center modal dialog with CSS:

```css
.center-container.modal { padding: 0!important; text-align: center;}
.center-container.modal:before { content: ''; display: inline-block; margin-right: -4px; height: 100%; vertical-align: middle;}
.center-container.modal .modal-dialog { display: inline-block; text-align: left; vertical-align: middle;}
```

### Vertically center modal dialog with JS:

```js
function reposition() {
  var modal = $(this);
  var dialog = modal.find('.modal-dialog');

  modal.css('display', 'block');
  dialog.css('margin-top', Math.max(0, ($(window).height() - dialog.height()) / 2));
}

$('.modal').on('show.bs.modal', reposition);

$(window).on('resize', function() {
  $('.modal:visible').each(reposition);
});
```

###  Popup modal from bottom

```css
.modal.fade .modal-dialog { transform: translate3d(0, 100vh, 0);}
.modal.in .modal-dialog { transform: translate3d(0, 0, 0);}
.modal .modal-dialog { position: absolute; left: 0; right: 0; bottom: 0;}
```

### Set modal dialog's max height:

```js
function setModalMaxHeight(element) {
  var $element = $(element);
  var $content = $element.find('.modal-content');
  var borderWidth = $content.outerHeight() - $content.innerHeight();
  var dialogMargin = $(window).width() < 768 ? 20 : 60;
  var contentHeight = $(window).height() - (dialogMargin + borderWidth);
  var headerHeight = $element.find('.modal-header').outerHeight() || 0;
  var footerHeight = $element.find('.modal-footer').outerHeight() || 0;
  var maxHeight = contentHeight - (headerHeight + footerHeight);

  $content.css({
    'overflow': 'hidden'
  });

  $element
    .find('.modal-body').css({
      'max-height': maxHeight,
      'overflow-y': 'auto'
    });
}

$('.modal').on('show.bs.modal', function() {
  $(this).show();
  setModalMaxHeight(this);
});

$(window).resize(function() {
  if ($('.modal.in').length !== 0) {
    setModalMaxHeight($('.modal.in'));
  }
});
```

### Keep popover open while it being hovered

```js
var originalLeave = $.fn.popover.Constructor.prototype.leave;
$.fn.popover.Constructor.prototype.leave = function(obj) {
  var self = obj instanceof this.constructor ?
    obj : $(obj.currentTarget)[this.type](this.getDelegateOptions()).data('bs.' + this.type);
  var container, timeout;

  originalLeave.call(this, obj);

  if (obj.currentTarget) {
    container = $(obj.currentTarget).siblings('.popover');
    timeout = self.timeout;
    container.one('mouseenter', function() {
      clearTimeout(timeout);
      container.one('mouseleave', function() {
        $.fn.popover.Constructor.prototype.leave.call(self, self);
      });
    });
  }
};
```

```js
$('[data-toggle=popover]').popover({
  trigger: 'hover',
  delay: { show: 50, hide: 400 }
});
```
