title: "Medoo"
date: 2015-04-20 01:53:14
tags: [PDO,Medoo]
categories: PHP
---
前陣子很常使用這個 db framework，覺得很方便也很好用，這邊做一下使用的經驗和用法，如果再沒有framework的情況下要避免像是基本的SQL injection的問題用這個會方便很多。

<!-- more -->

[官方網站](http://medoo.in/)

## 特色
* 非常的轻量 只有 13KB，只需include即可。
* 简单 非常的容易学习，快速上手。
* 强大 支持各种常见的SQL查询。
* 兼容 支持各种数据：MySQL, MSSQL, SQLite。
* 安全 防止SQL注入
* 免费 MIT 协议, 你可以进行任何修改。

一些基礎的CURD都有實作（基於PDO），但由於有時候一些需求的sql query比較複雜，這時候就需要用到自己寫query的狀況。

Medoo有提供類似pdo的`query()`，但這是進行二次封裝後的query，所以他僅支援fetch、fetchall、 fetchcolumn。

你也可以在當中指定格式 像是->PDO::FETCH_ASSOC

使用Medoo二次封裝的函數（如insert, update …）都有在一開始就避免了sql injection的問題，如果是自己query的狀態下則必須使用quote來避免sql injection

>Quote() places quotes around the input string and escapes special characters within the input string.

## 範例
``` php
$db = new Medoo();
$user_id = $db->quote($user_id);
$query = “select * from user where user_id = $user_id”;
$db->query($query)->fetch(PDO::FETCH_ASSOC);
原則上是建議再放置陣列時獨立每個項目
```

此外在導入Medoo時，有幾個地方可以修正

首先將medoo放置在libs當中，這會比較簡單，而且基本上不會去修改medoo

