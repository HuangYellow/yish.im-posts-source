title: "選擇指定 Homestead 版本安裝"
date: 2015-11-19 20:22:22
tags: [Laravel,Homestead]
categories: Laravel
---
![homestead-version](http://i.imgur.com/k08ez7M.png)

日前 Homestead 版本更新加入了 MySQL 5.7 及 Node 5.0，有可能會因為一些特殊的需求以及原因會想要安裝原有或舊版的 MySQL 及 Node，當然你可以透過移除 image 內的 MySQL 及 Node，但其實可以透過指定版本號的方式裝回原有的 image。

<!-- more -->

你可以在 [atlas homestead](https://atlas.hashicorp.com/laravel/boxes/homestead) 當中找到你所需要的 homestead image，舉例來說，開始支持 MySQL 5.7 及 Node 5.0 的 homestead 版本是`v0.3.1`，如果你需要的是 MySQL 5.6 以及 舊版 Node 可以選擇以下的版本，例如 `v0.2.5`。

接下來如果你已經升級成新版本（例如：`v0.3.3`），必須先移除原有的box：
``` bash
    $ vagrant box remove laravel/homestead
```

>請注意：如果你是透過升級的方式進行安裝 homestead，你可能會擁有多個 box，在輸入移除時會出現錯誤，只要依照他的說明進行指定版本的逐步移除就可以了。

接下來，我們可以透過指定版本的方式進行安裝指定的 homestead box：
``` bash
    $ vagrant box add laravel/homestead --box-version 0.2.5
```

>注意：不能用 `sudo` 安裝會把 owner 改成 root。

等待安裝後，就會是指定版本的 homestead了。

## Extra
在進行 box download 時，有可能因為網路問題導致下載中斷，而導致無法再度下載，其實只要移除`tmp`內的檔案就可以了，詳細路徑如下（ubuntu）：
``` bash
    $ /.vagrant.d/tmp
```
移除掉 `boxXXXXXXXXXXXXXXXXXXXX`開頭的檔案即可。

如果說 `homestead up` 時出現以下錯誤：
``` bash
    ==> default: Importing base box 'laravel/homestead'...

    ==> default: Matching MAC address for NAT networking...

    A VirtualBox machine with the name 'homestead' already exists.

    Please use another name or delete the machine with the existing

    name, and try again.
```
目前我這邊的解法是打開 virtual box 的介面，將原有 homestead 重新命名，如 homestead_old，再度重新執行 `homestead up`，再將原有的 homestead_old 移除即可。

或者是你可以參考[這篇blog](http://www.cnblogs.com/huangye-dream/p/4604973.html)的解法：
``` bash
    $ VBoxManage unregistervm homestead --delete
```
