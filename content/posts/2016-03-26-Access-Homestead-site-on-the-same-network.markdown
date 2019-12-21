---
layout: post
title:  "Access Homestead site on the same network"
date:   2016-03-26
categories: ['web development']
tags: ['tool']
---

#### Add the following line to your hosts

```
192.168.1.2    192.168.10.10
```

`192.168.1.2` should be your network cards IP address

#### Change the project's nginx site config

```
sudo vi /etc/nginx/sites-enabled/homestead.app
```

change

```
listen 80
```

to

```
listen 80 default_server
```

#### Once done all you need to do is

```
sudo service nginx reload
```

Now you can access the site from `192.168.1.2:8000`
