# Introduction

> **[danger] 提示**
>
> 如果需要评论需要梯子！


# JOIN

* `left join` : 左连接，返回左表中所有的记录以及右表中连接字段相等的记录。
* `right join` : 右连接，返回右表中所有的记录以及左表中连接字段相等的记录。
* `inner join` : 内连接，又叫等值连接，只返回两个表中连接字段相等的行。
* `full join` : 外连接，返回两个表中的行：`left join + right join`。
* `cross join` : 结果是笛卡尔积，就是第一个表的行数乘以第二个表的行数。
* `关键字 on` : 数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。

* 1、 on 条件是在生成临时表时使用的条件，它不管 on 中的条件是否为真，都会返回左边表中的记录。
* 2、where 条件是在临时表生成好后，再对临时表进行过滤的条件。这时已经没有 left join 的含义（必须返回左边表的记录）了，条件不为真的就全部过滤掉。

# 基础语法

```sql
mysql> SELECT * FROM Websites;
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
+----+--------------+---------------------------+-------+---------+
```

## 通用数据类型

| 数据类型 |	描述 |
| --- | --- |
| `CHARACTER(n)` |	字符/字符串。固定长度 n。 |
| `VARCHAR(n)` 或 `CHARACTER VARYING(n)` | 字符/字符串。可变长度。最大长度 n。 |
| `BINARY(n)` |	二进制串。固定长度 n。 |
| `BOOLEAN` |	存储 `TRUE` 或 `FALSE` 值 |
| `VARBINARY(n)` 或 `BINARY VARYING(n)` | 二进制串。可变长度。最大长度 n。 |
| `INTEGER(p)` |	整数值（没有小数点）。精度 p。 |
| `SMALLINT` |	整数值（没有小数点）。精度 5。 |
| `INTEGER` |	整数值（没有小数点）。精度 10。 |
| `BIGINT` |	整数值（没有小数点）。精度 19。 |
| `DECIMAL(p,s)` |	精确数值，精度 p，小数点后位数 s。例如：decimal(5,2) 是一个小数点前有 3 位数，小数点后有 2 位数的数字。 |
| `NUMERIC(p,s)` |	精确数值，精度 p，小数点后位数 s。（与 DECIMAL 相同） |
| `FLOAT(p)` |	近似数值，尾数精度 p。一个采用以 10 为基数的指数计数法的浮点数。该类型的 size 参数由一个指定最小精度的单一数字组成。 |
| `REAL` |	近似数值，尾数精度 7。 |
| `FLOAT` |	近似数值，尾数精度 16。 |
| `DOUBLE PRECISION` |	近似数值，尾数精度 16。 |
| `DATE` |	存储年、月、日的值。 |
| `TIME` |	存储小时、分、秒的值。 |
| `TIMESTAMP` |	存储年、月、日、小时、分、秒的值。 |
| `INTERVAL` |	由一些整数字段组成，代表一段时间，取决于区间的类型。 |
| `ARRAY` |	元素的固定长度的有序集合 |
| `MULTISET` |	元素的可变长度的无序集合 |
| `XML` |	存储 XML 数据 |

### MySQL 数据类型

* Text(文本) 类型

| 数据类型 | 描述 |
| --- | --- |
| `CHAR(size)` | 	保存固定长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的长度。最多 255 个字符。 |
| `VARCHAR(size)` | 	保存可变长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的最大长度。最多 255 个字符。 <br> 注释：如果值的长度大于 255，则被转换为 TEXT 类型。 |
| `TINYTEXT` | 	存放最大长度为 255 个字符的字符串。 |
| `TEXT` | 	存放最大长度为 65,535 个字符的字符串。 |
| `BLOB` | 	用于 BLOBs（Binary Large OBjects）。存放最多 65,535 字节的数据。 |
| `MEDIUMTEXT` | 	存放最大长度为 16,777,215 个字符的字符串。 |
| `MEDIUMBLOB` | 	用于 BLOBs（Binary Large OBjects）。存放最多 16,777,215 字节的数据。 |
| `LONGTEXT` | 	存放最大长度为 4,294,967,295 个字符的字符串。 |
| `LONGBLOB` | 	用于 BLOBs (Binary Large OBjects)。存放最多 4,294,967,295 字节的数据。 |
| `ENUM(x,y,z,etc.)` | 	允许您输入可能值的列表。可以在 ENUM 列表中列出最大 65535 个值。如果列表中不存在插入的值，则插入空值。 <br> 注释：这些值是按照您输入的顺序排序的。 <br> 可以按照此格式输入可能的值： ENUM('X','Y','Z')|
| `SET` | 	与 ENUM 类似，不同的是，SET 最多只能包含 64 个列表项且 SET 可存储一个以上的选择。 |

* Number(数字) 类型

|数据类型 |	描述 |
| --- | --- |
|`TINYINT(size)`	|带符号-128到127 ，无符号0到255。|
|`SMALLINT(size)`	|带符号范围-32768到32767，无符号0到65535, size 默认为 6。|
|`MEDIUMINT(size)`	|带符号范围-8388608到8388607，无符号的范围是0到16777215。 size 默认为9|
|`INT(size)`	    |带符号范围-2147483648到2147483647，无符号的范围是0到4294967295。 size 默认为 11|
|`BIGINT(size)`	|带符号的范围是-9223372036854775808到9223372036854775807，无符号的范围是0到18446744073709551615。size 默认为 20|
|`FLOAT(size,d)`	|带有浮动小数点的小数字。在 size 参数中规定显示最大位数。在 d 参数中规定小数点右侧的最大位数。|
|`DOUBLE(size,d)`	|带有浮动小数点的大数字。在 size 参数中规显示定最大位数。在 d 参数中规定小数点右侧的最大位数。|
|`DECIMAL(size,d)`	|作为字符串存储的 DOUBLE 类型，允许固定的小数点。在 size 参数中规定显示最大位数。在 d 参数中规定小数点右侧的最大位数。|

