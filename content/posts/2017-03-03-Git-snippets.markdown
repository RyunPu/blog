---
layout: post
title:  "Git snippets"
date:   2017-03-03
categories: ['web development']
tags: ['git']
---

### Working with forks

Clone your fork to your local machine

```bash
$ git clone git@github.com:USERNAME/FORKED-PROJECT.git
```

Add 'upstream' repo to list of remotes

```bash
$ git remote add upstream https://github.com/UPSTREAM-USER/ORIGINAL-PROJECT.git
```

Fetch from upstream remote

```bash
$ git fetch upstream
```

Check out your fork's local master branch

```bash
$ git checkout master
```

Merge the changes from upstream/master into your local master branch

```bash
$ git merge upstream/master
```

### Working with branches

Pushing to a remote

```bash
$ git push <REMOTENAME> <BRANCHNAME>
```
```bash
$ git push <REMOTENAME> HEAD:<BRANCHNAME>
```

Renaming branches

```bash
$ git push <REMOTENAME> <LOCALBRANCHNAME>:<REMOTEBRANCHNAME>
```

Deleting a remote branch

```bash
$ git push <REMOTENAME> :<BRANCHNAME>
```

Checkout a remote branch

```bash
$ git checkout -b <LOCALBRANCHNAME> <REMOTENAME>/<REMOTEBRANCHNAME>
```


### Adding an existing project to GitHub

Initialize the local directory as a Git repository

```bash
$ git init
```

Add the files in your new local repository. This stages them for the first commit

```bash
$ git add .
```

Commit the files that you've staged in your local repository

```bash
$ git commit -m "First commit"
```

In Terminal, add the URL for the remote repository where your local repository will be pushed

```bash
$ git remote add origin remoteRepositoryURL
```

Push the changes in your local repository to GitHub

```bash
$ git push -u origin master
```

see more: [github help](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/), [GitHub-Forking](https://gist.github.com/Chaser324/ce0505fbed06b947d962)
