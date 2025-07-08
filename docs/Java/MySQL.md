---
title: MySQL
createTime: 2025/07/08 17:03:15
permalink: /article/3qq8ixld/
---


# MySQL基础

## 前置操作

**下载MySQL**

。。。

**启动数据库**

```cmd
net start mysql80
net stop mysql80
```

**cmd连接数据库**

```cmd
mysql [-h 127.0.0.1] [-p 3306] -u root -p
```

**VSCode连接数据库**

1. 下载SQL Tools插件
2. 下载SQL驱动
3. 填写数据库信息

## 通用语法及分类

### DDL

> 数据定义语言，定义数据库对象（数据库，表，字段）

#### 数据库操作

**查询**

查询所有的数据库

```sql
SHOW DATABASES;
```

查询当前的数据库

```sql
SELECT DATABASE();
```

**创建**

```sql
CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集(utf8mb4)] [COLLATE 排序规则];
```

**删除**

```sql
DROP DATABASE [IF EXISTS] 数据库名;
```

**使用**

切换数据库

```sql
USE 数据库名;
```

#### 表操作

**查询**

查询当前数据库所有的表

```sql
SHOW TABLES;
```

查询表结构

```sql
DESC 表名;
```

查询指定表的建表语句

```sql
SHOW CREATE TABLE 表名;
```

**创建**

```sql
CREATE TABLE 表名(
    字段1 字段1类型 [COMMENT 字段1注释],
    字段2 字段2类型 [COMMENT 字段2注释],
    ...
    字段n 字段n类型 [COMMENT 字段n注释]
) [COMMENT 表注释];
```

**修改**

添加字段
```sql
ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];
```

修改数据类型

```sql
ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
```

修改字段名和字段类型

```sql
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];
```

删除字段

```sql
ALTER TABLE 表名 DROP 字段名;
```

修改表名

```sql
ALTER TABLE 表名 RENAME TO 新表名;
```

**删除**

删除表

```sql
DROP TABLE [IF EXISTS] 表名;
```

删除表并重新创建

```sql
TRUNCATE TABLE 表名;
```



#### 数据类型

**数值类型**

