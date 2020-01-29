---
layout: post
title: 'Google search develop for SEO - research log'
date: 2017-04-24
comments: true
categories: [Google SEO]
---
## Google search develop for SEO - research log

對於一個網站上線要讓 Google 容易搜尋到需要做很多事

多到爆炸,而且每年都有新東西出來, 實在看得很煩...

感覺網路都被 Google 控制了...

Google 甚至出了一個develop guide

如要最新的消息與規範可以到 [Introduction | Search | Google Developers](https://developers.google.com/search/docs/guides/)

因為以下寫的東西可能過幾年後又有新的東西要加了

最後會再補充一些 social media 的 meta tag...

注意

這只是列出提要, 具體細節可以看所附的想關參考連結或拿關鍵字餵 Google

不然這文章寫一個禮拜都還不一定寫得完

但主要的經驗會在文章中提到

### 網站上線要給 Google crawler 爬需要注意的東西

#### metadata

以下兩種方式

* 建立 mockuop data

* 建立 [Google search console(webmaster)](https://www.google.com/webmasters/#?modal_active=none) or [Google My Business](https://www.google.com/business/)(這通常是為了公司品牌或店家使用)

身為一個攻城獅

建立 mockup data 是基本(後續會介紹)

Google search console 可以讓你了解關於你的網站在 Google 上的一些情況, 像是被 search 多少次、曝光多少次或被  Google 建立了多少 index 等等, 還有很多東西, 也都會在加入許多新的功能, 所以最好定期去看一下

Google My Business 就是像下圖的東西, 但沒用過, 所以不知道具體的細節

<img class="left" src="https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-04-24%20%E4%B8%8A%E5%8D%8810.59.19.png?alt=media&amp;token=be4bbc76-bbb6-48d1-8cc6-4c6b0178cc49">

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/logdown%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-04-24%20%E4%B8%8A%E5%8D%8811.00.56.png?alt=media&token=eb25ad74-49e8-4fda-abb4-afac1fd8a963)

#### 準備接下來的東西

* [App Indexing](https://firebase.google.com/docs/app-indexing/)(有 App 的服務才要做, 不管是 iOS 或 Android 都可以做)

* [Mobile Friendly](https://developers.google.com/webmasters/mobile-sites/)(不管你的網站是 RWD 還是 AWD 都要處理, 不然你的 SEO 就準備說掰掰了)

* [AMP](https://www.ampproject.org/)(Google 提出的, Facebook 有個類似的叫 instant articles)

* Markup data(不管是 JSON-LD 還是 sechema 都很重要, sitemap 也不要忘了)

### 上述東西的一些細節

#### 關於 URL 這件事

* Canonical URLs - 主要固定的 url

非 mobile url 非 amp url 非 短網址, 需注意的是假如是產品列表頁, 可以不要在這個值加上像是(`p=1` or `page=2`) 等頁數的 query string 這可以讓分頁的 rank 算到這產品頁來

redirect 採用 301

儘量使用 `https`

只列出一些要注意的點

具體可參考

[使用標準網址](https://support.google.com/webmasters/answer/139066?hl=zh-Hant)

* Alternate URLs - 非主要性的 url

像是其他語系的 url 或 mobile url 或 amp url 等都是這類型的

更多關於 url 要注意的事

Google 有份文件

[Associate Your Online Resources](https://developers.google.com/search/docs/guides/associate-resources)

可以參考

懶得進去的下面有列舉一下要注意的 url 類型

* AMP page URLs (where supported)
* App URLs
* Mobile-specific website URLs
* Standard website URLs
* International sites URLs

怕有人不知道

最後補充個 Google crawler 的機制

crawler 一進入頁面會抓取頁面中所有連結且如果是站內連結

crawler 會再進去站內連結的頁面抓該頁面的資料

但如果網站有的頁面是原本的頁面上不會有 link 的那這樣 crawler 就不會抓到了

所以這時就要用提交 sitemap 的方式來讓 Google index 這頁面

關於 sitemap format 可參考 [sitemaps.org - Protocol](https://www.sitemaps.org/protocol.html)

對於很多頁面可能是 UGC(User Generated Content) 的頁面可以用提交 sitemap 的方式

最後針對 SPA 其實也是有解法的, 就目前來說 Google crawler 都可以抓 #! 了

可參考 [Webmaster Central Blog](https://webmasters.googleblog.com/2015/10/deprecating-our-ajax-crawling-scheme.html)

但何時會再改就是看 Google 心情了

#### 關於 metadata 這件事

[Introduction to Structured Data](https://developers.google.com/search/docs/guides/intro-structured-data)

眾所皆知的有

* Microdata
* JSON-LD
* RDFa

但其實都還是遵循 [schema.org](http://schema.org/) 中的規範

只是呈現的格式不同而已

==待更新==
