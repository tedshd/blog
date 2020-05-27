---
title: "在數位中所定義與使用語言與文字的規範"
date: 2020-05-25T16:56:05+08:00
draft: false
categories: []
---

## 前言

因為最近在做一些語系的整理

為了字型的關係

就整理了一下一些在數位資訊上面有關於文字與語言的一些規範

這裡會概括了系統與軟體開發與輸入裝置的處理

因為資訊量太廣

所以不一定會有個脈絡

基本上只有大概分一段一段的說明

## 初心者的誤區

1. 國家和語言有很強的關聯

這是很多人一開始處理多國語系都會有個誤解的

常常在系統中看到 `en-US`, `zh-TW`, `ja-jp`

就會下意識的把語言和國家綁定在一起

然後結果就是在該國家紙能顯示該語言

但現實是每個國家都不一定都只有使用一個語言啊~~

新加坡同時普遍用中文和英文(官方語言是英文)

2. 以為在限定的國家或系統才能使用限定的語言

這和上一個很類似, 以為用到某個國家的系統或是使用某個系統設定在某些國家就會限制了語言

這是錯誤的觀念

記住

**語言和國家沒絕對關係**

**語言和國家沒絕對關係**

**語言和國家沒絕對關係**

3. 拉丁文就是英文

這後面會提到

4. 語言和文字在定義上的有強烈的關係

在廣義的定義下確實如此

但真正探究下去其實不應該這樣說

這後面會提到

5. 鍵盤上沒有注音符號還是可以打中文啊

那現在很多鍵盤都沒有倉頡符號

那不就沒辦法用倉頡輸入法了嗎?

## 來講一下文字

有時大家常常聽到拉丁文這個東西

那麼拉丁文究竟是什麼文字?

相信不少人就會說英文啊

沒錯

但不太正確

英文就是拉丁文字的其中一部分

那拉丁文又是從哪裡來呢?

這又有點牽扯到語言了

