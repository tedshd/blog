---
title: "在 JavaScript 處理各個時區對應的日期時間"
date: 2022-10-04T11:16:31+08:00
draft: false
categories: [JavaScript, timeZone]
---

## Intro

在 JavaScript 中的日期時間是個當初沒有定義出良好設計的東西

這裡先舉幾個常見的問題

1. 日期格式問題
2. 日期呈現的語系問題
3. 時區問題
4. 12 小時 24 小時問題
...

以原生的 API 在處理日期時間大多得自己額外做許多事情或是套用一些第三方 libary 來協助達成目的

## 時區問題

這次主要是討論關於時區的問題

在早期只能用 `getTimezoneOffset()` 的方法搭配時區表去換算各地時區

現在倒是可以使用 `Intl.DateTimeFormat`

[refer - Date.prototype.getTimezoneOffset()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getTimezoneOffset)

[refer - Intl.DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat)

其實上述的問題, 在使用 `Intl.DateTimeFormat` 基本上都可以解決掉

詳細方式可以參以下文件

[refer - Intl.DateTimeFormat() constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat)

在時區中又有一個常常被忽視的的問題就是夏令時間(daylight savings time) 這個在夏季時就得把時間提前一小時的問題

如果自己處理時區就得記得處理這問題

使用 `Intl.DateTimeFormat` 的話系統已經自動處理了

## Intl.DateTimeFormat

這邊簡單介紹一下 `Intl.DateTimeFormat` 的一些用法與注意事項

```JavaScript
new Intl.DateTimeFormat(navigator.language, {
  timeZone: 'America/Los_Angeles',
  dateStyle: 'full',
  timeStyle: 'full'
}).format(new Date())
```

這個範例就表示了當前洛杉磯的時間

第一個參數是語系, 採用 BCP 47 標準, 基本上建議使用 `navigator.language` 或是自己寫死(特定情況時使用)或是另外帶入

第二個參數的物件除了 `timeZone` 是為了顯示指定時區之外其他的參數基本上都在定義顯示的型式

例如

```JavaScript
new Intl.DateTimeFormat(navigator.language, {
  year: 'numeric',
  month: '2-digit',
  day: '2-digit',
  hour: '2-digit',
  minute: '2-digit',
  second: '2-digit',
  hourCycle: 'h24',
}).format(new Date())
```

這樣就會返回 `YYYY/MM/dd HH:mm:ss` 的顯示方式

額外提幾個比較特別的參數

* timeZone: 時區的值使採用 IANA 所定義出的標準名稱基本就是像是 Asia/Taipei 這樣的格式, 有一個比較特別值是可以使用 'UTC' 表示當前的 UTC+0 時間(簡單說明就是時區零的時間)
* calendar: 是設定要使用的曆法, 例如: `calendar: 'chinese'` 就是農曆
* hour12: 是表示是要用 12 小時制或 24 小時制顯示, 用 24 小時制就不會另外顯示上午或下午

剩下的可以參考文件來使用

[refer - Intl.DateTimeFormat() constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat)

## 處理全球性的活動時間問題

接下來來處理實作面的問題

當服務擴及全球是需要在全球各地或是各別國家的特別節日等舉辦活動

時間就很重要

如果時間搞錯, 使用者根本無法在正確的時間參與到活動, 那就準備等著收到一堆抱怨

所以都會有以下策略來處理這樣的問題

### 說明活動開始的時間是對應哪個時區的時間

例如活動指定開始時間是 2022/12/25 08:00 GTM-7(洛杉磯時間)

這公告發在美國地區還沒什麼問題, 因為美國只有大概誇 5 個時區

但這公告對在亞洲和歐洲地區的人就很痛苦, 因為還得使用者自己換算成自己當地的時間

所以如果以全球性的活動來說這對跨比較多時區的人來說很不友善

但這也是有解法的

只要在 client 轉換成 client 當地的時間就可以了, 才比較容易讓使用者了解到正確的時間

### 針對不同區開始對應區域的公告與活動

這是比較常見的做法

大多時候可以針對像是不同國家的節慶活動或是各個區域不同的活動來處理

所以只要針對該地區的的時區設定就可以了

## 管理系統的設計

下面說明一個比較麻煩的情況

當需要設計一個面對全球性的推播或公告系統時會遇到上述的問題

在管理人員或運營人員在操作系統時

會有一個很基本的思維是

想要在美國國慶的時候設定推播通知

那很理所當然地在介面會希望就是選美國當地的時區, 之後再選美國當地的日期時間

不會希望要自己換算美國國慶的時間轉成自己當地的時間是什麼時間再去設定

這在時間處理上就會是一個很有趣的問題

JavaScript 的 Date 是帶有時區的(client 裝置設定的時區)

所以是需要做額外處理的

但原理也很簡單

先用 `new Date(value)` 把設定的時間取出來轉成 timestamp

例如: `new Date('2022-10-04T17:00:00')`

這會返回 **1664874000000**

但這是當前 client 設定時區的 2022-10-04 下午五點的 timestamp

並非期望時區的時間

這時就要做時區的校正

公式大概如下

`new Date(設定推播的時間).getTime() + 當前時區 - 設定推播的時區`

所以大概就是

`new Date(dateString).getTime() - new Date().getTimezoneOffset()*60*1000 - 設定推播的時區(毫秒)`

那只要把這個丟給後端讓後端依照這時間發送就可以了

到了這邊, 大概剩下一個問題就是麻煩的夏令時間(daylight savings time) 問題

因為不可能自己處理這問題

所以這邊採用了一個 [timezonedb](https://timezonedb.com/) 的服務

這個服務的 api 會返回當前所有時區而且是已經校正過夏令時間的時區

所以就可以拿取得這個服務的資料來當成自己的時區資料

最後的最後

剩下一個尷尬的小問題就是如果設定的時間和要推送的時間剛好是跨夏令時間的開始和結束時, 就會有一小時的誤差, 目前還沒想到比較好的解法, 只能在設定時儘量避掉這樣的情況