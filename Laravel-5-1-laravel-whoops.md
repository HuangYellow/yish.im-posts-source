title: "Laravel 5.1 laravel-whoops"
date: 2015-07-21 11:38:56
tags: Laravel
categories: Laravel
---
laravel 5 之後移除了whoops套件，所幸的是可以透過大神寫好的package把他裝載回來。

<!-- more -->

[github](https://github.com/guidovanbiemen/laravel-whoops)

## 安裝
``` bash
$ sudo composer require guidovanbiemen/laravel-whoops
```

## 設定

config/app.php

跟先前版本一樣，必須掛入providers，這邊建議在上面打上一些註解，例如

``` php
/*
 * laravel-whoops Service Providers...
 */
'Gvb\Whoops\ServiceProvider',

bootstrapp/app.php

$app->singleton(
    'Illuminate\Contracts\Debug\ExceptionHandler',
    'Gvb\Whoops\ExceptionHandler'
);
```

that's it.
接下來就可以看到熟悉的whoops畫面了。
