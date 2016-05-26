##  CREATE 创建
### CREATE DATABASE my_db 创建数据库
> CREATE DATABASE database_name

### CREATE TABLE 语句
> CREATE TABLE 表名称
  (
  列名称1 数据类型,
  列名称2 数据类型,
  列名称3 数据类型,
  ....
  )

  数据类型  |  描述
  --------- | -------------
  integer(size) int(size) smallint(size) tinyint(size)| 仅容纳整数。在括号内规定数字的最大位数。
  decimal(size,d) numeric(size,d) | 容纳带有小数的数字。 "size" 规定数字的最大位数。"d" 规定小数点右侧的最大位数。
  char(size)|容纳固定长度的字符串（可容纳字母、数字以及特殊字符）。在括号中规定字符串的长度。
   varchar(size)| 容纳可变长度的字符串（可容纳字母、数字以及特殊的字符）。在括号中规定字符串的最大长度。
  date(yyyymmdd) | 容纳日期

### 约束
- NOT NULL 约束强制列不接受 NULL 值。NOT NULL 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。
- PRIMARY KEY 约束唯一标识数据库表中的每条记录。主键必须包含唯一的值。主键列不能包含 NULL 值。每个表都应该有一个主键，并且每个表只能有一个主键。
- FOREIGN KEY
- DEFAULT 用于向列中插入默认值。如果没有规定其他的值，那么会将默认值添加到所有的新记录。

## INSERT INTO 增
> INSERT INTO 表名称 VALUES (值1, 值2,....)
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....) 指定所要插入数据的列
```
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
```

## DELETE 删

> DELETE FROM 表名称 WHERE 列名称 = 值
可以在不删除表的情况下删除所有的行。这意味着表的结构、属性和索引都是完整的：
DELETE FROM table_name 或 DELETE * FROM table_name

## Update 改

> UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```
UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing' WHERE LastName = 'Wilson'
```

## ALTER TABLE
> ALTER TABLE 语句用于在已有的表中添加、修改或删除列。
- 添加列:              ALTER TABLE table_name ADD column_name datatype
- 删除表中的列：        ALTER TABLE table_name DROP COLUMN column_name。注释：某些数据库系统不允许这种在数据库表中删除列的方式 (DROP COLUMN column_name)。
- 改变表中列的数据类型：ALTER TABLE table_name ALTER COLUMN column_name datatype


## 查询

### select
```
select 列名称(*) from 表名称
```
星号（*）是选取所有列的快捷方式。

### SELECT DISTINCT 语句
关键词 DISTINCT 用于返回唯一不同的值。
```
SELECT DISTINCT 列名称 FROM 表名称
```
查询列中所有不同值（排除相同值）

### where 子句
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值

操作符 | 描述
-------|-------
=|等于
<>或!=|不等于
>|大于
<|小于
>=|大于等于
<=|小于等于
between|在某个范围内
like | 搜索某种范围
> 引号的使用
SQL 使用单引号来环绕文本值（大部分数据库系统也接受双引号）。如果是数值，请不要使用引号。

### and & or 运算符
> AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来。

### order by 用于对结果集进行排序。
> ORDER BY 语句用于根据指定的列对结果集进行排序。
ORDER BY 语句默认按照升序对记录进行排序。
如果您希望按照降序对记录进行排序，可以使用 DESC 关键字。
ASC 升序
DESC 降序

#### 左连接 LEFT JOIN
```
select CustArchiveValueOld.id,CustArchiveValueOld.value from CustArchiveValueOld  LEFT JOIN ArchiveItem ON CustArchiveValueOld.archiveItemId=ArchiveItem.id
where CustArchiveValueOld.custArchiveLocalId in (18,19,20,21,22) and CustArchiveValueOld.measureDate >= '2015-12-07 15:56:35.028' and CustArchiveValueOld.measureDate <= '2016-12-07 15:56:35.028'
and ArchiveItem.code IN('AI-00000079','AI-00000080','AI-00000081','AI-00000082')
```
> 从CustArchiveValueOld表（左连接ArchiveItem表）中查询id 和 value 满足条件

#### COUNT() 函数返回匹配指定条件的行数。
- SQL COUNT(column_name)
语法： COUNT(column_name) 函数返回指定列的值的数目（NULL 不计入）：
- SQL COUNT(*)
语法： COUNT(*) 函数返回表中的记录数：
- SQL COUNT(DISTINCT column_name)
语法： SQL COUNT(DISTINCT column_name) 语法

## 操作符

#### Like
> LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。
% 定义通配符
- 以N开头 列 LIKE 'N%'
- 以N结尾 列 LIKE '%N'
- 包含NN 列 LIKE '%NN%'
- 不包含NN 列 NOT LIKE '%NN%'

#### 通配符
在搜索数据库中的数据时，SQL 通配符可以替代一个或多个字符。
SQL 通配符必须与 LIKE 运算符一起使用。

通配符 | 描述
-------| ------
% | 替代一个或多个字符
_ | 仅替代一个字符
[charlist] | 字符列中的任何单一字符
[^charlist] 或 [!charlist] | 不在字符列中的任何单一字符

#### IN
> IN 操作符允许我们在 WHERE 子句中规定多个值。

#### BETWEEN
> 操作符 BETWEEN ... AND 会选取介于两个值之间的数据范围。这些值可以是数值、文本或者日期。

## 函数
### date 函数
MySQL 中最重要的内建日期函数：

函数 | 描述
---- |------
NOW()|返回当前的日期和时间
CURDATE()|返回当前的日期
CURTIME()|返回当前的时间
DATE()|提取日期或日期/时间表达式的日期部分
EXTRACT()|返回日期/时间按的单独部分
DATE_ADD()|给日期添加指定的时间间隔
DATE_SUB()|从日期减去指定的时间间隔
DATEDIFF()|返回两个日期之间的天数
DATE_FORMAT()|用不同的格式显示日期/时间