| 类型         | 大小    | 有符号(SIGNED)范围                                           | 无符号(UNSIGNED)范围                                    | 描述              |
| ------------ | ------- | ------------------------------------------------------------ | ------------------------------------------------------- | ----------------- |
| TINYINT      | 1 byte  | (-128,127)                                                   | (0，255)                                                | 小整数值          |
| SMALLINT     | 2 bytes | (-32768, 32767)                                              | (0，65535)                                              | 大整数值          |
| MEDIUMINT    | 3 bytes | (-8388608, 8388607)                                          | (0，16777215)                                           | 大整数值          |
| INT或INTEGER | 4 bytes | (-2147483648, 2147483647)                                    | (0，4294967295)                                         | 大整数值          |
| BIGINT       | 8 bytes | (-2~63, 2^63-1)                                              | (0，2^64-1)                                             | 极大整数值        |
| FLOAT        | 4 bytes | (-3.402823466 E+38， 3.402823466351 E+38)                    | 0和(1.175494351 E-38，3.402823466 E+38)                 | 单精度浮点数值    |
| DOUBLE       | 8 bytes | (-1.7976931348623157 E+308, 1.7976931348623157 E+308)        | 0和(2.2250738585072014 E-308，1.7976931348623157 E+308) | 双精度浮点数值    |
| DECIMAL      |         | 依赖于M(精度)和D(标度)的值<br />精度：整个数的长度<br />标度：小数位数 | 依赖于M(精度)和D(标度)的值                              | 小数值(精确定点数 |

**字符串类型**

| 类型       | 大小                  | 描述                         |
| ---------- | --------------------- | ---------------------------- |
| CHAR       | 0-255 bytes           | 定长字符串                   |
| VARCHAR    | 0-65535 bytes         | 变长字符串                   |
| TINYBLOB   | 0-255 bytes           | 不超过255个字符的二进制数据  |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                 |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据       |
| TEXT       | 0-65 535bytes         | 长文本数据                   |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据 |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据             |
| LONGBLOB   | 0-4294 967 295 bytes  | 二进制形式的极大文本数据     |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                 |

**日期类型**

| 类型      | 大小 | 范围                                     | 格式                | 描述                     |
| --------- | ---- | ---------------------------------------- | ------------------- | ------------------------ |
| DATE      | 3    | 1000-01-01 至 9999-12-31                 | YYYY-MM-DD          | 日期值                   |
| TIME      | 3    | -838:59:59 至 838:59:59                  | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1    | 1901 至 2155                             | YYYY                | 年份值                   |
| DATETIME  | 8    | 1000-01-0100:00:00 至 9999-12-3123:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4    | 1970-01-01 00:00:01 至2038-01-1903:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |



### DML

> 数据操作语言，对数据库表中的数据进行增删改

**插入**

给指定字段增加数据

```sql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1, 值2,..);
```

给全部字段添加数据

```sql
INSERT INTO 表名 VALUES (值1, 值2, ...);
```

批量添加数据

```sql
INSERT INTO 表名 (字段名1,字段名2,...) VALUES(值1,值2,...),(值1,值2,...),(值1,值2,.);
INSERT INTO 表名 VALUES(值1, 值2,..),(值1, 值2,...),(值1, 值2, ..);
```

**修改**

```sql
UPDATE 表名 SET 字段1 = 值1, 字段2 = 值2, ... [WHERE 条件];
```

**删除**

```sql
DELETE FROM 表名 [WHERE 条件];
```



### DQL

> 数据查询语言，查询数据库中表的记录

**编写顺序**

```sql
SELECT   字段列表
FROM     表名列表
WHERE    条件列表
GROUP BY 分组字段列表
HAVING   分组后条件列表
ORDER BY 排序字段列表
LIMIT    分页参数
```

**执行顺序**

412356

#### 基本查询

查询多个字段

```sql
SELECT 字段1, 字段2, ... FROM 表名：
SELECT * FROM 表名;
```

设置别名

```sql
SELECT 字段1 [AS 别名1], 字段2 [AS 别名2] ... FROM 表名;
```

去除重复记录

```sql
SELECT DISTINCT 字段列表 FORM 表名;
```

#### 条件查询

```sql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

**条件**

| 比较运算符                | 功能                                     |
| ------------------------- | ---------------------------------------- |
| >, >=, <, <=, =, <> 或 != |                                          |
| BETWEEN ... AND..         | 在某个范围之内(含最小、最大值)           |
| IN(..)                    | 在in之后的列表中的值，多选一             |
| LIKE 占位符               | 模糊匹配(_匹配单个字符，%匹配任意个字符) |
| IS NULL                   | 是NULL                                   |

| 逻辑运算符 | 功能                        |
| ---------- | --------------------------- |
| AND 或 &&  | 并且 (多个条件同时成立)     |
| OR 或 II   | 或者 (多个条件任意一个成立) |
| NOT 或 !   | 非，不是                    |

#### 聚合函数

```sql
SELECT 聚合函数(字段列表) FROM 表名
```

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |

#### 分组查询

```sql
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件];
```

**WHERE 与 HAVING 区别**
执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤。
判断条件不同：where不能对聚合函数进行判断，而having可以。

**注意**
执行顺序:where > 聚合函数 > having。
分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义。

#### 排序查询

```sql
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1, 字段2 排序方式2;
```

**排序方式**
ASC：升序（默认）
DESC：降序

**如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序。**

#### 分页查询

```sql
SELECT 字段列表 FROM 表名 LIMIT 起始索引 查询记录数;
```

**注意**
起始索引从0开始，起始索引=（查询页码-1）* 每页显示记录数。
分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT。
如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10。

### DCL

> 数据控制语言，创建数据库用户，控制数据库的访问权限

#### 管理用户

**查询用户**

```sql
USE mysql;
SELECT * FROM user;
```

**创建用户**

```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```

**修改用户密码**

```SQL
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```

**删除用户**

```sql
DROP USER '用户名'@'主机名';
```

**注意**
主机名可以使用%通配。

#### 权限控制

| 权限                | 说明               |
| ------------------- | ------------------ |
| ALL, ALL PRIVILEGES | 所有权限           |
| SELECT              | 查询数据           |
| INSERT              | 插入数据           |
| UPDATE              | 修改数据           |
| DELETE              | 删除数据           |
| ALTER               | 修改表             |
| DROP                | 删除数据库/表/视图 |
| CREATE              | 创建数据库/表      |

**查询权限**

```sql
SHOW GRANTS FOR '用户名'@'主机名';
```

**授予权限**

```sql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

**撤销权限**

```SQL
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```

**注意**
多个权限之间，使用逗号分隔
授权时，数据库名和表名可以使用 * 进行通配，代表所有。

## 函数

### 字符串函数

