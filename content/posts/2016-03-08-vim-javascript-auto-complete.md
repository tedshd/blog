---
layout: post
title: 'Vim - JavaScript auto complete'
date: 2016-03-08
comments: true
categories: [Vim]
---
## Vim - JavaScript auto complete

因為同事幾乎都在用 Vim 但我每次都在看他們一直打字我看了就很痛苦 所以就建議他們用 auto complete 的功能, 但我個人因為很少用 Vim 所以就讓他們自己去找套件(我個人不喜歡在 Vim 上裝套件)

但他們似乎都遇到困難 所以我就找了一下找到個不用裝套件又可用在 Linux 和 Mac 上最簡單的 JavaScript auto complete 的方式, 應該是因為 Vim 已經內建了

只要在 .vimrc 設定

```shell
autocmd FileType javascript set omnifunc=javascriptcomplete#CompleteJS
```

使用就是輸入部分關鍵字後先按 `Ctrl + x` 再按 `Ctrl + o` 就可以了

![螢幕快照 2016-03-08 下午12.09.43.png](http://user-image.logdown.io/user/3170/blog/3202/post/604214/Au7OUhnSToG9vmSajeRr_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-03-08%20%E4%B8%8B%E5%8D%8812.09.43.png)

但只支援舊的 JavaScript API

[Refer - How to auto-complete JavaScript syntax in Vim](https://docs.oseems.com/general/application/vim/auto-complete-javascript)

如果要新的得再試別的方法
似乎可以補字庫進去
More

[VIM的JavaScript补全](http://efe.baidu.com/blog/vim-javascript-completion/)
