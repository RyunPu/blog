---
layout: post
title:  "Exit the Vim editor"
date:   2018-07-08
categories: ['web development']
tags: ['tool']
---

Hit the `i` key to enter "Insert mode". Hit the `Esc` key to enter "Normal mode". Then you can type `:` to enter "Command-line mode". To execute a command, press the `Enter` key.

* `:q` to quit (short for `:quit`)

* `:q!` / `ZQ` to quit without saving (short for `:quit!`)

* `:wq` to write and quit

* `:wq!` to write and quit even if file has only read permission (if file does not have write permission: force write)

* `:x` / `ZZ` to write and quit (similar to `:wq`, but only write if there are changes)

* `:exit` to write and exit (same as `:x`)

* `:qa` to quit all (short for `:quitall`)

* `:cq` to quit without saving and make Vim return non-zero error (i.e. exit with error)

<br>

> You can use `:help :quit` to see more details
