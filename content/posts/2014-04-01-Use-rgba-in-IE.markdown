---
layout: post
title:  "Use rgba in IE"
date:   2014-04-01
categories: ['web development']
tags: ['css']
---

```css
.class { background: rgba(0,0,0,.5); filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#7F000000",endColorstr="#7F000000");}
:root .class { filter: none;} /* IE9 */
```

with [Sass](http://sass-lang.com/), you can use:

```css
.class { background: rgba(0,0,0,.5); filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#{ie-hex-str($color)}",endColorstr="#{ie-hex-str($color)}");}
```

converter: [kilianvalkhof](http://kilianvalkhof.com/2010/css-xhtml/how-to-use-rgba-in-ie/)
