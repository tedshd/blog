---
layout: post
title: 'jQuery selector'
date: 2013-08-03
comments: true
categories: [jquery]
---
```
* 所有元素
E 所有E元素，
E:nth-child(n) 傳回在所屬父元素下，排行第 n 的元素 E。(注意: 從 1 開始算，而非從 0)
E:first-child 傳回在所屬父元素下，排行第一的元素(老大)
E:last-child 傳回在所屬父元素下，排行最後的元素(老么)
E:only-child 傳回在所屬父元素下，是唯一子元素(獨子)
E:empty 沒有任何子元素者(有文字也不算，例如 <span>TEXT</span> 就不合格)
E:enabled 未被停用的 UI 元素 E
E:disabled 被停用的 UI 元素 E
E:checked 被勾選的 UI 元素 E(適用於 Radio, Checkbox)
E:selected 被選取的 UI 元素 E(適用於 Select 下的 Option 元素)
E.myClassName CSS 類別設為 myClassName 的元素 E
E#myId id="myId" 的元素 E
E:not(s) 不符合 s 條件的元素 E，例如: $("span:not(:empty)") 即為找出有包含子元素的 span
E F 由包含在 E 底下的 F 元素，不必直接為父子關係，例如: F 可以是 E 的子元素的子元素。
E > F 找出父元素為 E 的 F 元素
E + F 找出緊接在 E 元素後方的 F 元素
E ~ F 找出緊接在 E 元素前方的 F 元素
E,F,G 利用逗號可以呈現 " 或 " 的聯集效果，指 E 元素或 F 元素或 G 元素
E[foo] 具有 foo 屬性 (Attribute) 的E元素(1.2.6 以前的版本亦可用 E[@foo] 表示，1.3 版本起取消 @ 符號的使用)
E[foo=bar] 有 foo 屬性，且 foo 屬性值為 bar 的 E 元素
E[foo!=bar] 有 foo 屬性，且 foo 屬性值不等於 bar 的 E 元素
E[foo^=bar] 有 foo 屬性，且 foo 屬性值以 bar 開頭的 E 元素
E[foo$=bar] 有 foo 屬性，且 foo 屬性值以 bar 結尾的 E 元素
E[foo*=bar] 有 foo 屬性，且 foo 屬性值中包含 bar 字眼的 E 元素
E[foo=bar][baz=bop] 同時具備 foo 及 baz 屬性，且其值分別為 bar 及 bop 的 E 元素
:even 由選取結果中只挑出第雙數個
:odd 由選取結果中只挑出第單數個
:eq(N) and :nth(N) 由選取結果中取出第 N 個，由 0 起算
:gt(N) 由選取結果中只保留第 N 個以後者(不含 N)
:lt(N) 由選取結果中只保留第 N 個以前者(不含 N)
:first 選取結果中的第一個，等同於 :eq(0)
:last 選取結果中的最後一個
:parent 選取包含子元素者(文字內容也算，例如:<span>Text</span>)
:contains('test') 選取元素內的文字包含特定字串者
:visible 選取所有可見的元素(包含 CSS display=block 或 inline, visibility=visible 但不含 <input type="hidden">)
:hidden 選取所有不可見的元素(包含 CSS display=none, visibility=hidden以及<input type="hidden">)
:input 選取所有表單輸入元素(包含 input, select, textarea, button).
:text 選取所有 <input type="text">
:password 選取所有 <input type="password ">
:radio 選取所有 <input type="radio ">
:checkbox 選取所有 <input type="checkbox">
:submit 選取所有 <input type="submit">
:image 選取所有 <input type="image">
:reset 選取所有 <input type="reset">
:button 選取所有 <input type="button">
:file 選取所有 <input type="file">

size() 或 length 傳回群組的物件個數
eq(N) 取出群組中第 N 個 jQuery 物件
get() 傳回元素的陣列
get(N) 取出第 N 個元素
index(element 或 jQuery 物件) 用來找某元素在選取結果中的排名順序，例如網頁上有五個 <div>，<div id="dvX"> 為第三個，則$("div").index(document.getElementById("dvX")) 可以得到 2 (由 0 起算，故第三個為 2)，$("div").index($("#dvX")) 也可得到同樣結果。元素不在群組時傳回 -1。
```
