---
layout: post
title:  "Using formdata objects"
date:   2015-04-08
categories: ['web development']
tags: ['javascript']
---

```js
var formData = new FormData();
formData.append('name', $('#name').val());
formData.append('file', $('#file')[0].files[0]);

$.ajax({
  url: $('#form').attr('action'),
  type: 'POST',
  cache: false,
  data: formData,
  processData: false,
  contentType: false
})
  .done(function(data) {
    console.log(data);
  })
  .fail(function() {
    console.log('请求失败');
  });
```

see more: [Using FormData Objects](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Using_FormData_Objects)
