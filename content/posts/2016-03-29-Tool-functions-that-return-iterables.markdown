---
layout: post
title:  "Tool functions that return iterables"
date:   2016-03-29
categories: ['web development']
tags: ['javascript']
---

```js
function objectEntries(obj) {
  let iter = Reflect.ownKeys(obj)[Symbol.iterator]();

  return {
    [Symbol.iterator]() {
      return this;
    },
    
    next() {
      let {
        done,
        value: key
      } = iter.next();

      if (done) {
        return {
          done: true
        };
      }

      return {
        value: [key, obj[key]]
      };
    }
  };
}
```

```js
const obj = { first: 'Jane', last: 'Doe' };

for (const [key, value] of objectEntries(obj)) {
  console.log(`${key}: ${value}`);
}
```

```js
// Output:
// first: Jane
// last: Doe
```

use generators：

```js
function* objectEntries(obj) {
  const propKeys = Reflect.ownKeys(obj);

  for (const propKey of propKeys) {
    yield [propKey, obj[propKey]];
  }
}
```

see more: [Iterables and iterators](https://exploringjs.com/es6/ch_iteration.html#objectEntries)
