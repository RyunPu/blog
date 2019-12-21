---
layout: post
title:  "Commands for Packager managers"
date:   2015-03-19
categories: ['web development']
tags: ['tool']
---

|&nbsp;                                   | npm                                 | composer                                                    | pip                                      | rubygem                        |
|-----------------------------------------|-------------------------------------|-------------------------------------------------------------|------------------------------------------|--------------------------------|
| Language                                | node \-v                            | php \-\-version                                             | python \-\-version                       | ruby \-v                       |
| Version                                 | npm \-\-version                     | composer \-\-version                                        | pip \-\-version                          | gem \-v                        |
| Location of the program file            | which npm                           | which composer                                              | which pip                                | which gem                      |
| List of all packages installed globally | npm ls \-g \-\-depth=0              | composer show \-\-installed \(locally\)                     | pip freeze                               | gem list                       |
| Info about a package                    | npm show \[package\-name\]          | composer show \[package\-name\]                             |                                          | gem list \[package\-name\]     |
| Install a package                       | npm install \[package\-name\] \-g   | composer require \[package\-name\] and run composer install | pip install\[package\-name\]             | gem install \[package\-name\]  |
| Uninstall a package                     | npm uninstall \[package\-name\] \-g | edit composer\.json and run composer update                 | pip uninstall\[package\-name\]           | gem uninstall\[package\-name\] |
| Outdated packages                       | npm \-g outdated                    | composer update \-\-dry\-run                                |                                          | gem outdated                   |
| Updated packages                        | npm \-g update \[package\-name\]    | composer update                                             | pip install\-\-upgrade \[package\-name\] | gem update \[package\-name\]   |
| Help                                    | npm help                            | composer help                                               | pip help                                 | gem help                       |
