title: "自動化測試 in PHP with Gulp, Node"
date: 2015-09-24 15:26:50
tags: [PHP,Testing]
categories: Laravel
---
本地端開發時會寫測試，但每次都必須要執行 phpUnit這個指令，工程師都是懶惰的..XD。幸運的是步驟沒有很複雜，只要安裝並設定就可以進行存檔後程式會自己跑測試，並且跟你說明測試有無通過。

<!-- more -->

## 本地端環境建立

### 依賴組件
* phpUnit
* node
* npm
* gulp


### PHPUnit 依賴套件

移到專案資料夾中，確定 vendor 中已掛入 phpunit
``` bash
$ ./vendor/bin/phpunit
```

### 安裝 nodejs

#### Ubuntu
>在ubuntu底下node已被佔用，需要額外加上nodejs的ppa解決。

``` bash
// 由於 node 已被佔用，需要另加 nodejs 的 ppa 解決
$ sudo add-apt-repository ppa:chris-lea/node.js
// 安裝
$ sudo apt-get install nodejs

// 如果原本有安裝 node 可能會衝突，移除相關指令
$ sudo apt-get autoremove node

// 確認安裝成功與版本好
$ nodejs -v
v0.10.37

// 如找不到 node 指令
$ sudo ln -s /usr/bin/nodejs /usr/bin/node
```

>Mac的用戶理論不會遇到這個問題，不過還是建議大家安裝[nvm Node Version Manager](https://github.com/creationix/nvm)

### 安裝 npm ( nodejs 的套件管理)

``` bash
$ sudo apt-get install npm
// 測試安裝成功
$ npm -v
1.4.28
```

### 安裝 global 環境的 Gulp

``` bash
$ sudo npm install -g gulp
```


## Laravel 5.1 專案相關套件安裝
移動到 Laravel 5.1 的專案資料夾安裝 gulp 和 laravel-elixir

``` bash
$ cd project-folder
```
確定 `package.json` 檔中有包含 `"laravel-elixir": "^3.0.0",` ，接下來開始安裝套件
``` bash
$ sudo npm install
```
試試寫在 `gulpfile.js` 中的預設值能不能正常運作

``` php
// Laravel 5.1 gulpfile.js 的預設值
    var elixir = require('laravel-elixir');
        elixir(function(mix) {
            mix.sass('app.scss');
    });
```

執行 `gulp` 的設定，右上有跑出通知代表成功！
``` bash
$ gulp
```

## 使用 laravel-elixir 在存檔時自動觸發 phpUnit
打開 `gulpfile.js`

``` php
// 將底下的 function 改寫為
    elixir(function(mix) {
        mix.phpUnit();
    });
```
存檔後在命令列上打 `gulp tdd` ，接下來試著去修改 php 或是 `tests` 中的檔案，開始自動化測試吧。


## 指令
``` bash
$ gulp tdd //運行gulpfile.js標籤有tdd的method(phpUnit, phpSpec)
$ gulp watch //監聽gulpfile.js所有的method
$ gulp //一樣是監聽所有method，但會先執行一次
$ gulp default //同上
```

實際上效果會是這樣子的：
[![auto](http://i.imgur.com/8FQzUkb.png)](https://youtu.be/R4X4Y_OTvA8_)

* [ref](https://laracasts.com/lessons/how-to-trigger-tests-on-save)

感謝JefferyWay和uh的幫助、鐵哥的TDD教學而誕生出這份筆記。