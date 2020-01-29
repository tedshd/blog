---
layout: post
title: 'Google Cloud Platform - Study Log'
date: 2015-09-28
comments: true
categories: [google cloud platform, google]
---
## Google Cloud Platform - Study Log

### Intro

之前有幸參加亞太區 Google Cloud Platform 發表會, 聽完後就有點心動(因為價錢低於 AWS), 但ㄧ直沒時間研究怎麼用就這樣拖了很久...

加上之前用的網路空間不穩又常常換硬體主機, 換完就要重建帳號很麻煩(雖然是免費的, 但去常常在假日跟我一起休息...)

所以打算把 demo code 和一些小東西丟到 GCP 試試, 改用 GCP(開始要花錢了...)

### Service type

#### Compute Engine

[Google Compute Engine](https://cloud.google.com/compute/)

簡單說就是 AWS 的 EC2

就是在上面 run VM 開 web service 的服務

### Usage for me

[f1-micro (vCPUs: shared, RAM: 0.60 GB) * does not support local SSD - 10GB storage](https://cloud.google.com/products/calculator/#id=09d716db-1840-4c5d-90b2-4e9f6449590a)

這樣 USD 5, 不含流量

但基本上對外流量是 1GB USD 0.01

所以還好

GCP 還有個優勢就是利用它呼叫 Google service 的 API(Map, youtube...) 是不算流量的(free!)

1. 先開個 VM

![螢幕快照 2015-09-29 下午4.13.09.png](http://user-image.logdown.io/user/3170/blog/3202/post/302354/jOyuia6MR5KEWR8yXI0S_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-09-29%20%E4%B8%8B%E5%8D%884.13.09.png)

2. 設定 SSH key

![螢幕快照_2015-09-29_下午8_00_04.png](http://user-image.logdown.io/user/3170/blog/3202/post/302354/THj1yAEvQ7a8FfCD8OCW_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-09-29_%E4%B8%8B%E5%8D%888_00_04.png)

3. 設定成靜態 IP, 這跟 AWS 一樣有組靜態 IP, 設定綁完給 VM 用就不會再算錢

![螢幕快照_2015-09-29_下午8_00_18.png](http://user-image.logdown.io/user/3170/blog/3202/post/302354/VY3oI7wQ52QIhA7j7otd_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-09-29_%E4%B8%8B%E5%8D%888_00_18.png)

4. 如果別人要 SSH 進來的話, 就到**中繼資料**加 key

![螢幕快照 2015-09-29 下午4.12.37.png](http://user-image.logdown.io/user/3170/blog/3202/post/302354/CPqWJD7R2XfUoffkjUoA_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-09-29%20%E4%B8%8B%E5%8D%884.12.37.png)

### Some help data

首頁

[Google Cloud Computing, Hosting Services & Cloud Support — Google Cloud Platform](https://cloud.google.com/)

價錢計算機

[Google Cloud Platform Pricing Calculator - Google Cloud Platform](https://cloud.google.com/products/calculator/)

Compute Engine 計價方式

[Google Compute Engine Pricing - Compute Engine - Google Cloud Platform](https://cloud.google.com/compute/pricing)

[流量計價方式](https://cloud.google.com/compute/pricing#network)
