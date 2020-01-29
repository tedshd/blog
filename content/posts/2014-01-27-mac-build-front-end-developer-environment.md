---
layout: post
title: 'Mac - Build Front End Developer Environment'
date: 2014-01-27
comments: true
categories: [mac]
---
## Mac - Build Front End Developer Environment

趁入手新 Mac 順便重溫一下如何建立給前端攻城獅爽爽用的開發環境
大部分都會涉及 terminal 操作
由於 Mac 是 unix, 基本上 terminal 操作指令都跟 Linux 一樣
[常見的指令](http://tedshd.logdown.com/posts/87094-linux-unix-command)
Mac 上取代預設 terminal 的好物 - [iTerm 2](http://www.iterm2.com/#/section/home)

## 1. 套件與環境

### Xcode 必裝

雖然前端攻城獅幾乎沒什麼人有在同時寫 ios 或 Mac 的 app, 但是還是要裝 Xcode, 不然會有不少東西裝不了(在裝 oh-my-zsh 和 Homebrew 時就被警告了)
<span style="color:red">裝完後至少要先開過一次, 不然會當做沒裝過</span>

### [Homebrew](http://brew.sh/)

Mac 上好用的套件管理工具, 相當於 linux 的 apt-get
用它安裝了 wget 與 git

```shell
brew install
brew uninstall
brew list
brew search
brew update
brew info

// example
brew install wget
brew install git
```

[Mac入门笔记（3）：一键装机](http://www.yangzhiping.com/tech/mac3.html)

### [Git(分散式版本控制系統)](http://git-scm.com/)

這應該是必裝的吧?
下面可參考
[Git 初學筆記 - 指令操作教學](http://blog.longwin.com.tw/2009/05/git-learn-initial-command-2009/)
[版本控制系統Git 精要| ihower 的Git 教室](http://ihower.tw/git/)
git 其實也有具 GUI 的 app 可用, 不過就沒研究了

### [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

有在用 terminal 的都會用到的
雖然以前在用 linux 的時候都是用 bash, 但是個人還是覺得 zsh 好用, 視個人習慣
zsh 附加換 theme 的功能
[themes](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)
找到自己喜歡主題

```shell
vim ~/.zshrc
```

找到 ```ZSH_THEME="candy"``` , 把 candy 換成自己想要的主題名稱
重啟 shell

```shell
source ~/.zshrc
```

常用的 alias

```shell
#mysql
export PATH="/usr/local/mysql/bin:$PATH"

# java
export PATH=/opt/local/bin:/opt/local/sbin:$PATH:/path/to/java/bin

# Short command aliases
alias 'l=ls'
alias 'la=ls -a'
alias 'll=ls -l'
alias 'v=vim'
alias 'rmall=sudo rm *'
alias 'cdw=cd ~/WebServer/Documents'

```

## 2. 開發工具

目前個人是用 Vim 與 sublime 所以大致說明一下

### [Vim](http://zh.wikipedia.org/w/index.php?title=Vim&variant=zh-tw)(Mac 預設)

vi 的進化版, 學過 Linux 的都一定知道 vi
以前不覺得 Vim 有多強, 只認為有 vi 就夠了, 直到 ~~膝蓋中了一箭~~ 要用 terminal 寫 code 才知道它的厲害
Vim 主要依靠 .vimrc 的設定檔來做個人化設定(可以參考網路上別人的設定)
[Vim 小抄 與 入門投影片](http://blog.longwin.com.tw/2010/05/vim-cheatsheet-ppt-learn-2010/)
[大家來學VIM(一個歷久彌新的編輯器)](http://www.study-area.org/tips/vim/index.html)
![Vi-vim-cheat-sheet.png](http://user-image.logdown.io/user/3170/blog/3202/post/177454/mWlvzoATz6t3V0oAWBPl_Vi-vim-cheat-sheet.png)
[Vim 環境設定 - vimrc](http://note.drx.tw/2008/01/vimrc-config.html)
[Macintosh Lion下初试Vim——配置vimrc文件](http://blog.csdn.net/yzhy_ocean/article/details/7272222)
[大家來學VIM（一個歷久彌新的編輯器）[九] set 功能設定](http://www.study-area.org/tips/vim/Vim-9.html)

基本的 .vimrc 設定(.vimrc 存在 ~ 底下)

```shell
" encode
set encoding=utf-8
set fileencodings=utf-8,ucs-bom,shift-jis,gb18030,gbk,gb2312,cp936,utf-16,big5,euc-jp,latin1

" highlight
syntax on

" highlight focus line
autocmd InsertLeave * se nocul
autocmd InsertEnter * se cul

" highlight search
set hlsearch
set incsearch

" 高亮显示对应的括号
set showmatch

" theme
colorscheme torte

" Tab
set tabstop=4

"  indent
set softtabstop=4
set shiftwidth=4

" smart alignment
set smartindent

" auto alignment
set autoindent

" show line number
set number

" history
set history=50

" 在状态行显示目前所执行的命令，未完成的指令片段亦会显示出来
" set showcmd

" 命令行（在状态行）的高度，默认为1,这里是2
set cmdheight=1

" 在编辑过程中，在右下角显示光标位置的状态行
set ruler

" 总是显示状态行
set laststatus=2

" 搜尋不分大小寫
set ic
```

### [Sublime](http://www.sublimetext.com/)

應該算是最多前端攻城獅用的 IDE 吧
[個人設定](http://tedshd.logdown.com/tags/sublime-text)
[Mac 上的一些快捷健](https://gist.github.com/lucasfais/1207002)

### 輔助開發用的 [fire.app](http://fireapp.kkbox.com/)

不管是寫 Haml, CoffeeScript, Sass 還是 HTML, JavaScript, CSS 都可以快速開發, 其中又具備 LiveReload(個人的 LiveReload 是配合 [chrome extension](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei))
也可以針對專案直接起一台 server
讓專案開發可以更快速
不過個人都是用在實驗或搞 prototype 用
[更新更強大的網頁設計師好幫手 Fire.app 基礎篇](http://demo.tc/Post/757)
硬派攻城獅的替代方案 - [YEOMAN](http://yeoman.io/) or [Grunt](http://gruntjs.com/)

## 3. 直接架一台 server 在 Mac 上(非必要)

雖然有許多方式可以在要測 AJAX 行為時起一台 server, 但生為一個懶人還是覺得直接架一個 server 起來用較方便

### Apache

Mac 已內建 Apache

```shell
sudo apachectl start
sudo apachectl stop
sudo apachectl restart
// check apache version
sudo apachectl -v
// or
httpd -v
```

Default server root
```
Library/WebServer/Documents
```

如要改變預設的 root

```shell
vim /etc/apache2/httpd.conf
// find /Library/WebServer/Documents and change it
```

### PHP

Mac 也內建 PHP 了

```shell
sudo vim /etc/apache2/httpd.conf
// find
#LoadModule php5_module libexec/apache2/libphp5.so
// del #
sudo apachectl restart
```

升級 PHP 可參考 [PHP 5.5/5.4/5.3 for OS X 10.6/10.7/10.8/10.9 as binary package](http://php-osx.liip.ch/)

### MySQL

這次 Mac 就沒附了(也可用 Homebrew 裝)
Install MySQL([http://dev.mysql.com/downloads/mysql/5.5.html](http://dev.mysql.com/downloads/mysql/5.5.html))
載 dmg 檔
在要下載時會問說是否要登入或註冊 Oracle 的帳號, 不必理它, 直接點下面小小一行的 **No thanks, just start my download.**
假如出現 **無法打開「mysql5.5.35-osx10.6-x86_64.pkg」, 因為它來自未識別的開發者** 的警告
這時要去 ```系統偏好設定``` -> ```安全性與隱私``` -> ```允許以下來源下載的應用程式``` 改成 ```任何來源``` 即可
設定 MySQL 密碼

```shell
/usr/local/mysql/bin/mysqladmin -u root password 'changepassword'
```

設定環境變數

```shell
vim ~/.zshrc
// add
#mysql
export PATH="/usr/local/mysql/bin:$PATH"
// save and then restart shell
source ~/.zshrc
```

#### Homebrew install

[Refer - Ruby on Rails 實戰聖經](https://ihower.tw/rails4/advanced-installation.html)

[Refer - Setting up a local web server on OS X](https://discussions.apple.com/docs/DOC-3083)

### 設定 virtual host

[Refer - How to set up Virtual Hosts in Apache on Mac OSX 10.10 Yosemite](http://coolestguidesontheplanet.com/set-virtual-hosts-apache-mac-osx-10-10-yosemite/)
