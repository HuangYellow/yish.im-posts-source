title: "Ubuntu 14.10 or later does not install in virtualbox"
date: 2015-05-16 10:34:17
tags: [Ubuntu]
categories: Ubuntu
---

## 安裝的時候螢幕是花屏…

其實這問題也不知道怎麼搞得，但後來在[URL](http://askubuntu.com/questions/541006/ubuntu-14-10-does-not-install-in-virtualbox)得到解答

### 在花屏的上面同時按下:

`Ctrl` + `Alt` + `F1`
### 接著再按下
`Ctrl` + `Alt` + `F7`
神奇的事情就發生了，就是可以安裝了。

## Guest additions ISO無法掛載

原則上就是一個可以隨心所欲修改解析度的東西，不知怎麼搞得弄完不能掛載，這邊是原始解答處:
[URL](http://www.ubuntugeek.com/fix-for-ubuntu-14-10-screen-resolution-issue-on-virtualbox.html)

``` bash
sudo apt-get install virtualbox-guest-dkms
```

然後`restart`就可以了，不過剛啟動又出現unity崩潰，嗯…看來新版本還是有些許問題啊…