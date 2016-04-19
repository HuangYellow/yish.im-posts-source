title: "Laravel 自訂擴展集合 (Custom collection)"
date: 2016-04-19 23:32:17
tags: laravel
categories: Laravel
---
[laravel collection](https://laravel.com/docs/5.2/eloquent-collections#custom-collections)

想放置一些邏輯或者工具來轉換 collection.

<!--more-->

前往 `Illuminate\Database\Eloquent\Model` 會發現有個 `newCollection` 的方法，可以看到他直接實體了`Illuminate\Database\Eloquent\Collection`，可以進行擴展。

這邊假設一個情境，我要 active 的所有文章 (status = 1)，我們可以有幾種做法。

## 直接透過 Repository ORM
這個方法就是一般的做法，就是透過 SQL 進行過濾：
``` php
class PostRepository
{
    protected $model;

    public function __construct(Post $model)
    {
        $this->model = $model;
    }

    public function getActiveAll()
    {
        return $this->model->where('status', 1)->get();
    }
}
```
或者你可以使用 model 的 scope 方法：
``` php
//Post.php
class Post extends Model
{
    public function scopeActive($query)
    {
        return $query->where('status', 1);
    }
}

//PostRepository
class PostRepository
{
    protected $model;

    public function __construct(Post $model)
    {
        $this->model = $model;
    }

    public function getActiveAll()
    {
        return $this->model->active()->get();
    }
}
```
關於 Query scope 可以參考[官方](https://laravel.com/docs/5.2/eloquent#query-scopes)。

>但如果需要的是 deactivate (status = 2)，就必須在 PostRepository 再寫一個方法...但僅僅是條件上的差異，也就是說假設一個頁面同時間要出現 active, deactivate 的內容，就必須 compact 兩包資料到前端或 api 當中。


## 擴展 Collection
在 5.2 的文檔出現了[custom-collections](https://laravel.com/docs/5.2/eloquent-collections#custom-collections)，查了一下[發現](http://heera.it/extend-laravel-eloquent-collection-object#.VxXeepN9560)很久以前大神們就有在擴展了。

``` php
class Post extends Model
{
    /**
     * Create a new Eloquent Collection instance.
     *
     * @param  array  $models
     * @return \App\Collection
     */
    public function newCollection(array $models = [])
    {
        return new PostCollection($models);
    }
}
```
在這裡我們將 newCollection 改為了 new PostCollection($models)，而非 `Illuminate\Database\Eloquent\Collection`，接著進行新建與繼承，並且建立我們所需要的方法。
```php
namespace App\Collections;

use Illuminate\Database\Eloquent\Collection;

class PostCollection extends Collection
{
    public function active()
    {
        return $this->where('status', 1);
    }

    public function deactivate()
    {
        return $this->where('status', 2);
    }
}
```

接著我們可以在 PostRepository 選取出整個 collection：
``` php
//PostRepository
class PostRepository
{
    protected $model;

    public function __construct(Post $model)
    {
        $this->model = $model;
    }

    public function getAll()
    {
        return $this->model->all();
    }
}
```
緊接著分別在 Service, Controller 寫下對應代碼：
``` php
//PostService
class PostService
{
    protected $postRepository;

    public function __construct(PostRepository $postRepository)
    {
        $this->postRepository = $postRepository;
    }

    public function all()
    {
        return $this->postRepository->all();
    }
}

//PostsController
class PostsController extends Controller
{
    protected $postService;

    public function __construct(PostService $postService)
    {
        $this->post = $post;
    }

    public function panel()
    {
        $posts = $this->postService->all();

        return view('posts.panel', compact('posts', $posts));
    }
}
```
我們就可以在 blade 頁面上這樣寫：
``` php

//get Active data
@foreach ($posts->active() as $post)
    //.....
@endforeach

//get deactivate data
@foreach ($posts->deactivate() as $post)
    //.....
@endforeach
```
相當方便。

如果說是 Api 的方式可以這樣寫：
``` php
//PostRepository 不需要做任何更動。

//PostService
class PostService
{
    protected $postRepository;

    public function __construct(PostRepository $postRepository)
    {
        $this->postRepository = $postRepository;
    }

    public function all($method = 'active')
    {
        return $this->postRepository->all()->{$method}();
    }
}
```

That's it.

