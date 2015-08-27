title: "Laravel Artisan"
date: 2015-03-22 16:56:21
tags: [Laravel,Artisan]
categories: Laravel
---

>[官方說明](http://laravel.tw/docs/4.2/artisan)

##推薦套件
* [Laravel Generator](https://github.com/JeffreyWay/Laravel-4-Generators)
* [從原始碼產生編輯器語法補完檔](https://github.com/barryvdh/laravel-ide-helper)
* [產生資料庫假資料使用](https://github.com/fzaninotto/Faker)

##基本操作指令
重新設定:
``` bash
    php artisan migrate:reset
```
執行:
``` bash
    php artisan migrate
```
安裝migration：
``` bash
    php artisan migrate:install(用於資料庫創見後第一次使用migration，但執行也會自動建立，因此可不用)
```
初始:
``` bash
    php artisan migrate:rollback
```
資料填充:
``` bash
    php artisan db:seed
```

http://laravel.tw/docs/4.2/migrations

##資料表建立與資料填充
建立可遷移檔案:
``` bash
    php artisan migrate:make create_users_table
```

[新增欄位](http://laravel.tw/docs/4.2/schema#adding-columns)

[資料填充](http://laravel.tw/docs/4.2/migrations#database-seeding)

##補充說明
schema:interger 的不支援長度屬性，預設會下Mysql的預設最大長度見[link](http://dev.mysql.com/doc/refman/5.1/en/integer-types.html)