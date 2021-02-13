### SELECT检索数据

#### SELECT语法基本格式

```mysql
select 要查询的列名 from 表名字 where 限制条件;
```

如果要查询表中的所有内容，使用星号（*）。

例子：

查看employee表中的name和age：

```mysql
select name,age from employee;
select name,age from employee where age>25;
select name,age,phone from employee where name='Mary';
```

#### "AND"和"OR"

WHERE后面的限制条件

