title: "Laravel IoC 簡單實作"
date: 2015-10-27 14:27:25
tags: [Laravel]
categories: Laravel
---
這個方法可以讓跟model或者repo無關的額外功能透過binding的方式載入：
``` php
<?php //route.php

Route::get('/', 'PostsController@index');
```

原始我會直接用DI的方式注入，但我發現這樣並不能達到抽換的效果，具體來說，應該是相依於抽象而不是實體。原始例子如下：

``` php
<?php //PostsController.php

class PostsController extends Controller
{
    public function __construct(AmazonMailer $mailer)
    {
        $this->mailer = $mailer;
    }

    public function index()
    {
        return $this->mailer->send('this is content');
    }
}
```

新建需要實作的幾個class與contract：

``` php
<?php //MailableInterface.php

interface MailableInterface
{
    public function send($content = null);
}
```
現在，我們寄信的功能是由Amazon的服務寄出，我必須實作這個合約：

``` php
<?php //AmazonMailer

class AmazonMailer implements MailableInterface
{
    public function send($content = null)
    {
        return 'Send the '.$content.' to somewhere.'; //這邊只是舉例子
    }
}
```

透過IoC去綁定我的interface：

``` php
<?php //route.php

App::bind('MailableInterface', 'AmazonMailer');
Route::get('/', 'PostsController@index');
```

IoC會幫我找尋實現這個contract的class，並且將他new出來，透過反射。
接下來修改原本controller：
``` php
<?php //PostsController.php

class PostsController extends Controller
{
    public function __construct(MailableInterface $mailer) //這邊依賴抽象，而非實體
    {
        $this->mailer = $mailer;
    }

    public function index()
    {
        return $this->mailer->send('this is content');
    }
}
```


這樣子的目的假使今天我們有用透過其他服務的寄信功能，我們可以這樣做：
``` php
<?php //MailgunMailer

class MailgunMailer implements MailableInterface
{
    public function send($content = null)
    {
        return 'Send the '.$content.' to somewhere by mailgun';
    }
}
```
修改Binding：
``` php
<?php //route.php

App::bind('MailableInterface', 'MailgunMailer');
Route::get('/', 'PostsController@index');
```

如果是多項的也沒問題：
``` php
<?php //route.php

App::bind('MailableInterface', 'MailgunMailer');
App::bind('NotifiableInterface', 'UserNotifier'); //這邊假設我們都已經實作了
Route::get('/', 'PostsController@index');
```
controller的部份則是這個樣子的：
``` php
<?php //PostsController.php

class PostsController extends Controller
{
    public function __construct(MailableInterface $mailer, NotifiableInterface $notifier)
    {
        $this->mailer = $mailer;
        $this->notifier = $notifier;
    }

    public function index()
    {
        return $this->mailer->send('this is content');
    }

    public function notice()
    {
        return $this->notifier->notify();
    }
}
```
Powerful and Simple, try it.
