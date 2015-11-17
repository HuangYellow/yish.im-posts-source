title: "php-cs-fixer with sublime text 3"
date: 2015-06-12 00:15:07
tags: [PHP,Sublime]
categories: Sublime
---

程式有既定的規範讓co-work和程式的可閱讀性大幅提升，也讓維護起來比較輕鬆。
PHP目前有PSR的規範，也有一套不錯的工具可以幫助自動化規範 PHP-CS-Fixer
先前介紹的是利用composer進行安裝php-cs-fixer的做法，但有個問題就是我想要在sublime裡面直接進行psr規格化，剛好看到laracasts有說到這部分就實作出來。

<!-- more -->

[php-cs-fixer @ composer](http://yish.im/2015/03/22/PHP-cs-fixer/)

[laracasts](https://laracasts.com/series/whats-new-in-laravel-5-1/episodes/1)

## Installation

>必要安裝`curl`

[PHP-cs-fixer Github](https://github.com/FriendsOfPHP/PHP-CS-Fixer)

## phar
有curl
``` bash
    curl http://get.sensiolabs.org/php-cs-fixer.phar -o php-cs-fixer
```
無curl
``` bash
    wget http://get.sensiolabs.org/php-cs-fixer.phar -O php-cs-fixer
```

移動php-cs-fixer到全域變數
``` bash
    sudo mv php-cs-fixer /usr/local/bin/php-cs-fixer
```
更改讀取權限
``` bash
    sudo chmod 777 php-cs-fixer
```

重新啟動terminal

## Sublime settings
* Tools -> Build System -> New Build System
* 建立PHP.sublime-build
指定shell_cmd
``` bash
{
    "shell_cmd": "php-cs-fixer fix $file --level=psr2"
}
```
* Done

## 操作
>當寫好一段程式時，按下預設的快捷鍵`ctrl` + `b`，就會自動幫你把程式修正成psr-2的格式了。

或者你可以用點選的方式Tools->Build



