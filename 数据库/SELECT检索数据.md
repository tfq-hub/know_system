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

```mysql
select name,age from employee where age<25 or age>30;
select name,age from employee where age>25 and age<30;
```

如果需要包含25和30两个数字的话

```mysql
select name,age from employee where age between 25 and 30;
```

#### "IN"和"NOT IN"

用于筛选“在”或“不在”某个范围内的结果

```mysql
select name,age,phone,in_dpt from employee where in_dpt in ('dpt3', 'dpt4');
select name,age,phone,in_dpt from employee where in_dpt not in ('dpt1', 'dpt3');
```

#### LIKE

like用来实现模糊匹配，和like联用的通常还有通配符，代表未知字符。

SQL中的通配符是`_`和`%`，其中`_`代表一个未指定字符，`%`代表不定个未指定字符。

```mysql
select name,age,phone from employee where phone like '1101__';
select name,age,phone from employee where name like 'J%';
```

#### ORDER BY

对结果排序，ASC：升序，DESC：降序。

```mysql
select name,age,phone,salary from employee order by salary DESC;
```

#### 内置函数和计算

| 函数名 | COUNT | SUM  | AVG      | MAX    | MIN    |
| ------ | ----- | ---- | -------- | ------ | ------ |
| 作用   | 计数  | 求和 | 求平均值 | 最大值 | 最小值 |

count可以用于任何类型，因为只是计数用，而sum、avg函数只能对数字类数据类型做计算，max和min可用于数值、字符串或是日期时间数据类型。

```mysql
select max(salary) as max_salary, min(salary) from employee;
```

as关键字可以给值重命名，比如最大值被命名为了 max_salary。

#### 子查询

```mysql
select of_dpt, count(proj_name) from project group by of_dpt having of_dpt in (select in_dpt from employee where name='Tom');
```

上面句子包含了两个select语句，第二个select语句将返回一个集合，然后被第一个select语句用in来进行判断。

having关键字和where关键字作用类似，都是用来进行条件筛选操作，区别在于having用于对分组后的数据进行筛选。

#### 连接查询（多表查询）

使用join xxx on语句

```mysql
select id,name,people_num from employee join department on employee.in_dpt = department.dpt_name order by id;
```

#### join和left join

join等同于inner join，即内连接，不满足on条件会直接过滤掉。

left join等同于left outer join，左外连接，不满足on条件的会保留左边那张表的数据，右边表数据直接显示NULL。

right join同上。

