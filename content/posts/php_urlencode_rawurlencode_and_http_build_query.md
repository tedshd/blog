---
title: "PHP - 使用 urlencode rawurlencode 的差異和使用 http_build_query"
date: 2021-01-14T17:21:53+08:00
draft: false
categories: [PHP]
---

## 最近剛好遇到個問題就順便筆記一下(但是遇到的問題和要寫的內文無關就是了 XD)

## 前言

基本上在 url query string 的 value 都要做 **url encode**

URL encode 會用到以下標準

[RFC 1738](https://tools.ietf.org/html/rfc1738)

[RFC 2396](https://tools.ietf.org/html/rfc2396)

[RFC 3986](https://tools.ietf.org/html/rfc3986)

主要會使用 `%` 字符來針對需要 escape 的字元做編碼

ex: `/` -> `%2F`, `+` -> `%2B` 等

但是主要又有幾個問題是基於 HTTP `GET` 和 `POST` 與 `application/x-www-form-urlencoded` 的問題

基本上在使用 HTML form 表單使用時

採用的會是把 ` ` 空格轉成 `+`

但這些都不算是大問題

因為基於 CGI 和程式語言的實作

會把 urldeode 回來

所以在程式語言接到 query string 時都是 urldecode 回來的值

**問題是在於 browser 上發出到 server 的 URL(就是打開 server 的 access log 看到進來的 Path 拉)**

就是該 URL 是不是有在 query string 上是經過 urlencode 的

一但是沒有 urlencode 的

server 接進來後可能就會有問題

給個最簡單的例子

我要搜尋 iphone7+

URL 就會是 `https://www.example.com/?q=iphone7%2B`

如果你的 URL 是 `https://www.example.com/?q=iphone7+`

程式語言接到的 query string 就會變成 `iphone7 `

當然就不是所預期的結果

正常的情況下如果是走 HTML submit

這樣當然在 input 填入 `iphone7+`

在 submit 時 browser 會幫你把 url encode

但是如果你是個 **a link**

是絕對不能用 `<a href="https://www.example.com/?q=iphone7+">iphone7+</a>`

得用 `<a href="https://www.example.com/?q=iphone7%2B">iphone7+</a>`

所以要記住一個原則

**要讓 server 收到的 URL 它的 query string 得是經過 url encode 的**

所以有些地方就得注意了

1. a link 的 url query string 得是 url encode 的

2. AJAX 在處理 API 時, 如果是 GET, query string 是要經過 url encode 的

也許有人會疑惑為啥在寫 web 時 2 的情況在使用時都沒有處理 url encode 阿

因為 library 已經幫你處理掉了

如果自己手刻一個 XMLHttpRequest 或是用 Postman 之類的工具去試試一個 GET 的 API 然後不處理 url encode 的話

就會出現問題了

那有人會疑惑說 POST 不用處理嗎?

POST 還真的不用處理

因為 POST 資料是在 content 裡面的

不是帶在 URL 上面

講了一堆廢話

還有一個要注意的重點

### 就是關於 ` ` 和 `+` 和 `%20` 的糾葛

PHP 有兩個 function

`urlencode`

`rawurlencode`

兩個 function 的實作的 RFC 是不同

簡單的說就是如下

```PHP
php > echo urlencode(' ');
+
php > echo rawurlencode(' ');
%20
```

兩種 encode 的結果會是不一樣的

**所以要注意的是用哪種 encode 就要用哪種 decode**

### 個人偏好

因為把 ` ` 轉成 `+` 是很古老的用法

且在一些情況底下容易出錯(但這種錯誤大多是使用上造成的錯誤), 基本上堅守著 **用哪種方式 encode 就用哪種方式 decode** 的原則就不太會有問題

所以當有問題發生時請先確認兩端的 encode decode 方式是否一致

因為大多數都是這個問題

## 遇到的問題

扯了那麼多廢話

現在才要開始講踩到的一個雷就是

在使用 `http_build_query` 時沒注意到的部分...

如前面提到的其實在 url query string 接進來時會自動處理 urldecode 回來原來的樣子

然後有個需求就是要做一個 redirect

redirect 有個重要的要點就是要處理 query string 決定要留哪些 query string 或過濾掉不要的 query string 後在 redirect 到新的 URL

所以身為一個懶人工程師當然是會用到 [http_build_query](https://www.php.net/manual/zh/function.http-build-query.php) 這個好用的 function

首先當然是要把當前的 URL 取出來處理

所以很理所當然的就是用到 [parse_url](https://www.php.net/manual/en/function.parse-url.php) 這個好用的 function

然後再把取出來的 query 用 [parse_str](https://www.php.net/manual/en/function.parse-str.php) 轉成 array

在做一些處理後就丟到 `http_build_query`

這樣完美的新 query string 就出來了誒

太棒了

```PHP
function url_update_query($url = '', $query_string = [])
  {
    $url_data = parse_url($url);
    $query_array = [];
    if (isset($url_data['query'])) {
      $query_data = $url_data['query'];
      parse_str($query_data, $query_array);
    }
    if (!empty($query_string)) {
      foreach ($query_string as $key => $value) {
        $query_array[$key] = $value;
      }
      $url_data['query'] = http_build_query($query_array, null, '&', PHP_QUERY_RFC3986);
    }

    $scheme   = isset($url_data['scheme']) ? $url_data['scheme'] . '://' : '';
    $host     = isset($url_data['host']) ? $url_data['host'] : '';
    $port     = isset($url_data['port']) ? ':' . $url_data['port'] : '';
    $user     = isset($url_data['user']) ? $url_data['user'] : '';
    $pass     = isset($url_data['pass']) ? ':' . $url_data['pass']  : '';
    $pass     = ($user || $pass) ? "$pass@" : '';
    $path     = isset($url_data['path']) ? $url_data['path'] : '';
    $query    = isset($url_data['query']) ? '?' . $url_data['query'] : '';
    $fragment = isset($url_data['fragment']) ? '#' . $url_data['fragment'] : '';

    return $scheme . $user . $pass . $host . $port . $path . $query . $fragment;
  }
```

然後上線後

就開始收到 error 了...

雖然使用情境不是上述的例子就是了(但也是一樣是 query string 相關的)

那為啥會寫一大串是因為我都照了上面的情況排查了一遍發現都不是上述的問題...

最後去檢查 access log 發現是有的過來的 log 根本就是沒有 url encode...

只是目前還沒找出來為何會有沒有 url encode 的來源

因為來源的連結全部都是有處理過的...

而且也不是 100% 的 log 都是沒處理的...

又因為不是重要的頁面所以 log 沒有加 User Agent(因為我們有做 log filter, 為了可以倒進去 elasticsearch 去用 kibana 看, 所以只有 filter 重要的值出來)

更新添加 User Agent 後再繼續觀察

[Refer - 百分號編碼](https://zh.wikipedia.org/wiki/%E7%99%BE%E5%88%86%E5%8F%B7%E7%BC%96%E7%A0%81)
