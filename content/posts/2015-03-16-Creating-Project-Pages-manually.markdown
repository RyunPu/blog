---
layout: post
title:  "Creating Project Pages manually"
date:   2015-03-16
categories: ['web development']
tags: ['git']
---

```bash
$ cd repository
```

```bash
$ git checkout --orphan gh-pages
```

add and commit some pages and then:

```bash
$ git push origin gh-pages
```

your Project Pages site will be available at ```https://username.github.io/projectname```

see also: [Getting Started with GitHub Pages](https://guides.github.com/features/pages/)
