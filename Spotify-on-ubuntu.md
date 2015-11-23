title: "Spotify on Ubuntu Settings"
date: 2015-07-24 19:50:25
tags: [ubuntu]
categories: Ubuntu
---
![spotify](http://i.imgur.com/7btlJ0p.png)

因為長期開發都是用 Ubuntu，最近終於開始付費使用 Spotify 了，由於他可以選擇高音質，但網頁版似乎不行，所以就研究了一下如何在 Ubuntu 下安裝 Spotify。

首先你可以參考[官方](https://www.spotify.com/tw/download/linux/)的步驟，這邊我的步驟是跟他一樣的。

接下來由於我帳號是使用 Facebook 做登入，但是當我按下去的時候我發現根本沒辦法登入，上網查了一下似乎要[額外設定](http://mikedixson.com/2014/11/solved-spotify-desktop-client-communication-failed/)：
``` bash
登入 Facebook > Security > App Passwords
```
接下來輸入 `Spotify` Facebook 就會產生一組密碼給你，這組密碼就是你登入 Spotify 的密碼，回到應用程式，輸入你的 Facebook Email 以及剛剛的密碼就可以登入了。

登入之後馬上選取`edit > preferences > playback > high quality streaming` 就可以享受高音質的音樂了。

## Optional
由於每次歌曲換的時候一直通知神煩，研究了一下關閉通知。

到這個檔案內修改內容：
``` bash
    /home/username/.config/spotify/Users/xxxxxxxxxx-user/prefs
```
新增一行config：
``` bash
    ui.track_notifications_enabled=false
```