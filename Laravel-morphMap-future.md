title: Laravel 新特性： Morph Map
date: 2016-01-20 12:32:22
tags: laravel
categories: Translate
---

有一個沒有在 Laravel 5.1 說明文件裡面的新特性`morphMap`。這個新特性是擴展了多型關聯，讓她可以更容易的使用。

<!--more-->

如果你在 Larave 5.1 之前使用過多型關聯，你會在資料表內看到類似這樣：

``` php
[
    "id" => 1,
    "comment" => "Hello world",
    "commentable_type" => "App\Models\Post",
    "commentable_id" => 5
]
```

欄位 `commentable_type` 包含了完整的 namespace 來關聯，這樣子會有幾個缺點：

1. 如果 namespace 改變了，你必須去寫 migration 來改變所有在你資料庫內的實例。

2. 冗長的 namespaces (像是 `App\Models\Customers\Projects\Bids\BidInvitation`)意思是說你的欄位必須設定最大長度。

3. 記不住完整的 namespace。

4. 最佳實踐是客戶端不需要知道完整的 namespaces。

5.1 感謝透過這個 pull request [#9891](https://github.com/laravel/framework/pull/9891) 加到 `Relation::morphMany()` 這個方法內。這個方法定義了全域映射的名字。你可以這樣做：

``` php
/* app/Providers/AppServiceProvider@boot */
    Relation::morphMap([
        'post' => App\Models\Post::class,
        'video' => App\Models\Video::class,
        'user' => App\Models\User::class,
    ]);
```

這允許你可以在資料庫使用 `post` 替代 `App\Models\Post`，並且會自動的映射它，當在你的 `Eloquent model` 設定關聯時。最好是在 service provider 做定義。我最近叫它 `AppServiceProvider`，所以現在你在資料庫內將看到這樣：

``` php
    [
        "id" => 1,
        "comment" => "Hello world",
        "commentable_type" => "post",
        "commentable_id" => 5
    ]
```

這樣子的結果會跟之前一樣完美的運作，這項特性在文件裡面沒有出現，所以現在沒有一個明確的作法。我強烈建議使用它，避免自己額外實現這項功能。

[原文網址](http://jjanusch.com/2016/01/morphmap-laravel/)