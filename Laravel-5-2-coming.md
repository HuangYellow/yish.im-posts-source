title: "Laravel 5.2 — 前瞻"
date: 2015-11-15 02:08:20
tags: Laravel-News
categories: Laravel-News
---

![laravel5.2](http://i.imgur.com/RxpYi6j.png)

根據[Laravel-news](https://laravel-news.com/2015/11/laravel-5-2-a-look-at-whats-coming/)的消息，laravel5.2即將發佈，以下有許多新特性讓人非常期待！

<!-- more -->

## 隱晦模型綁定（Implicit model binding）

隱晦模型綁定是一個新的特性，他將會自動綁訂一個模型到路由，以下是範例程式碼：

``` php
    Route::get('/api/posts/{post}', function(Post $post) {
        return $post;
    });
```

上述程式碼將會在背後直接呼叫 `Post::findOrFail($post)` 並且將它注入到 $post 這個變數。對於有經驗的Laravel開發者，這個功能就很像是已經存在的 [路由模型綁定](http://laravel.com/docs/5.1/routing#route-model-binding) ，但現在移除了手動綁定它。

## 排程任務附加額外輸出（Appending output from scheduled tasks）

[Laravel Scheduler](https://laravel-news.com/2014/11/laravel-5-scheduler/) 將可以附加來自於任務的輸出給檔案。

``` php
    $schedule->command('emails:send')
        ->hourly()
        ->appendOutputTo($filePath);
```

先前 Laravel 有包含`sendOutputTo`選項，它可以寫入最近的結果但不能附加。

## Laravel 5.2 表單陣列驗證（Laravel 5.2 Form Array Validation）

這個特性 Laravel-news作者有寫一份[完整教學](http://ericlbarnes.com/laravel-array-validation/)，有興趣的人可以去看看。

假設你有個表單，並且有個 input 輸入區域（當然，他是陣列的形式）：

``` php
<p>
    <input type="text" name="person[1][id]">
    <input type="text" name="person[1][name]">
</p>
<p>
    <input type="text" name="person[2][id]">
    <input type="text" name="person[2][name]">
</p>
```

在 Laravel 5.1 要加入驗證規則是必須跑迴圈並且個別加入相對應的驗證規則。已經不必要再做這些了，因為它已經 "Laravel化（Laravelized）"了：

``` php
    $v = Validator::make($request->all(), [
      'person.*.id' => 'exists:users.id',
      'person.*.name' => 'required:string',
    ]);
```

## Collections 通配符（Collections Wildcards）

當我們使用一個 collection 並且想要拉出資料，你現在可以使用 * 這個通配符：

``` php
    $posts->pluck('posts.*.title');
```

這將會返回所有在 posts 裡面的 title。

## 資料庫 Session 驅動（Database Session Driver）

資料庫的 session 驅動目前包含了 `user_id` 和
`ip_address`，所以你可以簡單的清除掉包含這個使用者的所有 sessions。

## MySQL JSON 欄位支援（MySQL JSON Column Types）
<blockquote class="twitter-tweet" lang="zh-tw"><p lang="en" dir="ltr">Upcoming Laravel 5.2 release also supports creating new MySQL JSON column types!</p>&mdash; Laravel (@laravelphp) <a href="https://twitter.com/laravelphp/status/665182225206542336">2015 11月 13日</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
MySQL 5.7.8 加入了支援原生的 JSON 資料類別。Laravel 5.2現在也加入了支援這個欄位類別了。

## 持續更新...