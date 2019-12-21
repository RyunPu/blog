---
layout: post
title:  "Git Diff with Beyond Compare"
date:   2015-03-27
categories: ['web development']
tags: ['tool']
---

Launch Beyond Compare, go to the Beyond Compare menu and run **Install Command Line Tools**.

### Diff

```bash
$ git config --global diff.tool bc3
```

To launch a diff using Beyond Compare, use the command：

```bash
$ git difftool file.ext
```

### Merge (Pro only)

```bash
$ git config --global merge.tool bc3
```

```bash
$ git config --global mergetool.bc3 trustExitCode true
```

To launch a 3-way merge using Beyond Compare, use the command：

```bash
$ git mergetool file.ext
```

see more: [Using Beyond Compare with Version Control Systems](http://www.scootersoftware.com/support.php?zz=kb_vcs_osx)
