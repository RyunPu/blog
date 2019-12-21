---
layout: post
title:  "Modernizr Methods"
date:   2014-04-25
categories: ['web development']
tags: ['javascript']
---

detecting css feature prefixes:

```js
Modernizr.prefixed('boxSizing') // 'boxSizing'
```

detecting dom feature prefixes:

```js
Modernizr.prefixed('requestAnimationFrame', window) // fn
```

mq() media query testing:

```js
Modernizr.mq('only screen and (max-width: 768px)')  // true
```

testProp():

```js
Modernizr.testProp('pointerEvents')  // true
```

testAllProps():

```js
Modernizr.testAllProps('boxSizing')  // true
```

hasEvent():

```js
Modernizr.hasEvent('gesturestart')  // true
```

see more: [modernizr docs](http://modernizr.com/docs/#s25)
