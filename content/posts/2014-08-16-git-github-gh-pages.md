---
layout: post
title: 'Git - GitHub gh-pages'
date: 2014-08-16
comments: true
categories: [git, github]
---
## Git - GitHub gh-pages

有時在 GitHub 上亂晃
常常發現一個問題就是有一些很有趣的前端實作, 或別人寫的一些功能沒有所謂的 demo page(當然有些是不需要 demo page)
我不知道是把 GitHub 當成備份的 codebase 或是覺得 demo 不重要所以沒放, 又或者是根本不知道要怎麼放
But
這都不重要
其實 GitHub 提供一個 gh-pages 的 branch(或者說是功能)可以讓我們這些前端攻城獅快速的建出個 demo page(<strong style="color:red">但不包含後端功能</strong>)

### 如何使用?

#### 1. 從 master 建出名為 `gh-pages` 的 branch

`git branch gh-pages`

![螢幕快照_2014-08-17_上午12_51_52.png](http://user-image.logdown.io/user/3170/blog/3202/post/220973/Aig3e92WQniG9jC7k6vg_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2014-08-17_%E4%B8%8A%E5%8D%8812_51_52.png)


### 2. 切到 gh-pahes 的 branch

`git checkout gh-pages`

![螢幕快照_2014-08-17_上午12_51_53.png](http://user-image.logdown.io/user/3170/blog/3202/post/220973/pjRYDGZQ6apuuAPzf7Yb_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2014-08-17_%E4%B8%8A%E5%8D%8812_51_53.png)


### 3. 把 gh-pages `git push` 上 GitHub

`git push`

![螢幕快照_2014-08-17_上午12_51_54.png](http://user-image.logdown.io/user/3170/blog/3202/post/220973/P9bJMwV8RledVKws4KBG_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2014-08-17_%E4%B8%8A%E5%8D%8812_51_54.png)

因為剛建出新的 branch, 該 branch 還未在 GitHub 上所以會提示你要用 `git push --set-upstream origin gh-pages`

### 4. 快樂的去 GitHub 拿網址

![螢幕快照_2014-08-17_上午12_55_02.png](http://user-image.logdown.io/user/3170/blog/3202/post/220973/QzdO4XAQ7iYka0DruqTg_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2014-08-17_%E4%B8%8A%E5%8D%8812_55_02.png)

![螢幕快照_2014-08-17_上午12_55_16.png](http://user-image.logdown.io/user/3170/blog/3202/post/220973/kdMyQ6tMQ1SSRBl6Sj9K_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2014-08-17_%E4%B8%8A%E5%8D%8812_55_16.png)

gh-pages 的 url 結構一律都是 http:// + `<GitHub user name>` + .github.io/ + `<repository name>`

### 5. 等等.. 網頁沒東西?

需注意的是該 url root 的 html 必須是 `index.html` 才會出預設的網頁, 其他的檔案路徑都是建立在該 url 上

### 6. Update

其實後續維護不太容易, 必須要熟悉 git 才知道要怎麼做
通常會在 `master` or 切出個 `dev` 來開發, 等開發完在 merge
所以在持續開發時, 要更新 demo page, 就必須要在 gh-pages merge 要更新的 branch

據說好像 grunt 還是 gulp 有套件可以自動 build, 但還沒試驗就是了
