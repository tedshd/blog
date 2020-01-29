---
layout: post
title: 'HTML - dns-prefetch, preconnect, prefetch, prerender 研究筆記'
date: 2017-09-11
comments: true
categories: [HTML]
---
## HTML - dns-prefetch, preconnect, prefetch, prerender 研究筆記

### Intro

這幾個 meta 屬性早在幾年前就有不少外國文章和少部分的國內大神介紹過了

但當時我一直抱持這它還在 [W3C 草案](https://www.w3.org/TR/resource-hints/), 所以不急著用的心態, 且瀏覽器支持不高, 所以一直無視它...

直到最近不知怎麼地想說來繼續增加我們服務的 head 中的 HTML tag 的數量吧 XD

就來研究一下這些屬性

### dns-prefetch

預先解析 DNS, 簡單說一句就是把你的網站會用到的 domain 都塞上去

但我有點質疑實用性就是了, 因為通常會用到的 domain 都幾乎在該頁面用到了, 幾乎功效不大

因為在 head 預讀時有可能還沒解析完, 實際頁面已經需要對該 domain 發 request 了...

**結論: 會改善但感覺改善幅度不大, 且你的服務內有用到多個 domain 或 subdomain 才有影響**

### preconnect

會對設定的 domain 做 DNS 解析與 handshake

不過我覺得最大的好處是預先對該 domain 做 handshake

但就像上述所說大部分的情況是會用到的 domain 幾乎都在頁面上了

**結論: 會改善但感覺改善幅度不大, 且你的服務內有用到多個 domain 或 subdomain 才有影響**

### prefetch

可以設定權重讓你去決定使用者可能會點擊的下一個頁面或其他需要的 resource 的權重比例

在當前頁面載入時瀏覽器會依照權重決定何時去載入該 resource

提前在當前頁面去要該 resource, 所以 server log 會發現在載入該頁面時 prefetch 設定的 resource 也會被拉

等到要用到該 resource 時然後會加快 response 的時間

但跟我期望的有點落差

我期望是先 cache 起來

然後再從 cache 拿就好了, 不用在重拿(測試時 header 的 cache-control 是設定 max-age)

但目前測試還是會重新跟 server 拿...(但我是設定 html 就是了, 不知 CSS JS 是否有差, 因為我們的服務 CSS JS 都會自己 cache 所以根本用不到這機制)

且時間也沒縮短(可能前提也是我們的服務 response 太快?

**結論: 實測後無感, 時間都差不多, 且又多了一個 prefetch 的 request access**

後端跟我說為啥 access 量增加了...

然後我去看 access log...

變兩倍...

### prerender

這很有趣

看定義是說會預先幫你 render 你所指定的頁面

它也表示會額外耗費 CPU 或 GPU 資源

但其實在你換頁時現今的 browser 都有處理一件事

就是當 browser 發現該頁面上的 layout 或 UI 與上一個幾乎一樣時

這部分的 layout 或 UI 是不會進行重繪的動作以增進效能

尤其這在 mobile browser 上更明顯

所以其實我對這 feature 感覺還好

**結論: 目前測不出來, 但實用性似乎不高誒, 又要額外耗費資源, 就看取捨**

以上是目前測試的結果

但不保證之後也是這樣的結果

畢竟還在草案

所以可能會有變動或翻掉都說不定
