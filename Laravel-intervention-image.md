title: "Laravel intervention image"
date: 2015-03-25 12:18:28
tags: laravel
categories: Laravel
---
前陣子需要對上傳圖片進行resize的動作，偶然找到這個可以resize跟對圖片做處理的package，用起來也相當簡單實用 intervention/image.

<!-- more -->

[Github](https://github.com/Intervention/image)
[official](http://image.intervention.io/)

>Laravel 4, 5

**他底層還是去呼叫GD函式庫，先確認是否有安裝。**

## 安裝
`composer.json`
``` json
"intervention/image": "2.1.3"
```
``` bash
composer update
```

`app.php`
``` php
//provider
'Intervention\Image\ImageServiceProvider',
//Facades
'Image' => 'Intervention\Image\Facades\Image', //這可以讓你用Image::的方式呼叫
```

## Example
>官方提供了相當多的圖片處理function，這邊我舉一個resize，依此類推。
``` php
//$file就是Input::file('image')
Image::make($file->getRealPath())->resize('800', '800')
            ->save('storage/images'.$filename);
```

依據自己需求進行調配各個function，應該可以解決處理圖片的問題。

enjoy it.

