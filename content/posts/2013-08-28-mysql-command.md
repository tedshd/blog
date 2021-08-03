---
layout: post
title: "MySQL command"
date: 2013-08-28
comments: true
categories: [mysql]
---

## MySQL Monitor

### Setting

```sql
mysql -u root -h <HOST> -P <PORT> <DATABASE_NAME> -p -A
```

### database

每一個 command 最後都要加 `;`

```sql
status;
create database database_name;
drop database database_name;
show databases;
show tables;
use database_name;
```

### table

```sql
create table table_name(
    column1 type1,
    column2 type2);
create table table_name(
    column1 type1,
    column2 type2) charset=utf8;


desc table_name;
show create table <table_name>

```

[MySQL 8.0 Reference Manual :: 3.3.2 Creating a Table - MySQL](https://dev.mysql.com/doc/refman/8.0/en/creating-tables.html)

[13.1.20 CREATE TABLE Statement - MySQL :: Developer Zone](https://dev.mysql.com/doc/refman/8.0/en/create-table.html)

| 欄位 1 | 欄位 2 | 欄位 3 |
| ------ | ------ | ------ |
| 資料 1 | 資料 2 | 資料 3 |

寫入資料

```sql
insert into 資料表名稱 (欄位名稱1,欄位名稱2) value(資料1,資料2);
```

顯示資料

```sql
select 欄位名稱1,欄位名稱2 from 資料表名稱;
select * from <table_name>;
select * from <table_name> limit 5;
select id,create_time from <table_name> limit 5;
select * from <table_name> where id = '123';
```

#### 刪除該 table 所有的資料

1. TRUNCATE

auto_increment 的欄位會 reset

```sql
truncate table <table_name>;
```

2. DELETE

```sql
delete from <table_name>;
// or
delete from <table_name> where id<100;
```

刪除全部資料的效能: TRUNCATE > DELETE

#### 刪除該 table

```sql
drop table <table_name>;
```

[MySQL – DELETE, TRUNCATE 及 DROP 的分別](https://www.opencli.com/mysql/mysql-truncate-delete-drop-difference)

### 資料型別

顯示欄位型別

```sql
show columns from <table>
```

### 字串型別

varchar -- 最多到 255 字
text
輸入時要加引號
如要輸入 `’\’`

### 日期時間型別

datetime--2011-8-8 00:00:00
date--2011-8-8
year--2011
time--00:00:00

sql TYPE timestamp

```php
// PHP
$timestamp = date("Y-m-d H:i:s");
```

```sql
CREATE TABLE t1 (
  created TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

[11.2.5 Automatic Initialization and Updating for TIMESTAMP and DATETIME](https://dev.mysql.com/doc/refman/8.0/en/timestamp-initialization.html)

## 修改欄位名稱

```sql
ALTER TABLE <table_name> CHANGE <old> <new> <varchar(255)>;
```

### 修改 table 裡 column 的編碼改成 utf8mb4

```sql
alter table <table_name> modify <column> varchar(255) CHARACTER SET utf8mb4
```

### where 多筆資料

```sql
SELECT * FROM users where id in (1,2,3,4,5);
```

### dump table

```shell
mysqldump -A --ssl-mode=DISABLED -u <user> -p<password> -h <host> <database> <table> | mysql -u root -h <host> -P <post> <database>
```

必要時需要另外添加參數

```shell
--column-statistics=0 --lock-tables=false
```

[Refer - mysqldump — A Database Backup Program](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html#option_mysqldump_column-statistics)

### 直接把 query 出來的一筆資料新增(複製)

```sql
insert into <table> (欄位1, 欄位2, 欄位3) select 欄位1, 欄位2, 欄位3 from <table> where id=10;
```

### troubleshooting

On Mac
Q:

```shell
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```

A:
mysql 沒啟動

```shell
mysql.server start
```

or 設定沒有設定 socket 的路徑

for mac brew 安裝的 mysql 在 `/usr/local/var/mysql` 所以設定就設定該路徑(底下不必有 mysql.sock)

```shell
[client]
socket=/usr/local/var/mysql/mysql.sock
[mysqld]
socket=/usr/local/var/mysql/mysql.sock
```

### Reference

[Basic MySQL Tutorial](https://www.mysqltutorial.org/basic-mysql-tutorial.aspx)
