title: "Material Theme on sublime text 3"
date: 2015-06-23 02:04:21
tags: [Theme,Sublime]
categories: Sublime
---
>日前在facebook跟laracasts上面看到很多人使用這個theme，感覺看起來很不錯，就順手安裝了一下，整體感覺很棒，也自己客製化了一些設定，以下是設定與步驟。

![material theme](https://camo.githubusercontent.com/9d75018f2674b0cf1919e4636c9751b3d7fa41ab/687474703a2f2f657175696e75736f63696f2e6769746875622e696f2f6d6174657269616c2d7468656d652f6173736574732f6d6174657269616c7468656d652e706e67)

##Installation

* [安裝Package Control(必要)](http://yish.im/2015/03/22/Sublime-text-3-on-Ubuntu/)

* Install package->Material Theme

* 重新啟動sublime

當然你也可以透過[github](https://github.com/equinusocio/material-theme)來安裝。

##Settings
接下來我們要開始設定，告訴sublime我們要使用這個theme。

###Preferences->Settings->User

```
{
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
    "theme": "Material-Theme.sublime-theme"
}
```

that's it.

###已知bug
在官方的document當中，[issue](https://github.com/equinusocio/material-theme#known-issues)，假如在搜尋或者取代時看不到下面的input，只要輕輕把他往上拉一下就可以看到了。

##個人化設定
以下是我開發時使用的設定，有興趣的同學可以參考：

###Preferences->Settings->User

####Ubuntu
```
{
    "caret_style": "phase",
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
    "translate_tabs_to_spaces": true,
    "font_face": "Monaco",
    "font_size": 16,
    "highlight_line": true,
    "highlight_modified_tabs": true,
    "ignored_packages":
    [
    "Vintage"
    ],
    "tab_size": 4,
    "theme": "Material-Theme.sublime-theme",
    "trim_trailing_white_space_on_save": true
}
```
####Mac
```
{
    "caret_style": "phase",
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
    "theme": "Material-Theme.sublime-theme",
    "font_size": 17,
    "highlight_line": true,
    "highlight_modified_tabs": true,
    "ignored_packages":
    [
        "Vintage"
    ],
    "tab_size": 4,
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true
}
```

此外，我覺得他的側欄字實在太過小了，也因此修改了當中的字體和存檔時的顏色
在`Browse packages..`資料夾底下建立：（沒有folder請自行建立）
```
    Material Theme/schemes/Material-Theme.sublime-theme
```
輸入以下設定：
```
[
    {
        "class": "sidebar_label",
        "font.size": 16
    },
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
[references](http://stackoverflow.com/questions/14685989/sublime-to-change-color-of-highlight-modified-tabs)
