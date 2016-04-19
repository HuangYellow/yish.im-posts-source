title: "Laravel-5-Generators-Extended"
date: 2015-07-21 11:48:02
tags: laravel
categories: Laravel
---
在 laravel4.2 的時候我非常依賴這個套件，原因是 laravel artisan 的指令不支援建立 model, scafford 等等，但5.1的時候已經支援了，相比之下 generator 就顯得可有可無了，但還是提供了幾個指令可以使用。

<!-- more -->

[github](https://github.com/laracasts/Laravel-5-Generators-Extended)

``` bash
$ composer require laracasts/generators
```

L5 includes a bunch of generators out of the box, so this package only needs to add a few things, like:

``` bash
* make:migration:schema
* make:migration:pivot
* make:seed
```
