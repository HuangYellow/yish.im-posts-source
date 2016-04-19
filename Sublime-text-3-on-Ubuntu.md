title: "Sublime text 3 on Ubuntu"
date: 2015-03-22 17:01:10
tags: [sublime,ubuntu]
categories: Sublime
---

剛剛嘗試將ubuntu的st2升級至st3，果然還是會遇到一些問題，但還好很快就解決了，以下是安裝的過程和紀錄。

<!-- more -->

## Package control

[package control](https://packagecontrol.io/installation#st3)

打開ST3，按下`ctrl` + `~`開啟console(View->show console)

將剛剛取得的安裝code貼上，按下`enter`

``` bash
import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

有了package control接下來就可以安裝很多套件了。

## 中文解決方案（Inputhelper)
>由於ubuntu的ibus輸入法不支援在ST上輸入中文（ST2也是），還好有人寫出套件來解決這個問題。

*如果你是藉由剛剛的`package control`安裝時會有問題，是因為packages的路徑不對，所以必須自己clone，解決方案如下。

將目錄切換到->`usr/username/.config/sublime-text-3/Packages`

``` bash
git clone https://github.com/xgenvn/InputHelper.git
```

大功告成！現在同時按下`ctrl` + `shift` + `z`會彈出Input helper的輸入框，enjoy it！