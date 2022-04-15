---
title: "網頁處理 RTL(右到左) 文字"
date: 2022-04-15T10:09:15+08:00
draft: false
categories: [HTML, JavaScript, RTL]
---

## 前言

在 web 的世界中有一個需要處理的是文字排版的呈現

因為從電腦到整個計算機科學的領域都是在拉丁語系為主宗的國家發展的

所以在介面的文字排版上自然以從左到右為主

但是在這世界上的文字排版有從左到右, 上到下, 右到左等呈現方式

所以需要依照需求或不同語系的文字上有相對應的處理, 尤其是在多語系的情況下

上到下的排版大多是書面用的排版, 相對在資訊領域比較少呈現, 且因為上到下的排版方式也大多是亞洲地區的國家, 在標準化的話語權不高

但也漸漸在 web 領域中有開始支援上到下的排版([writing-mode](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode))

且在資訊領域也大多是用左到右的呈現, 所以影響相對小

額外補充一下大部分的方塊文字像是中文、日文、韓文等其實左到右、右到左、上到下都可以書寫與呈現

但在部份語系像是

* 阿拉伯文
* 烏爾都文
* 庫德文
* 波斯文
* 希伯來文

上述文字排版就固定都是從右到左

除了希伯來文以外都是從阿拉伯文字延伸的, 就像是英文、德文、法文都是拉丁文延伸出來一樣

至於為何在世界各地的文字排版會有差異其實主要是起源於早期該文字是書寫的方式與被書寫在什麼材質上面

右到左主要起源於早期是文字是刻在石板上面, 左手拿鑿子, 右手拿錘子, 這樣從右到左是相對順手的

中文早期大多從上到下從右到左的排列主要起源於以前是也在竹片上捲成冊的(竹簡)

在單片竹片上面書寫自然是上到下, 那捲成冊之後在閱讀時為了方便持握, 會是左手拿著竹簡, 右手打開來看內容, 自然就變成了右到左來閱讀

不過現在大多也因為資訊科學的發展後在電子載體上就沿用左到右的排版

不過在書面印刷還是有保留上到下右到左的排版

不過有點扯遠了

## 實作 RTL(Right To Left) 的方式

這次主要是要處理 RTL 的問題

但其實在實作上也很好解

HTML tag 有個屬性是 `dir` 只要設定是 `rtl` 或是 `ltr` 就可以了

那麼要在什麼情況下設定這個東西?

大致上會在兩種情況設定

### 1. 多語系且有右到左語系

網站是多語系的網站時需要確認是否有右到左語系

所以只要在使用者決定好語系時針對該語系時需要呈現 RTL 的 tag 做處理就可以了

以下有個例子是 Apple 的官網就是如此設計的

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2FScreen%20Shot%202022-04-15%20at%2011.48.23%20AM.png?alt=media&token=c8a644ca-20bc-4d0a-83a2-16d8929a58d1)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2FScreen%20Shot%202022-04-15%20at%2011.47.18%20AM.png?alt=media&token=fd076287-6bef-49fd-90dc-5b6f00b6b472)

Apple 的官網就是在不同語系就設定不同的 dir 來讓過

### 2. UGC(user generated content) 有右到左語系的內容

像是討論區或是可以讓使用者輸入內容呈現的部分這部分也要注意處理

這樣的話呈現內容就不會是我們先掌控的

不像一般網站如果要呈現多語系, 那網站內容都會是自己的多語系檔與自己判斷多語系

這情況就可以使用 `dir` 的第三種設定 `auto`

瀏覽器會依照 useragent 的語系判斷是 RTL 的語系時就自動轉成右到左, 如果是一般 LTR 的語系需維持左到右

這個方法很實用但也有個小缺點

就是當內容一開始是 LTR 的文字時就會讓整個內容是 LTR

像是以下情況

```HTML
<p dir="auto">This content هذه الفقرة باللغة العربية ، لذا يجب الانتقال من اليمين إلى اليسار.</p>
```

會有點尷尬, 也不太確定這樣的呈現是不是可行的

但是可以用另一個方式就是用 regex 來確認內容是不是有 RTL 的字元

找了一下網路上整理出來的

```JavaScript
function IsRTL (s) {
  const rtlChars = '\u0591-\u07FF\u200F\u202B\u202E\uFB1D-\uFDFD\uFE70-\uFEFC'
  const rtlDirCheck = new RegExp('[' + rtlChars + ']')
  return rtlDirCheck.test(s)
}
```

這個 function 可以判斷內容是否含有 RTL 的字元

但這個也不適合有混合了 RTL 和 LTR 的內容

總之還是得自己評估採用哪種方式比較好

[dir - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/dir)

[Refer - 縱書與橫書](https://zh.wikipedia.org/wiki/%E7%B8%B1%E6%9B%B8%E8%88%87%E6%A9%AB%E6%9B%B8)