| 函数                     | 功能                                                      |
| ------------------------ | --------------------------------------------------------- |
| CONCAT(S1,S2,..Sn)       | 字符串拼接，将S1，S2，..Sn拼接成一个字符串                |
| LOWER(str)               | 将字符串str全部转为小写                                   |
| UPPER(str)               | 将字符串str全部转为大写                                   |
| LPAD(str,n,pad)          | 左填充，用字符串pad对str的左边进行填充，达到n个字符串长度 |
| RPAD(str,n,pad)          | 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度 |
| TRIM(str)                | 去掉字符串头部和尾部的空格                                |
| SUBSTRING(str,Start,len) | 返回从字符串str从start位置起的len个长度的字符串           |

### 数值函数

| 函数       | 功能                               |
| ---------- | ---------------------------------- |
| CEIL(x)    | 向上取整                           |
| FLOOR(x)   | 向下取整                           |
| MOD(x,y)   | 返回x/y的模                        |
| RAND()     | 返回0~1内的随机数                  |
| ROUND(x,y) | 求参数x的四舍五入的值，保留y位小数 |

### 日期函数

| 函数                                                         | 功能                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| CURDATE()                                                    | 返回当前日期                                      |
| CURTIME()                                                    | 返回当前时间                                      |
| NOW()                                                        | 返回当前日期和时间                                |
| YEAR(date)                                                   | 获取指定date的年份                                |
| MONTH(date)                                                  | 获取指定date的月份                                |
| DAY(date)                                                    | 获取指定date的日期                                |
| DATE_ADD(date, INTERVAL expr type)<br />DATE_ADD(NOW(), INTERVAL 70 YEAR) | 返回一个日期/时间值加上一个时间间隔expr后的时间值 |
| DATEDIFF(date1,date2)                                        | 返回起始时间date1和 结束时间date2之间的天数       |

### 流程函数

| 函数                                                       | 功能                                                     |
| ---------------------------------------------------------- | -------------------------------------------------------- |
| IF(value ,t, f)                                            | 如果value为true，则返回t，否则返回f                      |
| IFNULL(value1 , value2)                                    | 如果value1不为空，返回value1，否则返回value2             |
| CASE WHEN [val1] THEN [res1] ... ELSE [default] END        | 如果val1为true，返回res1，...否则返回default默认值       |
| CASE [expr] WHEN [val1] THEN [res1] ... ELSE [default] END | 如果expr的值等于val1，返回res1，...否则返回default默认值 |

## 约束

| 约束             | 关键字      |
| ---------------- | ----------- |
| 非空约束         | NOT NULL    |
| 唯一约束         | UNIQUE      |
| 主键约束         | PRIMARY KEY |
| 默认约束         | DEFAULT     |
| 检查约束(8.0.16) | CHECK       |
| 外键约束         | FOREIGN KEY |

### 外键约束

**添加**

```sql
-- 创建表时添加外键约束
CREATE TABLE 表名（
    列名 数据类型,
    [CONSTRAINT] [外键名称] FOREIGN KEY (外键列名) REFERENCES 主表(主表列名)
);
-- 建完表后添加外键约束
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名称) REFERENCES 主表名称(主表列名称);
```

**删除**

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

## 数据库设计

> 

## 多表查询

### 连接查询

- 内连接

  > 查询 A B 交集数据

  ```sql
  -- 隐式内连接
  SELECT 字段列表 FROM 表1, 表2... WHERE 条件;
  -- 显示内连接
  SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 条件;
  ```

- 外连接

  > 左外连接：查询A和交集部分的数据
  >
  > 右外连接：查询B和交集部分的数据

  ```sql
  -- 左外连接
  SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件;
  -- 右外连接
  SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件;
  ```

### 子查询

> 嵌套查询

**单行单列：**作为条件值，使用 = != > < 等进行条件判断

```sql
SELECT 字段列表 FROM 表 WHERE 字段名 = (子查询)
```

**多行单列：**作为条件值，使用in等关键字进行条件判断

```sql
SELECT 字段列表 FROM 表 WHERE 字段名 in (查询);
```

**多行多列：**作为虚拟表

```sql
SELECT 字段列表 FROM (子查询) WHERE 条件;
```

## 事务

**四大特征**

- 原子性（Atomicity）：事务是不可分割的最小操作单位，要么同时成功，要么同时失败
- 一致性（Consistency）:事务完成时，必须使所有的数据都保持一致状态
- 隔离性（lsolation）:多个事务之间，操作的可见性
- 持久性（Durability）:事务一旦提交或回滚，它对数据库中的数据的改变就是永久的

```sql
-- 开启事务
BEGIN;
-- 执行

-- 提交事务
commit;
-- 回滚事务
ROLLBACK;
```

**MySQL事务默认自动提交**

```sql
-- 查看事务的默认自动提交方式
SELECT @@autocommit;
-- 1 自动提交 0 手动提交
-- 修改事务提交方式
set @@autocommit = 0;
```

