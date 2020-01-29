---
layout: post
title: 'PHP - Geoip 設定 隨手紀錄'
date: 2018-01-09
comments: true
categories: [PHP geoip]
---
## PHP - Geoip 設定 隨手紀錄

之前有依照 php.net 中的文章設定

http://php.net/manual/en/book.geoip.php#117240

但在某次 php 升版後有點問題

所以放棄該用法

改採用 [GeoIP2-php](https://github.com/maxmind/GeoIP2-php) 這套件來處理

這是一個 MAXMIND 的服務出的套件, 也有其他程式語言的套件

其實 php.net 那方法是 MAXMIND 舊的方法, geoip2 是他們現在新的用法與服務

這服務有做 GeoIP 和 欺詐檢測 的服務

具體欺詐檢測有做啥我就沒研究了

[官網](https://www.maxmind.com/en/home)

過程我就不詳細介紹了

因為文件都有

這邊會介紹一些要注意的地方

主要是用 composer 安裝

然後用 autoload 載入

這流程應該 php 開發者會比較清楚, 反正也有 step by step 的教學與 sample code 可以看

```php
<?php
require_once 'vendor/autoload.php';
use GeoIp2\Database\Reader;

// This creates the Reader object, which should be reused across
// lookups.
$reader = new Reader('/usr/local/share/GeoIP/GeoIP2-City.mmdb');

// Replace "city" with the appropriate method for your database, e.g.,
// "country".
$record = $reader->city('128.101.101.101');

print($record->country->isoCode . "\n"); // 'US'
print($record->country->name . "\n"); // 'United States'
print($record->country->names['zh-CN'] . "\n"); // '美国'

print($record->mostSpecificSubdivision->name . "\n"); // 'Minnesota'
print($record->mostSpecificSubdivision->isoCode . "\n"); // 'MN'

print($record->city->name . "\n"); // 'Minneapolis'

print($record->postal->code . "\n"); // '55455'

print($record->location->latitude . "\n"); // 44.9733
print($record->location->longitude . "\n"); // -93.2323
```

這有個關鍵點

相信有玩過 GeoIP 的都清楚其實他就是個查表的行為, 會需要查 ip 對應的國家或城市

那這套當然也需要個 database

他有兩種 database 的格式 `mmdb` 和 `csv`

我是用 `mmdb`, 文件也建議用 mmdb

資料分兩種

1. geolite2 - 免費

    [geolite2](http://dev.maxmind.com/geoip/geoip2/geolite2/)

2. geoip2 - 付費

    [geoip2](https://www.maxmind.com/en/geoip2-city)

當然不用我說明應該也知道付費的會有更齊全的資料

所以這段

```php
$reader = new Reader('/usr/local/share/GeoIP/GeoIP2-City.mmdb');
```

就改成下載下來的 datebase file 的位置即可

當前(2.7.0) names 的語言還沒支援繁中, 只有簡中, 所以忽視它吧

他也有文件說明要如何呈現哪些資料

[http://maxmind.github.io/GeoIP2-php/](http://maxmind.github.io/GeoIP2-php/)

[GeoIP2 PHP API v2.7.0](http://maxmind.github.io/GeoIP2-php/doc/v2.7.0/)

稍微用了一下這套還不錯

如果只是測試有另一個服務叫 [ip-api](http://ip-api.com/)

有 api 可以用

http://ip-api.com/json

也支持 jsonp

http://ip-api.com/json?callback=geoip

所以前端可以直接用

但建議測試就好
