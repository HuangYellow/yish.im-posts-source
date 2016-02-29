title: "Homestead on Ubuntu"
date: 2016-01-02 20:40:18
tags: [laravel,ubuntu,homestead]
categories: Laravel
---

*Update !* new version. 20160102.

<!-- more -->

## 前置
### 安裝virtualbox
``` bash
    $ sudo apt-get install virtualbox
```

### 安裝vagrant
``` bash
    $ sudo apt-get install vagrant
```

*注意：目前用指令下載的vagrant版本是舊版的，當安裝時會出現錯誤，建議從官方網站進行下載安裝。
[官方網站](https://www.vagrantup.com/)

### 升級
``` bash
    $ sudo apt-get update
```

[官方參考](https://laravel.com/docs/5.2/homestead)

## 安裝配置

### 下載最新 laravel/homestead box
``` bash
    $ vagrant box add laravel/homestead
```

如果想要指定 box 版本，可以參考 [選擇指定 Homestead 版本安裝](http://yish.im/2015/11/19/Homestead-version/)

或者是下載失敗，可以透過直接連接的方式進行下載
``` bash
    $ vagrant box add laravel/homestead https://atlas.hashicorp.com/laravel/boxes/homestead
```

>註: 如果你下載失敗後會無法安裝是因為有 temp 卡住，可以參考 這篇 或者是自行到 .vagrant.d/tmp 底下把失敗的 temp 移除重新下載即可。

### clone Homestead
``` bash
    $ cd ~
    $ git clone https://github.com/laravel/homestead.git Homestead
```

### 初始化
``` bash
    $ bash init.sh
```

### 設定 SSH-KEY
``` bash
    $ ssh-keygen -t rsa -C "you@homestead"
```

### 建立對應資料夾
在家目錄(home)下建立 Code 資料夾
使用 `homestead edit` 指令編輯對應
``` bash
folders:
    - map: ~/Code //外層
      to: /home/vagrant/Code //vb裡面路徑
```

### 綁定域名

到 `/etc/hosts`
``` bash
    192.168.10.10  homestead.app
```
## 補充

### 關於如果你是需要在 virtual box 內又要安裝 homestead 說明 :

[問題說明網址](http://stackoverflow.com/questions/22575261/vagrant-stuck-connection-timeout-retrying
Required)

### 如有出現env home的問題
``` bash
cd etc/php5/cli/
sudo nano php.ini
約在line:612
找到variables_order = “GPCS”
修改為variables_order = “EGPCS”
```