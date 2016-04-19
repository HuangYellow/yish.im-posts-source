<<<<<<< HEAD:Laravel-make-helper.md
title: "Laravel 自訂 Helper"
date: 2016-02-21 22:46:38
tags: laravel
categories: Laravel
---
有時候我們想寫一些 helpers 來輔助開發專案時使用， Laravel 本身提供很多的 [helpers](https://laravel.com/docs/5.2/helpers)，但有時候因應需求要加入自己的 helpers 該怎麼實作？

<!--more-->

Laravel 本身的 helpers 存在於 `Illuminate/Support/helpers.php`，如果要自己新建屬於專案的 helpers，可以依照下列步驟進行新建：

1. 到 composer.json autoload 檔案
``` php
    "autoload": {
        "files": [
            "app/Helpers/helpers.php"
        ]
    },
```
2. 到 app/Helpers/ 建立檔案 helpers.php

That's it.

舉例來說，我們常用的 markdown 解析就可以透過 helper 來快速應用：

``` php
if ( ! function_exists('markdown')) {
    function markdown($text = null)
    {
        return Markdown::convertToHtml($text);
    }
}
```

由於是全域方法，所以可以在任何地方進行呼叫，像是 blade：
``` php
    markdown($article->description)

=======
title: "Laravel 5.2 專案結構心得(二): Helpers"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-09 21:01:47
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---
有時候我們想寫一些 helpers 來輔助開發專案時使用， Laravel 本身提供很多的 [helpers](https://laravel.com/docs/5.2/helpers)，但有時候因應需求要加入自己的 helpers 該怎麼實作？

<!--more-->

Laravel 本身的 helpers 存在於 `Illuminate/Support/helpers.php`，如果要自己新建屬於專案的 helpers，可以依照下列步驟進行新建：

1. 到 composer.json autoload 檔案
``` php
    "autoload": {
        "files": [
            "app/Helpers/helpers.php"
        ]
    },
```
2. 到 app/Helpers/ 建立檔案 helpers.php

That's it.

舉例來說，我們常用的 markdown 解析就可以透過 helper 來快速應用：

``` php
if ( ! function_exists('markdown')) {
    function markdown($text = null)
    {
        return Markdown::convertToHtml($text);
    }
}
```

由於是全域方法，所以可以在任何地方進行呼叫，像是 blade：
``` php
    markdown($article->description)

>>>>>>> 32a9fe0b3618ac6cdf842361f24d0c29895499cc:Laravel-5-2-new-architecture-helpers.md
```