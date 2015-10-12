title: "PHP-cs-fixer"
date: 2015-03-22 16:27:39
tags: [PHP]
categories: PHP
---


>程式有既定的規範讓co-work和程式的可閱讀性大幅提升，也讓維護起來比較輕鬆。
PHP目前有PSR的規範，也有一套不錯的工具可以幫助自動化規範 `PHP-CS-Fixer`

[參考網址](https://phphub.org/topics/547)

[github](https://github.com/FriendsOfPHP/PHP-CS-Fixer)

## 安裝

確保`/.composer/vendor/bin`目錄在你的`$PATH`中
``` bash
export PATH=~/.composer/vendor/bin:$PATH
```

以下是composer已搬移至user底下可全區呼叫composer

``` bash
composer global require fabpot/php-cs-fixer
```

## 使用
/path/to/dir 專案目錄
當然，也可以指定檔案
/path/to/file 檔案
``` bash
php-cs-fixer fix /path/to/dir
php-cs-fixer fix /path/to/file
```

默認是使用psr-2的規範，當然也可以自己指定想要的規範
``` bash
php-cs-fixer fix /path/to/project --level=psr0
php-cs-fixer fix /path/to/project --level=psr1
php-cs-fixer fix /path/to/project --level=psr2
php-cs-fixer fix /path/to/project --level=symfony
```

詳細操作也可以參考官方的[readme](https://github.com/FriendsOfPHP/PHP-CS-Fixer)