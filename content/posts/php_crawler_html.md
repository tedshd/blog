---
title: "PHP 爬蟲 抓取 HTML 內容"
date: 2022-04-22T15:43:33+08:00
draft: false
categories: [PHP, crawler]
---

## Intro

又是久違的寫爬蟲...

這次是接手大大們的 code

寫的是 PHP 版本

研究了一下寫法

才發現現在可以不使用第三方套件就可以處理了

所以這裡紀錄一下

## 取得 HTML 內容

1. 使用 curl
2. 使用 file_get_contents

curl 是我常用的方式
看了大大們的 code 才知道原來 file_get_contents 也可以取 http/https 內容...

這邊簡單貼一下兩種作法的範例

### curl

```PHP
function httpGet($url)
{
  $ch = curl_init();

  curl_setopt($ch,CURLOPT_URL,$url);
  curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
  curl_setopt($ch,CURLOPT_HEADER, [
    'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36'
  ]);

  $output=curl_exec($ch);

  curl_close($ch);
  return $output;
}
```

### file_get_contents

```PHP
function htmlContentGet($url) {
  $opts = [
    "http" => [
        "method" => "GET",
        "header" => "User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36\r\n"
    ]
  ];

  return file_get_contents($url, false, stream_context_create($opts));
}
```

如果需要一些特別的 header 或是 querystring 就在各自處理

另外提一下, 用 file_get_contents 也可以抓取本地檔案, 所以也可以打開本地的 html file(至少我以前用 file_get_contents 都是用來打開本地檔案的)

[refer - PHP: file_get_contents - Manual](https://www.php.net/manual/en/function.file-get-contents.php)

## 抓取 DOM

研究了一下也有不少方式可以做

因為上面方法回來的是 string

所以接下來最重要的事情是如何擷取出想要的內容

大致有兩種方式

1. 用 preg_replace, str_replace, strpos, substr 等方法處理
2. 針對 DOM 轉成物件來處理

各有優缺點

就看最後決定要怎麼做

這裡針對 2 的處理方式來處理

```PHP
$dom = new DOMDocument();
$dom->loadHTML($html_string, LIBXML_NOERROR);
```

這裡又細分兩種處理方式

1. DOM HTML
2. XPath

### DOM HTML

```PHP
$dom = new DOMDocument();
$dom->loadHTML($html_string, LIBXML_NOERROR);
$documentElement = $dom->documentElement;
```

### XPath

```PHP
$dom = new DOMDocument();
$dom->loadHTML($html_string, LIBXML_NOERROR);
$xpath = new DOMXpath($dom);
```

這兩種的差別就在於支援的取 DOM 的方式不同

documentElement 這個 Class 底下取得 DOM 物件的方法名稱大多和 JavaScript 的名稱一樣

可以參考以下文件

[refer - PHP: DOMElement - Manual](https://www.php.net/manual/en/class.domelement.php)

以下列舉一些範例

```PHP
$span = $documentElement->getElementsByTagName('span');

foreach( $span as $item ) {
    echo $item->textContent . "\n";
}

$img = $documentElement->getElementsByTagName('img');

foreach( $img as $item ) {
  echo $item->getAttribute('src') . "\n";
}
```

比較可惜的是它沒有抓取 class 的方式

這種情況就可以用取 XPath 的方式來做

基本上我個人是比較喜歡 XPath 的方式

因為相對比較好用

後續要調整也相對容易, 只要改動 XPath 就可以了

```PHP
$xpath = new DOMXpath($dom);
$desc = $xpath->query("/html/body/div[2]/div[2]/div/div[1]/a/img");

foreach( $desc as $item ) {
  echo $item->getAttribute('src') . "\n";
}
```

[refer - How to Parse HTML using PHP Native Classes](https://codingreflections.com/how-to-parse-html-using-php-native-classes/)

[refer - PHP: DOMDocument - Manual](https://www.php.net/manual/zh/class.domdocument.php)

## 結語

以上的方式都只適用於 SSR 的頁面

如果內容是動態產生的一律建議直接用打 API 的方式去拿內容