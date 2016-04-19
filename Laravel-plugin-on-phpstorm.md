title: "Laravel Plugin on PHPStorm"
date: 2015-11-09 12:03:23
tags: laravel
categories: Laravel
---
![phpstorm10](http://i.imgur.com/GqdCs6V.png?1)
這個套件可以幫助你快速對應到相對應的route, view, provider，非常強大。

<!-- more -->

[jetbrains plugin](https://plugins.jetbrains.com/plugin/7532)
[github](https://github.com/Haehnchen/idea-php-laravel-plugin)

## 前置
* 需具備[laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)

你可以透過安裝provider的方式進行安裝，或者可以直接wget generated好的檔案。

``` bash
$ wget https://gist.githubusercontent.com/barryvdh/5227822/raw/811f21a14875887635bb3733aef32da51fa0501e/_ide_helper.php
```

## 安裝
* 開啟PHPStorm

### Ubuntu
``` bash
Settings > Plugins > Browse Repositories
```
### Mac
``` bash
Preferences > Plugins > Browse Repositories
```

* 搜尋`Laravel Plugin` 安裝

* 重新啟動PHPStorm


## 啟用
### Ubuntu
``` bash
Settings > Other Settings > Laravel Plugin > Enable plugin for this project
```
### Mac
``` bash
Preferences > Other Settings > Laravel Plugin > Enable plugin for this project
```

接下來就可以使用這強大的套件功能了。

官網示意圖：
![demo](https://camo.githubusercontent.com/8531a9773fb4d15033317827b8ec2d6c8d233489/687474703a2f2f706c7567696e732e6a6574627261696e732e636f6d2f66696c65732f373533322f73637265656e73686f745f31343637302e706e67)

