---
layout: post
title:  "Commonly used Laravel commands"
date:   2016-03-19
categories: ['web development']
tags: ['laravel']
---

#### ```$ composer install```

如果我们需要使用第三方 package，如集成用户权限组，则要运行此命令更新 package 包

#### ```$ php artisan migrate```

如果我们新增了数据表或数据字段，则需要运行此命令

#### ```$ php artisan db:seed```

如果我们新增了数据表，但是没有生成对应的测试数据，可以运行此命令

#### ```$ php artisan migrate:refresh --seed```

初始化数据库

#### ```$ php artisan view:clear```

有时候更新代码，会出现模板缓存没更新的情况，运行此命令即可更新模板缓存

#### ```$ php artisan cache:clear```

有时候更新代码，会出现数据缓存 (memcache/redis) 没更新的情况，运行此命令即可更新数据缓存

#### ```$ php artisan key:generate```

生成应用的 key（会覆盖）

#### My alias

```
alias ci='composer install'
alias pam='php artisan migrate'
alias pads='php artisan db:seed'
alias pams='php artisan migrate:refresh --seed'
alias pavc='php artisan view:clear'
alias pacc='php artisan cache:clear'
alias pakg='php artisan key:generate'
```
