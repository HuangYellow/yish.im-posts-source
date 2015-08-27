title: "Markdown Support: Parsedown"
date: 2015-03-25 12:01:12
tags: [Laravel,Markdown]
categories: PHP
---
>Markdown是目前世界上最流行的編輯器之一，當然市面上很多選擇，但還是想要自己製作的話必須要有轉換才有辦法使用markdown的語法，Parsedown就是用於轉換的package.

[official](http://parsedown.org/)
[Github](https://github.com/erusev/parsedown.git)

##安裝
`composer.json`
``` json
"erusev/parsedown": "1.5.1"
```

##使用

###寫入
``` php
$parsedown = new Parsedown();

$parsedown->setMarkupEscaped(true)->text($data['description']);
//setMarkupEscaped是跳脫字元，他會將code的一些字元轉換成html
```
###讀取
``` php
$parsedown = new Parsedown();

$parsedown->parse($data['description']);
//parse 解析
```

that's it.