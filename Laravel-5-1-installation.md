title: "Laravel 5.1 installation"
date: 2015-07-21 10:43:09
tags: laravel
categories: Laravel
---
最近開始在碰laravel 5.1，本篇是安裝的過程記錄，相信可以幫助剛入門的新人與剛從4.2升級過來的朋友。

<!-- more -->

## 環境建立

**Required = homestead 2.0**

[尚未安裝嗎？請點這裡安裝](http://yish.im/2015/03/22/Homestead-2-0-on-Ubuntu/)

確保已安裝laravel安裝包，如果沒有請使用composer安裝
``` bash
$ composer global require "laravel/installer=~1.1"
```

``` bash
$ laravel new laravel5
```

等待跑完後 會出現

``` bash
Crafting application...
> php artisan clear-compiled
> php artisan optimize
Generating optimized class loader
Compiling common classes
> php artisan key:generate
Application key [xxxxxxxxxxxxxxxxxxx] set successfully.
Application ready! Build something amazing.
```

That's it.

## 錯誤解決方案

引發原因是沒有自動建立.env檔，可以透過手動進行新增。

複製**Application key**到剪貼簿

開啟**.env.example**複製全部內容

建立**.env**貼上

將剛剛的Application key貼到APP_KEY

到本地端輸入

``` bash
$ homestead edit
```

## 加入新站台
``` bash
sites:
- map: laravel5.app
to: /home/vagrant/Code/laravel5/public
```

### 關閉homestead
``` bash
$ homestead halt
```

重新啟動homestead 並且provision
``` bash
$ homestead up --provision
```

拜訪http://laravel5.app (http://laravel5.app/)
如果出現以下畫面，恭喜你完成任務！
![laravel5.1](http://i.imgur.com/U69PqFC.png)

## 後續補充 2015.7.23
>上述的解決方案是以手動的方式進行，artisan提供了一個更便捷的指令，可以自動產生一組新的key並且自動寫入到.env當中。

產生key並且放入env檔案
``` bash
$ php artisan key:generate
```