---
layout: post
title: "Git Cheatsheet"
date: 2019-03-25
categories: ["web development"]
tags: ["git"]
---

初始化:

```
❯ git init
```

gra 添加远程仓库:

```
❯ git remote add origin git@github.com:RyunPu/learn-git.git
```

> 根据需要添加远程仓库，`git@github.com:RyunPu/learn-git.git` 应该是你自己的仓库地址

glog 查看提交历史:

```
❯ git log --oneline --decorate --graph
```

gst 查看当前状态:

```
❯ git status
```

添加一个新文件，使用 ga 将文件添加到暂存区:

```
❯ git add README.md
```

> 使用 `git add .` 来添加所有文件

gcmsg 提交文件:

```
❯ git commit -m 'touch README.md'
```

文件在暂存区时，修改文件后，使用 gcam 提交文件:

```
❯ git commit -a -m 'modify README.md'
```

gp 第一次关联并上传到远程仓库:

```
❯ git push --set-upstream origin master
```

> 以后的上传可以直接使用 `git push`

gl 将代码从远程仓库取到本地:

```
❯ git pull
```

gb 创建分支 develop:

```
❯ git branch develop
```

gco 切换到分支 develop:

```
❯ git checkout develop
```

gcm 切换回 master:

```
❯ git checkout master
```

gbd 删除分支 develop:

```
❯ git branch -d develop
```

> 使用 `git push origin -d develop` 可以删除远程仓库的分支

gcb 创建分支 develop 并切换到 develop:

```
❯ git checkout -b develop
```

做些更改，使用 gp 将分支 develop 上传到远程仓库:

```
❯ git push origin develop
```

gcm 切换回 master，使用 gm 合并 develop:

```
❯ git checkout master
❯ git merge develop
```

> merge 的过程中可能需要解决冲突，使用 `git merge --abort` 可以放弃此次合并

gsh 查看某个提交:

```
❯ git show 3855451
```

> `3855451` 是对提交的引用，可以通过前面的 `glog` 来查看，当然你也可以通过 `HEAD~1` 这样的形式来引用

gd 比对某个提交:

```
❯ git diff 3855451
```

grb 在新位置重新提交:

```
❯ git checkout develop
❯ git rebase master
```

> 然后 `git checkout master && git merge develop`

gc! 修复当前提交:

```
❯ git commit -v --amend
```

> 使用 `gcn!` 即 `git commit -v --no-edit --amend` 来使用上次的提交信息  
> 或者 `gcan!` 即 `git commit -v -a --no-edit --amend`

grbi 开启交互式 rebase 过程

```
❯ git rebase -i e0f28ff
```

上面的命令表示 rebase `e0f28ff` 及之前的提交到当前，执行结果如下:

```
pick bfd724f hello from develop and master

# Rebase e0f28ff..bfd724f onto e0f28ff (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
...
```

然后将上面内容中的引用 `bfd724f` 前的 `pick` 改为 `edit`:

```
edit bfd724f hello from develop and master
```

> 更多命令可以查看输出内容的 `Commands` 部分

完成修改后，使用 grbc 继续:

```
❯ git commit -v -a --no-edit --amend
❯ git rebase --continue
```

> 使用 `git rebase --abort` 可以放弃此次 rebase

grhh 撤销某个的提交之前的更改或提交:

```
❯ git reset --hard 5597026
```

使用用交互式 rebase 撤销提交:

```
❯ git rebase -i 5597026
```

```
pick 39f0eaf hello again

# Rebase e0f28ff..bfd724f onto e0f28ff (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
...
```

然后将上面内容中的引用 `39f0eaf` 前的 `pick` 改为 `drop`:

```
drop 39f0eaf hello again
```

> 保存退出后，`39f0eaf` 就不存在了

grev 反转某个提交:

```
❯ git revert f7cad2f
```

> revert 将某个提交恢复提交之前的状态，作为一个新的提交，与原来的提交并存

gstall 临时存放工作目录的改动

```
❯ git stash --all
```

gstp 取出之前存放的改动

```
❯ git stash pop
```

reflog 引用记录:

```
❯ git reflog
5961845 (HEAD -> master) HEAD@{0}: reset: moving to HEAD
5961845 (HEAD -> master) HEAD@{1}: checkout: moving from f7cad2f793ac794b07da61ed91eef364b6e406bf to master
f7cad2f HEAD@{2}: checkout: moving from master to f7cad2f
```

> 误删某个提交后，可尝试从 reflog 中找回，然后 `git checkout f7cad2f`，然后根据需要操作
