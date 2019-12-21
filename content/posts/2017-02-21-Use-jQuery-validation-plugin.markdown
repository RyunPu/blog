---
layout: post
title:  "Use jQuery validation plugin"
date:   2017-02-21
categories: ['web development']
tags: ['javascript']
---

#### Set default error message

```js
$.extend($.validator.messages, {
  required: "这是必填字段",
  remote: "请修正此字段",
  email: "请输入有效的电子邮件地址",
  url: "请输入有效的网址",
  date: "请输入有效的日期",
  dateISO: "请输入有效的日期 (YYYY-MM-DD)",
  number: "请输入有效的数字",
  digits: "只能输入数字",
  creditcard: "请输入有效的信用卡号码",
  equalTo: "你的输入不相同",
  extension: "请输入有效的后缀",
  maxlength: $.validator.format("最多可以输入 {0} 个字符"),
  minlength: $.validator.format("最少要输入 {0} 个字符"),
  rangelength: $.validator.format("请输入长度在 {0} 到 {1} 之间的字符串"),
  range: $.validator.format("请输入范围在 {0} 到 {1} 之间的数值"),
  max: $.validator.format("请输入不大于 {0} 的数值"),
  min: $.validator.format("请输入不小于 {0} 的数值")
});
```

#### Set custom error message

```js
$('form').validate({
  rules: {
    email: {
      required: true,
      email: true
    }
  },

  messages: {
    email: {
      required: '邮箱不能为空',
      email: '邮箱格式不正确'
    }
}
});
```

#### Submit with AJAX

```js
$('form').validate({
  submitHandler: function(form) {
    $.post('ajax.php', $(form).serialize(), function(data) {
      console.log(data);
    }, 'json');
  }
});
```

#### addMethod

```js
$.validator.addMethod('pattern', function(value, element, param) {
  return this.optional(element) || param.test(value);
}, 'Invalid format.');

$('form').validate({
  rules: {
    email: {
      required: true,
      pattern: /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/
    }
  }
});
```

see more: [jquery-validation](https://github.com/jquery-validation/jquery-validation)
