---
layout: post
title: 'CSS4 - 關於 css4 and postcss 的一些想法'
date: 2015-11-20
comments: true
categories: [css, postcss]
---
## CSS4 - 關於 css4 and postcss 的一些想法

### 前言

在年末才來發這篇文...

在今年大家開始瘋 [react](https://facebook.github.io/react/)(咦? AngularJS 勒...), [Babel](https://babeljs.io/), [postcss](https://github.com/postcss/postcss)

好像沒聽過上述這幾個詞就沒法自稱前端工程師(還好我現在都自稱打字員)

到了最近才有空閒研究 postcss 到底在做啥

一開始聽說可以無痛接軌未來(welcome to feature), 不像 [Sass](http://sass-lang.com/) 未來如果要轉換就不好轉換(其實見仁見智啦)

聽起來好潮喔, 但很忙沒時間搭理它

而且這年頭的 tool 都越來越多步驟和許多工具要搞, 除非靜下心來專心研究, 不然哪有時間搞啊(感覺像是逃避的藉口...)

直到了最近自己有些小東西要改, 需要用到變數的功能, 就想到 CSS4 不是有大家夢寐以求的 var() 功能嗎(感覺潮潮的)

就花了點時間研究一下 [postcss](https://github.com/postcss/postcss) 這在 github 的專案

一看下去不得了, 包山包海一卡車功能, 還包含了之前聽別人介紹的連 Sass 的部分寫法的功能都有...

看完的瞬間想翻桌, 只是要寫個 CSS, RD 何苦為難 RD 呢, 我不需要那麼多功能啊~

還好有仔細看到主要 CSS4[<a href="#ps1">註</a>] 是用 [cssnext](http://cssnext.io/) 這專案來處理(網站還用回到未來的梗...)

所以我就果斷使用 cssnext 就好了(我真的很討厭用一套工具還要裝許多套件, 然後有的套件還不一定是你需要的不然就是有套件的部分功能是重複的...)

### gulpfile 設定

現在有一大堆 build tool 像是 [grunt](http://gruntjs.com/), [gulp](http://gulpjs.com/), [browserify](http://browserify.org/), [webpack](https://webpack.github.io/) 等工具

我還是習慣用 gulp, 除非等 gulp 不合需求才會再去看 browserify 或 webpack 怎麼用

```javascript
var gulp = require('gulp');
var cssnext = require('gulp-cssnext');

gulp.task('default', function() {
    gulp.run('css');

    gulp.watch(['./src/**'], function(event) {
        gulp.run('css');
    });
});

gulp.task('css', function() {
  gulp.src('src/*.css')
    .pipe(cssnext({
        compress: true
    }))
    .pipe(gulp.dest('./build/'));
});
```

### 結語

以下為我自己個人看法, 絕對不是要戰網路上的大大和大神們(本魯小弟什麼咖啊)

所以聽聽就好

個人覺得上述講的 postcss 啊, cssnext 啊等等都是在自嗨

大家一定會說:『靠!你什麼咖啊?竟然敢這樣說』

因為我發現有個現實點就是 CSS4[<a href="#ps1">註</a>] 在 W3C 根本還在草案啊(翻桌)

[Selectors Level 4](http://www.w3.org/TR/selectors4/)

連 var() 都還是在編輯中的草案

[CSS Custom Properties for Cascading Variables Module Level 1](https://drafts.csswg.org/css-variables/)

[CSS4 Selectors](http://css4-selectors.com/) 上也說它就是還在草案階段

不了解 W3C 流程的可以看一下 [World Wide Web Consortium Process Document](http://www.w3.org/2015/Process-20150901/)

依 W3C 的進度就知道真的還很遙遠, 真的可能得像回到未來一樣得搭時光車到 30 年後才能用...

所以這不是在自嗨那什麼才是自嗨

如果問我會不會用, 我會說我會玩一下, 但現在應該還不會用在公司的專案上


Refers 就在上述連結中, 所以文末就不附了

<span id="ps1">[註]經友人補充雖然說 CSS4, 但在 W3C 上不這樣說, 它其實是 Selectors Level 4</span>
