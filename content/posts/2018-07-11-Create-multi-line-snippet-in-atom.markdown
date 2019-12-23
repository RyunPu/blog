---
layout: post
title:  "Create multi-line snippet in atom"
date:   2018-07-11
categories: ['editor']
tags: ['atom']
---

#### Use `\n`

```
'.source.gfm':
  'language bash':
    'prefix': 'bash'
    'body': '```bash\n$ $1\n```'
```

#### Use multiline strings

```
'.source.gfm':
  'language bash':
    'prefix': 'bash'
    'body': '''
      ```bash
      $ $1
      ```
    '''
```
