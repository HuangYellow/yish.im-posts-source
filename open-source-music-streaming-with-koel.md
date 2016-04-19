title: "開放原始碼的音樂串流網站 Koel"
date: 2015-12-17 14:46:54
tags: laravel-news
categories: Translate
---
![](https://d1zj60nuin5mrx.cloudfront.net/media/2015/12/14104909/koel.png)

根據 [Laravel-news](https://laravel-news.com/2015/12/open-source-music-streaming-with-koel/) 的消息，最近 Phan An 發布了一套開放原始碼的專案給大家參考使用，相當不錯。

<!-- more -->

## 想在自己的電腦上執行你的音樂庫嗎？

開發者 Phan An 決定建立一個品牌 app 名字就叫： [Koel](http://koel.phanan.net/) 用來解決這個問題。Koel 是一個個人音樂串流 app，並且他是開放原始碼，基於 Laravel 和 Vue.js 製作的。

>“我想要更簡單的安裝”

Phan說明為何他選擇 Laravel 作為開發 app的工具。

使用 Koel 的前提是你必須擁有音樂檔案。

Koel 非常簡單，他並不會處理上傳，所以他不能串 Spotify。取而代之的，你直接把音樂上傳到你的 Server 並且是可以讀取的路徑下 - 最好是 root 以外的路徑 - 並且設定 Koel 去同步掃描它。

![](https://d1zj60nuin5mrx.cloudfront.net/media/2015/12/14111000/koel-settings-1200x590.png)

Koel 的特色包含了搜尋、排序、瀏覽藝人或相簿、播放清單、連結/取消連結歌曲，並且你可以建立使用者來分享歌曲。這邊提供了幾個快速鍵使用：

* F 是全站搜尋框

* 輸入播放的歌曲，如果有多首歌被選取，預設是把它們加入到佇列的最下面，Shift + Enter是加到佇列的上面。加入時按住 Shift 可以把多首歌曲加到一個組合播放內。
* 空白鍵切換歌曲
* J 是播放在佇列的下一首歌曲
* K 是播放在佇列的上一首歌曲

現在你可以在 [Github](https://github.com/phanan/koel) 下載並安裝 Koel。

[原文網址](https://laravel-news.com/2015/12/open-source-music-streaming-with-koel/)
