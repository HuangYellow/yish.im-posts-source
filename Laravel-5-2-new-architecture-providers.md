title: "Laravel 5.2 專案結構心得(三): Providers"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-09 21:10:47
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---
放置可獨立運作的功能，跟 helper 不同的地方是: 可以透過 boot or register method 可以進行緩加載，當使用 Service Provider 的功能時才會進行呼叫。

<!--more-->

情境：在 Laravel 5 之後我們沒有像之前 Laravel 4 之前可以定義 local or production environment，但在 production environment 下不應該加載像是 `debugbar / ide_helper` 等開發用的服務。

有了 Service Provider，我們可以簡單地寫一個 provider 來進行環境的判斷和加載需要的服務。

把需要加載的套件與需要綁定的 facade 寫到 properties，讓後續加載或新增較為方便。

``` php
    /**
    * @需要加載的 Service Providers...
    */
    protected $providers = [
            'Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider',
            'Barryvdh\Debugbar\ServiceProvider',
            'GrahamCampbell\Exceptions\ExceptionsServiceProvider',
        ];

    /**
    * @需要綁定的 alias facade...
    */
    protected $aliases = [
            'Debugbar' => 'Barryvdh\Debugbar\Facade',
        ];
```

在 register method 內寫入判斷，讓服務可以順利加載。

``` php
    /**
     * Register the application services.
     *
     * @return void
     */
    public function register()
    {
        if ($this->app->isLocal() && ! empty($this->providers)) {

            foreach ($this->providers as $provider) {
                $this->app->register($provider);
            }

            if ( ! empty($this->aliases)) {
                foreach ($this->aliases as $alias => $facade) {
                    $this->app->alias($alias, $facade);
                }
            }
        }
    }
```

[register 和 boot method 差別在哪裡? 什麼情境下如何選擇使用它?](https://laravel.tw/docs/5.1/providers)

情境2：新建了一個 validation extend 指令，很多地方要用到但不知道在哪個時候加載。

>注意：我們是"擴充" Laravel validation 的機制而非像情境1一樣僅使用基本的 app->register，我們必須要等所有功能加載完才能加載這個服務。

``` php
    public function boot()
    {
        $this->registerActiveRules(request()->all());
    }

    public function registerActiveRules($request)
    {
        app('validator')->extend('active', function ($attribute, $value, $parameters, $validator) {
            return app(ActiveValidator::class)->active($value);
        });
    }
```
