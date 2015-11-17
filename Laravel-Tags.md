title: "Laravel Tags"
date: 2015-03-25 10:40:04
tags: Laravel
categories: Laravel
---

前陣子因為需求要實作標籤功能，發現有cartalyst/tags這個package，這是一個能夠讓你快速生成標籤與原有內容做關聯的package，相當方便。

<!-- more -->

[official](https://cartalyst.com/manual/tags/1.0)

[Github](https://github.com/cartalyst/tags)

>Laravel 4

## 安裝
`composer.json`
``` php
"cartalyst/tags": "~1.0"
```

``` bash
composer update
```

## 配置
tag的功能是需要透過table做紀錄的，也因此需要做一次migration.
``` bash
php artisan migrate --package=cartalyst/tags
```

>建立將package裡面的migration複製到database/migrations，這樣日後直接下`php artisan migrate`即可。

## Model配置
接下來，必須使用trait來告知是哪個model要使用tags
``` php
use Cartalyst\Tags\TaggableTrait;
use Cartalyst\Tags\TaggableInterface;

class Product extends Eloquent implements TaggableInterface
{
    use TaggableTrait;
    ...
    ...
}
```

that's it, 這樣就算配置好了。

## 使用

### 新增tags
``` php
// 取得原有文章
$post = Post::find(1);
// 或者可以是新增時加入tags
$post = Post::create($data);

// 字串
$post->tag('foo, bar, baz');

// 陣列
$post->tag([ 'foo', 'bar', 'baz' ]);
```

### 刪除tags
``` php
// 取得原有文章
$post = Post::find(1);

// string
$post->untag('bar, baz');

// array
$post->untag([ 'bar', 'baz' ]);

// 移除所有標籤
$post->untag();
```

### 更新（設定）tags
``` php
// 取得原有文章
$post = Post::find(1);

// string
$post->setTags('foo, bar, baz');

// array
$post->setTags([ 'foo', 'bar', 'baz' ]);

// 使用slug欄位做驗證檢查用
$post->setTags([ 'foo', 'bar', 'baz' ], 'slug');
```

### 搜尋標籤
>當然，事情沒這麼順利，到目前為止都沒有什麼問題，但仔細一看你會發現，當你在搜尋標籤時，英數都可以找到相對應的資料，但中文就是沒辦法，原因就在於tags在選取時是利用`slug`這個欄位作為get value，但是你會發現中文的根本無法寫入slug這個欄位！原因就是他的function是去呼叫底層的`function ascii`這個編碼格式相信大家都不陌生，沒錯，他的記憶位元並不足夠儲存中文，所以標籤如果打中文，理所當然的就存不進去了。

也因此我們必須利用`name`這個欄位作為我們的url slug，那麼該怎麼做呢？
``` php
$post = Post::whereTag('foo', 'name');
```
that's it, 就是這麼簡單。

### 取得有foo, bar其中之一標籤的文章
``` php
$post = Post::withTag('foo, bar')->get();
//A:foo B:bar C:foo,bar -> ABC都會進來
```
### 取得單篇文章所有tags
``` php
$post = Post::find(1);
$post->tags;
```

### 取得所有tags
``` php
$tags = Post::allTags();
```

### 選用

取得定界符
``` php
$delimiter = Post::getTagsDelimiter();
```

設定定界符
``` php
Post::setTagsDelimiter(';');
```

如果覺得slug不用真的浪費的人（或者是覺得上面用name的方式不好的），也可以自己進行改寫
>The Tags package needs a way to create a sluggified tagged name, to achieve this, by default we use the Illuminate\Support\Str::slug method but if required you can easily swap the Slug Generator method to one that fits your own needs.

#### 取得slug
``` php
$generator = Post::getSlugGenerator();
```

#### 自定義slug function
``` php
// Through a function string
Product::setSlugGenerator('slugify_string');

// Through a class@method string
Product::setSlugGenerator('MyGenerator::slug');

// Through a Closure
Product::setSlugGenerator(function($name) {
    return str_replace(' ', '_', strtolower($name));
});
```

如果需要知道更多的參數設定可以參考[官網](https://cartalyst.com/manual/tags/1.0)

enjoy it.










