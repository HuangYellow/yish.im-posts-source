title: "Laravel-5-Generators-Extended"
date: 2015-07-21 11:48:02
tags: [Laravel]
categories: Laravel
---
>在laravel4.2的時候我非常依賴這個套件，原因是laravel artisan的指令不支援建立model, scafford等等，但5.1的時候已經支援了，相比之下generator就顯得可有可無了，但還是提供了幾個指令可以使用。

[github](https://github.com/laracasts/Laravel-5-Generators-Extended)

```
$ composer require laracasts/generators
```

L5 includes a bunch of generators out of the box, so this package only needs to add a few things, like:

```
* make:migration:schema
* make:migration:pivot
* make:seed
```
