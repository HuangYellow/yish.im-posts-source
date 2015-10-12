title: "Laravel debugbar"
date: 2015-03-22 16:48:41
tags: [Laravel]
categories: Laravel
---

>先前介紹[Clockwork](http://mombuyish.github.io/php/2015/03/13/Clockwork/)這套通用的PHP debug套件，接下來來介紹一下專屬for laravel的debugbar


[Github](https://github.com/barryvdh/laravel-debugbar)

>laravel 4 / 5 support!

## 安裝
    composer require barryvdh/laravel-debugbar

## 設定
`app.php`
``` php
'Barryvdh\Debugbar\ServiceProvider',
'Debugbar' => 'Barryvdh\Debugbar\Facade',
```
接著產生相關`config`

``` bash
    php artisan vendor:publish
```

還有些細節調整在官方的repo上都可以看到，可依據需求做調整，這個工具可以加快開發速度而且可以提前知道自己寫的code是否有效能以及其他問題，相當方便。