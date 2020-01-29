---
layout: post
title: 'AMP - Accelerated Mobile Pages 研究筆記'
date: 2017-02-24
comments: true
categories: [AMP]
---
## AMP - develop log

### Intro

這是針對對 AMP 有基本概念的筆記, 基本概念請去 [amp project](https://www.ampproject.org) 看就好

知道 AMP 是啥的再來看這文章會較有用

-- 我是分隔線 ---

會被 cache 在 Google domain 下

更新分主動 / 被動

主動(跟 Google 說該頁面有更新)

被動(當有任何人開啟該 AMP 頁面, Google 會在背後重新跟該頁面 AMP url 重新拉來 cache,但 15s 內不重新拉)

### 限制

1. 廣告問題(需第三方有支援的廣告商, amp-ad 中有支援的)

2. AJAX cross domain 問題(需 server side allow)

3. Cookie 讀不到

4. user login 問題(需使用 AMP 的元件)

5. App Indexing on Google Search & AMP 衝突(Google 正在解這問題)

6. 不能跑 JavaScript, 所以你的 AMP 頁面不能有自己的 JavaScript code(這很這重要)

可以先看一下 AMP 的規範

[AMP HTML Specification](https://www.ampproject.org/docs/reference/spec)

先把這些問題與情況列出來, 覺得 ok 再往下看

**使用新技術一定有風險, 技術使用有賺有賠, 使用前應詳閱文件或他人心得.**

這裡會稍微講一下文件中沒提到的一些東西或技術背景, 但沒去挖 source code, 所以只會說明解決了啥問題, 不會涉及技術實作

如有錯誤歡迎指正

### Google 如何知道有 AMP 的頁面

使用 `<link>` tag

在非 AMP 頁面使用

```HTML
<link rel="amphtml" href="https://www.example.com/url/to/amp/document.html">
```

在 AMP 頁面使用

```HTML
<link rel="canonical" href="https://www.example.com/url/to/full/document.html">
```

以下文章有說明

[Prepare Your Page for Discovery and Distribution](https://www.ampproject.org/docs/get_started/create/prepare_for_discovery)

### 基本 AMP 結構

```
<!doctype html>
<html amp lang="en">
  <head>
    <meta charset="utf-8">
    <script async src="https://cdn.ampproject.org/v0.js"></script>
    <title>Hello, AMPs</title>
    <link rel="canonical" href="http://example.ampproject.org/article-metadata.html" />
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
    <script type="application/ld+json">
      {
        "@context": "http://schema.org",
        "@type": "NewsArticle",
        "headline": "Open-source framework for publishing content",
        "datePublished": "2015-10-07T12:02:41Z",
        "image": [
          "logo.jpg"
        ]
      }
    </script>
    <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
  </head>
  <body>
    <h1>Welcome to the mobile web</h1>
  </body>
</html>
```

裡面有個有趣的地方就是 `<style>` 的部分

因為 amp project 的 js 有處理 amp component, 會影響 UI 渲染, 所以會先讓畫面不可見

但實際上是不會那麼慢, 因為 js 提前處理完就會顯示

[Refer - Create Your AMP HTML Page](https://www.ampproject.org/docs/tutorials/create/basic_markup)

### Style

使用 `<style amp-custom>` 來放置 style

* 一個頁面只能有一個 tag

* size 須小於 50k

可參考

[Supported CSS – AMP](https://www.ampproject.org/docs/guides/responsive/style_pages)

### AMP Components

[Components / Tags – AMP](https://www.ampproject.org/docs/reference/components)

### Analytics

AMP 有自己的 GA 使用方式

是以 `<amp-analytics>` 的 component 呈現

而非使用 js 的 `ga()` 來處理

不用這個用一般網頁用的 `ga()` 的話 GA 是送不出去的(這跟 Google 確認過了)

基本範例

```html
<amp-analytics type="googleanalytics">
<script type="application/json">
{
    "vars": {
        "account": "UA-XXXXXX-X"
    },
    "triggers": {
        "trackPageview": {
            "on": "visible",
            "request": "pageview",
            "vars": {
                "title": "<?php echo htmlspecialchars($title); ?>",
                "documentLocation": "<?php echo $site_url; ?>"
            }
        }
    }
}
</script>
</amp-analytics>
```

目前有個很大的問題就是

針對 DOM 的事件每一個都需要用到對應的 `<amp-analytics>`

所以舉例來說

當有一個 list 有 10 個 items 要記錄點擊的 GA, 那就要出現 10 個 `<amp-analytics>`

(這 issue 目前 Google 內部有再討論是否要處理)

所以是直接把 `<amp-analytics>` 包成一個 functiuon 來處理較方便(server side render 的話)

`<amp-analytics>` 是可以動態產生的

但需要注意的是當 `<amp-analytics>` 能夠被 js parse 下來處理的時候

**對應的 DOM 必須在頁面上可見的**, 且是非藏起來不可見的, 不然 GA 是不會運作的

具體可以參考以下文件

[Adding Analytics to your AMP pages](https://developers.google.com/analytics/devguides/collection/amp-analytics/)

關於 AMP 與非 AMP 的 GA 數據可以在`維度` 中`使用者`的`資料來源` 中區分出來

<img src="https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-08-28%20%E4%B8%8B%E5%8D%8812.42.10.png?alt=media&amp;token=5ac3278c-44e3-464c-b2bf-58d0fcd6b548">

可以使用自訂區隔處理會比較好看數據

不建議另外用一個 ga-id 因為 ga session 會斷掉(ga id 不同, 資料的完整性不夠)

但目前也有這問題(跨 AMP 到 non-AMP)

所以要解決從 AMP 到 non-AMP oogle 提出以下解法

[Set up Google AMP Client ID API](https://support.google.com/analytics/answer/7486764)


[AMP vs non-AMP traffic](https://developers.google.com/analytics/devguides/collection/amp-analytics/#amp_vs_non-amp_traffic)


### AMP 目的與目標

加速 mobile page 速度(廢話

那具體上 AMP 有處理哪些東西

我這會列舉一些我有注意到的部分, 但實際上應該還有不少我沒注意到的, 畢竟沒有把所有的東西都試一遍

#### Style

當然能繼續使用 `<link>` 去載入你的 CSS

但發現在一些情境下會發生 CSS 被延後載入(這應該是跟 amp 的 js 的機制有關, 他不會先處理非同步載入的 CSS

我遇到的 case 是當我加上 `<amp-analytics>` 後就這樣了

但也不是沒解法

解法就是直接用 `<style amp-custom>` 直接包你的 CSS 樣式

不用 `<link>` 載入 CSS

讓它一起進入 amp 的 js 的處理

但要注意的是**一頁只能有一個 `<style amp-custom>`**

[Style & Layout](https://www.ampproject.org/docs/guides/responsive_amp)

#### Placeholders & fallbacks

AMP 針對圖片有處理 Placeholders 和 fallback

讓使用者輕鬆使用

[Placeholders & fallbacks](https://www.ampproject.org/docs/guides/responsive/placeholders)

#### `<amp-img>`

為何要用 `<amp-img>` 並非使用 `<img>` 就好

* 只對第一屏的圖做請求

* 處理延遲載入(lazy load)

[Include Images & Video](https://www.ampproject.org/docs/guides/amp_replacements)

#### `<amp-app-banner>`

這更好用了

這是針對有 app link 的服務

以前有類似的像 [branch.io](https://branch.io/)

但聽使用過的人說還是有機率會 fail

iOS 有 smart banner(雖然不錯, 但不理想, user 關掉後再也不會出現, 對 user 而言很合理, 但對服務來說不太想要這樣

Android 得自己幹

但這元件就是 branch.io 這服務要做的事, 然後 AMP 幫你做了

他的機制是當你有設定 app link 時他會 parse 分析出來並出 banner 來提示 user 用 APP 開或到 Google Play 或 Apple store

### Validate AMP

1. Add `#development=1` on url and open browser develop tool console tab.

2. Web tool [validator.ampproject.org](https://validator.ampproject.org/)

3. Browser extension [Chrome](https://chrome.google.com/webstore/detail/amp-validator/nmoffdblmcmgeicmolmhobpoocbbmknc) or [Opera](https://addons.opera.com/en-gb/extensions/details/amp-validator/)

[Validate AMP Pages](https://www.ampproject.org/docs/guides/validate)

[AMP 測試 - Google Search Console](https://search.google.com/test/amp)

**千萬要記住有任何 error 的話 Google 都不會 cacahe 成 AMP**

### AMP & App Indexing on Google Search

有 AMP 出現後不會出現 App Indexing on Google Search

Google 說這是 **Bug**

基本上 Google search result 是要 AMP 和 App Indexing on Google Search 都出現

Google 正在修這個問題

### 結語

就目前看到搜尋結果的情況

~~隨然 Google 沒有明示, 但很明顯 AMP 的搜尋結果有都被排在前面~~

~~所以整體來說對排名還是有影響的~~

**更新**

跟 Google 證實了一下, 不影響 rank, 所以是不影響 SEO 排名

為什麼會有這假象, Google 說了可能是因爲原本的頁面 SEO 太爛, 因為 AMP 是 best practice 所以造成該頁面 rankng 變好

但對原本就很好的 rankng 的頁面根本沒影響

且有趣的是說因為 AMP 還是有諸多限制, 所以很多有 AMP 的服務其實到第二頁或當你點擊上面的東西進入更深層或其他站內的頁面時, 都幾乎直接回到 mobile page 並非 AMP page

但單純從 amp 的 js 處理的一些東西就可以看出這 library 非常的有價值, 因為它暗地裡幫你處理許多效能問題

如果想稍微優化現有 service 當然也可以用 AMP project 的這套 js 來幫你處理

最後補充一下, 因為我們的服務上 AMP 對流量影響會很大所以目前還在測試上線階段也沒有全上

所以一開始列舉的一些問題是我們假設上線後可能面臨的情況
