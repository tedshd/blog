---
layout: post
title: "Let's Encrypt - Has a certificate problem in Android Chrome"
date: 2016-07-17
comments: true
categories: [ssl, nginx]
---
## Let's Encrypt - Has a certificate problem in Android Chrome

If you use Let's Encrypt as SSL certificate

Then setting this in Nginx

```config
ssl_certificate /etc/letsencrypt/live/<domain>/cert.pem;
```

You can find it maybe has problem in Android Chrome

Now you can modify this

```config
ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
```

### Test your SSL

[SSL Server Test](https://www.ssllabs.com/ssltest/index.html)



[Refer - Let’s encrypt certificate not working for Andriod’s Google Chrome](https://community.letsencrypt.org/t/lets-encrypt-certificate-not-working-for-andriods-google-chrome/7184)
