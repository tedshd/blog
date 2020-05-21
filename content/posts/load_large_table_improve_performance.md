---
title: "如何在網頁載入比較大量的資料時增加效能?"
date: 2020-05-21T10:13:23+08:00
draft: false
categories: []
---

## 前言

在後台系統會常遇到的問題就是要呈現大量的資料(表單)

通常在這情況下會有兩種方式呈現資料

1. 分頁

2. 無限滾動

但是這都要在 model 額外做不少工

例如: 處理分頁, 處理排序, 處理搜尋

這些都是要再花時間處理的

這邊將會介紹一下如何在不太改動 model 的情況下提升前端效能

當然在真的是非常的大量的資料時還是真的要在 model 提供參數去 query DB

## 現況

因為新的需求需要添加到不少的資料

但是因為時程短加上再添加的資料量也不會大的誇張(約共 2000 左右的量

所以還是一次全部載入


## 問題點

首先會先遇到的問題就是

一次載入 2000 多筆資料頁面就開始變很慢(因為還有圖片)

打開 chrome developtool 就會發現 DOMContentLoaded 要到 13s 左右

慢到爆炸

這 13s 還不包含之後要執行的 JavaScript 與畫面渲染

因為還有圖片

所以 2000 多個圖片載完後

整個頁面花了 1 分鐘多...

[screenshot image](/images/螢幕快照_2020-05-21_下午1.49.36.png)

## 解決方案

### 先把圖片改成 lazyload

從瀏覽器一次載入 2000 多筆資料瞬間變成只載入頁面會呈現的圖片

但是 DOMContentLoaded 還是要 12s 左右啊~~

[screenshot image](/images/螢幕快照_2020-05-21_下午3.01.21.png)

### 解決 DOMContentLoaded 問題

因為後台的資料表單是 SSR(server side render) 從 PHP 噴的

所以一定會有個問題就是 2000 多筆的 table HTML DOM 很多

然後因為是從 server side 噴到瀏覽器上

所以會有一個卡的點就是 DB query 的效能(這部分已經優化過了, 在這次的案例是一次全撈出來是要優化什麼啊)

那只要 DB query 卡到的話

就會延遲頁面的呈現

因為 server side 是把所有的 response content 都好了才會噴回去瀏覽器

當然在 PHP 可以用 `ob_flush` 和 `flush` 來處理

[Refer - 強迫 PHP 將 Buffer 的資料提前輸出](https://blog.longwin.com.tw/2010/12/php-buffer-flush-2010/)

[Refer - PHP flush()與ob_flush()的區別詳解](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/240051/)

但是目前沒有想要這樣做

因為目前的程式結構有點複雜, 所以就沒有用這方法實作

所以最後是決定把這一頁改成 CSR(client side render)

用 AJAX 拉資料下來

### JavaScript 優化

因為是後台的操作會有 CRUD 的行為, 原本這些行為就都是 AJAX 處理

所以在 JavaScript 有很多操作行為的事件綁定(event binding)

所以就把這些行為改成事件委派(event delegation)

### 關於分頁, 排序和搜尋的處理

資料量變多後 PM 最喜歡說我希望有搜尋和排序這樣比較方便看資料誒

但是我們已經把所以資料經由 AJAX 取回到瀏覽器上了

這時就可以用一個 jQuery 超好用的 plugin [DataTables](https://datatables.net/)

這 plugin 可以把 client 的 data 重新處理成具有分頁排序和搜尋的 table

也支援把已經在頁面上的 table 或 AJAX response 或是在 JavaScript 中的 data 重新處理

## 結論

當上述的東西處理完後

[screenshot image](/images/螢幕快照_2020-05-21_下午2.55.41.png)

DOMContentLoaded 因為改成 AJAX 所以會少很多(12s -> 2s)

因為資料改成 AJAX 產生, 這速度比 SSR 快多了

再不看畫面 render 的情況下 loading 速度已經提高很多了

基本上上述這些只會動用到前端的程式即可達到成效不錯的優化了

## 額外補充

### 測試 JavaScript 效能

可以用 runtime 來測試

```JavaScript
var startTime = new Date().getTime();

var endTime = new Date().getTime();
console.log('testName: ' + (endTime - startTime) + 'ms');
```

### DataTables AJAX 處理

[Refer - ajax](https://datatables.net/reference/option/ajax)

[Refer - columns.data](https://datatables.net/reference/option/columns.data)

[Refer - columns.render](https://datatables.net/reference/option/columns.render)

[Refer - [jQuery] jQuery DataTables 資料行加入checkbox、按鈕，關閉資料行排序、改變下拉選單的每頁顯示幾筆、變更DataTables樣式…等功能 Part5 final](https://dotblogs.com.tw/shadow/2018/04/03/065712)

### 套用 DataTables 後的 image lazyload 處理

因為現在使用的 image lazyload 會是觀察當前畫面的圖片後在確認這些圖片是否在可視範圍才會加載

所以當有分頁時

因為換分頁時會是新的 table DOM(table DOM 會重建) 所以換分頁後的圖片是之前沒有被觀察的

所以換分頁後得再重新觀察當前頁面的圖片

DataTables 有 page 的 event 可以監聽分頁切換

[Refer - page](https://datatables.net/reference/event/page)

這邊圖片延遲載入是使用自己參照 Google 的開發文件寫的 code [simpleImgLazyLoad](https://github.com/tedshd/simpleImgLazyLoad)
