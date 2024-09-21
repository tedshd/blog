---
title: "MySQL export import 紀錄"
date: 2024-05-05T03:46:07+08:00
draft: false
categories: []
---

## Intro

紀錄一下 MySQL 匯出與匯入資料的一些情況

## 匯出

```shell
mysqldump --column-statistics=0 -u <user> -h <host> -P 3306 -p <database> > output_file.sql
```

`--column-statistics=0` 忽略掉一些匯出時的一些資訊, 節省容量

匯出資料庫中個別的 table

```shell
mysqldump --column-statistics=0 -u <user> -h <host> -P 3306 -p <database> <table> > output_file.sql
```

## 匯入

```shell
 mysql -u <user> -h <host> -P 3306 -p <database> < ./file.sql
```

如果要忽略一些錯誤並強制執行可以添加 `-f`

```shell
 mysql -f -u <user> -h <host> -P 3306 -p <database> < ./file.sql
```

## troubleshooting

## 如果遇到有 table 的欄位是使用 binary 的形式像是 point 匯出時在匯入會出現格式錯誤

如果欄位中有以 `point` 的型態儲存經緯度數據

有可能會出現這個問題 `ERROR 1416 (22003): Cannot get geometry object from data you send to the GEOMETRY field`

這時候就需要添加 `--hex-blob` 參數

[mysqldump — A Database Backup Program](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html#option_mysqldump_hex-blob)

```shell
mysqldump --column-statistics=0 --hex-blob -u <user> -h <host> -P 3306 -p <database> > file.sql
```

## 如果遇到匯入時的權限而且無法改變要匯入的 mysql 的使用者的權限時

出現像是 `Access denied; you need (at least one of) the SUPER or SYSTEM_VARIABLES_ADMIN privilege(s) for this operation` 的錯誤

而且你使用的 user 是無法透過

```sql
GRANT SUPER ON *.* TO 'your_username'@'localhost';
FLUSH PRIVILEGES;
```

等指令改權限

可以移除掉 .sql 中部分的內容來略過

`SET @@SESSION.SQL_LOG_BIN= 0;`

`SET @@GLOBAL.GTID_PURGED=/*!80000 '+'*/ '';`

`SET @@SESSION.SQL_LOG_BIN = @MYSQLDUMP_TEMP_LOG_BIN;`

[Access denied; you need (at least one of) the SUPER privilege(s) for this operation](https://stackoverflow.com/a/59454713)