現在最廣泛的語系算是[印歐語系](https://zh.wikipedia.org/wiki/%E5%8D%B0%E6%AC%A7%E8%AF%AD%E7%B3%BB)

而其中的[拉丁語系](https://zh.wikipedia.org/wiki/%E6%8B%89%E4%B8%81%E8%AF%AD)在古歐洲經由羅馬帝國向外發展

所以[拉丁字母](https://zh.wikipedia.org/wiki/%E6%8B%89%E4%B8%81%E5%AD%97%E6%AF%8D)也就很廣泛的使用(文化侵略的結果)

上面提到英文是拉丁文部分之一

是因為實際上拉丁文不只是 A ~ Z 26 個字母

德文, 法文等也是用拉丁字母

但是這些語言額外多有各種音對應的字母

所以會有所謂的[延伸拉丁字母](https://zh.wikipedia.org/wiki/%E8%A1%8D%E7%94%9F%E6%8B%89%E4%B8%81%E5%AD%97%E6%AF%8D)

| 尖音 | 重音 | 折音 | 分音/德語變音 | 軟音 | 鼻音 | 鼻化元音 | 合字 | 來自盧恩字母 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Á É Í Ó Ú Ý | À È Ì Ò Ù | Â Ê Î Ô Û | Ä Ë Ï Ö Ü Ÿ | Ç Ş | Ã Õ Ñ | Ą Ę Į Ų | Æ Œ Ø Ĳ | Þ |
| á é í ó ú ý | à è ì ò ù | â ê î ô û | ä ë ï ö ü ÿ | ç ş | ã õ ñ | ą ę į ų | æ œ ø ĳ ß | þ |

這邊後面再輸入裝置時會在特別提到

## 語言與地區規範

### 文字

[ISO 15924](https://zh.wikipedia.org/wiki/ISO_15924)

也有應用在字型上

字型的 metadata 會跟你說該字型有哪些文字可以用

下圖為 Google 有名的自創字體 noto 的繁體字型所帶有的資訊

![image](/images/螢幕快照_2020-05-26_下午4.22.39.png)

額外補充一下

因為大部分會是用 opentype 的字型

opentype 是微軟和 Adobe 共同開發的, 所以微軟的文件有詳細的介紹

所以這裡也貼一下 metadata 裡面的 table format 介紹

[OpenType™ Layout Common Table Formats](https://docs.microsoft.com/en-us/typography/opentype/spec/chapter2)

這裡有個網站可以上傳字型檔(必須是 opentype 格式, 即 `.otf`, `.ttf`, `.ttc`) 確認該字型的資訊

[font-inspector](https://opentype.js.org/font-inspector.html)

### 語言

[ISO 639](https://en.wikipedia.org/wiki/ISO_639)

普遍使用於各個系統中的語言代碼

底下目前有定義到 ISO 639-6

但是普遍使用的是 639-1 到 639-3

[ISO 639-1](https://zh.wikipedia.org/wiki/ISO_639-1%E4%BB%A3%E7%A0%81%E8%A1%A8) 列表

### 國家(地區)

[ISO 3166-1](https://zh.wikipedia.org/wiki/ISO_3166-1)

定義國家的代碼

都需要大寫

上述兩者常常以 `語言-國家` 或 `語言_國家` 的形式組合在一起

而大多的語言編碼都是基於 [BCP 47](http://www.rfc-editor.org/rfc/bcp/bcp47.txt)

`language-extlang-script-region-variant-extension-privateuse`

* language - 語言
* extlang - 地方語言擴充
* script - 文字
* region - 國家
* variant - 方言 [IANA](https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority) 定義
* extension
* privateuse

大多數的組合會是 `language-extlang-region`

在其中 [RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) 主要定義了用 `-` 連接

這邊得先提醒

在不同的系統中所採用的規範是略有所不同的

所以必須要清楚在哪些系統平台上是採用哪些規範

以免在程式處理上出現問題

這裡列舉一下常見的系統平台

### Web

通常是以 `Accept-Language` 為判定基礎

以 [BCP 47](http://www.rfc-editor.org/rfc/bcp/bcp47.txt) 定義了語系區域的呈現格式

[W3C - Language tags in HTML and XML](https://www.w3.org/International/articles/language-tags/#rfc) 有具體的說明

比較特別的一點是其實關於 region 並沒有規範強制要大寫

只是因為在 [ISO 3166-1](https://zh.wikipedia.org/wiki/ISO_3166-1) 中規定都要大寫

所以約定成俗

### Android

[開發文件](https://developer.android.com/reference/java/util/Locale)其實就有說明了

也一樣遵循 [BCP 47](http://www.rfc-editor.org/rfc/bcp/bcp47.txt)

* language 使用 ISO 639-2 / ISO 639-3

* script 使用 ISO [15924-4](https://zh.wikipedia.org/wiki/ISO_15924)

* region 使用 [ISO 3166-2](https://zh.wikipedia.org/wiki/ISO_3166-2) / [UN M.49 numeric-3](https://en.wikipedia.org/wiki/UN_M49)

但是有的人應該會發現為何 `toString` 後會是

`language + "_" + country + "_" + (variant + "_#" | "#") + script + "-" + extensions`

這樣的組合

ex: **zh_CN_#Hans**

因為這是基於 [ICU - International Components for Unicode](http://site.icu-project.org/home) 定義的規則

裡面的 [Locale](http://userguide.icu-project.org/locale)

### iOS

[Language and Locale IDs](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPInternational/LanguageandLocaleIDs/LanguageandLocaleIDs.html)

由 language 和 locale 組成

language 走 ISO 639-1 / 639-2

locale 走 ISO 3166-1

但是比較特別的是

locale

| Locale ID syntax | Examples | Description |
| --- | --- | --- |
| [language designator] | en, fr | An unspecified region where the language is used. |
| [language designator]_[region designator] | en_GB, zh_HK | The language used by and regional preference of the user. |
| [language designator]-[script designator] | az-Arab, zh-Hans | An unspecified region where the script is used. |
| [language designator]-[script designator]_[region designator] | zh-Hans_HK | The script used by and regional preference of the user. |

這條規則目前沒找到規範

但是文件也提到如果要更詳細的話也是要遵循 [BCP 47](http://www.rfc-editor.org/rfc/bcp/bcp47.txt) 的格式定義

### Linux

沒有標準的定義格式

[地區設定](https://zh.wikipedia.org/wiki/%E5%8C%BA%E5%9F%9F%E8%AE%BE%E7%BD%AE)

`language[_territory[.codeset]][@modifier]`

language 用 ISO 639-1

territory 用 ISO 3166-1

### Windows

Windowa Vista 之後使用 [RFC 4646](https://tools.ietf.org/html/rfc4646)

`<language>-<Script>-<REGION>_<sort order>`

## 來聊一下鍵盤輸入法

鍵盤上面所有的按鍵都是有定義標準的 key code

基本上就是那兩大家 MS 和 Apple 定義出來的

當然還有些按鍵因應各個廠商的需求會自己去定義, 這邊就不討論

所以這就有個問題了

鍵盤到底可不可以打出任何語言的文字?

答案是可以的

而且不分系統

以 Mac 為例

Mac 已經內建了所有語言的輸入法

只要切到該輸入法就可以輸入該語言的文字了

但會發現一個問題

有的文字沒有按鍵可以按

這又要牽扯到一個問題

鍵盤的 layout

有分 ISO, ANSI, JIS

有在用 Mac 外接鍵盤的應該都有看過

Mac 在外接鍵盤時會叫你按左 shift 右邊和右 shift 左邊

之後就會叫你選 layout

### ISO 對應歐規(歐洲的國家)

![image](/images/螢幕快照_2020-05-26_下午5.39.26.png)

### ANSI 對應美規(大部分的國家)

![image](/images/螢幕快照_2020-05-26_下午5.38.54.png)

### JIS 對應日規(日本)

![image](/images/螢幕快照_2020-05-26_下午5.40.04.png)

為何要分這三種 layout 是因為打字區需要的按鍵數量是不一樣的

ISO 需要有延伸拉丁字母

ANSI 只要 A ~ Z

JIS 也有一些獨立使用的按鍵

這些按鍵在系統都是讀得到 key code 的

只是輸入法有沒有對應的輸出而已

所以鍵盤底層的韌體會定義好該按鍵是要送什麼 keycode

而判定 keycode 是系統和輸入法的工作

所以真正影響的實際上只有鍵盤的 layout 和輸入法會打出什麼

和作業系統設定的語言與國家無關, 也和鍵盤上面的印字無關

### 結語

在整理字型時, 如果上述的東西需要有大概的了解

這樣對整理字型的使用會是更佳的容易
