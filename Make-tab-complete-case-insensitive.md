title: "讓 Homestead 的 Tab Complete 不識別大小寫"
date: 2015-11-20 03:14:05
tags: laravel-news
categories: Translate
---

根據 [Laravel-News](https://laravel-news.com/2015/11/make-homestead-tab-complete-case-insensitive/) 文章提到 [Matt Stenson](https://twitter.com/mpstenson/) 近期在 twitter 分享一個實用的小技巧，那就是如何在 homestead 下面輸入指令時不會辨識大小寫。

<!-- more -->

文章中提到：如果你是 Mac 的開發人員，只需要安裝 [oh my zsh](http://ohmyz.sh/) 就可以達到這樣子的效果，但在 homestead 底下由於是 ubuntu 的關係則需要在設定一些項目。

舉例來說：當你使用 ohmyzsh 時，輸入 `homestead` 底下會分別出現：`/Homestead` 以及 `homestead` 這兩個選項，而如果是使用原生的 bash 則不會有同時出現的情況。

具體的設定方式就是：先連入 homestead 輸入：
``` bash
    $ echo set completion-ignore-case on | sudo tee -a /etc/inputrc
```

接著關閉 homestead (`homestead halt`)，並且 `homestead up`，連入 `homestead ssh`，現在，你可以一樣使用這項功能了。
