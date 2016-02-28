title: "Sublime 快速 Snippets with PHP"
date: 2016-01-11 23:28:07
tags: [sublime,php]
categories: Sublime
---

Sublime snippets 是 Sublime 相當實用的自定義快捷鍵方法，這個 repo 將會提供一些已經寫好的快捷鍵來快速建立 PHP 一些常用的 method 與 class。

<!--more-->

## 安裝

[Github Repo 網址](https://github.com/Mombuyish/sublime-fast-snippets-with-php)

這個 repo 必須安裝在你的 sublime 路徑下:

ubuntu:
```
    .config/sublime-text-3/Packages/User
```

mac:
```
    ~/Library/Application Support/Sublime Text 3/Packages/User
```

windows:
```
    Sublime Text 3/Packages/User
```

接著你可以使用 `git clone` 來下載它:

```
    git clone https://github.com/Mombuyish/sublime-fast-snippets-with-php.git
```

或者你可以直接下載壓縮檔，並且解壓縮到上述指定路徑下。

## 用法

這邊提供了幾個快速建立的方法，其中可以注意到的是: 除了幾個建立的方法之外，其他的快捷鍵部分是參考 `PHPStorm`的設定，這可以讓你之後使用 `PHPStorm` 時能快速上手，相當實用:

當然，支援使用 `tab` 來做 slug 的上下切換。

| 快捷鍵  | 作用                             |
| --------- |--------------------------------------|
| _c        | 建立建構式方法               |
| class     | 建立含有 namespace 的 class           |
| aclass    | 建立含有 namespace 的 abstract class  |
| echo    | echo  |
| fore    | foreach  |
| forek    | foreach with key  |
| inc    | include  |
| inco    | include_once  |
| prif    | 建立 private 方法   |
| prisf    | 建立 private static 方法   |
| prof    | 建立 protected 方法   |
| prosf    | 建立 protected static 方法   |
| pubf    | 建立 public 方法   |
| pubsf    | 建立 public static 方法   |
| rqr    | require   |
| rqro    | require_once   |
| thr    | throw new...   |


## 注意事項
為了避免使用者在非 PHP 的檔案下使用這些快捷鍵，因此必須定義檔案名稱與 `<?php` 才能使用這些快捷鍵。

Enjoy it.