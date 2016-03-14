title: "Laravel 5.2 專案結構心得(五): Services"
categories: Laravel
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: 'yes'
metaAlignment: center
coverMeta: in
coverSize: partial
date: 2016-03-14 22:42:59
tags: laravel
keywords:
- laravel
- architecture
thumbnailImage: thumbnail.png
coverImage: cover.png
---
Service 用來放置切分好的流程，讓 controller 依據需求更換流程和修改。

<!--more-->

情境 : 建立文章同時會新建自訂標籤、並且把登入者加入追蹤文章清單當中。

``` php
    /**
     * @param array $data
     * @return static
     */
    public function createByAuthUser(array $data)
    {
        //透過 Laravel relations 建立文章
        $article = auth()->user()->articles()->create($data);

        //轉換標籤
        $this->article->setTransFormTags();

        //寫入標籤
        $article->tag(mb_strtolower($data['tags']));

        //加入追蹤
        $article->traces()->save($this->trace->saveAuthUser());

        return $article;
    }
```