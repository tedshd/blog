---
title: "Web 服務確認 IP Location 的幾種做法"
date: 2022-04-25T10:15:23+08:00
draft: false
categories: [web, ip]
---

## Intro

在很多實務上的需求, 需要了解 client 過來的請求是來自哪裡或來自哪個國家

最常見的方式就是依靠來源的 IP 判斷(這裡排除 proxy, VPN 或造假來源的因素)

而在 HTTP protocol 中, 會把 IP 附在 header(至於帶在哪個 header 與支援哪些 header 主要取決於各個語言對 HTTP 的實作)

[header Sample](https://tedshd.io/demo/php/ip.php)

上述範例只是取幾個比較常見的會帶上去的 header

至於更加詳細的 header 支援與取得 IP 時需要注意哪些事情可以參考以下文章

[Refer - 如何正確的取得使用者 IP？](https://devco.re/blog/2014/06/19/client-ip-detection/)

而為何可以用 IP 能夠確認出是在哪個地區國家甚至城市呢?

主要是因為有 IANA(Internet Assigned Numbers Authority) 進行了 IP 網段的分配

又有細分 ABCDE 級網段

這裡先大略講一下

相關資訊可以去看網路概論等相關的資料

[Refer - 各國IPv4位址分配列表](https://zh.wikipedia.org/wiki/%E5%90%84%E5%9C%8BIPv4%E4%BD%8D%E5%9D%80%E5%88%86%E9%85%8D%E5%88%97%E8%A1%A8)

[Refer - 已分配的/8 IPv4位址網段列表](https://zh.wikipedia.org/wiki/%E5%B7%B2%E5%88%86%E9%85%8D%E7%9A%84/8_IPv4%E5%9C%B0%E5%9D%80%E5%9D%97%E5%88%97%E8%A1%A8)

## 方法

現在有幾種方法可以處理這件事情

但是經有上述的介紹可以知道其實最主要的基本判斷就是得知道哪些 IP 段對應哪些國家

那接下來就是有哪些方法可以來做這件事了

大致上分兩個方向

1. 自己處理

2. 使用第三方服務處理

第一種方式就是自己建立與維護一組 IP table 的資料庫

來比對哪些 IP 對應的國家

比較常用的有 [GeoIP2](https://www.maxmind.com/en/geoip2-services-and-databases?lang=en) 和 [GeoLite2](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data??lang=en)

GeoIP2 需要付費, 但是更新頻繁, 也可以對應較多的區域城市細節

GeoLite2 免費, 但只能查到國家

記得還有一些服務也有提供 IP table 資料庫

也可以多找找看

第二種方式是我個人比較喜歡的方式, 主要是不用自己維護 IP table

主要會有幾種方式可以處理

1. 掛 CDN 服務或第三方服務使用服務提供的 header

2. 使用 Cloudflare worker 建立 API 來取資料

3. 使用 https://ip-api.com/ 服務來取得 location

AWS 的 CDN 服務 cloudfront

[Adding the CloudFront HTTP headers](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-cloudfront-headers.html)

header 有 `cloudfront-viewer-country` 可以取得 ISO 3166 的國家代碼

Cloudflare 設定

[Configuring Cloudflare IP Geolocation](https://support.cloudflare.com/hc/en-us/articles/200168236-Configuring-Cloudflare-IP-Geolocation)

設定完之後

就可以在 header 收到 `cf-ipcountry` 的 header 就會是 ISO 3166 的國家代碼

我個人是覺得掛 CDN 是相對簡單解決的方法

至於使用 Cloudflare worker 也是個不錯的方案

只要設定好跑 worker 的 url

然後要跑的 code 範例

```JavaScript
addEventListener("fetch", event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  return new Response(JSON.stringify({
    "country": request.cf.country
  }), {
    headers: {
    "Content-Type": "application/json"
    }
  })
}
```

這樣就會回傳請求時的國家了

[Refer - Request](https://developers.cloudflare.com/workers/runtime-apis/request/)
[Refer - Response](https://developers.cloudflare.com/workers/runtime-apis/response/)

當然 worker 免費方案下也是有請求限制

ip-api 的話已經是現成的 API 了

可以直接使用

免費方案也是有請求限制的

## 總結

自己搞 ip table 的方式和使用 cloudfront 與 cloudflare 的方式都比較適合是在 server 端判斷 location 會用到

worker 和 ip-api 適合是需要在 client 時判斷用

不過 ip-api 的 api 支援帶入 ip 取 local, 所以就可以在 server 使用

## 最後補充

因為很少在用 GCP

問了相關專業人士後

其實 GCP 的服務也有類似的方式可以處理

是掛在 GCP 的 Cloud Load Balancing 裏面

[Create custom headers in backend services](https://cloud.google.com/load-balancing/docs/https/custom-headers)

如果要用 cloud function 或是 App Engine 也是有特別的 header 可以用

[Request Headers and Responses](https://cloud.google.com/appengine/docs/standard/go/reference/request-response-headers)

[Refer - Free IP-based GeoLocation with Google Cloud Functions](https://medium.com/mop-developers/free-ip-based-geolocation-with-google-cloud-functions-f92e20d47651)