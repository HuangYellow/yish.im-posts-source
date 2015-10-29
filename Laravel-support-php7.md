title: "Homestead 現在支援PHP 7了"
date: 2015-10-29 14:22:33
tags: [Laravel-news]
categories: [Laravel-news]
---

譯者：Yish

![homestead](http://i.imgur.com/CxQCsIB.png)

Laravel Homestead 本月迎來新的更新：支援PHP 7。

如果你已經在使用 PHP 5.x 的 Homestead box，你可以透過克隆 laravel/homestead 資源庫 php-7 的分支來進行升級。（在新的資料夾內）：

``` php
git clone -b php-7 https://github.com/laravel/homestead.git Homestead
```

接下來將直接將 box 加入到已存在的 `Homestead.yaml` 的上面：
``` php
box: laravel/homestead-7
```

最後，你可以在有包含 laravel/homestead 資源庫的底下執行 `vagrant up` 這個指令。

如果你需要更多訊息可以前往[官方手冊](http://laravel.com/docs/5.1/homestead#upgrading-to-php-7)或者查看 Laracasts的[PHP 7](https://laravel-news.com/2015/08/videos-to-learn-about-php-7/) 影片系列教學。

[原文地址](https://laravel-news.com/2015/10/homestead-now-with-php-7-support/)