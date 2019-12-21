---
layout: post
title:  "Make a sticky footer"
date:   2016-03-10
categories: ['web development']
tags: ['javascript', 'css']
---

### Our html

```html
<body>
  <main></main>
  <footer></footer>
</dody>
```

### Use CSS

```css
html { position: relative; min-height: 100%;}
body { margin-bottom: 50px;}
footer { position: absolute; left: 0; right: 0; bottom: 0; height: 50px;}
```

with calc():

```css
main { min-height: calc(100vh - 50px);}
footer { height: 50px;}
```

with flexbox:

```css
html { height: 100%;}
body { min-height: 100%; display: flex; flex-direction: column;}
main { flex: 1;}
```

with grid:

```css
html { height: 100%;}
body { min-height: 100%; display: grid; grid-template-rows: 1fr auto;}
footer { grid-row: 2 / 3;}
```

### Use JavaScript

```js
function activateStickyFooter(selector) {
  function adjustFooterCssTopToSticky() {
    // remember to set the position of the footer as relative
    const footer = document.querySelector(selector);
    const bounding_box = footer.getBoundingClientRect();
    const footer_height = bounding_box.height;
    const window_height = window.innerHeight;
    const above_footer_height = bounding_box.top - getCssTopAttribute(footer);

    if (above_footer_height + footer_height <= window_height) {
      const new_footer_top = window_height - (above_footer_height + footer_height);
      footer.style.top = new_footer_top + 'px';
    } else if (above_footer_height + footer_height > window_height) {
      footer.style.top = null;
    }
  }

  function getCssTopAttribute(htmlElement) {
    const top_string = htmlElement.style.top;
    if (top_string === null || top_string.length === 0) return 0;
    const extracted_top_pixels = top_string.substring(0, top_string.length - 2);
    return parseFloat(extracted_top_pixels);
  }

  adjustFooterCssTopToSticky()
  window.addEventListener('resize', adjustFooterCssTopToSticky);
}
```
