---
title: "使用 IMAP & SMTP 來加強處理 Gmail"
date: 2021-01-12T10:18:11+08:00
draft: false
categories: []
---

## Intro

Gmail 提供 IMAP & SMTP 的功能

#### 內送郵件 (IMAP) 伺服器

* imap.gmail.com
* 需要安全資料傳輸層 (SSL)：是
* 通訊埠：993

#### 外寄郵件 (SMTP) 伺服器

* smtp.gmail.com
* 需要安全資料傳輸層 (SSL)：是
* 需要傳輸層安全性 (TLS)：是 (如果可用)
* 需要驗證：是
* 安全資料傳輸層 (SSL) 通訊埠：465
* 傳輸層安全性 (TLS)/STARTTLS 通訊埠：587

[Refer - 透過其他電子郵件平台查看 Gmail](https://support.google.com/mail/answer/7126229)

簡單的說 IMAP(Internet Message Access Protocol) 可以存取該 mail 的信件

SMTP(Simple Mail Transfer Protocol) 是可以利用該 mail 發信

詳細說明可以參照 wiki

[Refer - 網際網路資訊存取協定](https://zh.wikipedia.org/wiki/%E5%9B%A0%E7%89%B9%E7%BD%91%E4%BF%A1%E6%81%AF%E8%AE%BF%E9%97%AE%E5%8D%8F%E8%AE%AE)

[Refer - 簡單郵件傳輸協定](https://zh.wikipedia.org/wiki/%E7%AE%80%E5%8D%95%E9%82%AE%E4%BB%B6%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE)

另外還有 POP3(Post Office Protocol) 這個和 IMAP 類似的協定

[Refer - 郵局協定](https://zh.wikipedia.org/wiki/%E9%83%B5%E5%B1%80%E5%8D%94%E5%AE%9A)

主要 POP3 和 IMAP 的差異主要差在 POP3 是把信件內容拉下來, IMAP 不會, IMAP 是即時連線存取, 但是 IMAP 的好處就是即時連線同步, 這樣在多個裝置就可以即時的更新信件的狀態

所以在一些常見的客戶端程式例如 outlook 或是 Mac OS 裡面的郵件都是利用這些協定在處理 email

這邊當然也可以利用支援這些協定的程式語言寫一些功能來處理 email

## 使用情境

因為公司的服務每天會有大量的 feedback mail 寄到設定的 Gmail 信箱

雖然會有實習生協助整理和處理 feedback mail 但是還是很花人力

這年頭最貴的就是人力了

所以公司有個基於 Python 的程式在協助處理 feedback mail

那程式主要做的事情就是簡單的辨識 SPAM 與替 feedback 的內容打上 tag 以便於之後快速處理使用者的 feedback

## How to do?

1. 先開啟 Gmail 裡面的 IMAP 的功能

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-11%20%E4%B8%8B%E5%8D%884.04.52.png?alt=media&token=be7f6b2c-28bf-4716-bda3-35e8a890507c)

2. 設定用於第三方應用程式驗證的密碼(並非 Google OAuth)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-11%20%E4%B8%8B%E5%8D%884.09.50.png?alt=media&token=85f3770d-ee49-4163-b0d1-c3bb8cb49cc2)

![](https://firebasestorage.googleapis.com/v0/b/storage-bucket-83851.appspot.com/o/blog%2F%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202021-01-11%20%E4%B8%8B%E5%8D%884.11.15.png?alt=media&token=84d05c47-29c7-4bae-8786-735afad5f7a4)

3. 開始寫程式

## 怎麼開始寫 code?

這邊以 Python 為例

在開始前得先搞懂流程要幹什麼

1. 連接 IMAP server
2. 撈信件
3. 讀取信件主旨(subject) 和信件內容(content) 和確認附件(attachement)

### smaple code

以下使用 Python

#### 建立 IMAP server 連去信箱讀取信件

```python
from datetime import datetime, timedelta, date

import imaplib
import email

from email.header import decode_header
# pip install imap-tools
from imap_tools.imap_utf7 import encode, decode

ACCOUNT = '@gmail.com'
PWD = ''

mail = imaplib.IMAP4_SSL('imap.gmail.com')
mail.login(ACCOUNT, PWD)
status, data = mail.list()
mail.select('inbox')
# 取前一天的時間
today = (date.today() - timedelta(1)).strftime("%d-%b-%Y")
# 找出前一天未讀的信件
typ, data = mail.search(None, '(UNSEEN)', '(SENTSINCE {0})'.format(today))

# 取到 message id list(message id 就是每封信的 id)
ids = data[0]
id_list = ids.split()

for i in id_list:
    typ, data = mail.fetch(i, '(RFC822)')
    if typ == 'OK':
        print('get mail ok')

    for response_part in data:
            if isinstance(response_part, tuple):
                rawMail = response_part[1].decode()
                # 取得信件
                msg = email.message_from_string(rawMail)
```

基本上到這裡拿到 msg 就是這封信件的資訊了

就可以取出來做一些處理

例如: 判斷來信者來回信, 判斷內容替信件添加標籤 等等

關於 `imap.search` 可以如何使用可參考

[Refer - Python's imaplib (Example)](https://coderwall.com/p/gorteg/python-s-imaplib)

#### 回信

幾本上回信也是寄信的一種

寄信的部分就是得用到 SMTP

幾本上的流程就是

1. 連接 Gmail 的 SMTP server

2. 寫信

3. 寄信

4. 關閉連接

以下為範例

