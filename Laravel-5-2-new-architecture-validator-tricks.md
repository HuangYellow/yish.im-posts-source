title: "Laravel 5.2 專案結構心得(十): Validator 小技巧"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-14 23:20:59
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---

想像 Laravel 的驗證 rules 一樣，輸入特定字就會進行驗證。

<!--more-->

``` php
    return [
        'title' => 'max:100',
        'tags' => 'tags:5',
    ];
```
這樣看起來棒多了，更好一點的還可以這樣做：將數量提取到 config 設定。

``` php
    return [
        'title' => 'max:100',
        'tags' => 'tags:' . config('tags.article.limit'),
    ];
```

``` php
    //規則制定
    public function rules()
    {
        return [
            'title' => 'required|unique:articles|max:100',
        ];
    }

    //改寫驗證訊息
    public function messages()
    {
        return [
            'title.required' => config('article.validation.title.required'),
        ];
    }
```

``` php
    //validate tags.
    app('validator')->extend('tags', function ($attribute, $value, $parameters, $validator) {
        return app(TagValidator::class)->limit($value, $parameters);
    });
```
# BUT !
自訂驗證的時候為什麼像是 max:100 他的參數可以 assign 到 messages 裡面而我的不行呢？

>因為你必須 replace 在 message 裡面寫的 :tags

``` php
    app('validator')->replacer('tags', function ($message, $attribute, $rule, $parameters) {
        return str_replace(':tags', array_shift($parameters), $message);
    });
```

訊息複寫 :

``` php
    public function messages()
    {
        return [
            'tags.tags' => '標籤限制 :tags 個！',
        ];
    }
```