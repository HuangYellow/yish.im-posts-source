title: "SublimeCodeIntel + laravel IDE helper on sublime text 3"
date: 2015-07-16 17:50:52
tags: [laravel,sublime]
categories: Sublime
---
使用laravel IDE helper能快速在sublime coding當中知道內建laravel method，相當於內部語法提示。

<!-- more -->

## Required
[Package_control](http://yish.im/2015/03/22/Sublime-text-3-on-Ubuntu/#Package_control)

## SublimeCodeIntel

[Github](https://github.com/SublimeCodeIntel/SublimeCodeIntel)

``` bash
Package control > Install package > SublimeCodeIntel
```

[關於快捷鍵](https://github.com/SublimeCodeIntel/SublimeCodeIntel#using)

### 引發的錯誤解決方法

當我安裝好上述之後，我發現我還是無法使用(ubuntu)，看了一下console是說

>Could not import subprocess32 module, falling back to subprocess module

根據官方github上面說道：[說明](https://github.com/SublimeCodeIntel/SublimeCodeIntel#using)

[official](https://github.com/SublimeCodeIntel/SublimeCodeIntel#notes)

*For the next major version of SublimeCodeIntel (v3.0.0) you will have to ensure that CodeIntel package (https://pypi.python.org/pypi/CodeIntel) is installed on your system usually by using pip or easy_install. The Code intelligence will be handled by that package and the command codeintel it will install.*

*Please start trying to install the CodeIntel package as soon as possible to make sure you are ready for the upcoming version of SublimeCodeIntel:*

1. *Install Python 2 and pip (http://www.pip-installer.org/en/latest/installing.html).*
2. *Install (or upgrade) CodeIntel by typing the following in a terminal: pip install -U codeintel*

作者意思是如果是*SublimeCodeIntel (v3.0.0)*必須要具備 pyhon 2 and pyhon-pip這個指令：

``` bash
$ sudo apt-get install python-pip
```
``` bash
$ sudo pip install -U codeintel
```

再度遇到一些錯誤，是說我gcc庫無法載入的問題，結果發現大部分用ubuntu的人都會有此問題，應該是內建的pyhon版本太舊所導致：[ref](http://stackoverflow.com/questions/11094718/error-command-gcc-failed-with-exit-status-1-while-installing-eventlet)

*Your install is failing because you don't have the python development headers installed. You can do this through apt on ubuntu/debian with:*

``` bash
$ sudo apt-get install python-dev
```

*for python3 use:*

``` bash
$ sudo apt-get install python3-dev
```

*For eventlet you might also need the libevent libraries installed so if you get an error talking about that you can install libevent with:*

``` bash
$ sudo apt-get install libevent-dev
```

## laravel IDE helper

[Github](https://github.com/barryvdh/laravel-ide-helper)

``` bash
$ sudo composer require barryvdh/laravel-ide-helper
```

config/app.php
providers

``` php
Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```

接下來輸入產生ide helper檔案

``` php
$ php artisan ide-helper:generate
```

That's it.

## Ctags & SublimeCodeIntel 差異
[ref](http://cloudbbs.org/forum.php?mod=viewthread&tid=3620)

*安装sublimecodeintel后， 按alt+鼠标左键也能和ctags一样跳转到函数声明的地方。 但是如果有两个文件声明了同样名称的函数， sublimecodeintel只会跳转到第一个找到的函数， 而ctags会让你选择要跳转到哪个文件。所以我们一般还是用ctags的跳转功能。*

此外其實在sublime text 3當中已經有內建的Go To difinition，也可以多加利用（但還是喜歡Ctags的快速）。
