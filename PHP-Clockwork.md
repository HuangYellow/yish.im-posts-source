title: "PHP-Clockwork"
date: 2015-03-22 14:28:59
tags: [Laravel,PHP]
categories: PHP
---

>Javascript開發者可以利用chrome當中的開發工具列進行效能與除錯等功能，PHP有額外套件也可以做到這樣子的功能 - Clockwork！

[google chrome套件 - Clockwork](https://chrome.google.com/webstore/detail/clockwork/dmggabnehkmmfmdffgajcflpdjlnoemp?hl=en)

加入到chrome後按下F12就可以看到新增了一個tabs，到這邊其實傳統的PHP就可以開始作業了，但由於我用的是Laravel 4.2，因此需要進行額外的composer包安裝。

[github](https://github.com/itsgoingd/clockwork)


>This extension provides out of the box support for Laravel, Slim 2 and CodeIgniter 2.1 frameworks, you can add support for any other or custom framework via an extensible API.


*如果是開發web app則使用以下包
[embeddable web app version of Clockwork](http://github.com/itsgoingd/clockwork-web)

## 安裝
composer.json
``` bash
"itsgoingd/clockwork": "~1.6"
```

## 設定
以下都是以laravel環境進行，雖然說laravel其實有個介面更好的[laravel-debugbar](https://github.com/barryvdh/laravel-debugbar)，但還是需要預防萬一...。

這邊建議自己獨立出app.php，利用`append_config`進行加入開發工具。
`app/config/app.php`
``` php
'Clockwork\Support\Laravel\ClockworkServiceProvider',
```
這個套件必須運作於debug的環境下，透過下面的命列列將相關設定放入你的`config`

``` bash
php artisan config:publish itsgoingd/clockwork --path vendor/itsgoingd/clockwork/Clockwork/Support/Laravel/config/
```

`app/config/app.php`
``` php
'Clockwork' => 'Clockwork\Support\Laravel\Facade',
```

Ok,可以運作了，很簡單吧。


## 範例
``` php
    Clockwork::startEvent('finduser', 'find user email.'); //事件開始
    $user = User::find(1);
    Clockwork::info($user->email);
    Clockwork::endEvent('finduser');
```

接著在工具列中就會看到一些相關的資料，這將會讓開發時不確定因素降到最低（因為可以即時知道哪邊效能或queries有問題，相當方便）。