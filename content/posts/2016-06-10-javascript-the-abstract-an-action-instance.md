---
layout: post
title: 'JavaScript - 動作行為抽象化實例'
date: 2016-06-10
comments: true
categories: [JavaScript]
---
## JavaScript - 動作行為抽象化實例

其實標題真的不知道要怎麼定

因為只是要說明一個實例, 但又不想扯到其他太制式的東西(設計模式), 但這範例又可用於其他地方, 所以到最後就用了個似是而非的標題了...

先說一下可能的使用情境

當你在做一個動作時要做一件事 ex: 呼叫 API、紀錄 GA、狀態改變之類的事情

sample code

```javascript
document.querySelector('a').addEventListener('click', function () {
    // GA or call API or do somethong
});
```

以紀錄 GA 為例

但是如果是紀錄 GA 點擊事件就會有許多區域要記錄點擊來瞭解使用者點哪個區域較多, 就要在不同區域綁定不同的 GA 但日子一久或程式變大的情況要找哪有綁 GA 就很不好找, 所以這時就需要有個 interface 來統整這事情

```javascript
document.querySelector('#item').addEventListener('click', function () {
    // GA or call API or do somethong
    interfaceGa(this);
});

document.querySelector('#banner').addEventListener('click', function () {
    // GA or call API or do somethong
    interfaceGa(this);
});

function interfaceGa(argument) {
    var name = argument.getAttribute('data-ga');
    switch(name) {
        case 'product-items':
            ga('send', 'event', 'items', 'click', argument.getAttribute('data-name'));
            break;
        case 'product-banner':
            ga('send', 'event', 'banner', 'click', argument.getAttribute('data-name'));
            break;
    }
}
```

![interface.png](http://user-image.logdown.io/user/3170/blog/3202/post/736758/kBxO0u4RPmhv5InIM6zW_interface.png)

這樣就很好管理 GA 事件且在頁面上的 DOM 也可以快速知道該 component 是負責什麼 GA 事件, 因為可以快速查到

在其他用法上 interface 重要的是有個能判別的點, 然後再用 `switch` 去選擇該做的事, 只是該例子是把 switch 要判斷的東西擺在 DOM 的 data attribute

還可加個有趣的用法

```javascript
function interfaceGa(argument) {
    var name = argument.getAttribute('data-ga'),
        status;
    switch(name) {
        case 'product-items':
            status = true;
            if (status) {
                ga('send', 'event', 'items', 'click', argument.getAttribute('data-name'));
            }
            break;
        case 'product-banner':
            status = true;
            if (status) {
                ga('send', 'event', 'banner', 'click', argument.getAttribute('data-name'));
            }
            break;
    }
}
```

當你要管理的事情如果臨時要開開關關或是依需求需要開關, 這也會方便管理

所以以上要說的就是在程式變複雜時可以適當地把許多定義出有要做的事情做一層 interface 管理

這似乎是某個設計模式, 但我也臨時找不出這是叫啥設計模式...
