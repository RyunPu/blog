---
layout: post
title:  "Highlight code in Jekyll"
date:   2014-03-22
categories: ['web development']
tags: ['jekyll']
---

推荐的：

```
{% highlight ruby linenos %}
def foo
    puts 'foo'
end
{% endhighlight %}
```

简洁的：

```
    ```ruby
        def foo
            puts 'foo'
        end
    ```
```

最终效果：

```ruby
def foo
    puts 'foo'
end
```
