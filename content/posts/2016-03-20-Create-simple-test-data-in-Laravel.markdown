---
layout: post
title:  "Create simple test data in Laravel"
date:   2016-03-20
categories: ['web development']
tags: ['laravel']
---

#### 创建一个新的模型类 Todo

`$ php artisan make:model Todo -m`

#### 在 *xxx_create_todos_table.php* 里创建表结构

```php
$table->increments('id');
$table->text('item');
$table->boolean('completed')->default(0);
$table->timestamps();
```

#### 数据库迁移

`$ php artisan migrate`

#### 在 *ModelFactory.php* 里定义 Todo

```php
$factory->define(App\Todo::class, function (Faker\Generator $faker) {
  return [
    'item' => $faker->paragraph
  ];
});
```

#### 插入数据

`$ php artisan tinker`

`$ factory(App\Todo::class, 20)->create()`

#### 在 *routes.php* 里注册路由

```php
Route::get('/api/todos', function () {
  return App\Todo::paginate(10);
});

Route::delete('/api/todos/{id}', function ($id) {
  App\Todo::findOrFail($id)->delete();
});

Route::post('/api/todos', function () {
  $todo = new App\Todo;
  $todo->item = request()->item;
  $todo->save();
});

Route::put('/api/todos/{id}', function ($id) {
  $todo = App\Todo::find($id);
  $todo->item = request()->item;
  $todo->save();
});
```

see also: [Available Column Types](https://laravel.com/docs/5.1/migrations#creating-columns), [Faker](https://github.com/fzaninotto/Faker)
