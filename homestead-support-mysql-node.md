title: Laravel Homestead 支持 MySQL 5.7 & Node 5.0
date: 2015-11-17 23:21:09
tags: Laravel-News
categories: Laravel-News
---

![support](http://i.imgur.com/YdMqYwT.png)

根據 [Laravel News](https://laravel-news.com/2015/11/laravel-homestead-now-with-mysql-5-7-and-node-5-0/) 報導，目前的 Homestead 0.3.3 已經支持 MySQL 5.7 & Node 5.0。

<!-- more -->

最近一次的 Homestead 更新，已經將MySQL 5.7 以及 Node 5.0 納入 Homestead 的 Image內，只要你進行更新即可完成：

``` bash
    $ vagrant box update
```

此外值得注意的地方就是：MySQL 5.7 此次的更新已經包含了[JSON欄位類別](https://dev.mysql.com/doc/refman/5.7/en/json.html)的支援，這項類別將在 [Laravel 5.2](https://laravel-news.com/2015/11/laravel-5-2-a-look-at-whats-coming/) 正式支援。