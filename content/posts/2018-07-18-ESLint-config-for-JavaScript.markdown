---
layout: post
title:  "ESLint Config for JavaScript"
date:   2018-07-18
categories: ['web development']
tags: ['tool']
---

### eslint-config-airbnb-base

#### Install

1. List the correct versions of each package:

```
❯ npm info "eslint-config-airbnb-base@latest" peerDependencies
{ eslint: '^5.16.0 || ^6.1.0', 'eslint-plugin-import': '^2.18.2' }
```

2. Install the package:

```
❯ yarn add eslint eslint-plugin-import eslint-config-airbnb-base -D
```

#### Usage

```
❯ npx eslint --init
```

```
// .eslintrc.js
module.exports = {
  "env": {
    "browser": true,
    "es6": true
  },
  "extends": "airbnb-base",
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "rules": {
    "semi": ["error", "never"]
  }
};
```

### eslint-config-standard

#### Install

1. List the correct versions of each package:

```
❯ npm info "eslint-config-standard" peerDependencies

{
  eslint: '>=6.2.2',
  'eslint-plugin-import': '>=2.18.0',
  'eslint-plugin-node': '>=9.1.0',
  'eslint-plugin-promise': '>=4.2.1',
  'eslint-plugin-standard': '>=4.0.0'
}
```

2. Install the package:

```
❯ yarn add eslint eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard eslint-config-standard -D
```

#### Usage

```
❯ npx eslint --init
```

```
// .eslintrc.js
module.exports = {
  "env": {
    "browser": true,
    "es6": true
  },
  "extends": "standard",
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "rules": {
    "comma-dangle": ["error", "always-multiline"]
  }
};
```

see also: [configuring](http://eslint.cn/docs/user-guide/configuring)，[rules](https://cn.eslint.org/docs/rules/)
