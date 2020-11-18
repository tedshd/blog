---
title: "JavaScript - 處理一些排序的方式"
date: 2020-11-18T03:52:33+08:00
draft: false
categories: [JavaScript]
---

常常會遇到用 JavaScript 處理一些資料結構的排序

這裡會列舉一些使用情境與案例

## 取出排名前幾名的資料(排名的值不重複)

### 資料

```javascript
var data = {
  123: {
    count: 123,
    type: "video",
    source: "",
  },
  345: {
    count: 345,
    type: "video",
    source: "",
  },
  99: {
    count: 99,
    type: "image",
    source: "",
  },
  1: {
    count: 1,
    type: "video",
    source: "",
  },
  9786: {
    count: 9786,
    type: "image",
    source: "",
  },
  347: {
    count: 347,
    type: "video",
    source: "",
  },
};
```

### 處理方式

```javascript
function topNine(data) {
  var arr = [];
  (tmp = Object.keys(data).reverse()), (l = tmp.length >= 9 ? 9 : tmp.length);
  for (let i = 0; i < l; i++) {
    arr.push(data[tmp[i]]);
  }
  return arr;
}
```

處理範例為取出前 9 筆

這樣的處理是使用 Object 的 Key 的排序本身是升冪排序

為了讓代碼好讀懂

使用了 `Object.keys(data).reverse()` 反轉陣列使其變成降冪排序

這樣跑 for 迴圈就可以自然而然的從 0 開始

考慮到資料可能不到 9 筆

所以用 `(tmp.length >= 9) ? 9 : tmp.length` 來處理迴圈要跑的次數

這樣這個函數就可以回傳前 9 名的資料了

但是這樣的資料結構有個問題就是範例資料的 **count** 必須是唯一值, 因為 JSON Object 不能重複 key

## 取出排名前幾名的資料(排名的值重複)

### 資料

```javascript
var data = [
  {
    source: "",
    type: "image",
    ts: 1600860409000,
    liked: 9680,
  },
  {
    source: "",
    type: "image",
    ts: 1603438465000,
    liked: 11746,
  },
  {
    source: "",
    type: "image",
    ts: 1602389743000,
    liked: 13289,
  },
  {
    source: "",
    type: "image",
    ts: 1605334079000,
    liked: 14095,
  },
  {
    source: "",
    type: "image",
    ts: 1602652312000,
    liked: 14138,
  },
  {
    source: "",
    type: "image",
    ts: 1603275324000,
    liked: 14310,
  },
  {
    source: "",
    type: "image",
    ts: 1603600329000,
    liked: 14448,
  },
  {
    source: "",
    type: "image",
    ts: 1603080713000,
    liked: 14625,
  },
  {
    source: "",
    type: "image",
    ts: 1604823132000,
    liked: 15351,
  },
  {
    source: "",
    type: "image",
    ts: 1604919156000,
    liked: 15373,
  },
  {
    source: "",
    type: "image",
    ts: 1601123545000,
    liked: 15442,
  },
  {
    source: "",
    type: "image",
    ts: 1601544281000,
    liked: 16659,
  },
  {
    source: "",
    type: "image",
    ts: 1605088396000,
    liked: 17137,
  },
  {
    source: "",
    type: "image",
    ts: 1602749094000,
    liked: 17483,
  },
  {
    source: "",
    type: "image",
    ts: 1600928882000,
    liked: 17928,
  },
  {
    source: "",
    type: "image",
    ts: 1602562980000,
    liked: 18217,
  },
  {
    source: "",
    type: "image",
    ts: 1603709259000,
    liked: 21845,
  },
  {
    source: "",
    type: "image",
    ts: 1602470351000,
    liked: 22292,
  },
  {
    source: "",
    type: "image",
    ts: 1603887487000,
    liked: 22559,
  },
  {
    source: "",
    type: "image",
    ts: 1602846057000,
    liked: 22824,
  },
  {
    source: "",
    type: "image",
    ts: 1601465442000,
    liked: 25226,
  },
  {
    source: "",
    type: "image",
    ts: 1604736681000,
    liked: 25580,
  },
  {
    source: "",
    type: "image",
    ts: 1601285690000,
    liked: 25796,
  },
  {
    source: "",
    type: "image",
    ts: 1601693594000,
    liked: 26078,
  },
];
```

### 處理方式

```javascript
function topNine(data) {
  var arr = [];
  var i, j, temp;
  for (i = 0; i < data.length - 1; i++) {
    for (j = 0; j < data.length - 1 - i; j++) {
      if (data[j]["liked"] < data[j + 1]["liked"]) {
        temp = data[j];
        data[j] = data[j + 1];
        data[j + 1] = temp;
      }
    }
  }
  var l = data.length >= 9 ? 9 : data.length;
  for (var n = 0; n < l; n++) {
    arr.push(data[n]);
  }
  return arr;
}
```

這個也不太難理解

第一個迴圈依照 **liked** 跑了一個降冪的氣泡排序(一般情況都是跑升冪)

```javascript
temp = data[j];
data[j] = data[j + 1];
data[j + 1] = temp;
```

這邊使用 variable swap 的技巧來做前後兩個值的交換

```javascript
c = a;
a = b;
b = c;
```

第二個迴圈就是取出前 9 筆的 **liked** 數

一樣是在 `data.length >= 9 ? 9 : data.length` 確認未滿 9 筆的話就有多少取多少
