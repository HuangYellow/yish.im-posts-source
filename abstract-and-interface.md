title: "abstract and interface 抽象與介面"
date: 2015-05-25 21:04:48
tags: PHP
categories: PHP
---
前陣子去PHP也有DAY時有幸聽到Sean Liu大的講解OOP的基礎結構，覺得相當棒，所以也寫了一篇關於interface與abstract的demo，希望能幫助剛入門的同學快速進入結構化的PHP。

<!-- more -->

首先，我們必須搞清楚`interface`, `abstract`的關係：

* `interface`這是一個制定規範的規範說明文件。
* `abstract`定義一個類別所需要的抽象類。

嗯...看不懂？
我想應該也是正常的，我一開始也是看不懂這是什麼XD

用實際例子來進行說明吧！

## 範例
首先，我要做一個知道哪些鳥類會飛、速度是多少，所以我們可以創立一個interface來說明寫進來的鳥都必須要具備兩種能力，`會飛`, `飛的速度`。

``` php
interface flyInterface
{
    public function fly();
    public function speed();
}

```

接下來，我要定是哪個類別具有這些能力，因此我建立`bird`這個`class`，並且規定鳥類都必須是要會飛、以及速度。

``` php
class bird implements flyInterface
{
    public function fly()
    {
        return "Yes, I can fly";
    }

    public function speed()
    {
        return "50";
    };
}

```

ok, 接下來我們會遇到一個狀況，就是如果這樣寫的話，每隻鳥的速度就都一樣了，這不合理，對吧？我希望的結果是由每種鳥來自己定義自己的飛行速度，也因此要將function改為抽象，讓繼承鳥這個類別的鳥種能夠有自訂飛行速度的能力。

``` php
abstract class bird implements flyInterface
{
    public function fly()
    {
        return "Yes, I can fly";
    }

    abstract public function speed(); //由繼承的類別實作他
}

```

看起來很棒，對吧？接下來我們就可以快樂的建立`麻雀`這個類別，並且繼承他是鳥類的類別，也就是說他會飛、但飛行速度必須自訂。


``` php
class Sparrow extends bird
{
    public function speed()
    {
        return "30";
    }
}
```

所以當我執行以下程式時，我就會得到我想要的效果：

``` php
$Sparrow = new Sparrow(); //新增一隻麻雀
echo $Sparrow->fly().", ".$Sparrow->speed(); //output:Yes, I can fly, 30
```

看起來運作得很不錯，那麼當我要新增`老鷹`時，我只需要這樣做：

``` php
class Eagle extends bird
{
    public function speed()
    {
        return "100";
    }
}
```
嗯...試試看。

``` php
$Eagle = new Eagle(); //新增一隻老鷹
echo $Eagle->fly().", ".$Eagle->speed(); //output:Yes, I can fly, 100
```

## 範例-2

首先，我們有兩個類別，分別是`human`, `animal`，並且我希望能夠將他們分門別類並且讓他們有各自的能力，依照剛剛的做法，我們應該會製作兩個`class`來先做種類分類。

``` php
abstract class Human
{
    public function run()
    {
        return "I can run";
    }

    public function talk()
    {
        return "I can talk";
    }

    abstract public function sex();
}


abstract class Animal
{
    public function jump()
    {
        echo "I can jump";
    }

    public function eat()
    {
        echo "I can eat";
    }
}
```

這時候問題產生了，我要規定`human`與`animal`的interface，但我發現，如果是像範例1這樣做的話，人類明明也會jump與eat，畢竟人類也是動物演化來的嘛，因此我先定義兩個`interface`

``` php
interface HumanInterface
{
    public function run();
    public function talk();
    public function sex();
}

interface AnimalInterface
{
    public function jump();
    public function eat();
}
```

這次，我這樣寫：
``` php

//Mary是人類，並且擁有人類能力與動物能力
class Mary extends Human implements HumanInterface, AnimalInterface
{
    //將抽象method實現
    public function sex()
    {
        return "I am girl";
    }

    //由於implements AnimalInterface，必須實現AnimalInterface的能力
    public function jump()
    {
        return "I am human, but I can jump";
    }

    public function eat()
    {
        return "I am human, but I can eat too";
    }
}

```

看起來完美極了，接下來驗證想法：
``` php
$Mary = new Mary();
echo $Mary->run(); // I can run
echo $Mary->talk(); // I can talk
echo $Mary->sex(); // I am girl
echo $Mary->jump(); // I can jump
echo $Mary->eat(); // I can eat
```

以上範例希望有幫助。

enjoy it.
