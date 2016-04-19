title: "將PHPUnit與自動化測試導入Laravel 4.2"
date: 2015-09-26 18:59:44
tags: [php,testing]
categories: Laravel
---
在Laravel4.2的專案中雖然Taylor已經幫我寫好了phpUnit，但是沒有將其預設掛載進來，所以我們必須自己手動將它加入（Laravel 5之後已經成為預先掛載），並且配合先前的測試推播來達到自動化測試的效果。

<!-- more -->

## Composer
導入phpUnit
``` bash
    $ sudo composer require phpunit/phpunit
```

## Node
依序安裝以下需求組件
``` bash
    $ sudo npm install -g gulp
    $ sudo npm install gulp-notify
    $ sudo npm install gulp-phpunit
```

或者你可以在根目錄下建立`package.json`，並貼上寫好的script
``` bash
{
  "private": true,
  "devDependencies": {
    "gulp": "^3.8.8"
  },
  "dependencies": {
    "gulp-notify": "^2.2.0",
    "gulp-phpunit": "^0.9.1"
  }
}
```
接著執行安裝指令
``` bash
    $ sudo npm install
```

## Gulp
在根目錄下新建`gulpfile.js`
``` js
var gulp    = require('gulp'),
    notify  = require('gulp-notify'),
    phpunit = require('gulp-phpunit');

gulp.task('phpunit', function() {
    var options = {debug: true, notify: true, stderr: true};
    gulp.src('app/tests/*.php')
        .pipe(phpunit('', options))
        .on('error', notify.onError({
            title: "Failed Tests!",
            message: "Error(s) occurred during testing..."
        }))
        .pipe(notify('done.'));
});

gulp.task('default', function(){
    gulp.run('phpunit');
    gulp.watch('app/**/*.php', function(){
        gulp.run('phpunit');
    });
});
```

接下來就可以透過指令達到監聽
``` bash
$ gulp
or
$ gulp default
```

that's it.

## Elixir
>本章節會將當前laravel 5的強大elixir掛入4.2的專案內

根目錄下建立`package.json`
``` bash
{
  "private": true,
  "devDependencies": {
    "gulp": "^3.8.8"
  },
  "dependencies": {
    "laravel-elixir": "^3.0.0"
  }
}
```

新建`gulpfile.js`
``` js
var elixir = require('laravel-elixir');

elixir(function(mix) {
    mix.phpUnit('./app/*.php');
});
```

由於在elixir內已經先寫好了幾個task，可以像先前的教學一樣有一些指令
``` bash
$ gulp tdd //運行gulpfile.js標籤有tdd的method(phpUnit, phpSpec)
$ gulp watch //監聽gulpfile.js所有的method
$ gulp //一樣是監聽所有method，但會先執行一次
$ gulp default //同上
```