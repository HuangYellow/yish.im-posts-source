title: "Ctags with Sublime text 3 On Mac/ubuntu"
date: 2015-06-10 22:34:58
tags: [Ctags,Sublime]
categories: Sublime
---

>Ctags是一個相當好用的代碼追蹤工具，他會建立一個tag 索引檔讓開發人員能快速在class, method之間做切換與追蹤。

[Github](https://github.com/SublimeText/CTags)

# Installation
## Mac
>先行確認安裝[Homebrew](http://brew.sh/)

``` bash
    brew install ctags
```

## Ubuntu
``` bash
    sudo apt-get install ctags
```

# Sublime settings
## 安裝
* 首先必須安裝[Package Control](http://yish.im/2015/03/22/Sublime-text-3-on-Ubuntu/)

* Package Controll:Install Package -> Ctags

* Restart Sublime

* 接下來會發現對著專案按下右鍵時會出現`Ctags:Rebuild Tags`->點選->然後等待他產生出`.tag`, `.tags_sorted_by_file`(需要一點時間才會完成)
好了之後對著程式的class, method name右鍵會看到`Go To Definition` , `Navigate to Definition`, 就可以達到快速在method之間追蹤與調用查詢。

## 疑難排解
### Mac安裝出現錯誤
Q:我的Mac在安裝的時候出現了:error: [Errno 1] b'/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/ctags: illegal option -- R\nusage: ctags [-BFadtuwvx] [-f tagsfile] file ...\n'怎麼解決？

引發原因:
`ctags這個指令並不包含在PATH內，必須自己手動加入。`

[在官方github上面有說明](https://github.com/SublimeText/CTags#os-x)

在Preferences > Package Settings > Ctags > Settings - User加入:

``` bash
{
    "command": "/usr/local/bin/ctags",
}
```

詳細說明可以在Preferences > Package Settings > Ctags > Settings - Default裡面看到(約在第10行)的command這個指令的說明。

### 注意項目
>當專案新增了新的class, method就必須重新產生`Ctags:Rebuild Tags`建立索引檔

>如果專案是要production or co-work, 記得把`.tag`, `.tags_sorted_by_file`加入`.gitignore`

### 加強
如果說要讓ctags能夠autocomplete你的class, method name可以在Preferences > Package Settings > Ctags > Settings - User加入:
``` bash
{
    "autocomplete": true,
}
```

## 快捷鍵
[官方有提供預設快捷鍵](https://github.com/SublimeText/CTags#commands-listing)

>以下是我在Mac上的個人配置設定

Preferences > Package Settings > Ctags > Key Bindings - User
``` bash
[
  {
    "command": "navigate_to_definition",
    "keys": ["super+t", "super+t"]
  },
  {
    "command": "search_for_definition",
    "keys": ["super+t", "super+y"]
  },
  {
    "command": "jump_prev",
    "keys": ["super+t", "super+b"]
  },
  {
    "command": "rebuild_tags",
    "keys": ["super+t", "super+r"]
  }
]
```

## 其他
[這邊有大大針對ROR做的一些細節設定與配置](http://toyroom.bruceli.net/tw/2014/02/23/sublime-text-integration-with-ctags.html)
[大陸網站](http://jingyan.baidu.com/article/48206aeafba820216ad6b3f5.html)
