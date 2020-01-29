---
layout: post
title: 'Slack - bot 研究雜記'
date: 2016-05-28
comments: true
categories: [slack]
---
## Slack - bot 研究雜記

最近 bot 很夯

再加上公司需要一些自動部署與指令化的一些流程要改善, 所以就來研究一下

剛好我們是用 Slack 所以就先來試試 Slack bot 了

### Intro

先說明下最簡單的指令化處理事件的流程

![bot.png](http://user-image.logdown.io/user/3170/blog/3202/post/734936/S29JhWJdQ6qMF0w2i440_bot.png)

大致上就是如此

再來說明一下 Slack bot 流程

![slack_bot.png](http://user-image.logdown.io/user/3170/blog/3202/post/734936/eDj3Ctc1Rh6U8wVcOI3T_slack_bot.png)

所以我們需要做兩件事

* 在 Slack 建立一支 bot

* 建立 bot client 的程式

在此先說明一下 bot client

Slack bot client 是用 nodejs 寫的, 但基本上會寫 JavaScript 就可以了, 而 bot client 是放在任何可以連上網路的機器, 只要能跑 nodejs 的環境即可, 所以基本上可以先在 local 測完再上到線上的機器

### 建立 Slack bot

[Bot Users](https://api.slack.com/bot-users)

#### 建立 bot

Go to url `https://<your team name>.slack.com/apps/manage/A0F7YS25R-bots`

Add a new configuration

![螢幕快照 2016-05-28 下午10.22.39.png](http://user-image.logdown.io/user/3170/blog/3202/post/734936/rG79uE4iSA2AWLX6EUdm_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202016-05-28%20%E4%B8%8B%E5%8D%8810.22.39.png)

#### 安裝 botkit

[Botkit](https://howdy.ai/botkit/)

依照頁面指示即可見出自己的 Slack bot

### 遇到的問題

在 local 端測試時都很順

在上線時一開始測試也都 ok, 但當我斷開線上環境時卻 GG 了, 我的機器人立刻顯示下線, 這先說一下就是當 bot 啟動時 bot 會顯示上線, 但當 bot 的程式停止時就會在 Slack 顯示離線

在 local 端都沒發現是因為在測試時直接下 `node bot.js` 是直接在前景 run, 但是在用 ssh 時, 在斷開時就會停止執行 node

所以必須把 node 在線上環境執行時是在背景執行

但這又遇到了問題

用 `node bot.js &` 沒用

用 `nohup node bot.js &` 也沒用

最後是靠一個叫 [forever](https://www.npmjs.com/package/forever) 的套件處理才成功的讓 node 在背景執行

接下來就要研究替 bot 加上一些功能了

