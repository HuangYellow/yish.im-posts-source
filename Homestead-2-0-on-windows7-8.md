title: "Homestead 2.0 on windows7/8"
date: 2015-07-28 23:56:06
tags: [laravel,homestead,windows]
categories: Laravel
---
一直以來我開發的環境都是在Ubuntu和Mac當中，最近看到laravel越來越多人投入，但光是環境就讓人打退堂鼓，因此自己試著在windows上裝homestead，以下是安裝過程當中的筆記。

<!-- more -->

## 前置作業
1. 安裝VirtualBox(https://www.virtualbox.org/)
2. 安裝Vagrant(https://www.vagrantup.com/)
3. 重新啟動電腦
4. 安裝git(https://git-scm.com/)

## Cmd
>確認vagrant version

``` bash
$ vagrant -v
```

![cmd](http://i.imgur.com/aRs35I1.png)

### 安裝 Homestead Vagrant box

``` bash
vagrant box add laravel/homestead
```
[官方安裝說明](http://laravel.tw/docs/5.1/homestead#installation-and-setup)

### clone Homestead repo

``` bash
git clone https://github.com/laravel/homestead.git Homestead
```

## Git Bash
(以下操作皆在git bash當中，請各位同學注意)

### 設定對應與站台
cd 到`Homestead`資料夾
``` bash
bash init.sh
```
前往C:\Users\你的使用者名稱
會看到`.homestead`這個資料夾
點進去會看到`Homestead.yaml`
開啟編輯
設定要對應的folders與site
![Homestead.yaml](http://i.imgur.com/tLLuk8j.png)

``` bash
folders: - map: C:\Users\你的使用者名稱\Code
        to: /home/vagrant/Code
sites:
        - map: laravel5.app
        to: /home/vagrant/Code/laravel5/public
```

到`C:\Users\你的使用者名稱` 新增`Code`資料夾

### 產生ssh key
``` bash
ssh-keygen -t rsa -C "you@homestead"
```

cd 到`Homestead`資料夾底下

#### 初始化/產生Vagrantfile

``` bash
$ vagrant init
```
#### 啟動vagrant
``` bash
$ vagrant up
```

#### 連入homestead
``` bash
$ vagrant ssh
```

#### 安裝laravel installer
``` bash
$ sudo composer global require "laravel/installer=~1.1"
```

#### 建立專案
``` bash
$ laravel new laravel5
```

## 本地域名對應
開啟
``` bash
C:\Windows\System32\drivers\etc\hosts
```

加入
``` bash
#homestead
192.168.10.10 laravel5.app
```

拜訪http://laravel5.app
![laravel5](http://i.imgur.com/TXTwVqv.png)
恭喜你完成挑戰!
(備註：如果想離開homestead，只要輸入exit即可)


## 新增站台
>這邊其實跟之前沒有差異，但一樣在這放上新增步驟

### 到.homestead/Homestead.yaml編輯
``` json
sites:
        - map: test002.app
        to: /home/vagrant/Code/test002/public
```

編輯
``` bash
C:\Windows\System32\drivers\etc\hosts
```

加入
``` bash
#homestead
192.168.10.10 test002.app
```

### Git Bash
#### 關閉vagrant
``` bash
$ vagrant halt
```

#### 重新啟動vagrant provision
``` bash
$ vagrant up --provision
```

#### 連入vagrant
``` bash
$ vagrant ssh
```

cd Code/

#### 建立專案
``` bash
$ laravel new test002
```

that's it.


Ref:https://phphub.org/topics/1106