---
layout: post
title: 'Coding Style'
date: 2013-09-10
comments: true
categories: [javascript, develop]
---
## Coding Style

### 條件判斷

在 PHP & JavaScript 中有許多邏輯判斷
當有許多條件要去檢查時, 一般來說就是用 **if** 一直寫下去
最後就造成下面的情況(以 PHP 為例)
```php
if ($a === $b)
{
    if ($c)
    {
        if ($c >= 10)
        {
            if ($d)
            {
                // do something
                // ...
            }
        return;
        }
    return;
    }
}
```
這樣下去就沒完沒了, 而且縮排會越來越多, 要看 code 也很不方便
所以假如就已作條件檢查來說
可以用以下的做法
```php
// check condition 1
if ($a !== $b)
{
    return;
}

// check condition 2
if (!$c || $c === '')
{
    return;
}

// check condition 3
if ($c < 9)
{
    return;
}

// check condition 4
if (!d)
{
    return;
}

// do something
// ...
```
做個 **反向思考** , 把不適合的條件列出再一一 return or 作處理
剩下的便是所需要的
> 從巢狀式結構變成區域式
> 結構也較為清晰
> debug 也較容易

有時也會遇到應該用 **switch** 卻用 **if** 去一直加下去的情況
所以當 **if** 用到 __*3 個*__ 以上時, 就要思考要用什麼敘述來達到目的比較好
也許可以用 ```switch```

### function

有時遇到很多 code 重複時, 我們可以抽離這些重複的部分, 把它放到一個 function 中
要用時在再去呼叫那個 function

[Refer-代码的抽象三原则](http://www.ruanyifeng.com/blog/2013/01/abstraction_principles.html)

### 以錯誤為優先處理

JavaScript

```javascript
function doSomething(data) {
    if (data.status === 'fail') {
        // handle error
    } else {
        // handle ok
    }
}
```
