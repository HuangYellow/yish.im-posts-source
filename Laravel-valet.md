title: "Laravel Valet 安裝與設定"
date: 2016-05-06 17:24:56
tags: [laravel,valet]
categories: Laravel
---
Laravel 最近發佈 valet，跟 homestead 最大的不同是 homestead 是一整個虛擬映像檔，而 valet 是基於本地的開發環境，開發人員可以依據自己的需求選擇自己需要的開發環境加速開發，詳細說明可以參考[官方網站](https://laravel.com/docs/5.2/valet)。

<!--more-->

以下將會 step by step 進行安裝與設定：

必要項目：
* composer
* homebrew

## Composer

[官方網站](https://getcomposer.org/download/)

``` bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '92102166af5abdb03f49ce52a40591073a7b859a86e8ff13338cf7db58a19f7844fbc0bb79b2773bf30791e935dbd938') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

綁定 composer 指令
``` bash
$ mv composer.phar /usr/local/bin/composer
```

.bash_profile PATH 綁定
``` bash
export PATH="$PATH:$HOME/.composer/vendor/bin"
```

## Homebrew

[官方網站](http://brew.sh/)

``` bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
好了之後先 update
``` bash
$ brew update
```

<div class="tip">
    特例問題
    ``` bash
    homebrew cannot create directory at 'etc/bash_completion.d': Permission denied
    ```
</div>

具體解決方案是修改權限：
``` bash
$ sudo chown <username> /usr/local/etc
```

## Valet

確認 brew service 運作正常
``` bash
$ brew services list
```

#### 安裝 php 7
```
$ brew install php70
//這邊由於 php70 開頭套件過多，他會詢問，這邊選擇 homebrew/php/php70
```
詳細可以參考[這個](https://github.com/Homebrew/homebrew-php)

#### 安裝 MariaDB or Mysql
``` bash
$ brew install mariadb
```
接著啟動服務
``` bash
$ brew services start mariadb
```

#### 安裝 valet

建立全域 valet 指令：
``` bash
$ composer global require laravel/valet
```

安裝：
``` bash
$ valet install
```

#### 檢查是否安裝成功
``` bash
ping foobar.dev
```

#### 建立服務

建立 mapping dictionary
``` bash
$ mkdir ~/Sites
```

進入 Sites
``` bash
$ cd ~/Sites
```

執行 park
``` bash
$ valet park
```

### 建立 laravel 專案
``` bash
$ laravel new blog
```
如果沒有 laravel 這個指令可以參考[這裡](https://laravel.com/docs/5.2/installation)

或者可以輸入指令:
``` bash
$ composer global require "laravel/installer"
```
### 拜訪建立的專案
```
    http://blog.dev
```

That's it.

