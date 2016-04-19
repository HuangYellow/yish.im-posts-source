title: "Laravel 5.2 專案結構心得(四): Repositories"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-09 21:44:47
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---
Repository 用來放置直接與 Entities 和 Eloquent, DB 作直接操作的資源庫，它不應該包含邏輯判斷。

<!--more-->

情境: 功能需求：需要取得文章列表，但可能會使用 user_id 或者是 post_id 得到列表。

``` php
    protected $model;

    public function __construct(Post $model)
    {
        $this->model = $model;
    }

    public function getListById($post_id = null)
    {
      $this->model->find($post_id);
    }

    public function getListByUserId($user_id = null)
    {
      $this->model->where('user_id', $user_id)->get();
    }
```

>注意：不應該在 Repository 這層去寫任何的邏輯判斷，讓她保持簡單跟單一職責：只做和資料庫或 Entities 溝通的功能。