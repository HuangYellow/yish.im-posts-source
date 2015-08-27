title: "Laravel 5.1 laravel-debugbar"
date: 2015-07-21 11:44:27
tags: [Laravel]
categories: Laravel
---
>跟laravel 4 一樣的debugbar，相當方便實用！

[github](https://github.com/barryvdh/laravel-debugbar)

##安裝
```
$ sudo composer require barryvdh/laravel-debugbar
```

##設定
config/app.php

```
'Barryvdh\Debugbar\ServiceProvider',

'Debugbar' => 'Barryvdh\Debugbar\Facade',
```

如果想要更彈性設置，可以將debugbar的config publish到config內
```
$ sudo php artisan vendor:publish
```

that's it.
