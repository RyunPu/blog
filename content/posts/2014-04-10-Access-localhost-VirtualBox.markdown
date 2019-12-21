---
layout: post
title:  "Access localhost from VirtualBox"
date:   2014-04-10
categories: ['mac']
tags: ['mac']
---

just follow the steps:

* In VirtualBox > Preferences > Network, set up a host-only network

* Activate the 2nd adapter and set it with Host-only Adapter and the only Name attribute we just created like 'vboxnet0'

* In C:\WINDOWS\system32\drivers\etc, you may need to use this configuration for convenience

```
196.168.56.1    localhost
```

note: if you are using [gruntjs](http://gruntjs.com/), you may need to change the 'hostname' to '0.0.0.0'

see more: [justinmarsan](http://www.justinmarsan.com/blog/hacks/2012/11/15/mac-osx-virtualbox-windows-localhost-mamp/)
