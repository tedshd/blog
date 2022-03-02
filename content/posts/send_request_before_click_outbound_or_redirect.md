---
title: "在點擊連結或是 redirect 前送出請求"
date: 2022-03-02T11:21:17+08:00
draft: false
categories: [javascript, safari, browser]
---

## Intro

有時在看 GA 的 Web 數據時會發現在 Safari 的點擊 click 事件似乎會比較少

其實這背後是有原因的

主要是各個瀏覽器再處理新 direct 時的行為不一致所導致的

在 Safari 上面發生 direct 到新的 URL 的行為(超連結或是 JS 處理) 時

事件觸發過程中的任何請求會中斷甚至不會發出請求

所以這就是為何在 GA 中的 Safari 的 click 數量會有些異常的原因

雖然 GA 預設會做 setTimeout 處理

但是也不一定是百分之百處理成功

所以最佳處理方式還是自己在用個 settimeout 包起來後再 direct

像是以下範例

```javascript
link.addEventListener('click', (e) => {
  e.preventDefault();

  window.gtag('event', 'click', {
    event_category: 'link'
  });

  setTimeout(() => {
    location.href = e.target.href
  }, 250)
})
```

如果真的要確保 GA 送完才做 direct

GA 也有提供事件發送的 callback 處理

[Know when an event has been sent](https://developers.google.com/analytics/devguides/collection/gtagjs/sending-data#know_when_an_event_has_been_sent)

但是如果網路不好的話或是 GA 事件發送請求太久會造成卡畫面的問題

是不太建議使用

同理

在自己處理 click 要發送紀錄 log 之類的行為更是要這樣處理

[Refer - tracking-outbound-link-clicks-in-google-analytics.markdown](https://github.com/EyalAr/Tech-Blog-Posts/blob/master/posts/tracking-outbound-link-clicks-in-google-analytics.markdown)

## 加碼

在自己設計發送 log 的情況時(例如需要額外的點擊紀錄等)

建議直接採用 GET 的方式發送然後也不要等回傳

可以使用以下的方式處理

```javascript
const apiLog = function (type, data) {
  const logImage = new Image(0, 0)
  logImage.classList.add('log_image')
  logImage.src = 'https://example.com/log?type=' + type + '&data=' + data
  document.body.appendChild(logImage)
  setTimeout(() => {
    let img = document.querySelectorAll('.log_image')[0]
    if (img) {
      img.outerHTML = ''
      img = null
    }
  }, 100)
}
```