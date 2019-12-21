---
layout: post
title:  "Add Readmore in Jekyll"
date:   2014-03-21
categories: ['web development']
tags: ['jekyll']
---

当然，你可以使用 Jekyll 自带的 post.excerpt 并在 \_config.yml 中配置 excerpt\_separator，但这样做时并不能灵活的添加 ’Readmore‘，因此可以使用下面的方法：

```html
{% if post.content contains '<!-- more -->' %}
    {{ post.content | split:'<!-- more -->' | first }}
    <p class="more"><a href="{{ post.url }}">Read More &raquo;</a></p>
{% else %}
    {{ post.content }}
{% endif %}
```

然后在文章换行处添加 `<!-- more -->`
