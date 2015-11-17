title: "Afterglow Theme on sublime text 3"
date: 2015-07-24 19:50:25
tags: [Theme,Sublime]
categories: Sublime
---
Afterglow theme是一款相當漂亮的theme，並且提供了很多彈性的設置讓使用者可以快速調整適合自己的工作環境。

<!-- more -->

![afterglow](https://github.com/YabataDesign/afterglow-theme/raw/master/Screenshots/Afterglow-default.png)



## Installation

* [安裝Package Control(必要)](http://yish.im/2015/03/22/Sublime-text-3-on-Ubuntu/)

* Install package->Theme - Afterglow

* 重新啟動sublime

當然你也可以透過[Github](https://github.com/YabataDesign/afterglow-theme)來安裝。

## Settings
接下來我們要開始設定，告訴sublime我們要使用這個theme。

### Preferences->Settings->User

``` json
{
    "theme": "Afterglow.sublime-theme",
    "color_scheme": "Packages/Theme - Afterglow/Afterglow.tmTheme"
}
```

that's it.

## 額外選項
>在官方的github當中提供了相當多的選擇供大家使用，像是icons, tab padding, 甚至是color scheme都可以選擇，可以到官方的[Github](https://github.com/YabataDesign/afterglow-theme)選擇自己喜歡的樣式。

## 個人化設定
以下是我開發時使用的設定，有興趣的同學可以參考：

### Preferences->Settings->User

#### All
``` json
{
    "caret_style": "phase",
    "color_scheme": "Packages/Theme - Afterglow/Afterglow-monokai.tmTheme",
    "font_face": "Source Code Pro",
    "font_size": 16,
    "highlight_line": true,
    "highlight_modified_tabs": true,
    "ignored_packages":
    [
        "Vintage"
    ],
    "tab_size": 4,
    "theme": "Afterglow.sublime-theme",
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true,
    "sidebar_size_14": true,
    "sidebar_row_padding_medium": true,
    "status_bar_brighter": true,
    "tabs_padding_medium": true,
}
```

在`Browse packages..`資料夾底下建立：（沒有folder請自行建立）

* ubuntu
``` bash
    Theme - Afterglow/schemes/Afterglow.sublime-theme
```

* Mac
``` bash
    /Users/username/Library/Application Support/Sublime Text 3/Packages/Theme - Afterglow/schemes/Afterglow.sublime-theme
```

輸入以下設定：(讓文件編輯時連同檔案名稱一起高亮)
``` json
[
    {
        "class": "tab_label",
        "parents": [{"class": "tab_control", "attributes": ["file_light"]}],
        "attributes": ["dirty"],
        "settings": ["highlight_modified_tabs"],
        "fg": [125, 00, 125]
    },
    {
        "class": "tab_label",
        "parents": [{"class": "tab_control", "attributes": ["file_medium"]}],
        "attributes": ["dirty"],
        "settings": ["highlight_modified_tabs"],
        "fg": [125, 00, 125]
    },
    {
        "class": "tab_label",
        "parents": [{"class": "tab_control", "attributes": ["file_medium_dark"]}],
        "attributes": ["dirty"],
        "settings": ["highlight_modified_tabs"],
        "fg": [255, 161, 52]
    },
    {
        "class": "tab_label",
        "parents": [{"class": "tab_control", "attributes": ["file_dark"]}],
        "attributes": ["dirty"],
        "settings": ["highlight_modified_tabs"],
        "fg": [255, 161, 52]
    }
]
```

### Source Code Pro 字體安裝
>這個字體是由Adobe公司專門出給程式開發者專用的字體，用了之後感覺很不錯。

[Github](https://github.com/adobe-fonts/source-code-pro)

點選`Latest release`下載.zip

將TTF打開，複製裡面的所有檔案，放到指定的路徑下安裝字體。

#### Mac
``` bash
    /Library/Fonts
```
#### ubuntu
``` bash
    當前使用者 home/.fonts
```
ubuntu用戶如果沒有.fonts資料夾請自己用mkdir的方式建立，並修改權限。

重新開啟sublime後，就可以好好享受coding的環境了。
