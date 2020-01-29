---
layout: post
title: 'Apache - dir permission cnfig'
date: 2015-05-07
comments: true
categories: [apache]
---
## Apache - dir permission cnfig

If yooouo want use virtual host

Yoou can set `/etc/apache2/extra/httpd-vhosts.conf` this file

Add

```shell
<Directory /Users/ted/tedadev/local/bomb01>
    AllowOverride All
    Options Indexes MultiViews FollowSymLinks
    Require all granted
</Directory>
<VirtualHost *:80>
    DocumentRoot "/Users/ted/tedadev/local/bomb01"
    ServerName www.bomb01.com
    ErrorLog "/Volumes/RamDisk/ysm-error.log"
    CustomLog "/Volumes/RamDisk/ysm-access.log" common
</VirtualHost>
```

[Refer - Forbidden 403, You don’t have permission to access /~username/ on this server](http://coolestguidesontheplanet.com/forbidden-403-you-dont-have-permission-to-access-username-on-this-server/)
