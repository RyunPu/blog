---
layout: post
title:  "Enable directory listing in Nginx"
date:   2016-03-27
categories: ['web development']
tags: ['tool']
---

#### Open the `homestead.app` file

```bash
$ sudo vi /etc/nginx/sites-enabled/homestead.app
```

#### Add `autoindex on` in the location block

```
location / {
    autoindex on;
    autoindex_exact_size off;
    autoindex_localtime on;
    try_files $uri $uri/ /index.php?$query_string;
}
```

#### Restart Nginx

```bash
$ sudo service nginx reload
```
