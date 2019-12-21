---
layout: post
title:  "Prevent page scrolling when a modal is open"
date:   2016-03-28
categories: ['web development']
tags: ['javascript', 'css']
---

### Use CSS

```css
body.modal-open {
  height: 100vh;
  overflow-y: hidden;
  padding-right: 15px; /* Avoid width reflow */
}
```

### Use JavaScript

```js
// When the modal is shown, we want a fixed body
document.body.style.position = 'fixed';
document.body.style.top = `-${window.scrollY}px`;

// When the modal is hidden, we want to remain at the top of the scroll position
const scrollY = document.body.style.top;
document.body.style.position = '';
document.body.style.top = '';
window.scrollTo(0, parseInt(scrollY || '0') * -1)
```

see more: [Prevent page scrolling when a modal is open](https://css-tricks.com/prevent-page-scrolling-when-a-modal-is-open/)
