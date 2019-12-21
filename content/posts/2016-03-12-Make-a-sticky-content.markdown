---
layout: post
title:  "Make a sticky content"
date:   2016-03-12
categories: ['web development']
tags: ['javascript', 'css']
---

### Use CSS

```css
.content { position: sticky; top: 0;}
```

### With Bootstrap 3

##### Via data attributes：

```html
<div data-spy="affix" data-offset-top="60" data-offset-bottom="200">
  ...
</div>
```

##### Via JavaScript：

```js
$('#myAffix').affix({
  offset: {
    top: 0,
    bottom: function () {
      return (this.bottom = $('.footer').outerHeight(true))
    }
  }
})
```

### With Semantic UI

```js
$('.ui.sticky').sticky({
  context: '#context'
});
```

see also: [sticky](https://github.com/garand/sticky)