* Date/Time(日期/时间) 类型

|数据类型 | 	描述 |
| --- | --- |
| `DATE()` |	日期。格式：YYYY-MM-DD <br> 注释：支持的范围是从 '1000-01-01' 到 '9999-12-31'|
| `DATETIME()` |	*日期和时间的组合。格式：YYYY-MM-DD HH:MM:SS <br> 注释：支持的范围是从 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'|
| `TIMESTAMP()` |	*时间戳。TIMESTAMP 值使用 Unix 纪元('1970-01-01 00:00:00' UTC) 至今的秒数来存储。格式：YYYY-MM-DD HH:MM:SS <br> 注释：支持的范围是从 '1970-01-01 00:00:01' UTC 到 '2038-01-09 03:14:07' UTC|
| `TIME()` |	时间。格式：HH:MM:SS <br> 注释：支持的范围是从 '-838:59:59' 到 '838:59:59'|
| `YEAR()` |	2 位或 4 位格式的年。 <br> 注释：4 位格式所允许的值：1901 到 2155。2 位格式所允许的值：70 到 69，表示从 1970 到 2069。|

## CREATE DATABASE

> `CREATE DATABASE` 语句用于创建数据库。

```sql
CREATE DATABASE dbname;
```

## CREATE TABLE

> `CREATE TABLE` 语句用于创建数据库中的表。

```sql
-- column_name 参数规定表中列的名称。
-- data_type 参数规定列的数据类型（例如 varchar、integer、decimal、date 等等）。
-- size 参数规定表中列的最大长度。
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```

```sql
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
```

### 约束（Constraints)

>* 约束用于规定表中的数据规则。约束可以在创建表时规定，或者在表创建之后规定(`ALTER TABLE`)。
>* `NOT NULL` - 指示某列不能存储 NULL 值。
>* `UNIQUE` - 保证某列的每行必须有唯一的值。
>* `PRIMARY KEY` - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
>* `FOREIGN KEY` - 保证一个表中的数据匹配另一个表中的值的参照完整性。
>* `CHECK` - 保证列中的值符合指定的条件。
>* `DEFAULT` - 规定没有给列赋值时的默认值。

```sql
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```

### NOT NULL 约束

> `NOT NULL` 约束强制列不接受 `NULL` 值。

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);

-- 在一个已创建的表的 "Age" 字段中添加 NOT NULL 约束
ALTER TABLE Persons MODIFY Age int NOT NULL;
-- 在一个已创建的表的 "Age" 字段中删除 NOT NULL 约束
ALTER TABLE Persons MODIFY Age int NULL;
```

### UNIQUE 约束

>* `UNIQUE` 约束唯一标识数据库表中的每条记录。
>* `UNIQUE` 和 `PRIMARY KEY` 约束均为列或列集合提供了唯一性的保证。

> **[warning] 注意**
>
> 每个表可以有多个 `UNIQUE` 约束，但是每个表只能有一个 `PRIMARY KEY` 约束。

```sql
CREATE TABLE Persons(
	P_Id int NOT NULL,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	UNIQUE (P_Id)
)

-- 添加约束
ALTER TABLE Persons ADD UNIQUE (P_Id)
-- 添加多字段约束
ALTER TABLE Persons ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)
-- 撤销约束
ALTER TABLE Persons DROP INDEX uc_PersonID
```

### PRIMARY KEY 约束 

>* `PRIMARY KEY` 约束唯一标识数据库表中的每条记录。
>* 主键必须包含唯一的值。
>* 主键列不能包含 `NULL` 值。
>* 每个表都应该有一个主键，并且每个表只能有一个主键。

```sql
CREATE TABLE Persons(
	P_Id int NOT NULL,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	PRIMARY KEY (P_Id)
)

-- 添加 PRIMARY KEY 约束
ALTER TABLE Persons ADD PRIMARY KEY (P_Id)
-- 撤销 PRIMARY KEY 约束
ALTER TABLE Persons DROP PRIMARY KEY
```

### FOREIGN KEY 约束 

> 一个表中的 `FOREIGN KEY` 指向另一个表中的 `UNIQUE KEY(唯一约束的键)`。

```sql
CREATE TABLE Orders (
	O_Id int NOT NULL,
	OrderNo int NOT NULL,
	P_Id int,
	PRIMARY KEY (O_Id),
	FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)
)

-- 添加约束
ALTER TABLE Orders ADD FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)
-- 撤销约束
ALTER TABLE Orders DROP FOREIGN KEY fk_PerOrders
```

### CHECK 约束 

>* `CHECK` 约束用于限制列中的值的范围。
>* 如果对单个列定义 CHECK 约束，那么该列只允许特定的值。
>* 如果对一个表定义 CHECK 约束，那么此约束会基于行中其他列的值在特定的列中对值进行限制。

```sql
-- 在 "Persons" 表创建时在 "P_Id" 列上创建 CHECK 约束。CHECK 约束规定 "P_Id" 列必须只包含大于 0 的整数。
CREATE TABLE Persons(
	P_Id int NOT NULL,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	CHECK (P_Id>0)
)

