### MySQL基本操作

#### 启动MySQL

```shell
sudo mysql 
sudo mysql -A  # 添加 -A 参数，不预读表结构
sudo mysql -u 用户名  # 指定登录用户 
```

### 新建数据库

```mysql
create database mysql_test;
```

#### 连接数据库

```mysql
use mysql_test;
```

#### 新建数据表(book)

这里**新建了一个 `book` 的数据表**，并且有 `id` 和 `name` 两个字段

```mysql
create table book (
    book_id int primary key, 
    book_name char(20) not null
);
```

#### 展示数据表名字

```mysql
show tables;
```

#### 插入数据

这里三种方法插入数据，其中第一和第二种相同，第三种 `name` 字段会为默认会是 `NULL` ，但是因为上面设置表的时候，这个字段是 `not null` 的，所以会报错。

```mysql
insert into book(book_id, book_name) values(01, 'b1');
insert into book values(02, 'b2');
insert into book(book_id) values(03);
```

#### 查看数据表内容

```mysql
use library;
select * from book;

mysql> select * from book;
+---------+-----------+
| book_id | book_name |
+---------+-----------+
|       1 | b1        |
|       2 | b2        |
+---------+-----------+
2 rows in set (0.00 sec)
```

#### 删除数据表

删除 `book` 这个数据表。

```mysql
drop table book;
```

#### 删除数据库

```mysql
drop database library;
```

#### 查看warnings

```mysql
show warnings;
```

#### 加载SQL脚本

```mysql
source /home/cookiery/MySQL/SQL4/MySQL-04-01.sql
```

