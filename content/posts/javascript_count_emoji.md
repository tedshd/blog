---
title: "JavaScript 計算 emoji"
date: 2022-01-04T05:42:00+08:00
draft: false
categories: [JavaScript, emoji]
---

## 在 Web 中的 emoji 處理

在普遍的字串計算長度的部分

一個字元是單位是一

但是因為 emoji unicode 後面定義的

這超出了原有 JavaScript 原有定義的範圍

所以 emoji 的字串長度一率都是從 2 起跳

這在 Web 中會造成有需要處理字串長度的地方就會出現問題

例如:

input 文字的長度限制的使用

```HTML
<input type="text" maxlength="10">
```

字串需要計算長度時

```JavaScript
string.length;
```

尤其是在現在行動裝置的普及, 內建的鍵盤已經有 emoji 的輸入可以使用

更會大大的增加在需要的邏輯處理會出現問題

## 如何解決

有一個方便的套件 [runes](https://github.com/dotcypress/runes) 會把 emoji 識別出來

所以就可以解決掉 emoji 的問題了

## 背後原理

其實背後的原理也不難

就是去比對 emoji 的 unicode 碼

比對該字串是不是 emoji 的 unicode 碼

以下有 emoji 的網站可以試試看

[https://getemoji.com/](https://getemoji.com/)

## 後續補充

所以在處理字串長度時就可以用 runes 套件得到的長度去限制

不使用原有的方式去限制

作者使用 runes 這個名稱也很有意思

runes 是盧恩文的意思, 也是拉丁文的起源, 相當於中文中的甲骨文

也是屬於以形會意

所以用來代表 emoji 也是以形會意真的是蠻有意思的命名