layout: not
title: "Laravel : command not found on Homestead 2.0"
date: 2015-04-23 19:41:34
tags: [Laravel,Homestead]
categories: Laravel
---
>這篇其實是先前觀念不清楚而導致認知錯誤，筆記一下。

##引發的錯誤
在安裝homestead時我以為他裡面很智能的幫我裝了laravel也就是這行指令
``` bash
composer global require "laravel/installer=~1.1"
```

直到我剛剛想說來安裝laravel5來試試看，使用了
``` bash
laravel new project_name
```

結果噴出這個錯誤
``` bash
laravel: command not found
```
##解決
看了一下之後發現原來homestead雖然把路徑寫入了，但預設是沒有安裝 `laravel/installer`的
也就是說一樣要到homestead裡面
``` bash
composer global require "laravel/installer=~1.1"
```

終於可以高速建專案了....

##Extra
剛剛發生一個很特別的狀況
``` bash
laravel new project_name
```
會發生一個錯誤，就是key產生不出來
``` bash
[UnexpectedValueException]
Could not parse version constraint ^1.2.2: Invalid version string "^1.2.2"
```

後來才發現是自己的composer太久沒更新...
跑一次
``` bash
composer self-update
```
重新跑專案就會產生了
``` bash
Application key [一段亂數產生的key] set successfully.
```