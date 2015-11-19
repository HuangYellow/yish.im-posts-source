title: PHPStorm 10 on Ubuntu
date: 2015-11-09 10:56:52
tags: ubuntu
categories: Ubuntu
---
![phpstorm10](http://i.imgur.com/GqdCs6V.png?1)

隨著新的PHP7即將發佈，PHPStorm也迎來了版本更新，在MAC上基本上是不會遇到安裝問題（也許要更新java版本？），但如果是ubuntu則需要修改一些設定才能順利使用，這次的版本更新有明顯感覺到速度上的差異，並且支援新的PHP7 highlight，趕快更新吧！

<!-- more -->

## 前置
你可以先宣告接下來都使用sudo
``` bash
$ sudo -s
```

到[官方網站](https://www.jetbrains.com/phpstorm/)下載`.tar.gz`

## 安裝

解壓縮
``` bash
$ tar xfz PhpStorm-x.y.tar.gz
```

將檔案移動到`opt/phpstorm`底下，或者是你想要的地方
``` bash
$ mv PhpStorm-x.y /opt/phpstorm
```

切換到home目錄下：
``` bash
$ cd ~
```

新建 `phpstorm.desktop`
``` bash
$ nano phpstorm.desktop
```

依據需求進行配置：先配置搜尋出現的icon
``` bash
[Desktop Entry]
Name=PhpStorm
Type=Application
Exec=phpstorm.sh
Terminal=false
Icon=webide
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE;
Name[en]=PhpStorm
```

安裝：
``` bash
$ desktop-file-install phpstorm.desktop
```

建立執行關聯：
``` bash
$ ln -s /opt/phpstorm/bin/phpstorm.sh /usr/local/bin
```
複製icon到根目錄下：
``` bash
$ cp /opt/phpstorm/bin/webide.png /usr/share/pixmaps/webide.png
```
* 接下來你會發現實際執行時unity上面icon會出現問號，並且實際去執行時無法執行，這原因是因為原本我有安裝PhpStorm 9，但我移除後，desktop的部份還沒有`更新路徑`的關係：

切換到`desktop icon`底下編輯文件（如果沒有還是遇到此狀況請自行新增檔案）：
``` bash
$ cd ~/.local/share/applications
$ nano jetbrains-phpstorm.desktop
```
修改對應的路徑與icon：
``` bash
[Desktop Entry]
Version=1.0
Type=Application
Name=PhpStorm
Icon=/opt/phpstorm/bin/webide.png
Exec="/opt/phpstorm/bin/phpstorm.sh" %f
Comment=Develop with pleasure!
Categories=Development;IDE;
Terminal=false
StartupWMClass=jetbrains-phpstorm
```
that's it.