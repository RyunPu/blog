---
layout: post
title:  "JavaScript 模块化"
date:   2018-07-15
categories: ['web development']
tags: ['javascript']
---

### 为什么需要模块化

> JavaScript 最初是一门用于构建小型网站的语言。但是今天，网站正在向 Web 应用发展，所需代码和功能正在变得越来越大。开发人员需要一种方法来分离功能，同时指定相应依赖。就像 C++ 和 Java 依赖外部库（例如数学库）来计算基本的数学方程式，而无需重写它们。因此，库使得语言不用重复书写代码和委托功能，这就像模块对于 JavaScript 的作用。模块有助于开发人员实现功能分离并组织代码库。使用模块的最大原因之一是 JavaScript 的全局命名空间很容易受到污染。函数是 JavaScript 中唯一创建新作用域方法。因此，未在函数中声明的任何内容都是全局命名空间的一部分。同时，我们在 JavaScript 顶层声明的每个函数都是全局可用的，因此不能再次创建同一名称的函数。通常，这会导致命名空间受到污染，我们很难找到和重用相关代码。但是有时我们并不希望某个函数随处可用。为了使一个 JavaScript 文件中的函数仅对另一个单独的 JavaScript 文件可用，我们可以使用模块。尽管还有许多其他原因，使用模块化功能的主要原因有：
> * 简化依赖关系管理
> * 代码组织：让功能从我们的应用中分离，提供封装
> * 提供代码可重用性
> * 去耦（减轻重构的痛苦）
> * 代码可扩展性

### ES5 中的模块化

#### 立即执行函数

```js
(function () {}())
```

#### 输入全局变量

```js
(function ($) {})(jQuery)
```

#### 对象写法

```js
var module = {
  message: '你好!',
  sayHello: function() {
    console.log(this.message);
  }
};
```

#### 构造器写法

```js
var Module = function() {
  var message = '你好!';

  function sayHello() {
    console.log(message);
  }

  return {
    sayHello: sayHello
  };
};
```

### 模块化规范

目前流行的 JavaScript 模块化规范有 CommonJS、AMD、CMD 以及 ES6 的模块系统。

#### CommonJS

CommonJS 是服务器端模块的规范，Node.js 采用了这个规范。根据这个规范，每一个文件就是一个模块，其内部定义的变量是属于这个模块的，不会对外暴露，也就是说不会污染全局变量。CommonJS 的核心思想就是通过 require 方法来同步加载所要依赖的其他模块，然后通过 exports 或者 module.exports 来导出需要暴露的接口。

```js
// a.js
var message = '你好!';

function sayHello() {
  console.log(message);
}

module.exports = {
  sayHello: sayHello
};
```

```js
// b.js
var greet = require('./a');
greet.sayHello();
```

#### AMD

AMD 全称是”Asynchronous Module Definition”, 中文名是”异步模块定义”。AMD 规范则是非同步加载模块，允许指定回调函数。由于 Node.js 主要用于服务器编程，模块文件一般都已经存在于本地硬盘，所以加载起来比较快，不用考虑非同步加载的方式，所以 CommonJS  规范比较适用。但是，如果是浏览器环境，要从服务器端加载模块，这时就必须采用非同步模式，因此浏览器端一般采用 AMD 规范。require.js 就采用了 AMD 规范的实现。AMD 通过 define 来定义一个模块，然后使用 require 来加载一个模块。

##### define(id, [depends], callback)

```js
// a.js
define(function () {
  var message = '你好!';

  function sayHello() {
    console.log(message);
  }

  return {
    sayHello: sayHello
  };
});
```

##### require([module], callback)

```js
// b.js
require(['a'], function (greet) {
  greet.sayHello();
})
```

#### CMD

CMD 全称是”Common Module Definition”, 中文名是”普通模块定义”。CMD 规范是阿里的玉伯提出来的，sea.js 采用了这个规范。它和 requirejs 非常类似，即一个 JavaScript 文件就是一个模块，但 CMD 是通过按需加载的方式，而不是必须在模块开始就加载所有的依赖。

```js
// a.js
define(function(require, exports, module) {
  var message = '你好!';

  function sayHello() {
    console.log(message);
  }

  exports.sayHello = sayHello;
});
```

```js
// b.js
define(function(require, exports, module) {
  var greet = require('./a');
  greet.sayHello();
});
```

#### UMD

UMD 全称是”Universal Module Definition”, 中文名是”通用模块定义”。使用 UMD 可以同时支持多种模块化规范。

```js
(function(root, factory) {
  if (typeof define === 'function' && define.amd) {
    define(['jquery', 'underscore'], factory);
  } else if (typeof module === 'object' && module.exports) {
    module.exports = factory(require('jquery'), require('underscore'));
  } else {
    root.returnExports = factory(root.$, root._);
  }
}(typeof self !== 'undefined' ? self : this, function($, _) {
  return {};
}));
```

#### ES6 Module

之前的几种模块化方案都是前端社区自己实现的，只是得到了大家的认可和广泛使用，而 ES6 的模块化方案是真正的规范。在 ES6 中，我们可以使用 import 关键字引入模块，通过 exprot 关键字导出模块。

```js
import Vue from 'vue'
import Vuex from 'vuex'
import ls from '../utils/localStorage'
import router from '../router'
import * as moreActions from './actions'
import * as moreGetters from './getters'

// ...

export default new Vuex.Store({
  state,
  getters,
  mutations,
  actions
})
```
