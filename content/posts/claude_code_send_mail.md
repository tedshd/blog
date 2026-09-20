---
title: "claude code 操作發送信件"
date: 2026-09-20T19:56:16+08:00
draft: false
categories: [claude code, ai]
---

# claude code 操作發送信件

## 前言

因為公司業務需求有時候要常常臨時發信或是批次發信

甚至需要臨時要有 cc 或是 bcc 的情況

在後台寫一個介面功能要顧及所有功能也是很麻煩

所以嘗試用 LLM 來操作發信的情況

## 前置作業

準備能夠發信的 client 程式

我這邊的案例是使用 mailgun + PHP

這個對不懂程式的人來說可以直接叫 claude code 或是 gemini 去完成

剩下的就是規劃流程和工作方式

## 流程

每個人可以依照情境和需求自己規劃流程和工作方式

我的規劃會有以下檔案

* mail_template_xxx.md
* mail_list.csv
* mail_log.csv
* send_mail.php
* config.json

### mail_template_xxx.md

信件範本的 markdown

例如 `mail_template_反饋追蹤.md`, `mail_template_新功能發佈.md`, 等等

markdown 內容格式

```
    ## subject

    [服務名稱] 功能反饋問題回覆

    ## content

    ```text
    [使用者名稱]，您好：<br><br>

    感謝貴機關共同支持 XXX 建置與推動！<br><br>

    如操作上有任何疑問，歡迎來信洽詢，我們將盡快協助您。<br>
    感謝您的支持與配合<br><br>
    ```

```

### mail_list.csv

收件人的列表

```csv
email, fullname,
ted@xxx.com.tw,許OO
lin@xxx.com.tw,林OO
```

### mail_log.csv

信件發送的紀錄

必須讓 `send_mail.php` 裡面有發信後把該次發信紀錄到這個檔案的功能

我這邊自己定義了

收信信箱,姓名,主旨,內容,發送時間

### send_mail.php

發信的程式

### config.json

mailgun 設定

## 實戰

最好全程在 `plan mode` 或是 `manual mode`

```
現在我要確認寄信的功能
目前都還是規劃
不要寄出
現在有新的 backend/scripts/mail_send/mail_list.csv
要依照 backend/scripts/mail_send/mail_template_新功能發佈.md
當作範本寄出
## content 裡面的 [使用者名稱]
要換成 backend/scripts/mail_send/mail_list.csv 裡面的 fullname
幫我確認
backend/scripts/mail_send/standalone_send_mail.php 能夠滿足需求嗎?
另外也要確認發信後是不是會更新記錄到 backend/scripts/mail_send/mail_log.csv
```

```
幫我跑第一個
backend/scripts/mail_send/mail_list.csv
ted@xxx.com.tw,許OO
試試看
```

```
好,那就正式寄給全部 81 位收件人吧
```
