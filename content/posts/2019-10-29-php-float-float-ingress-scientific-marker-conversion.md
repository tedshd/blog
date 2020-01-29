---
layout: post
title: 'php - float 浮點數科學記號轉換'
date: 2019-10-29
comments: true
categories: [php]
---
## php - float 浮點數科學記號轉換

[php - float](https://www.php.net/manual/en/language.types.float.php)

php 的浮點數大小受限於系統, 且會自動轉換成科學記號呈現, 但是一般人不會去看科學記號

```php
echo 0.0000234;
// 2.34E-5
```

在呈現上希望轉換回小數點的呈現

可以用以下方法做到

```php
$s = 0.0000234;
trim(rtrim(sprintf("%.10f", $s), '0'), '.');
// 0.0000234
```

這邊 `sprintf` 只取 10 位數

因為就之前遇到的系統超過 10 位數都會是不精確的浮點數
