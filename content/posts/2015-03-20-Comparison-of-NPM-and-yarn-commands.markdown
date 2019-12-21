---
layout: post
title:  "Comparison of NPM and yarn commands"
date:   2015-03-19
categories: ['web development']
tags: ['tool']
---

| npm \(v5\)                                 | Yarn                                     |
|--------------------------------------------|------------------------------------------|
| npm install                                | yarn add                                 |
| \(N/A\)                                    | yarn add \-\-flat                        |
| \(N/A\)                                    | yarn add \-\-har                         |
| npm install \-\-no\-package\-lock          | yarn add \-\-no\-lockfile                |
| \(N/A\)                                    | yarn add \-\-pure\-lockfile              |
| npm install \[package\] \-\-save           | yarn add \[package\]                     |
| npm install \[package\] \-\-save\-dev      | yarn add \[package\] \-\-dev             |
| \(N/A\)                                    | yarn add \[package\] \-\-peer            |
| npm install \[package\] \-\-save\-optional | yarn add \[package\] \-\-optional        |
| npm install \[package\] \-\-save\-exact    | yarn add \[package\] \-\-exact           |
| \(N/A\)                                    | yarn add \[package\] \-\-tilde           |
| npm install \[package\] \-\-global         | yarn global add \[package\]              |
| npm update \-\-global                      | yarn global upgrade                      |
| npm rebuild                                | yarn add \-\-force                       |
| npm uninstall \[package\]                  | yarn remove \[package\]                  |
| npm cache clean                            | yarn cache clean \[package\]             |
| rm \-rf node\_modules && npm install       | yarn upgrade                             |
| npm version major                          | yarn version \-\-major                   |
| npm version minor                          | yarn version \-\-minor                   |
| npm version patch                          | yarn version \-\-patch                   |