-- 定义多个列的 CHECK 约束
CREATE TABLE Persons (
	P_Id int NOT NULL,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')
)

ALTER TABLE Persons ADD CHECK (P_Id>0)
ALTER TABLE Persons DROP CONSTRAINT chk_Person
```

### DEFAULT 约束

> `DEFAULT` 约束用于向列中插入默认值。如果没有规定其他的值，那么会将默认值添加到所有的新记录。

```sql
CREATE TABLE Persons(
    P_Id int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) DEFAULT 'Sandnes'
)

ALTER TABLE Persons ALTER City SET DEFAULT 'SANDNES'
ALTER TABLE Persons ALTER City DROP DEFAULT
```

## CREATE INDEX

> `CREATE INDEX` 语句用于在表中创建索引。在不读取整个表的情况下，索引使数据库应用程序可以更快地查找数据。

```sql
CREATE INDEX index_name ON table_name (column_name)
```

## DROP

```sql
-- 删除表中的索引
DROP INDEX table_name.index_name

-- 删除表
DROP TABLE table_name

-- 删除数据库
DROP DATABASE database_name

-- 删除表内的数据，但并不删除表本身
TRUNCATE TABLE table_name
```

## ALTER

> `ALTER TABLE` 语句用于在已有的表中添加、删除或修改列。

```sql
-- 删除 "Person" 表中的 "DateOfBirth" 列
ALTER TABLE Persons DROP COLUMN DateOfBirth
```

## AUTO INCREMENT

> `Auto-increment` 会在新记录插入表中时生成一个唯一的数字。默认地，AUTO_INCREMENT 的开始值是 1，每条新记录递增 1。

```sql
CREATE TABLE Persons(
	ID int NOT NULL AUTO_INCREMENT,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	PRIMARY KEY (ID)
)
-- 设置 AUTO_INCREMENT 的起始值
ALTER TABLE Persons AUTO_INCREMENT=100
```

## SELECT DISTINCT

> `SELECT DISTINCT` 在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。

```sql
SELECT DISTINCT column_name,column_name FROM table_name;
```

```sql
mysql> SELECT DISTINCT country FROM Websites;
+---------+
| country |
+---------+
| USA     |
| CN      |
+---------+
```

## ORDER BY

>* `ORDER BY` 关键字用于对结果集按照一个列或者多个列进行排序。
>* `ORDER BY` 关键字默认按照**升序**对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

```sql
SELECT column_name,column_name
FROM table_name
ORDER BY column_name,column_name ASC|DESC;
```

```sql
order by A,B        -- 这个时候都是默认按升序排列
order by A desc,B   -- 这个时候 A 降序，B 升序排列
order by A ,B desc  -- 这个时候 A 升序，B 降序排列
```

## INSERT INTO

> `INSERT INTO` 语句用于向表中插入新记录。

```sql
INSERT INTO table_name VALUES (value1,value2,value3,...);
INSERT INTO table_name (column1,column2,column3,...) VALUES (value1,value2,value3,...);
```

INSERT INTO Websites (name, url, alexa, country) VALUES ('百度','https://www.baidu.com/','4','CN');

```sql
mysql> INSERT INTO Websites (name, url, alexa, country) VALUES ('百度','https://www.baidu.com/','4','CN');
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|  6 | 百度         | https://www.baidu.com/    |     4 | CN      |
+----+--------------+---------------------------+-------+---------+
```

> **[info] insert into select、select into from的区别？**
>
> Use this for infomation messages.

```sql
insert into scorebak select * from socre where neza='neza'   --插入一行,要求表scorebak 必须存在
select *  into scorebak from score  where neza='neza'  --也是插入一行,要求表scorebak 不存在
```

## UPDATE

> `UPDATE` 语句用于更新表中的记录。

```sql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```

```sql
mysql> UPDATE Websites SET alexa='5000', country='USA' WHERE name='菜鸟教程';
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/    |  5000 | USA     |
|  4 | 微博         | http://weibo.com/         |    20 | CN      |
|  5 | Facebook     | https://www.facebook.com/ |     3 | USA     |
|  6 | 百度         | https://www.baidu.com/    |     4 | CN      |
+----+--------------+---------------------------+-------+---------+
```

## DELETE

> `DELETE` 语句用于删除表中的记录。

```sql
DELETE FROM table_name
WHERE some_column=some_value;
```

```sql
mysql> DELETE FROM Websites WHERE name='Facebook' AND country='USA';
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | CN      |
|  6 | 百度         | https://www.baidu.com/  |     4 | CN      |
+----+--------------+-------------------------+-------+---------+
```

## SELECT TOP 子句

> `SELECT TOP` 子句用于规定要返回的记录的数目。

```sql
SELECT column_name(s)
FROM table_name
LIMIT number;
```

```sql
mysql> SELECT * FROM Websites LIMIT 2;
+----+--------+-------------------------+-------+---------+
| id | name   | url                     | alexa | country |
+----+--------+-------------------------+-------+---------+
|  1 | Google | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝   | https://www.taobao.com/ |    13 | CN      |
+----+--------+-------------------------+-------+---------+
```

## LIKE 操作符

> `LIKE` 操作符用于在`WHERE`子句中搜索列中的指定模式。
>* `%` 符号用于在模式的前后定义通配符（默认字母）。
>* `NOT` 选取不匹配模式的记录。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```

