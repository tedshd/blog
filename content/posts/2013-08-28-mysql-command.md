---
layout: post
title: 'MySQL command'
date: 2013-08-28
comments: true
categories: [mysql]
---
## MySQL Monitor

### Setting
```
mysql -u root -h <HOST> -P <PORT> <DATABASE_NAME> -p -A
```

### Command

每一個 command 最後都要加 ;
```
status;
create database 資料庫名稱;
drop database 資料庫名稱;
show databases;
use 資料庫名稱;
select database();
create table 資料表名稱(欄位名稱1 資料型別1,欄位名稱2 資料型別2);
create table 資料表名稱(欄位名稱1 資料型別1,欄位名稱2 資料型別2) charset=utf8;
show tables;
確認資料表的欄位結構
drop table 資料表名稱;
desc 資料表名稱;
show create table <table name>
```

| 欄位1 | 欄位2 | 欄位3 |
|------|-------|------|
| 資料1 | 資料2 | 資料3 |

寫入資料
```
insert into 資料表名稱 (欄位名稱1,欄位名稱2) value(資料1,資料2);
```
顯示資料
```
select 欄位名稱1,欄位名稱2 from 資料表名稱;
select * from 資料表名稱;
select * from <table name> limit 5;
select id,create_time from <table name> limit 5;
select * from <table name> where id = '123';
```

### 資料型別

int
float
double

顯示欄位型別

```
show columns from <table>
```

### 字串型別
varchar -- 最多到255字
text
輸入時要加引號
如要輸入’
\’

### 日期時間型別

datetime--2011-8-8 00:00:00
date--2011-8-8
year--2011
time--00:00:00

sql TYPE timestamp

```
// PHP
$timestamp = date("Y-m-d H:i:s");
```

### 修改 table 裡 column 的編碼改成 utf8mb4

```mysql
alter table <table name> modify <column> varchar(255) CHARACTER SET utf8mb4
```

### troubleshooting

On Mac
Q:
```
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```
A:
mysql 沒啟動

```
mysql.server start
```

or 設定沒有設定 socket 的路徑

for mac brew 安裝的 mysql 在 `/usr/local/var/mysql` 所以設定就設定該路徑(底下不必有 mysql.sock)

```
[client]
socket=/usr/local/var/mysql/mysql.sock
[mysqld]
socket=/usr/local/var/mysql/mysql.sock
```
