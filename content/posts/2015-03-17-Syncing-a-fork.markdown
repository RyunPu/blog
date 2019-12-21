---
layout: post
title:  "Syncing a fork"
date:   2015-03-17
categories: ['web development']
tags: ['git']
---

```bash
$ git remote add upstream https://github.com/username/projectname.git
```

```bash
$ git pull upstream master(git fetch upstream, git merge upstream/master)
```

```bash
$ git push origin master
```

see more: [Syncing a fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
