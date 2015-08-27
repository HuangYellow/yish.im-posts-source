title: "Homestead 2.0 on Ubuntu"
date: 2015-03-22 17:03:18
tags: [Laravel,Ubuntu]
categories: Laravel
---

>新版本的homestead在安裝上與之前差異其實沒有很大，但是我還是不爭氣的卡關，後來終於解決了，原則上比較會出現問題的地方是ubuntu官方提供的vagrant是舊版的，必須自己去官方下載安裝才能執行，然後在add box這段冗長的加入過程中有可能會因為網路不穩出現檔案損毀的問題，以及最後如果你是virtualbox內安裝ubuntu，然後ubuntu裡面又安裝homestead很抱歉的你會卡在rsa_key過不去，因為你沒有虛擬化技術VT-x/AMD-V。

[問題說明網址](http://stackoverflow.com/questions/22575261/vagrant-stuck-connection-timeout-retrying
Required)

##前置
`安裝virtualbox`
``` bash
sudo apt-get install virtualbox
```

`安裝vagrant`
``` bash
sudo apt-get install vagrant
```

*注意：目前用指令下載的vagrant版本是舊版的，當安裝時會出現錯誤，建議從官方網站進行下載安裝。
[官方網站](https://www.vagrantup.com/)

`升級`
``` bash
sudo apt-get update
```

[官方參考](http://laravel.tw/docs/4.2/homestead)

``` bash
virtualbox add vagrant
vagrant box add laravel/homestead
```


`安裝composer`
``` bash
cd /home/username
sudo curl -sS https://getcomposer.org/installer | php
```

`*注意：如果出現缺少，可以輸入`
``` bash
sudo apt-get install curl
sudo apt-get install php5-cli
```

`移動composer`
將composer.phar移動到`usr/local/bin`，讓他變成全域指令
``` bash
sudo mv composer.phar /usr/local/bin/composer
```


##安裝
``` bash
composer global require "laravel/homestead=~2.0"
```
跑完後會在`home/username` 發現`.composer`這個資料夾

接下來把路徑寫入
``` bash
sudo nano .bashrc
export PATH=~/.composer/vendor/bin:$PATH
```

###非常重要：重新啟動terminal

`初始化`
``` bash
homestead init
```

`產生key`
``` bash
ssh-keygen -t rsa -C "your@email.com"
```
然後依據需求在填問題（但建議直接enter過去就可以了）

*注意：原先`Homestead`是直接放在`home`底下，現在則是`.homestead` 所以`Homestead.yaml`也放在裡面了


##建立mapping folder:Code資料夾
folders:
``` bash
 -map:~/Code
 to /home/vagrant/Code
```
在home底下建立`Code` folder

``` bash
mkdir Code
sudo chmod -R 777 Code/
```

`編輯hosts`
``` bash
cd /etc
sudo nano hosts
```
`加入域名`
``` bash
192.168.10.10 homestead.app
```

`啟動homestead`
``` bash
homestead up
```
##補充
`如有出現env home的問題`
``` bash
cd etc/php5/cli/
sudo nano php.ini
約在line:612
找到variables_order = “GPCS”
修改為variables_order = “EGPCS”
```