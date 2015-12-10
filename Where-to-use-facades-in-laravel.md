title: "在 Laravel 的哪裡使用 Facades？"
date: 2015-12-10 12:14:11
tags: [facade,laravel]
categories: Learning-Laravel
---
Laravel 的 facade 美化非常強大，但它也可以是痛苦的，學著如何去使用它，或者不使用它而是使用依賴祝不僅可以幫助你的程式碼更容易理解，也可以用於之後的作業中。

<!-- more -->

facades 是 Laravel 把複雜的系統透過一層包裝使它更容易使用，它提供了靜態的呼叫方法直接向預先載入的 service provider 做存取，無論是 Laravel 本身或是你自己的 service provider，它讓你可以更簡單使用以及快速開發，避免了在你的程式碼當中直接進行依賴注入。

在 Laravel 5~ 泰勒更進一步的包裝了更多的函式 例如 view(), redirect() 讓我們的程式碼更加容易閱讀以及更加美觀。然而這是必要去包裝的嗎？你應該這樣使用它們？簡短的來說：是的，你應該用它們，但詳細的描述來說：這包含了很多模糊地帶，所以必須看情況使用。

## 使用以及測試FACADES

一般來說調用 facade `view()` 會是底下這樣：
``` php
public function index()
{
    return view('home.welcome');
}
```

其實跟底下這樣寫意思是一樣的：

``` php
    return View::make('home.welcome');
```

這是其中一個在 Laravel 5 引進的語法糖，這看起來很棒，這簡化了呼叫流程，為何不能隨時隨地使用呢？

Facades 應用在 controller 我是沒有任何問題的，而且我非常喜歡在上面使用。我的 controller 通常都是透過 Behat 進行測試與驗收，我的商務邏輯測試則是使用單元測試，然而當我開始使用 facades 在我的業務層，我們將會看到有趣的幾個問題。

底下是一個使用 `App::make()` 或者 `app()` 常見的使用案例：

``` php
public function handle(SomeCommand $command)
{
    $service = app(MyRequiredService::class);
    $service->doThingsWith($command->input);
}
```

對於上面案例，這邊有兩個問題：

1. 為何不在命令處理的建構式時注入服務？
2. app()它到底在幹嘛？

當在寫測試的時候，開發者必須知道應用程式什麼事情才能適當的隔離一些外部行為（這是期望的狀況下）。最後開發者終於知道這個依賴 `app()` 原來是在做這樣的事情：
``` php
    App::make($service);
```
原來是在做 `App::make()`，那我們可以在測試的 mock `App::make()`：

``` php
public function test_make_was_called()
{
    App::shouldReceive('make')->andReturn($mockService);
}
```

可是為何要這麼做，都包好了幹嘛還要自己做呢？為了這樣做，你必須引入 Laravel 應用，然後寫測試（設定 facade以及相關內容），這不能夠更簡單的依賴注入或 mock 嗎？這樣寫測試要導入 Laravel 應用....。它可以更加簡單，但為何我會說上面是個好例子？原因非常簡單，我們的 controller 通常是不會進行單元測試的。他們是測試整個邏輯的一部分，我們需要整個運作的系統，所以所有的依賴都會被測試，我們不會 mock 隱藏的依賴。整個運作的系統，所以所有的依賴都會被測試，我們不會 mock 隱藏的依賴。

避免使用 facades 在我們的業務層還有另一個好處: 我們不需要寫測試的時候引入整個應用，我們可以繼承 `PHPUnit_Framework_TestCase` 以及依賴注入它。這會使得測試變快，而程式碼就會像這樣：

``` php
class MyCommandHandler
{
     private $service;

     public function __construct(MyService $service)
     {
         $this->service = $service;
     }

     public function handle(MyCommand $command)
     {
         $this->service->doThingsWith($command->input);
     }
}
```

現在我們可以更加簡單的 mock service 以及正確的隔離我們的命令，而且不需要 `app()`, `view()` 以及任何的 facade 設定。

## 結論
Facades 是一個相當強大的工具，而且在應用程式某些地方使用如輔助函數，視圖，或者是你的 controller (也許還有其他地方用也不錯)。不過我建議你不要放在業務層。每個 Facade 都綁定了一個單獨 Laravel 物件，所以它只是一個相當簡單的注入代表對象（這邊可以把 facade 想成是美化的意思），如果你不確定 facades 對應哪個 物件，你可以參考 [Laravel’s facade reference](http://laravel.com/docs/5.1/facades#facade-class-reference)。

Facades 不是壞的，不是邪惡的（儘管很多說明說他們就是...）。它們是一個偉大的工具，在某些情況下 Facade真的可以讓你優美的進行依賴注入使用（像是在複雜的系統上使用）如果它們在程式內看起來很棒，就不應該避免使用它們。只是你要了解什麼時候使用它們，以及為何使用它們。過度的使用就會像是開發模式一樣，導致一些問題。

[原文網址](http://learninglaravel.net/where-to-use-facades-in-laravel/link)
