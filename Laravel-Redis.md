title: "Laravel Redis"
date: 2015-03-22 16:25:09
tags: [Laravel,Redis]
categories: Laravel
---

>在laravel配置中其實很多東西已經配置好了，需要做的就僅僅是改變一些設定。
以下是配置redis or memcached
基本上這兩套是目前用於存cache & session最主流的做法
原則就上就redis or memcached + mysql

>安裝redis or memcached這部分就跳過了，基本上是不會有問題產生。

以下以redis為例，memcached也是一樣的做法。

## 設定
cache
`app/config/cache.php`
``` php
'driver' => 'file',
```
修改為
``` php
'driver' => 'redis',
```

就這樣，相當簡單吧。
以此類推

session
`app/config/session.php`
``` php
'driver' => 'file',
```
修改為
``` php
'driver' => 'redis',
```

## 補充
當然在laravel當中也提供了一些設定，如果是希望用專屬的cache or session做一台主機，主要資料存在另一台，下面也提供了幾個設定
分別在

`app/config/cahce.php`
`app/config/database.php`

thats it.