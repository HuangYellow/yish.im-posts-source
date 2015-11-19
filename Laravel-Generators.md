title: "Laravel Generators"
date: 2015-03-22 16:52:06
tags: laravel
categories: Laravel
---

Genertors是一套程式產生器，透過指令的狀態下快速產生對應文件，是由laracasts.com的Jeffery所開發的套件。

<!-- more -->

[Github](https://github.com/JeffreyWay/Laravel-4-Generators) / Laravel 4

[Github](https://github.com/laracasts/Laravel-5-Generators-Extended) / Laravel 5

## 安裝
`composer.json`
``` json
    "require-dev": {
        "way/generators": "~2.0"
    }
```
## 設定
``` bash
    composer update --dev
```

`app.php`
``` php
'Way\Generators\GeneratorsServiceProvider'
```

## 指令參照
* generate:model
* generate:view
* generate:controller
* generate:seed 建立seed檔，並建立faker
* generate:migration 建立schema檔案，可給參數自定義建立欄位
* generate:pivot 未知，好像和資料表有關
* generate:resource 自動建立所有對應MVC，不包含程式
* generate:scaffold 起手架，會自動建立所有對應MVC含基礎程式，加migrations & seeds （Router需自行定義）

>先前版本使用scafford會自動建立views，但作者jeffery認為自動生成後大部分的user還是會將原有表單刪除，索性將自動生成view內容的功能移除，詳情請看[issues](https://github.com/JeffreyWay/Laravel-4-Generators/issues/314)