---
layout: post
title: 'Header -  Accept-Language & Content-Language'
date: 2019-12-02
comments: true
categories: [HTTP]
---
## Header -  Accept-Language & Content-Language

### Intro

多國語系的判定主要靠這兩個來處理

[Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language)

[Content-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Language)

這裡的語言代碼一率遵循 [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)

### Accept-Language

系統或是 client 需要帶在 request header 中

表示 client 所使用的語言

有時會帶有 location 資訊(location 依照 [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) 標準且都是大寫

多語言時用 `,` 分隔

會在後面用 `q` 表示權重

```http
accept-language: zh-TW,zh;q=0.9,en-US;q=0.8,en;q=0.7
```

這個  header 常被用來判斷 client 的主要語言來判斷處理要回給 client 用哪個語言

### Content-Language

server 帶在 response header 中

用以表示該 response 是提供哪些語言的內容

一樣可以是單純的 `lang` 或是 `<lang>-<location>` 也可以用 `,` 分隔多語言

也可以在 HTML 中宣告

```html
<html lang="de">
```

### W3C I18n Checker

W3C 提供一個可以確認的網站

[W3C I18n Checker](https://validator.w3.org/i18n-checker/)

### [向 Google 提供網頁的本地化版本](https://support.google.com/webmasters/answer/189077)

1. HTML meta tag
2. HTTP header
3. Sitemap

使用以上三種方法來讓 Google 爬

### Keypoint

1. 可以依照 `Accept-Language` 裡面的多語系權重去判斷要給予使用者適合的語系
2. 不管是 W3C 還是 Google 其實都建議不能單純的依靠上述來判斷語系, 還是需要有提供能讓使用者手動切換語言的選項
3. Chrome 的同步設定會連 browser 慣用語言的設定一起同步...
