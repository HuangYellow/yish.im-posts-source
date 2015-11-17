title: "Laravel reCaptcha"
date: 2015-03-22 17:10:13
tags: [Laravel,reCaptcha]
categories: Laravel
---
![reCaptcha](http://i.imgur.com/xa6mIaZ.gif)
最近google提供了RECAPTCHA新版本，比原先的recaptcha好用太多了，雖說在測試階段一旦測試太多次他還是會要求輸入驗證碼，但第一次打開時他會顯示一個很複雜的驗證碼，刷新後就會是很簡單的英文字，用起來真的不錯，於是就想辦法用於新的laravel專案上。

<!-- more -->

原先是自己把recaptchalib.php放到自訂的libraries，再經由各項設定來到app/config/recaptcha當中，但後來發現有提供recaptcha for laravel4，而且還可以切換版本！不多說就直接加入了，以下是加入的步驟跟一個簡單的範例。

[Github](https://github.com/greggilbert/recaptcha)

如果是Laravel 4請使用 1.1.x版本
`composer.json`
``` bash
"greggilbert/recaptcha": "1.1.5"
```

Laravel 5 則使用 2.0.x
``` bash
"greggilbert/recaptcha": "2.0.1"
```

``` bash
composer update
```

## 用法
`composer update`之後，接著就可以很簡單的使用這個驗證了。
首先要到[google recaptcha](https://www.google.com/recaptcha/intro/index.html)弄一個key，並且綁定域名，這邊可以綁定一個local的域名，並不僅限於一定要online的域名，如我使用homestead時我設定了homestead.app作為我的域名，這也是可以的。

`app/config/app.php`
``` php
'Greggilbert\Recaptcha\RecaptchaServiceProvider',
```

將`config`檔案放置`/config/packages/`方便設定
``` bash
php artisan config:publish greggilbert/recaptcha
```
``` bash
app/config/packages/greggilbert/recaptcha/config.php
```
    輸入site key, secret key

當然也可以自訂一些錯誤訊息...
`app/lang/[lang]/validation.php`
``` php
"recaptcha" => 'The :attribute field is not correct.',
```

在view/form使用方式相當簡單，如下：
``` php
Form::captcha()
```

在controller的validation時則僅需這樣使用：
``` php
$rules = ['g-recaptcha-response' => 'required|recaptcha']
```

相當的簡單好用，以上範例適用於Laravel 4，Laravel 5的話可能要過陣子使用時再補上心得。