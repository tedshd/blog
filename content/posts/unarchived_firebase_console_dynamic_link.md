---
title: "Unarchived firebase console dynamic link"
date: 2022-10-22T21:05:11+08:00
draft: false
categories: [fierbase]
---

Sometimes a dynamic link is accidentally archived.

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2FScreen_Shot_2022-10-22_at_9_17_52_PM.png?alt=media&token=af826e6a-8d67-40bb-8f17-f8c5fd2ca7c8)

But doesn't have any option show archived dynamic link list.

BTW

You have a way to unarchived this dynamic link.

## Use POST API update this dynamic link

1. Find your filebase console auth data

You can edit dynamic link data and then catch request when save it.

Find this request `https://firebasedurablelinks-pa.clients6.google.com/v1/updateDurableLink?alt=json&key=<YOUR KEY>` and copy header

2. Build POST data

```shell
curl --location --request POST 'https://firebasedurablelinks-pa.clients6.google.com/v1/updateDurableLink?alt=json&key=<YOUR KEY>' \
--header 'Authorization: <YOUR Authorization>' \
--header 'Origin: https://console.firebase.google.com' \
--header 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.1.2 Safari/605.1.15' \
--header 'Referer: <REFER YOUR PROJECT LINK>?linkUrl=<YOUR ARCHIVED DYNAMIC LINK>' \
--header 'Host: firebasedurablelinks-pa.clients6.google.com' \
--header 'Cookie: <YOUR COOKIE>' \
--header 'X-Goog-AuthUser: <REFER YOUR ORIGIN REQUEST>' \
--header 'Content-Type: text/plain' \
--data-raw '{"durableLink":{"shortDurableLink":{"link":"<YOUR ARCHIVED DYNAMIC LINK>"}},"newDurableLink":{"shortDurableLink":{"visibility":"UNARCHIVED"}},"newDurableLinkMask":"short_durable_link","projectInfo":{"projectNumber":"<YOUR PROJECT NUMBER>"}}'
```

Finally you can unarchived this dynamic link.

Have a nice day.

[Refer - Where are archived Dynamic Links?](https://stackoverflow.com/questions/54086964/where-are-archived-dynamic-links)