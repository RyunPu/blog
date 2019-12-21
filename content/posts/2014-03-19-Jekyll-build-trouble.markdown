---
layout: post
title:  "Jekyll build trouble"
date:   2014-03-19
categories: ['web development']
tags: ['jekyll']
---

初次安装 Jekyll，出现 ’Failed to build gem native extension‘ 的报错，花了不少时间寻找问题的答案，关键在于升级你的Ruby版本，建议使用 RVM 或者 Rbenv，我使用的是 RVM：

```bash
$ \curl -sSL https://get.rvm.io | bash -s stable
```

完成这步剩下的直接 OK，如果还有问题可以参考 [Jekyll troubleshooting](http://jekyllrb.com/docs/troubleshooting/)
