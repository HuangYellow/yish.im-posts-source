title: "Laravel 5.2 專案結構心得(一): 專案命名與 Entities"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-02-25 00:02:42
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---
先前在開發專案時，一直對於 Laravel 結構做各種嘗試，現在有想出比較好的做法，當然依據專案需求會有不同的做法，歡迎大家給予建議。

<!--more-->

首先我會將整個 `app` 這個 folder 當作專案的 application，作為專案的實際操作層，我會希望 namespace 是我專案的名稱，Laravel 提供了指令可以直接修改

``` bash
    $ artisan app:name ProjectName
```

也就是說原本是在 `App\Controllers` 會變成 `Lottery\Controllers`。

這樣在進行升級或遷移的時候主要部份就會是在 `app` 這個底下，這意味著在往後的升級都更加簡單，想想 4.x 升級到 5.x 是一件很可怕的災難。

接著我會創建 `Entities` folder 來放置 Model & Relation methods & Scope，這代表了 model 就是很單純的做兩件事情，關係建立和額外的條件。

``` php
<?php

namespace Lottery\Entities;

use Illuminate\Database\Eloquent\Model;

class Lottery extends Model
{
    protected $fillable = [
        'user_id', 'status', 'type'
    ];

    protected $table = 'lotterys';

    public function user()
    {
        return $this->belongsTo(User::class);
    }
}
```

你可以透過 Laravel 寫好的 artisan 指令建立到指定的 folder，像是這樣:

```php
    $ artisan make:model Project/Model
```

`支持參數 -m 可以順帶連 migration 都建立出來。`

參考底層 `Illuminate\Database\Eloquent\Model` 可以看到更多好用的 properties。(ex: $perPage = 15 etc...)。

下一篇會說明 Providers。