```sql
mysql> --选取 name 以字母 "G" 开始的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE 'G%';
+----+--------+------------------------+-------+---------+
| id | name   | url                    | alexa | country |
+----+--------+------------------------+-------+---------+
|  1 | Google | https://www.google.cm/ |     1 | USA     |
+----+--------+------------------------+-------+---------+

mysql> --选取 name 以字母 "k" 结尾的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE '%k';
Empty set (0.00 sec)

mysql> --选取 name 包含模式 "oo" 的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE '%oo%';
+----+--------+------------------------+-------+---------+
| id | name   | url                    | alexa | country |
+----+--------+------------------------+-------+---------+
|  1 | Google | https://www.google.cm/ |     1 | USA     |
+----+--------+------------------------+-------+---------+

mysql> --选取 name 不包含模式 "oo" 的所有客户
mysql> SELECT * FROM Websites WHERE name NOT LIKE '%oo%';
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | CN      |
|  6 | 百度         | https://www.baidu.com/  |     4 | CN      |
+----+--------------+-------------------------+-------+---------+
```

## 通配符

>* 通配符可用于替代字符串中的任何其他字符。
>* `%` 替代 0 个或多个字符。
>* `_` 替代一个字符。
>* `[charlist]` 字符列中的任何单一字符。MySQL 中使用 `REGEXP` 或 `NOT REGEXP` 运算符 (或 `RLIKE` 和 `NOT RLIKE`) 来操作正则表达式。
>* `[^charlist]`、`[!charlist]` 不在字符列中的任何单一字符。

```sql
mysql> -- 选取 name 以一个任意字符开始，然后是 "oogle" 的所有客户
mysql> SELECT * FROM Websites WHERE name LIKE '_oogle';
+----+--------+------------------------+-------+---------+
| id | name   | url                    | alexa | country |
+----+--------+------------------------+-------+---------+
|  1 | Google | https://www.google.cm/ |     1 | USA     |
+----+--------+------------------------+-------+---------+

mysql> -- 选取 name 以 "G" 开始，然后是一个任意字符，然后是 "o"，然后是一个任意字符，然后是 "le" 的所有网站
mysql> SELECT * FROM Websites WHERE name LIKE 'G_o_le';
+----+--------+------------------------+-------+---------+
| id | name   | url                    | alexa | country |
+----+--------+------------------------+-------+---------+
|  1 | Google | https://www.google.cm/ |     1 | USA     |
+----+--------+------------------------+-------+---------+

mysql> -- 选取 name 以 "G"、"F" 或 "s" 开始的所有网站
mysql> SELECT * FROM Websites WHERE name REGEXP '^[GFs]';
+----+--------+------------------------+-------+---------+
| id | name   | url                    | alexa | country |
+----+--------+------------------------+-------+---------+
|  1 | Google | https://www.google.cm/ |     1 | USA     |
+----+--------+------------------------+-------+---------+
```

## IN 操作符

> `IN` 操作符允许您在 WHERE 子句中规定多个值。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...);
```

```sql
mysql> -- 选取 name 为 "Google" 或 "菜鸟教程" 的所有网站
mysql> SELECT * FROM Websites WHERE name IN ('Google','菜鸟教程');
+----+--------------+------------------------+-------+---------+
| id | name         | url                    | alexa | country |
+----+--------------+------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/ |     1 | USA     |
|  3 | 菜鸟教程     | http://www.runoob.com/ |  5000 | USA     |
+----+--------------+------------------------+-------+---------+

mysql> SELECT * FROM Websites WHERE name='Google' OR name='菜鸟教程';
+----+--------------+------------------------+-------+---------+
| id | name         | url                    | alexa | country |
+----+--------------+------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/ |     1 | USA     |
|  3 | 菜鸟教程     | http://www.runoob.com/ |  5000 | USA     |
+----+--------------+------------------------+-------+---------+
```

## BETWEEN 操作符

>* `BETWEEN` 操作符用于选取介于两个值之间的数据范围内的值。这些值可以是数值、文本或者日期。

> **[info] 使用别名的场景**
>
>* 在查询中涉及超过一个表。
>* 在查询中使用了函数。
>* 列名称很长或者可读性差。
>* 需要把两个列或者多个列结合在一起。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

```sql
-- 选取 alexa 介于 1 和 20 之间的所有网站
mysql> SELECT * FROM Websites WHERE alexa BETWEEN 1 AND 20;
+----+--------+-------------------------+-------+---------+
| id | name   | url                     | alexa | country |
+----+--------+-------------------------+-------+---------+
|  1 | Google | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝   | https://www.taobao.com/ |    13 | CN      |
|  4 | 微博   | http://weibo.com/       |    20 | CN      |
|  6 | 百度   | https://www.baidu.com/  |     4 | CN      |
+----+--------+-------------------------+-------+---------+

mysql> SELECT * FROM Websites WHERE alexa NOT BETWEEN 1 AND 20;
+----+--------------+------------------------+-------+---------+
| id | name         | url                    | alexa | country |
+----+--------------+------------------------+-------+---------+
|  3 | 菜鸟教程     | http://www.runoob.com/ |  5000 | USA     |
+----+--------------+------------------------+-------+---------+

-- 选取 alexa 介于 1 和 20 之间但 country 不为 USA 和 IND 的所有网站
mysql> SELECT * FROM Websites WHERE (alexa BETWEEN 1 AND 20) AND country NOT IN ('USA', 'IND');
+----+--------+-------------------------+-------+---------+
| id | name   | url                     | alexa | country |
+----+--------+-------------------------+-------+---------+
|  2 | 淘宝   | https://www.taobao.com/ |    13 | CN      |
|  4 | 微博   | http://weibo.com/       |    20 | CN      |
|  6 | 百度   | https://www.baidu.com/  |     4 | CN      |
+----+--------+-------------------------+-------+---------+

