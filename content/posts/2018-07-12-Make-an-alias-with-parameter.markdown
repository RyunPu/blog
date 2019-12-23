---
layout: post
title:  "Make an alias with parameter"
date:   2018-07-12
categories: ['web development']
tags: ['tool']
---

Add the function in **.zshrc** file

```
function gitall() {
  git add .
  if [ "$1" != "" ]; then
    git commit -m "$1"
  else
    git commit -m "add posts"
  fi
  git push
}
```

Then

```bash
$ gitall "add posts"
```
