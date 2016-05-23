title: "Laravel Socialite"
date: 2016-05-23 14:20:05
tags: [laravel]
categories: Laravel
---
由 Taylor 開發的 OAuth 套件，支援 Facebook, Twitter, Google, LinkedIn, GitHub and Bitbucket。

<!--more-->

[Github](https://github.com/laravel/socialite)

# 安裝 & 設定
``` php
$ composer require laravel/socialite
```
``` php
'providers' => [
    // Other service providers...

    Laravel\Socialite\SocialiteServiceProvider::class,
],

'Socialite' => Laravel\Socialite\Facades\Socialite::class,
```

## facebook
在 `app/services.php` 新建屬於 facebook 的 key
``` php
    'facebook' => [
        'client_id' => 'app_id',
        'client_secret' => 'app_secret',
        'redirect' => 'callback 的 url',
    ],
```

## Twitter
``` php
    'twitter' => [
        'client_id' => 'API Key',
        'client_secret' => 'API Secret',
        'redirect' => 'callback 的 url',
    ],
```

# 範例
Facebook
設定一個 link "login via facebook"
``` php
//AuthController@loginFromFacebook
return Socialite::driver('facebook')->redirect();
```
callback 的 method
``` php
//AuthController@callbackFacebook
$user = Socialite::driver('facebook')->user(); //得到 facebook 資料
```
這邊可以 dd() 檢查資料是否有得到。

Twitter
設定一個 link "login via Twitter"
``` php
//AuthController@loginFromTwitter
return Socialite::driver('twitter')->redirect();
```
callback 的 method
``` php
//AuthController@callbackTwitter
$user = Socialite::driver('twitter')->user(); //得到 twitter 資料
```
這邊必須注意，Twitter 帳號是需要電話綁定的，詳細可以到 [TwitterApp](https://apps.twitter.com/) 設定。