mysql> SELECT * FROM access_log WHERE date BETWEEN '2016-05-10' AND '2016-05-14';
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
+-----+---------+-------+------------+
```

## 别名

```sql
-- 列的 SQL 别名语法
SELECT column_name AS alias_name FROM table_name;
-- 表的 SQL 别名语法
SELECT column_name(s) FROM table_name AS alias_name;
```

```sql
mysql> SELECT name AS n, country AS c FROM Websites;
+--------------+-----+
| n            | c   |
+--------------+-----+
| Google       | USA |
| 淘宝         | CN  |
| 菜鸟教程     | USA |
| 微博         | CN  |
| 百度         | CN  |
+--------------+-----+

-- 把三个列（url、alexa 和 country）结合在一起，并创建一个名为 "site_info" 的别名
mysql> SELECT name, CONCAT(url, ', ', alexa, ', ', country) AS site_info FROM Websites;
+--------------+-----------------------------------+
| name         | site_info                         |
+--------------+-----------------------------------+
| Google       | https://www.google.cm/, 1, USA    |
| 淘宝         | https://www.taobao.com/, 13, CN   |
| 菜鸟教程     | http://www.runoob.com/, 5000, USA |
| 微博         | http://weibo.com/, 20, CN         |
| 百度         | https://www.baidu.com/, 4, CN     |
+--------------+-----------------------------------+
```

* 示例： 选取 "菜鸟教程" 的所访问记录。我们使用 "Websites" 和 "access_log" 表，并分别为它们指定表别名 "w" 和 "a"

```sql
mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | CN      |
|  6 | 百度         | https://www.baidu.com/  |     4 | CN      |
+----+--------------+-------------------------+-------+---------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+
9 rows in set (0.00 sec)

mysql> SELECT w.name, w.url, a.count, a.date FROM Websites AS w, access_log AS a WHERE a.site_id=w.id and w.name="菜鸟教程";
+--------------+------------------------+-------+------------+
| name         | url                    | count | date       |
+--------------+------------------------+-------+------------+
| 菜鸟教程     | http://www.runoob.com/ |   100 | 2016-05-13 |
| 菜鸟教程     | http://www.runoob.com/ |   220 | 2016-05-15 |
| 菜鸟教程     | http://www.runoob.com/ |   201 | 2016-05-17 |
+--------------+------------------------+-------+------------+

-- 不带别名的相同的 SQL 语句
mysql> SELECT Websites.name, Websites.url, access_log.count, access_log.date  FROM Websites, access_log  WHERE Websites.id=access_log.site_id and Websites.name="菜鸟教程";
+--------------+------------------------+-------+------------+
| name         | url                    | count | date       |
+--------------+------------------------+-------+------------+
| 菜鸟教程     | http://www.runoob.com/ |   100 | 2016-05-13 |
| 菜鸟教程     | http://www.runoob.com/ |   220 | 2016-05-15 |
| 菜鸟教程     | http://www.runoob.com/ |   201 | 2016-05-17 |
+--------------+------------------------+-------+------------+
```

## 连接(JOIN)

<img src="/assets/images/01.png">

>* `JOIN` 子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段。
>* `INNER JOIN` ：如果表中有至少一个匹配，则返回行
>* `LEFT JOIN` ：即使右表中没有匹配，也从左表返回所有的行
>* `RIGHT JOIN` ：即使左表中没有匹配，也从右表返回所有的行
>* `FULL JOIN` ：只要其中一个表中存在匹配，则返回行

### INNER JOIN

> `INNER JOIN` 关键字在表中存在至少一个匹配时返回行。

```sql
SELECT column_name(s) FROM table1 INNER JOIN table2 ON table1.column_name=table2.column_name;
SELECT column_name(s) FROM table1 JOIN table2 ON table1.column_name=table2.column_name;
```

<img src="/assets/images/02.png">

```sql
mysql> SELECT Websites.name, access_log.count, access_log.date FROM Websites INNER JOIN access_log ON Websites.id=access_log.site_id ORDER BY access_log.count;
+--------------+-------+------------+
| name         | count | date       |
+--------------+-------+------------+
| 淘宝         |    10 | 2016-05-14 |
| 微博         |    13 | 2016-05-15 |
| Google       |    45 | 2016-05-10 |
| 菜鸟教程     |   100 | 2016-05-13 |
| 菜鸟教程     |   201 | 2016-05-17 |
| 菜鸟教程     |   220 | 2016-05-15 |
| Google       |   230 | 2016-05-14 |
+--------------+-------+------------+
```

### LEFT JOIN

> `LEFT JOIN` 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

```sql
SELECT column_name(s) FROM table1 LEFT JOIN table2 ON table1.column_name=table2.column_name;
-- 在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN。
SELECT column_name(s) FROM table1 LEFT OUTER JOIN table2 ON table1.column_name=table2.column_name;
```

<img src="/assets/images/03.png">

```sql
mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | CN      |
|  6 | 百度         | https://www.baidu.com/  |     4 | CN      |
+----+--------------+-------------------------+-------+---------+

mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+

