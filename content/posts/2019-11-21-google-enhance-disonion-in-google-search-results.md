---
layout: post
title: 'Research - 加強在 Web 服務在搜尋引擎與部分社群的呈現'
date: 2019-11-21
comments: true
categories: [Google]
---
## Research - 加強在 Web 服務在搜尋引擎與部分社群的呈現

這是一份紀錄著如何加強 SEO? 的筆記

參考來源大部分會是 Google 文件或者是 blog 發佈的消息與部分試驗出來的結果

僅供參考

### 從 0 到 1

#### 建立 [Gogole search console](google search console)

#### [瞭解 Sitemap](https://support.google.com/webmasters/answer/156184)

#### social metag og

* [schema.org](https://schema.org) & [json-ld](https://developers.google.com/search/docs/guides/intro-structured-data)
* [The Open Graph protocol](https://ogp.me/)
* [facebook og](https://developers.facebook.com/docs/sharing/webmasters#markup)
  * [Sharing Debugger](https://developers.facebook.com/tools/debug/sharing/)
* [twitter card](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started)
  * [card validator](https://cards-dev.twitter.com/validator)
* [Pinterest Rich Pins](https://developers.pinterest.com/docs/rich-pins/overview/?)
  * [Rich Pins Validator](https://developers.pinterest.com/tools/url-debugger/)

#### [結構化資料格式](https://developers.google.com/search/docs/guides/intro-structured-data#structured-data-format)

[結構化資料測試工具](https://search.google.com/structured-data/testing-tool)

#### Google rich content

[探索 Search Gallery](https://developers.google.com/search/docs/guides/search-gallery)

#### favicon

[web - favicon 使用筆記](http://tedshd.logdown.com/posts/7834497-web-icon-use-notes)

#### [可讓 Google 識別的特殊標記](https://support.google.com/webmasters/answer/79812)

#### lang

#### PWA(Option)

#### AMP(Option)

#### App link(Option)

#### [Google News Publisher Center - Partnerdash](https://partnerdash.google.com/partnerdash/d/news#p:id=pfehome)(Option)

#### [Google My Business - Stand Out on Google for Free](https://www.google.com/business/)(Option)

#### [提高在 Google 搜尋中的能見度](https://developers.google.com/search)

#### wiki(Option)

建立 wiki 頁面, 因為 Google 會把 wiki 中相關頁面呈現在前面

對品牌較有效益

#### [更新您的 Google 知識面板](https://support.google.com/knowledgepanel/answer/7534842?hl=zh-Hant)(Option)

#### [Google Knowledge Graph Search API](https://developers.google.com/knowledge-graph)(Option)

Knowledge Graph & 知識面板是 Google 一個很猛的計畫

涵蓋範圍不只是只有 web

### 當有 1 之後

#### 資料品質

[Follow the structured data guidelines](https://developers.google.com/search/docs/guides/sd-policies)

[品質指南](https://support.google.com/webmasters/answer/35769#quality_guidelines)

> 避免使用下列手法：
>
> 自動產生的內容
> 加入連結配罝
> 建立沒有原創內容或極少原創內容的網頁
> 偽裝
> 幕後重新導向
> 隱藏的文字或連結
> 入口網頁
> 剪輯的內容
> 加入無法有效增值的聯盟計畫
> 載入含有無用關鍵字的網頁
> 建立具有惡意行為的網頁，例如網路詐騙，或是植入病毒、木馬程式或其他惡意程式
> 濫用結構化資料標記
> 對 Google 傳送自動查詢

[隱藏的文字與連結](https://support.google.com/webmasters/answer/66353)

> 為操控 Google 搜尋排名而在內容中加入隱藏的文字與連結，可能會遭系統視為詐欺行為，同時也違反 Google 的《網站管理員指南》。隱藏文字 (例如過多關鍵字) 的方式有很多種，例如：
>
> 在白色背景上使用白色文字
> 將文字藏在圖片底下
> 透過 CSS 將文字放置於畫面外
> 將字型大小設為 0
> 透過建立某個小字元的連結來隱藏連結，例如段落中的連字號

[濫填關鍵字](https://support.google.com/webmasters/answer/66358)

#### [在搜尋結果中顯示合適的網頁標題和摘要](https://support.google.com/webmasters/answer/35624?hl=zh-Hant)

#### 圖片

[Web - HTML metadata image size with open graph...etc](http://tedshd.logdown.com/posts/7858371-web-html-metadata-image-size-with-open-graph-etc)

#### [網址檢查工具](https://support.google.com/webmasters/answer/9012289)

#### [向 Google 說明您的出站連結限制](https://support.google.com/webmasters/answer/96569)

* `rel="sponsored"` - Ad
* `rel="ugc"` - User generate content
* `rel="nofollow"` - not follow link

#### [在測試網站時保持 Google 搜尋排名的最佳做法](https://support.google.com/webmasters/answer/7238431)

不過就我的經驗在搞 A/B 測試時沒在導頁的

#### [整合重複的網址](https://support.google.com/webmasters/answer/139066)

如果要有效的 redirect 頁面請使用 301 作為永久導頁用

#### 本地化(多國語系)

[管理多地區和多語言版本的網站](https://support.google.com/webmasters/answer/182192)

[向 Google 提供網頁的本地化版本](https://support.google.com/webmasters/answer/189077)

* HTML tag

```html
<link rel="alternate" hreflang="en-us" href="http://en-us.example.com/page.html" />
```

* HTTP header

```
Link: <http://example.com/file.pdf>; rel="alternate"; hreflang="en", <http://de-ch.example.com/file.pdf>; rel="alternate"; hreflang="de-ch", <http://de.example.com/file.pdf>; rel="alternate"; hreflang="de"
```

* stiemap

```xml
<url>
    <loc>http://www.example.com/deutsch/page.html</loc>
    <xhtml:link rel="alternate" hreflang="de" href="http://www.example.com/deutsch/page.html"/>
    <xhtml:link rel="alternate" hreflang="de-ch" href="http://www.example.com/schweiz-deutsch/page.html"/>
    <xhtml:link rel="alternate" hreflang="en" href="http://www.example.com/english/page.html"/>
</url>
```

> 請勿使用 IP 分析來調整內容。 分析 IP 位置資訊相當困難，而且往往並不可靠。此外，Google 可能無法正確檢索您網站的變化版本。雖然有部分例外，但 Google 檢索器在大多數情況下是源自美國，我們也不會為了偵測網站變化版本而試圖變更位置。如要針對特定地區提供內容，請採用本文列出的方式 (hreflang、替代網址和明確連結)。

當然如果是 App 服務那就沒差了, 因為又不用顧及 Google 爬蟲 XD

#### [保持簡單的網址結構](https://support.google.com/webmasters/answer/76329)

> 您可以試著在網址中使用標點符號。http://www.example.com/green-dress.html 這樣的網址比 http://www.example.com/greendress.html 更實用。建議您在網址中使用連字號 (-)，而不要使用底線 (_)。
