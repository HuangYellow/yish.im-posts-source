title: "Laravel 5.2 專案結構心得(九): Request"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-14 22:55:59
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---

在真正執行 method 前所作的請求處理，這邊通常會放上表單驗證。

<!--more-->

``` bash
    $ artisan make:request Name
```

情境 : 建立文章和客製化驗證失敗的訊息以及桌機與手機回傳的內容。

``` php
    //規則制定
    public function rules()
    {
        return [
            'subject' => 'required|unique:articles|max:100',
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

可以覆寫 response method 讓手機版返回 json 格式。

``` php
    public function response(array $errors)
    {
        if (is_mobile()) {
            foreach ($errors as $error) {
                //validate_failed 是自己寫的 helper 不是內建的
                return validate_failed($error);
            }
        }

        return parent::response($errors);
    }
```