title: "Laravel 5.2 — 前瞻"
date: 2015-11-03 02:08:20
tags: [Laravel-news]
categories: [Laravel-news]
---

![laravel5.2](http://i.imgur.com/5WZba0s.png)

Laravel 5.2 的開發工作正在如火如荼的進行中，而且截至目前為止已經宣布了加入許多很棒的新特性進來，讓我們趕緊來看看有什麼功能吧！

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

這個新特性是讓我最興奮的。事實上，我寫了一個[完整教學](http://ericlbarnes.com/laravel-array-validation/)如何使它能夠運作，而且他已經是最受歡迎的文章了。

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
	$posts->pluck(‘posts.*.title’);
```

這將會返回所有在 posts 裡面的 title。

## 資料庫 Session 驅動（Database Session Driver）

資料庫的 session 驅動目前包含了 `user_id` 和
`ip_address`，所以你可以簡單的清除掉包含這個使用者的所有 sessions。

## 還有更多...
隨著 Laravel 5.2 發布時間越來越靠近，我確信一些新的特行將會逐一發佈，我將會繼續在下面更新這篇文章。確認你有訂閱 [newsletter](https://laravel-news.com/newsletter/) 方便更新時通知你。

[原文地址](https://laravel-news.com/2015/11/laravel-5-2-a-look-at-whats-coming/)