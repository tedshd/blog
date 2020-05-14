---
title: "php - 載入文字轉成圖片"
date: 2020-05-14T09:50:42+08:00
draft: false
categories: ['php']
---

## 需求

讀取一段文字後

可以決定字型

最後要轉成圖片

## 使用的工具

* php7.2

* freetype

提前說明需要用到 GD(這通常預設就啟動了)

freetype 通常會需要另外安裝

如何先檢查有沒有 GD 和 freetype

先用 phpinfo 檢查即可

```shell
-> % php -a
Interactive shell

php >
```

之後再打

```PHP
echo phpinfo();
```

就會 output 資訊了

在搜尋 `gd`

```shell
gd

GD Support => enabled
GD Version => bundled (2.1.0 compatible)
GIF Read Support => enabled
GIF Create Support => enabled
JPEG Support => enabled
libJPEG Version => 9 compatible
PNG Support => enabled
libPNG Version => 1.6.32
WBMP Support => enabled
XBM Support => enabled
```

有安裝過 freetype 的話

就會一起顯示 **FreeType Support**

```shell
gd

GD Support => enabled
GD Version => bundled (2.1.0 compatible)
FreeType Support => enabled
FreeType Linkage => with freetype
FreeType Version => 2.10.1
GIF Read Support => enabled
GIF Create Support => enabled
JPEG Support => enabled
libJPEG Version => 9 compatible
PNG Support => enabled
libPNG Version => 1.6.37
WBMP Support => enabled
XBM Support => enabled
WebP Support => enabled
```

目前環境是 Mac OSX 10.14.6

安裝 freetype 的方式大致上有三種

1. 重新編譯 PHP

2. brew 安裝新的 PHP

3. [用別人寫的安裝 PHP 的指令](https://php-osx.liip.ch/)

因為剛好之前是用 Mac 自帶的 PHP 來用(PHP 7.1.23)

就順便用 brew 安裝 PHP 7.2 也順便改成用 brew 安裝的 PHP 7.2 當之後本地端的開發

brew 安裝完後其實就也一起裝好 freetype 了

這裡額外提一下自己其實有部分的開發都用 docker 開發了, 因為 PHP 版本不一(升級成本太高了, 且 PHP 不是開發主力) 所以就用 docker 封裝管理不同的服務

所以得注意一下 PHP 語法和 extension 的支援

[Refer - macos缺少freetype終極解決方案](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/41900/)

[Refer - Mac缺少freetype解决方案](https://blog.si-yee.com/2019/03/19/Mac%E7%BC%BA%E5%B0%91freetype%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88/)

## Code

先使用 `imagettftext`

[Refer](https://www.php.net/manual/zh/function.imagettftext.php)

需要再使用 `imagepng` 來輸出成圖片

[Refer](https://www.php.net/manual/en/function.imagepng.php)

以下為簡單的範例

```PHP

// 先建立一個畫布
$im = imagecreatetruecolor(1400, 320);

// 建立顏色
$white = imagecolorallocate($im, 255, 255, 255);
$black = imagecolorallocate($im, 0, 0, 0);
// 建立一個塗滿背景的區域
imagefilledrectangle($im, 0, 0, 1400, 320, $white);

// 文字
$text = '中文繁體 text';
// 字型
$font = 'NotoSansTC-Regular.otf';
// 輸出的檔案
$file = 'font.png';

// 添加文字到圖片中
imagettftext($im, 112, 0, 10, 160, $black, $font, $text);
// 輸出成 PNG
imagepng($im, $file, 9);
```

當然要輸出成其他圖片格式 PHP 也有 `imagejpeg` 等 function 可以使用