mysql> SELECT Websites.name, access_log.count, access_log.date FROM Websites LEFT JOIN access_log ON Websites.id=access_log.site_id ORDER BY access_log.count DESC;
+--------------+-------+------------+
| name         | count | date       |
+--------------+-------+------------+
| Google       |   230 | 2016-05-14 |
| 菜鸟教程     |   220 | 2016-05-15 |
| 菜鸟教程     |   201 | 2016-05-17 |
| 菜鸟教程     |   100 | 2016-05-13 |
| Google       |    45 | 2016-05-10 |
| 微博         |    13 | 2016-05-15 |
| 淘宝         |    10 | 2016-05-14 |
| 百度         |  NULL | NULL       |
+--------------+-------+------------+
```

> **[warning] 在使用 LEFT JOIN 时， ON 和 WHERE 条件的区别 ？**
>
>* `ON` 条件是在生成临时表时使用的条件，它不管 on 中的条件是否为真，都会返回左边表中的记录。
>* `WHERE` 条件是在临时表生成好后，再对临时表进行过滤的条件。这时已经没有 LEFT JOIN 的含义（必须返回左边表的记录）了，条件不为真的就全部过滤掉。

### RIGHT JOIN 

> `RIGHT JOIN` 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。

```sql
SELECT column_name(s) FROM table1 RIGHT JOIN table2 ON table1.column_name=table2.column_name;
-- 在某些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN。
SELECT column_name(s) FROM table1 RIGHT OUTER JOIN table2 ON table1.column_name=table2.column_name;
```

<img src="/assets/images/04.png">

```sql
mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | CN      |
+----+--------------+-------------------------+-------+---------+

mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
|  10 |       6 |   111 | 2016-03-09 |
+-----+---------+-------+------------+

mysql> SELECT websites.name, access_log.count, access_log.date FROM websites RIGHT JOIN access_log ON access_log.site_id=websites.id ORDER BY access_log.count DESC;
-- 等价于
mysql> SELECT w.name, a.count, a.date FROM websites AS w RIGHT JOIN access_log AS a ON a.site_id=w.id ORDER BY a.count DESC;
-- 等价于
mysql> SELECT w.name, a.count, a.date FROM websites w RIGHT JOIN access_log a ON a.site_id=w.id ORDER BY a.count DESC;
+--------------+-------+------------+
| name         | count | date       |
+--------------+-------+------------+
| NULL         |   545 | 2016-05-16 |
| Google       |   230 | 2016-05-14 |
| 菜鸟教程     |   220 | 2016-05-15 |
| NULL         |   205 | 2016-05-14 |
| 菜鸟教程     |   201 | 2016-05-17 |
| NULL         |   111 | 2016-03-09 |
| 菜鸟教程     |   100 | 2016-05-13 |
| Google       |    45 | 2016-05-10 |
| 微博         |    13 | 2016-05-15 |
| 淘宝         |    10 | 2016-05-14 |
+--------------+-------+------------+
```

## UNION 操作符

> `UNION` 操作符合并两个或多个 SELECT 语句的结果。

> **[danger] UNION 使用注意**
>
> UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。

```sql
-- UNION 操作符选取不同的值。
SELECT column_name(s) FROM table1 UNION SELECT column_name(s) FROM table2;
-- UNION 操作符允许选取重复的值。
SELECT column_name(s) FROM table1 UNION ALL SELECT column_name(s) FROM table2;
```

```sql
mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | IND     |
+----+--------------+-------------------------+-------+---------+

mysql> SELECT * FROM apps;
+----+------------+-------------------------+---------+
| id | app_name   | url                     | country |
+----+------------+-------------------------+---------+
|  1 | QQ APP     | http://im.qq.com/       | CN      |
|  2 | 微博 APP   | http://weibo.com/       | CN      |
|  3 | 淘宝 APP   | https://www.taobao.com/ | CN      |
+----+------------+-------------------------+---------+

mysql> SELECT country FROM Websites UNION SELECT country FROM apps ORDER BY country;
+---------+
| country |
+---------+
| CN      |
| IND     |
| USA     |
+---------+

mysql> SELECT country FROM Websites UNION ALL SELECT country FROM apps ORDER BY country;
+---------+
| country |
+---------+
| CN      |
| CN      |
| CN      |
| CN      |
| IND     |
| USA     |
| USA     |
+---------+
```

## INSERT INTO SELECT

> `INSERT INTO SELECT` 语句从一个表复制数据，然后把数据插入到一个已存在的表中。

```sql
-- 从一个表中复制所有的列插入到另一个已存在的表中
INSERT INTO table2 SELECT * FROM table1;
-- 从一个表中复制希望的列插入到另一个已存在的表中
INSERT INTO table2 (column_name(s)) SELECT column_name(s) FROM table1;
```

```sql
mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | IND     |
+----+--------------+-------------------------+-------+---------+

mysql> SELECT * FROM apps;
+----+------------+-------------------------+---------+
| id | app_name   | url                     | country |
+----+------------+-------------------------+---------+
|  1 | QQ APP     | http://im.qq.com/       | CN      |
|  2 | 微博 APP   | http://weibo.com/       | CN      |
|  3 | 淘宝 APP   | https://www.taobao.com/ | CN      |
+----+------------+-------------------------+---------+

