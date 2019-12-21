---
layout: post
title:  "Preview image before uploaded"
date:   2017-02-20
categories: ['web development']
tags: ['javascript']
---

#### Via `URL.createObjectURL`

```js
function previewImgFile(file, callback) {
  if (typeof callback === 'function') {
    callback(URL.createObjectURL(file));
  }
}
```

#### Via `FileReader`

```js
function previewImgFile(file, callback) {
  var reader = new FileReader();

  reader.onload = function(e) {
    if (typeof callback === 'function') {
      callback(e.target.result);
    }
  };

  reader.readAsDataURL(file);
}
```

#### Useage

```js
document.querySelector('[type="file"]').addEventListener('change', function(e) {
  var preview = document.querySelector('#preview');
  var files = e.target.files;

  for (var i = 0; i < files.length; i++) {
    previewImgFile(files[i], function(res) {
      var tpl = '<img src=' + res + ' />';
      preview.insertAdjacentHTML('beforeend', tpl);
    });
  }
});
```
