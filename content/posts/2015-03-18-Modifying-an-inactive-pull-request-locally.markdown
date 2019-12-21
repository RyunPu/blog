---
layout: post
title:  "Modifying an inactive pull request locally"
date:   2015-03-18
categories: ['web development']
tags: ['git']
---

```bash
$ git fetch origin pull/ID/head:BRANCHNAME
```

```bash
$ git checkout BRANCHNAME
```

When you're ready, you can push the new branch up:

```bash
$ git push origin BRANCHNAME
```

see more: [Checking out pull requests locally](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/checking-out-pull-requests-locally)
