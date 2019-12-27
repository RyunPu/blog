---
layout: post
title:  "npx is cool"
date:   2018-07-17
categories: ['web development']
tags: ['tool']
---

### About

> npx is a tool intended to help round out the experience of using packages from the npm registry — the same way npm makes it super easy to install and manage dependencies hosted on the registry, npx makes it easy to use CLI tools and other executables hosted on the registry. It greatly simplifies a number of things that, until now, required a bit of ceremony to do with plain npm.

### Easily run commands

```
❯ npx cowsay hello
npx: installed 10 in 3.659s
 ____________
< hello >
 ------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```


### Run local commands

```
❯ yarn add atomic-algolia -D
❯ npx atomic-algolia
[Algolia] Adding 25 hits to dev_Blog
[Algolia] Updating 0 hits to dev_Blog
[Algolia] Removing 25 hits from dev_Blog
[Algolia] 113 hits unchanged in dev_Blog
{
  objectIDs: [...],
  taskID: { dev_Blog: 5366258650 }
}
```

### Run commands with different Node.js versions

```
❯ npx -p node@7 node -v
v7.10.1
```

### Run GitHub source code

```
❯ npx github:piuccio/cowsay hello
❯ npx https://gist.github.com/zkat/4bc19503fe9e9309e2bfaa2c58074d32
```

### Run http-server

```
❯ npx http-server -p 4000
npx: installed 27 in 9.767s
Starting up http-server, serving ./
Available on:
  http://127.0.0.1:4000
  http://192.168.0.100:4000
Hit CTRL-C to stop the server
```

see also: [awesome-npx](https://github.com/junosuarez/awesome-npx)
