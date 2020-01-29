---
layout: post
title: '‎Sublime Text - Plug-In'
date: 2013-09-02
comments: true
categories: [sublime-text]
---
## Plug-In

**Install by Package Control**

Fisrt use sublime need install Package Control
Ctrl + ~
show command line
enter
```sh
import urllib2,os; pf='Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),'wb').write(urllib2.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read()); print 'Please restart Sublime Text to finish installation'
```
restart sublime
finish

### ZenCoding
### jsFormat
讓 js 整齊
ctrl + alt + f
[GitHub](https://github.com/jdc0589/JsFormat)
### SublimeTmpl
載入預設的樣板
### [Emmet](http://docs.emmet.io/)
快速輸入
### Gist
### BracketHighlighter
### Themes

* Dayle Rees Color Schemes
* Farzher
* [Fox](https://sublime.wbond.net/packages/Theme%20-%20Fox)

### sublime-jslint
[GitHub](https://github.com/fbzhong/sublime-jslint)
```json
{
    // Path to the jslint jar.
    // Leave blank to use bundled jar.
    "jslint_jar": "",

    // Options pass to jslint.
    "jslint_options": "--continue --nomen --regexp --sloppy",

    // Ignore errors, regex.
    "ignore_errors":
    [
        // "Expected an identifier and instead saw 'undefined' \(a reserved word\)"
    ],

    // run jslint on save.
    "run_on_save": true,

    // debug flag.
    "debug": false
}
```
### javascript and jQuery API Completions
[GitHub](https://github.com/slene/Sublime-JavaScript-API-Completions)
### Better Completion
### PHPLntel
### SublimeLinter
[SublimeLinter-for-ST2](https://github.com/SublimeLinter/SublimeLinter-for-ST2)
```javascript
"sublimelinter_popup_errors_on_save": true
"sublimelinter_mark_style": "fill"
"sublimelinter_gutter_marks": true
```
### ColorPicker
調色盤
[GitHub](http://weslly.github.io/ColorPicker/)
### SCSS
[GiHub](https://github.com/MarioRicalde/SCSS.tmbundle)
### SFTP
利用 SFTP 連 server
[Sublime SFTP](http://wbond.net/sublime_packages/sftp)
### DocBlockr
加強添加注釋
/** 按 ```tab```
[GitHub](https://github.com/spadgos/sublime-jsdocs)
### ASCII-Decorator
利用 ASCII 文字當注釋
選擇要轉的文字後, 選選單的 Edit -> ASCII-Decorator, 就會轉換了
[GitHub](https://github.com/viisual/ASCII-Decorator)
### Bootstrap 3 Snippets
[GitHub](https://github.com/JasonMortonNZ/bs3-sublime-plugin)
### Marking Changed Rows
[GitHub](https://github.com/Harurow/sublime_markingchangedrows)
### ColorHighlighter
顯示 HEX 顏色
[GitHub](https://github.com/Monnoroch/ColorHighlighter)
### AlignTab
對齊 :, =, ...
[GitHub](https://github.com/randy3k/AlignTab)
### Find Function Definition
找到 function 定義的位置
[Find Function Definition](https://sublime.wbond.net/packages/Find%20Function%20Definition)
### sublimetext-markdown-preview
Preview Markdown 文件
[sublimetext-markdown-preview](https://github.com/revolunet/sublimetext-markdown-preview)
### sublimeBookmark
可以 mark line, 方便臨時標記找 code
[sublimeBookmark](https://github.com/bollu/sublimeBookmark)

### CSS format
[CSS Format](https://packagecontrol.io/packages/CSS%20Format)

## Sublime text 3

### JSLint
[JSLint](https://github.com/73rhodes/Sublime-JSLint)

### JSHint
[jshint](https://github.com/jshint/jshint)

### sublimeLinter

### SublimeLinter-annotations
highlight TODO, README and FIXME
[SublimeLinter-annotations](https://github.com/SublimeLinter/SublimeLinter-annotations)
