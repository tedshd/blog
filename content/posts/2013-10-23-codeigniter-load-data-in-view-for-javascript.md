---
layout: post
title: 'Codeigniter - load data in view for JavaScript'
date: 2013-10-23
comments: true
categories: [Codeignite]
---
## load data in view for JavaScript

如果要從後端帶資料給 JavaScript, 很常用 AJAX 的方式, 但假如是頁面在 load 進來時就需要使用後端的資料, 一開始就把資料帶在頁面上然後再用 JavaScript 取得頁面上的資料是一個較佳的方式(至少說省下一個 request).

### controller
```php
<?php

...
public function index()
{
    // TODO $server_data load data for JavaScript
    $server_data = array(
        "data_01" => array(
            "title" => "title 01",
            "num" => 01,
            "con" => array(
                "con_01" => "news",
                "con_02" => "sport",
                "con_03" => "tech",
            ),
        ),
        "data_02" => array(
            "title" => "title 02",
            "num" => 02,
            "con" => array(
                "con_01" => "life",
                "con_02" => "movie",
                "con_03" => "cars",
            ),
        ),
    );

    // do something

    $data["static_data"] = json_encode($server_data);
    $this->load->view("welcome", $data);
}
...

?>
```

### views
```php
<!-- show data on views and hide it -->
<input id="server-data" type="hidden" value='<?php echo $static_data; ?>'>
```

### JavaScript(jQuery)
```javascript
var data;
data = $.parseJSON($('#server-data').val());
// data is object
```
