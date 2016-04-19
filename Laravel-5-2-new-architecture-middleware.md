title: "Laravel 5.2 專案結構心得(八): Middleware"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-14 22:50:59
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---

相當於 4.2 的 filter 機制，只是更加彈性，可以依據需求新建和 pass value。

<!--more-->

``` bash
    $ artisan make:middleware Name
```

情境 : 被黑名單的登入使用者將不能拜訪或送值給指定 method。

``` php
    public function handle($request, Closure $next)
    {
      if (auth()->user()->status == config('list.black')) {
        return redirect config('list.black.redirectURL'))->with('error', config('list.black.message'));
      }

      return $next($request);
    }
```

到app/Http/Kernel.php 註冊你的 class。

``` php
    protected $routeMiddleware = [
        /** @middleware validation. */
        'blockade' => \Blog\Http\Middleware\Blockade::class,
    ];
```

## Tips
>在某條件下你希望可以 pass value 到 handler 那邊作處理。

``` php
    Route::get('{id}', [
        'middleware' => 'blockade:advertisers',
        'as' => 'articles.show',
        'uses' => 'ArticlesController@show'
    ]);
```

``` php
    public function handle($request, Closure $next, $type = 'advertisers')
    {
        //do somethings.......
    }
```

>仔細觀察 $request，它可以取得很多資料。
``` php
$request->route()->parameters() //取得 uri 上的 property [array]
```

更多方法可以到Illuminate\Http\Request 挖掘。