mysql> INSERT INTO Websites (name, country) SELECT app_name, country FROM apps;
Query OK, 3 rows affected (0.15 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | IND     |
|  7 | QQ APP       |                         |     0 | CN      |
|  8 | 微博 APP     |                         |     0 | CN      |
|  9 | 淘宝 APP     |                         |     0 | CN      |
+----+--------------+-------------------------+-------+---------+

mysql> INSERT INTO Websites (name, country) SELECT app_name, country FROM apps WHERE id=1;
Query OK, 1 row affected (0.00 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | IND     |
| 10 | QQ APP       |                         |     0 | CN      |
+----+--------------+-------------------------+-------+---------+
```

## NULL

### NULL 值

> `NULL` 值代表遗漏的未知数据。

```sql
-- 选取在 "Address" 列中带有 NULL 值的记录
SELECT LastName,FirstName,Address FROM Persons WHERE Address IS NULL
-- 选取在 "Address" 列中不带有 NULL 值的记录
SELECT LastName,FirstName,Address FROM Persons WHERE Address IS NOT NULL
```

# 函数

## Date 函数

| 函数 | 描述 | 
| --- | --- |
| `NOW()` |	返回当前的日期和时间 |
| `CURDATE()` |	返回当前的日期 |
| `CURTIME()` |	返回当前的时间 |
| `DATE()` |	提取日期或日期/时间表达式的日期部分 |
| `EXTRACT()` |	返回日期/时间的单独部分，比如年、月、日、小时、分钟等等。 | 
| `DATE_ADD()` |	向日期添加指定的时间间隔 | 
| `DATE_SUB()` |	从日期减去指定的时间间隔 |
| `DATEDIFF()` |	返回两个日期之间的天数 |
| `DATE_FORMAT()` |	用不同的格式显示日期/时间 |

MySQL 使用下列数据类型在数据库中存储日期或日期/时间值：

* DATE - 格式：`YYYY-MM-DD`
* DATETIME - 格式：`YYYY-MM-DD HH:MM:SS`
* TIMESTAMP - 格式：`YYYY-MM-DD HH:MM:SS`
* YEAR - 格式：`YYYY` 或 `YY`

### NOW()、CURDATE()、CURTIME()

```sql
mysql> SELECT NOW(),CURDATE(),CURTIME();
+---------------------+------------+-----------+
| NOW()               | CURDATE()  | CURTIME() |
+---------------------+------------+-----------+
| 2020-11-10 13:36:24 | 2020-11-10 | 13:36:24  |
+---------------------+------------+-----------+
```

### DATE()

```sql
CREATE TABLE Orders(
`OrderId` INT(11) NOT NULL AUTO_INCREMENT,
`ProductName` VARCHAR(255),
`OrderDate` DATE,
PRIMARY KEY(`OrderId`)
);
mysql> INSERT INTO Orders(ProductName,OrderDate) VALUES ('Jarlsberg Cheese', NOW());
mysql> SELECT ProductName, DATE(OrderDate) AS OrderDate FROM Orders;
+------------------+------------+
| ProductName      | OrderDate  |
+------------------+------------+
| Jarlsberg Cheese | 2020-11-10 |
+------------------+------------+
```

### EXTRACT()

> 返回日期/时间的单独部分，比如年、月、日、小时、分钟等等。

```sql
EXTRACT(unit FROM date)

-- MICROSECOND
-- SECOND
-- MINUTE
-- HOUR
-- DAY
-- WEEK
-- MONTH
-- QUARTER
-- YEAR
-- SECOND_MICROSECOND
-- MINUTE_MICROSECOND
-- MINUTE_SECOND
-- HOUR_MICROSECOND
-- HOUR_SECOND
-- HOUR_MINUTE
-- DAY_MICROSECOND
-- DAY_SECOND
-- DAY_MINUTE
-- DAY_HOUR
-- YEAR_MONTH
```

```sql
mysql> SELECT * FROM Orders;
+---------+------------------+------------+
| OrderId | ProductName      | OrderDate  |
+---------+------------------+------------+
|       1 | Jarlsberg Cheese | 2020-11-10 |
+---------+------------------+------------+

mysql> SELECT EXTRACT(YEAR FROM OrderDate) AS OrderYear, EXTRACT(MONTH FROM OrderDate) AS OrderMonth, EXTRACT(DAY FROM OrderDate) AS OrderDay  FROM Orders;
+-----------+------------+----------+
| OrderYear | OrderMonth | OrderDay |
+-----------+------------+----------+
|      2020 |         11 |       10 |
+-----------+------------+----------+
```

### DATE_ADD()、DATE_SUB()

>* `DATE_ADD()` 向日期添加指定的时间间隔。
>* `DATE_SUB()` 向日期减去指定的时间间隔。

```sql
DATE_SUB(date,INTERVAL expr type)
DATE_ADD(date,INTERVAL expr type)
-- date 参数是合法的日期表达式。
-- expr 参数是您希望添加的时间间隔。
-- type 参数可以是下列值：
-- MICROSECOND
-- SECOND
-- MINUTE
-- HOUR
-- DAY
-- WEEK
-- MONTH
-- QUARTER
-- YEAR
-- SECOND_MICROSECOND
-- MINUTE_MICROSECOND
-- MINUTE_SECOND
-- HOUR_MICROSECOND
-- HOUR_SECOND
-- HOUR_MINUTE
-- DAY_MICROSECOND
-- DAY_SECOND
-- DAY_MINUTE
-- DAY_HOUR
-- YEAR_MONTH
```

```sql
mysql> SELECT * FROM Orders;
+---------+------------------+------------+
| OrderId | ProductName      | OrderDate  |
+---------+------------------+------------+
|       1 | Jarlsberg Cheese | 2020-11-10 |
+---------+------------------+------------+

mysql> SELECT OrderId,DATE_ADD(OrderDate,INTERVAL 45 DAY) AS OrderPayDate FROM Orders WHERE OrderId=1;
+---------+--------------+
| OrderId | OrderPayDate |
+---------+--------------+
|       1 | 2020-12-25   |
+---------+--------------+

mysql> SELECT * FROM Orders;
+---------+------------------+------------+
| OrderId | ProductName      | OrderDate  |
+---------+------------------+------------+
|       1 | Jarlsberg Cheese | 2020-11-10 |
+---------+------------------+------------+
```

### DATEDIFF()

> 返回两个日期之间的天数。

```sql
DATEDIFF(date1,date2)
```

```sql
mysql> SELECT DATEDIFF('2008-11-30','2008-11-29') AS DiffDate;
+----------+
| DiffDate |
+----------+
|        1 |
+----------+
```

### DATE_FORMAT()

> 以不同的格式显示日期/时间数据

```sql
DATE_FORMAT(date,format)
```

| 格式 | 描述 |
| --- | --- |
| `%a` | 缩写星期名 |
| `%b` | 缩写月名 |
| `%c` | 月，数值 |
| `%D` | 带有英文前缀的月中的天 |
| `%d` | 月的天，数值（00-31） |
| `%e` | 月的天，数值（0-31） |
| `%f` | 微秒 |
| `%H` | 小时（00-23） |
| `%h` | 小时（01-12） |
| `%I` | 小时（01-12） |
| `%i` | 分钟，数值（00-59） |
| `%j` | 年的天（001-366） |
| `%k` | 小时（0-23） |
| `%l` | 小时（1-12） |
| `%M` | 月名 |
| `%m` | 月，数值（00-12） |
| `%p` | AM 或 PM |
| `%r` | 时间，12-小时（hh:mm:ss AM 或 PM） |
| `%S` | 秒（00-59） |
| `%s` | 秒（00-59） |
| `%T` | 时间, 24-小时（hh:mm:ss） |
| `%U` | 周（00-53）星期日是一周的第一天 |
| `%u` | 周（00-53）星期一是一周的第一天 |
| `%V` | 周（01-53）星期日是一周的第一天，与 %X 使用 |
| `%v` | 周（01-53）星期一是一周的第一天，与 %x 使用 |
| `%W` | 星期名 |
| `%w` | 周的天（0=星期日, 6=星期六） |
| `%X` | 年，其中的星期日是周的第一天，4 位，与 %V 使用 |
| `%x` | 年，其中的星期一是周的第一天，4 位，与 %v 使用 |
| `%Y` | 年，4 位 |
| `%y` | 年，2 位 |

```sql
mysql> SELECT DATE_FORMAT(NOW(),'%b %d %Y %h:%i %p');
+----------------------------------------+
| DATE_FORMAT(NOW(),'%b %d %Y %h:%i %p') |
+----------------------------------------+
| Nov 10 2020 02:04 PM                   |
+----------------------------------------+

mysql> SELECT DATE_FORMAT(NOW(),'%m-%d-%Y');
+-------------------------------+
| DATE_FORMAT(NOW(),'%m-%d-%Y') |
+-------------------------------+
| 11-10-2020                    |
+-------------------------------+

mysql> SELECT DATE_FORMAT(NOW(),'%d %b %y');
+-------------------------------+
| DATE_FORMAT(NOW(),'%d %b %y') |
+-------------------------------+
| 10 Nov 20                     |
+-------------------------------+

mysql> SELECT DATE_FORMAT(NOW(),'%d %b %Y %T:%f');
+-------------------------------------+
| DATE_FORMAT(NOW(),'%d %b %Y %T:%f') |
+-------------------------------------+
| 10 Nov 2020 14:04:56:000000         |
+-------------------------------------+
```

## AVG() 

> 返回数值列的平均值。	

```sql
SELECT AVG(column_name) FROM table_name
```

```sql
mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
|  10 |       6 |   111 | 2016-03-09 |
+-----+---------+-------+------------+

mysql> SELECT AVG(count) AS CountAverage FROM access_log;
+--------------+
| CountAverage |
+--------------+
|     168.0000 |
+--------------+

mysql> SELECT site_id, count FROM access_log WHERE count > (SELECT AVG(count) FROM access_log);
+---------+-------+
| site_id | count |
+---------+-------+
|       1 |   230 |
|       5 |   205 |
|       3 |   220 |
|       5 |   545 |
|       3 |   201 |
+---------+-------+
```

## COUNT()

> 返回匹配指定条件的行数

```sql
-- 返回指定列的值的数目（NULL 不计入）
SELECT COUNT(column_name) FROM table_name;
-- 返回表中的记录数
SELECT COUNT(*) FROM table_name;
-- 返回指定列的不同值的数目
SELECT COUNT(DISTINCT column_name) FROM table_name;
```

```sql
SELECT COUNT(DISTINCT count) FROM access_log;
```

## MIN()


> 返回指定列的最小值。

```sql
SELECT MIN(column_name) FROM table_name;
```

```sql
mysql> SELECT * FROM Websites;
+----+--------------+-------------------------+-------+---------+
| id | name         | url                     | alexa | country |
+----+--------------+-------------------------+-------+---------+
|  1 | Google       | https://www.google.cm/  |     1 | USA     |
|  2 | 淘宝         | https://www.taobao.com/ |    13 | CN      |
|  3 | 菜鸟教程     | http://www.runoob.com/  |  5000 | USA     |
|  4 | 微博         | http://weibo.com/       |    20 | IND     |
| 10 | QQ APP       |                         |     0 | CN      |
+----+--------------+-------------------------+-------+---------+

mysql> SELECT MIN(alexa) AS min_alexa FROM Websites;
+-----------+
| min_alexa |
+-----------+
|         0 |
+-----------+
```

## GROUP BY

> `GROUP BY` 语句可结合一些聚合函数来使用，根据一个或多个列对结果集进行分组。

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```































































