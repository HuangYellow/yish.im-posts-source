title: PHP7 on Homestead nginx 問題
date: 2016-01-04 21:34:25
tags: [laravel,homestead]
categories: Laravel
---

新版本的 Homestead v0.4.0 近期已經發佈，這個版本最大的更動就是將 PHP 升級至 7，而在這當中遇到了一個關於 nginx 的錯誤，還好只需要修正路徑即可。

<!-- more -->

引發錯誤的原因是在於當你在 Homestead.yaml 新建站台後，輸入 `homestead up --provision` 它會幫你對應以及 enabled site，但在 enabled 時還是去呼叫 php5-fpm。

所以在新建站台後，我得到了 `Bad Gateway 502`，找了一些文件後發現原來是這個問題，加以修正後就可以正常運行了。

``` bash
    $ sudo nano /etc/nginx/sites-enabled/專案Domain

    //change line fastcgi_pass for:
    $ fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;

    $ sudo service nginx restart
    $ sudo service php7.0-fpm reload
```

[參考網址](http://stackoverflow.com/questions/34473185/502-bad-gateway-nginx-1-9-7-in-homestead-laravel-5)