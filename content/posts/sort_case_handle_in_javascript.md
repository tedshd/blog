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
  '123': {
    'count': 123,
    'type': 'video',
    'source': ''
  },
  '345': {
    'count': 345,
    'type': 'video',
    'source': ''
  },
  '99': {
    'count': 99,
    'type': 'image',
    'source': ''
  },
  '1': {
    'count': 1,
    'type': 'video',
    'source': ''
  },
  '9786': {
    'count': 9786,
    'type': 'image',
    'source': ''
  },
  '347': {
    'count': 347,
    'type': 'video',
    'source': ''
  },
};
```

### 處理方式

```javascript
function topNine(data) {
  var arr = [];
  tmp = Object.keys(data).reverse(),
    l = (tmp.length >= 9) ? 9 : tmp.length;
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

但是這樣的資料結構有個問題就是範例資料的 count 必須是唯一值, 因為 JSON Object 不能重複 key

## 取出排名前幾名的資料(排名的值重複)

...TODO
