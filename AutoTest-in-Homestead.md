title: "在Homestead下運行即時通知測試 on Ubuntu / Mac"
date: 2015-09-26 17:28:33
tags: [PHP,Testing]
categories: Laravel
---

這篇是延伸更進一步將即時通知測試帶入 homestead。

<!-- more -->

## 在homestead下運行即時通知測試
>先前的[自動化測試 in PHP with Gulp, Node](http://yish.im/2015/09/24/AutoTest-in-PHP/)是在本地端執行，接下來將會在homestead底下進行配置。

其實homestead該有的組件都已經安裝好了，但問題就是出在:他的即時推播沒辦法送到外面，由於是虛擬機，而gulp是在監聽本地的行為，因此必須額外掛載相關組件

https://github.com/fgrehm/vagrant-notify


## Ubuntu
先將homestead關閉
``` bash
$ homestead halt
```
接下來安裝其組件
``` bash
$ sudo vagrant plugin install vagrant-notify
```
當中如果缺少ruby請進行安裝(此組件是由ruby開發)
``` bash
$ sudo apt-get install ruby
```
啟動homestead，並且必須要provision
``` bash
$ homestead up --provision
```

測試
``` bash
$ notify-send test message
```
![message](https://camo.githubusercontent.com/928ddd616d9bfa65dd934878fc3016ee4aeeda6d/687474703a2f2f692e696d6775722e636f6d2f747a4f4c7647592e676966)
如果有看到訊息彈出表示安裝成功

接下來連入homestead
``` bash
$ sudo homestead ssh
```
切換到專案資料夾底下，依照需求輸入對應指令
## 指令
``` bash
$ gulp tdd //運行gulpfile.js標籤有tdd的method(phpUnit, phpSpec)
$ gulp watch //監聽gulpfile.js所有的method
$ gulp //一樣是監聽所有method，但會先執行一次
$ gulp default //同上
```

## Mac
>mac的調整方式非常折騰，他不能像是ubuntu的做法，必須透過額外的terminal-notifier來做推播，以下是部署的筆記（感謝Oomusou大大的強力技術支援）

先將homestead關閉
``` bash
$ homestead halt
```
接下來安裝其組件
``` bash
$ sudo vagrant plugin install vagrant-notify
```
當中如果缺少ruby請進行安裝(此組件是由ruby開發)
``` bash
$ sudo apt-get install ruby
```
接下來安裝 [terminal-notifier](https://github.com/julienXX/terminal-notifier)。
可以透過homebrew或者直接下載[編譯](https://github.com/julienXX/terminal-notifier/releases)好的檔案

接著到/usr/local/bin底下，建立一個名為`notify-send`的script檔案，並且將相關對應規則寫入
``` bash
#!/bin/zsh
if [ "$4" = "Green!" ]; then
 /Applications/terminal-notifier.app/Contents/MacOS/terminal-notifier -appIcon "$2" -title "$4" -message "$5"
else
   /Applications/terminal-notifier.app/Contents/MacOS/terminal-notifier -appIcon "$2" -title "$6" -message "$7"
fi
```
啟動homestead，並且必須要provision
``` bash
$ homestead up --provision
```
接下來連入homestead
``` bash
$ sudo homestead ssh
```
單元測試成功與失敗，修改關注檔案，如果成功跳出成功與失敗表示就成功了！

## 本地與homestead差異
主要是差在回應速度，由於homestead是虛擬機的關係，當你在虛擬環境下做任何操作，尤其是在測試這個部分他反應速度會非常緩慢(本地反應時間大概是毫秒，而虛擬機則是以秒為單位)，這違反了FIRST原則的第一個:Fast(夠快)，但它的好處就是你不需要把本地環境搞亂，安裝一堆相依組件，再透過額外掛載的推播一樣可以達到效果，要用哪個版本可以由使用者做取捨和當前環境來做決定，我個人比較傾向本地跑測試，因為主要是夠快，而且測試應該是專注於邏輯，所以不會存在環境問題，anyway，趕緊寫測試吧!