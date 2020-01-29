---
layout: post
title: 'php - loop directory'
date: 2017-12-13
comments: true
categories: [PHP]
---
## php - loop directory

Sometime need use php loop directory list all file in this directory

```php

$directory = scandir('./js');
foreach($directory as $file) {
    if ($file === '.' || $file === '..') {
        continue;
    }
    echo $file;
    echo "\n";
}

```
