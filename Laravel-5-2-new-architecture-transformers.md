title: "Laravel 5.2 專案結構心得(七): Transformers"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-14 22:45:59
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---

Transformer 用來對最後輸出的結果進行轉換，可以選擇讓資料呈現更符合期待和需求。

<!--more-->

情境 : Mobile 和 Desktop 最後回傳不同內容，並且格式必須篩選整理過。

``` php
    class ArticleTransformer extends Transformer
    {
        public function transform($instance)
        {
            return [
                'id'   => $instance->id,
                'title'       => $instance->title,
                'content'   => markdown($instance->content), //這邊透過自訂的 helper 做 markdown convert.
                'created_at'    => js_time($instance['created_at']), //透過自訂的 helper 做 js time convert.
                'updated_at'    => js_time($instance['updated_at']),
            ];
        }
    }
```

由於必須讓使用 transformer 的開發人員知道必須實作一個 transform ，所以定義一個 abstract class and abstract method.
``` php
    abstract class Transformer
    {
        //也許這邊可以加入一些 property....

        abstract public function transform($instance);
    }
```

也許可以再寫一個 method 來判斷 User-Agent : 在 Controller 就可以寫成
``` php
    public function show($id)
    {
        $article = $this->articleService->getData($id);

        return (is_mobile()) ? $this->transformer->transform(['data' => $article, 'status' => 'success']) : view('articles.show', compact('article'));
    }
```
