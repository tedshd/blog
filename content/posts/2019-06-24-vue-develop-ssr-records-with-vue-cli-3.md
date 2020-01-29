---
layout: post
title: 'Vue - 使用 Vue cli 3 開發 SSR 紀錄'
date: 2019-06-24
comments: true
categories: [Vue]
---
## Vue - 使用 Vue cli 3 開發 SSR 紀錄

### Intro

因為工作需求需要一個能夠 SSR 的工具

由於是接手別的團隊回來的程式也剛好要做大動作的重構(打掉重練

之前的團隊是使用 koot.js

個人花了點時間看了一下還不錯, 但是

1. 對 react 不太熟

2. 居然還是用 less, 我在 2017 就已經捨棄使用預處理器來處理樣式了, 擁抱 CSS L4

3. 還是比較喜歡 Vue 的架構

所以就心痛的來研究一下 Vue cli 處理 SSR 的方式

官方有文件

[Vue.js 服务器端渲染指南](https://ssr.vuejs.org/zh/)

看完以後

恩...

好麻煩啊

使用工具和 framework 的目的就是要無腦使用啊

還要寫一大堆 code 幹嘛

這邊先列出自己的需求

1. SSR 而且需要是 [Universal](https://blog.v123582.tw/2016/04/03/不可不知的前端趨勢-Isomorphic-與-UniversalJS/) 的處理方式

2. 在樣式能夠使用 postcss 處理 CSS L4

3. 能夠處理 Metadata

4. 能夠把環境需求用設定處理掉或根本不用設定就處理掉

5. 因為工作需求需要多語系..

6. 最好是要有 PWA

所以就開始了痛苦的尋找之旅

### Result

#### 使用 [vue cli](https://cli.vuejs.org)

之前從第一版就開始在使用了, 所以算是比較熟的, 且學習成本低

跟 react 比我比較喜歡 vue 的寫法

且到了第三版的現在已經越來越成熟且方便設定

還有自己的生態圈

插件可以方便找查與安裝

**第 6 點滿足**

#### 使用 [vue-cli-plugin-ssr](https://github.com/Akryum/vue-cli-plugin-ssr)

這個用 vue ui 在找 plugin 時有不少人用

預設不用設定

在開發時就可以直接把 vue 轉成 SSR 輸出來看很方便(寫一套就自動幫你處理好 SSR & CSR)

**第 1 點滿足**

#### 處理非同步資料 client & server side

[Data Pre-Fetching and State](https://ssr.vuejs.org/guide/data.html#data-store)

主要就是先處理 API 然後 response 回來的資料放到 store 裡

這邊可以結合 [axios](https://github.com/axios/axios) 去使用

#### 處理 Meta data

這比較麻煩

除了要 SSR 以外必須也需要能在 CSR 一起處理掉

有一個套件蠻多人推的是 [vue meta](https://github.com/nuxt/vue-meta)

但是在搭配上述的 `vue-cli-plugin-ssr` 時, vue meta 的 SSR 設定是不 work 的

有人開了 [issue](https://github.com/Akryum/vue-cli-plugin-ssr/issues/33) 但是被擺很久了...

其實很多套件都可以處理 SSR 和 CSR 的 meta tag

但是在跟 [vue-cli-plugin-ssr](https://github.com/Akryum/vue-cli-plugin-ssr) 搭配時都遇到個問題就是當 meta 資訊是從後端動態來的話就不行了

因為從 api 來的話要在 SSR 處理必須要在 vue component 中的 `serverPrefetch` 先處理 async 回來的動作

然後把 API 拉回來的資料放到 store 中處理才能讓 SSR 處理時有資料

但是 meta tag 的資訊很不好處理

必須要遵循以下文件中的方式

[Head Management](https://ssr.vuejs.org/zh/guide/head.html)

但是試過用 mixin 沒法處理 meta 上的 case...

如果把 meta 的資料獨立 API 處理也許有機會

最後只好自己寫個 function 做 hack 的處理

在 `computed` 做了一個 init 的 function 來處理建立 metadata

但是目前這 function 處理 CSR 的部分還不算太 ok, 因為自己目前都是動態砍掉 HTML DOM 在重建 DOM 會有些微效能上的問題

#### 樣式處理

Vue 採用 CSS module 的設計

Vue cli 使用了 CSS Loader

但是個人其實不是很喜歡使用 CSS module 的方法

因為它是採用動態處理 style 的方式

在某些 case 底下會造成 UI 大量重繪

這在畫面上體驗很差

除非自己做一個 loading 處理掉這問題

再加上如果要使用 CSS L4 feature 得有些調整

最後使用 [postcss-import](https://github.com/postcss/postcss-import)

就可以維持用 CSS loader 且在使用 import 可以適當的使用 CSS L4 而且是可以做簡單的模組化

#### 使用 [vue-cli-plugin-i18n](https://github.com/kazupon/vue-cli-plugin-i18n)

切換語系

[语言环境变更](https://kazupon.github.io/vue-i18n/zh/guide/locale.html)

這部分還沒試驗

#### device detect

這套健在 `vue-cli-plugin-ssr` 底下無痛使用可以在 SSR 的情況就處理依照 UA 判斷 device

[mobile-device-detect](https://github.com/duskload/mobile-device-detect)

### 目前情況

這些解決方案目前還沒用在線上環境

主要因為發現接回來的東西根本沒必要那麼的費工

加上合適的新專案喊停了

所以目前還是在研究階段

有興趣這邊有研究一下我目前正在研究用的 prototype

[ssr](https://github.com/tedshd/vue_ssr)
