title: "Select 使用 DB::raw() - 讓你的資料運作得更好"
date: 2015-12-12 18:29:04
tags: laravel
categories: Laravel-Daily
---

當從資料庫撈取資料時，有時候你會想利用額外的過濾來選取你所需要的資料 － 並且撈取後還希望用 SQL 的一些條件狀態來過濾。

<!-- more -->

在 Laravel 當中 - 你可以透過 [Accessor fields](http://laraveldaily.com/why-use-appends-with-accessors-in-eloquent/) 或者 PHP 原生的 迴圈來取得結果。但有一個更好的方法 － 把過濾的機制在資料庫查詢時就把它做掉。

想像一下真實的狀況 － 在資料表當中你有`性別`這個欄位`1`代表的是男性，而`2`則是代表女性。但是在頁面上你是要顯示文字而不是數字，簡單來說，你就必須在 blade 裡面寫上`IF`的判斷陳述來決定你要顯示什麼：

``` php
<td>{{ ($user->gender == 1) ? 'Male' : 'Female' }}</td>
```

但有時候事情沒那麼單純，你不可能每次都這麼華麗的過濾它 － 你需要資料回傳時就已經處理好了 － 最好的範例做法是來自 [Datatables.net](http://datatables.net/) 的 [server-side with AJAX calls](http://datatables.net/examples/data_sources/server_side.html)，預期的狀態就是透過 JSON 來做驗證。

所以我們必須在 SQL 查詢中使用 `IF`判斷陳述，事實上，在 `MySQL`當中有 [CASE-WHEN statement](https://dev.mysql.com/doc/refman/5.7/en/case.html) 這樣子的判斷陳述：

``` php
SELECT
  (CASE WHEN (gender = 1) THEN 'M' ELSE 'F' END) AS gender_text
  FROM users;
```

現在如何在 Laravel 當中做到相同的事情？ 在查詢生成器你有 `select()` 這個方法，他可以讓你簡單取出資料並且列出來，對吧？你可以透過 `raw query`把它放進去 `select()` 就像參數一樣：

``` php
$users = DB::table('users')
  ->select(DB::raw("
  name,
  surname,
  (CASE WHEN (gender = 1) THEN 'M' ELSE 'F' END) as gender_text")
);
```

接著你可以看到，`DB::raw()` （對了，別忘記 `use Illuminate\Support\Facades\DB`）允許你在裡面寫上基本的 SQL 判斷陳述。

另一個常用的用法是 `group` 陳述。在有時候，你需要使用 MySQL 的方法，例如 `COUNT()`，你可以使用 `DB::raw()`。這邊有個簡單的範例，你也可以參考[官方查詢生成器文件](http://laravel.com/docs/5.1/queries#selects)

``` php
$users = DB::table('users')
                     ->select(DB::raw('count(*) as user_count, status'))
                     ->where('status', '<>', 1)
                     ->groupBy('status')
                     ->get();
```

這個技巧是 Laravel 查詢生成器當中相當有用的方法之一，當需要的時候，他不會限制你執行 SQL 查詢。

[原文網址](http://laraveldaily.com/select-with-dbraw-make-your-database-work/)