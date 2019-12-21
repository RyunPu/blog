---
layout: post
title:  "Live reloading Chrome extension with WebSocket"
date:   2016-03-30
categories: ['web development']
tags: ['tool']
---

#### Install `ws`

```bash
$ npm install ws --save-dev
```

#### gulpfile.js

```js
gulp.watch(['build/**/*.{js,css,jpeg,png}'], ['reload']);

// send `reload` massage
var WebSocketServer = require('ws').Server;
var wss = new WebSocketServer({
  port: 9191
});

gulp.task('reload', function() {
  var client, i, len, ref, results;

  ref = wss.clients;
  results = [];

  for (i = 0, len = ref.length; i < len; i++) {
    client = ref[i];
    results.push(client.send('reload'));
  }

  return results;
});
```

#### background.js

```js
var reloadSocket = new WebSocket('ws://localhost:9191');

reloadSocket.onopen = function() {
  console.log('connected');
};

reloadSocket.onmessage = function(msg) {
  if (msg.data === 'reload') {
    // reload extension
    chrome.runtime.reload();
  }
};

chrome.tabs.query({
  active: true,
  currentWindow: true
}, function(tabs) {
  if (!tabs[0].url.includes('chrome-extension://')) {
    // reload page
    chrome.tabs.reload();
  }
});
```
