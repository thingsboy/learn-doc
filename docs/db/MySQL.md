# MySQL数据库

> 关于MySQL关系型数据库的文档说明。

## 1. 连接远程MySQL

```mysql
mysql -h [远程ip] -P [端口] -u root -p[密码]
```

# 2. 使用数据库

```mysql
use database;
```

mysql -h 127.0.0.1 - P 3306 -u root -pmysql

show databases;

use card-terminal;

show tables;

alter table table_name add 字段  varchar(100) null;

ALTER TABLE table_name CHANGE 当前字段 目标字段 int(11) NULL;