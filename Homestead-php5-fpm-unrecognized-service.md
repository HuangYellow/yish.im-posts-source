title: 'Homestead: php5-fpm: unrecognized service 解決方案'
date: 2016-03-01 00:43:22
tags: [laravel,homestead]
categories: Laravel
keywords:
- homestead
- laravel
clearReading: true
thumbnailImage: thumbnail.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
coverImage: cover.png
coverMeta: in
coverSize: partial
---
這個錯誤引發的原因是因為在先前 Homestead 2.x 時你有安裝過了，而目前 laravel/homestead 已經更新至 3.x 但由於 global 版本號還是停留在 2.x 導致執行時還是把 nginx 的 fpm 設定寫入 php5-fpm。

<!--more-->

[解決問題關鍵](http://laravel.io/forum/01-24-2016-solved-homestead-php5-fpm-unrecognized-service)

這位大大也遇到同樣的問題，而他發現了是因為他曾經安裝過 laravel/homestead global 舊版本，而只更新 box 的版本 0.4.1 導致於所有專案都無法啟動與執行，先前的作法是去修改 nginx 設定，但這不太對，而具體的解決方案是去更新 global 的 laravel/homestead。

移除先前的 laravel/homestead:
``` bash
    $ sudo composer global remove laravel/homestead
```
接著安裝新版本:
``` bash
    $ sudo composer global require laravel/homestead
```

接著到 Homstead 資料夾下執行 `vagrant up` 一切就正常了，而 php 版本也正式來到 7(歡呼)。

如果需要綁定指令或區別，可以參考[官方說明](https://laravel.tw/docs/5.2/homestead)。