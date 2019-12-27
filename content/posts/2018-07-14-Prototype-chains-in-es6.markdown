---
layout: post
title:  "Prototype chains in es6"
date:   2018-07-14
categories: ['web development']
tags: ['javascript']
---

```js
class Person {
  constructor(name) {
    this.name = name
  }
}

class Employee extends Person {
  constructor(name, title) {
    super(name)
    this.title = title
  }
}

const ryun = new Employee('Ryun', 'Front-End Engineer')
```

![image](https://user-images.githubusercontent.com/6168498/71349132-2b0a0880-25a9-11ea-8838-f43b847ccd1f.png)
