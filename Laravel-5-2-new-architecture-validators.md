title: "Laravel 5.2 專案結構心得(六): Validators"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-14 22:43:59
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---

Validator 用來放置客製化的驗證條件，這會讓驗證機制看起來更加簡潔。

<!--more-->

情境 : 在某些情況下有些客製化驗證，像是驗證文章內有沒有禁止字元（例如廣告訊息）。

``` php
    public function validate($param = null)
    {
         //從 Repo 得到存在資料庫內的關鍵字
         $words = implode("|", $this->forbidden->getKeyWords()->toArray());

         //防止空資料時造成 preg_match 失敗而作的例外處理
         if (empty($words)) return true;

         //回傳是否通過驗證
         return boolval( ! preg_match("/{$words}/si", $param, $matches));
    }
```

這時候可以 extend validator ，也許可以選擇新建一個 ServiceProvider :
``` php
    //validate words.
    app('validator')->extend('forbiddenWords', function ($attribute, $value, $parameters, $validator) use ($request) {
                return app(ForbiddenValidator::class)->validate($request[$attribute]);
    });
```