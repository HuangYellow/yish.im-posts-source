title: "Laravel Environment"
date: 2015-03-22 16:58:50
tags: laravel
categories: Laravel
---

在開發專案時會遇到一種狀況，就是要production時必須修改很多的地方與設定，而且還要考慮與設定權限來屏蔽掉敏感資訊，但laravel已經提供了相當方便的方式可以讓開發者快速建立各個不同環境的設定以快速部署程式。

<!-- more -->

[官方說明](http://laravel.tw/docs/4.2/configuration)

`bootstrap/start.php`
``` php
$env = $app->detectEnvironment(array(
            //'{環境名稱}' => array( '{主機名稱1}' , '{主機名稱2}' ),
            'docker' => array('docker_hostname'),
));
```

>在命令列輸入`hostname`可查看當前主機名稱

>注意：請勿使用「testing」當作環境名稱，它是專門為單元測試保留的。

## 建立環境敏感檔案
在專案目錄底下建立`.env.{環境名稱}.php，一般而言與 composer.json 檔案同目錄。

example:
`.env.local.php`
``` php
return array(
        'mysql' => array(
            'host'      => 'localhost',
            'database'  => 'member_center',
            'username'  => 'homestead',
            'password'  => 'secret',
        ),
);
```

建立敏感檔案後，修改原有設定來讀取全域環境變數。

`/app/config/database.php`
``` php
'mysql' => array(
            'driver'    => 'mysql',
            'host'      => $_ENV['mysql.host'],
            'database'  => $_ENV['mysql.database'],
            'username'  => $_ENV['mysql.username'],
            'password'  => $_ENV['mysql.password'],
            'charset'   => 'utf8',
            'collation' => 'utf8_general_ci',
            'prefix'    => '',
        ),
```

## 補充說明
1. 得到目前環境名稱：
``` bash
    echo App::environment();
    php artisan env
```

2. 預設環境為production,但該環境的隱藏設定檔請取名為 .env.php

>如果該主機名稱並沒有對應的環境名稱，就會被設為production