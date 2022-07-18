---
title: mysql
date: 2021-04-14 17:09:36
tags: mysql
---

#### #安装 MySQL 服务端、核心程序

```bash
 sudo apt-get install mysql-server
```

#### #安装 MySQL 客户端

```bash
 sudo apt-get install mysql-client
```

#### 安装结束后，用命令验证是否安装并启动成功：

```bash
sudo netstat -tap | grep mysql
```

#### \# 启动 MySQL 服务

```bash 
sudo service mysql start
```

#### 使用 root 用户登录，实验楼环境的密码为空，直接回车就可以登录 

```mysql
mysql -u root
```

#### 查看数据库

```mysql
show databases;
```

#### 连接数据库

选择连接其中一个数据库，语句格式为 `use <数据库名>`，这里可以不用加分号，这里我们选择 `information_schema` 数据库：

```mysql
use information_schema
```

#### 查看表

使用命令 `show tables;` 查看数据库中有哪些表

#### 退出

```mysql
quit
```

首先，我们创建一个数据库，给它一个名字，比如 `mysql_shiyan`，以后的几次实验也是对 `mysql_shiyan` 这个数据库进行操作。 语句格式为 `CREATE DATABASE <数据库名字>;`，（注意不要漏掉分号 `;`），前面的 CREATE DATABASE 也可以使用小写，具体命令为：

```sql
CREATE DATABASE mysql_shiyan;
```

#### 数据表

![table](G:\Blog_Djk\Hexo\source\_posts\mysql\table.png)

在数据库中新建一张表的语句格式为：

```sql
CREATE TABLE 表的名字
(
列名a 数据类型(数据长度),
列名b 数据类型(数据长度)，
列名c 数据类型(数据长度)
);
```

我们尝试在 `mysql_shiyan` 中新建一张表 `employee`，包含姓名，ID 和电话信息，所以语句为：

```sql
CREATE TABLE employee (id int(10),name char(20),phone int(12));
```

![image-20210415001650791](G:\Blog_Djk\Hexo\source\_posts\mysql\image-20210415001650791.png)

刚才我们新建了两张表，使用语句 `SELECT * FROM employee;` 查看表中的内容，可以看到 employee 表中现在还是空的：

![06](G:\Blog_Djk\Hexo\source\_posts\mysql\sql-02-06.png)

我们通过 INSERT 语句向表中插入数据，语句格式为：

```sql
INSERT INTO 表的名字(列名a,列名b,列名c) VALUES(值1,值2,值3);
```

#### 约束

![image-20210415003404290](G:\Blog_Djk\Hexo\source\_posts\mysql\image-20210415003404290.png)

如果你是接着上一个实验开始操作的话，记得先使用如下命令删掉 mysql_shiyan 数据库：

```sql
drop database mysql_shiyan;
```

#### 主键

![image-20210415004644305](G:\Blog_Djk\Hexo\source\_posts\mysql\image-20210415004644305.png)

在 `MySQL-03-01.sql` 中，这里有主键：

![07](G:\Blog_Djk\Hexo\source\_posts\mysql\sql-03-07.png)

也可以这样定义主键：

![08-](G:\Blog_Djk\Hexo\source\_posts\mysql\1sql-03-08-.png)

#### 默认值约束

在 `MySQL-03-01.sql` 中，这段代码包含了 DEFAULT 约束：

```sql
people_num INT(10) DEFAULT 10,
```

#### 唯一约束

唯一约束 (UNIQUE) 比较简单，它规定一张表中指定的一列的值必须不能有重复值，即这一列每个值都是唯一的。

在 `MySQL-03-01.sql` 中，也有 UNIQUE 约束：

![11](G:\Blog_Djk\Hexo\source\_posts\mysql\sql-03-11.png)

#### 外键约束

一个表可以有多个外键，每个外键必须 REFERENCES (参考) 另一个表的主键，被外键约束的列，取值必须在它参考的列中有对应值。

![12-](G:\Blog_Djk\Hexo\source\_posts\mysql\1sql-03-12-.png)

在 INSERT 时，如果被外键约束的值没有在参考列中有对应，比如以下命令，参考列 (department 表的 dpt_name) 中没有 dpt3，则 INSERT 失败：

```sql
INSERT INTO employee VALUES(02,'Jack',30,3500,114114,'dpt3');
```

#### 实验楼mysql

```sql
REATE DATABASE mysql_shiyan;

use mysql_shiyan;

CREATE TABLE department
(
  dpt_name   CHAR(20) NOT NULL,
  people_num INT(10) DEFAULT '10',
  CONSTRAINT dpt_pk PRIMARY KEY (dpt_name)
 );

CREATE TABLE employee
(
  id      INT(10) PRIMARY KEY,
  name    CHAR(20),
  age     INT(10),
  salary  INT(10) NOT NULL,
  phone   INT(12) NOT NULL,
  in_dpt  CHAR(20) NOT NULL,
  UNIQUE  (phone),
  CONSTRAINT emp_fk FOREIGN KEY (in_dpt) REFERENCES department(dpt_name)
 );
 
CREATE TABLE project
(
  proj_num   INT(10) NOT NULL,
  proj_name  CHAR(20) NOT NULL,
  start_date DATE NOT NULL,
  end_date   DATE DEFAULT '2015-04-01',
  of_dpt     CHAR(20) REFERENCES department(dpt_name),
  CONSTRAINT proj_pk PRIMARY KEY (proj_num,proj_name)
 );
```

> To do:
>
> 1. 约束的继续理解
>
>     

### MySQL-约束（constraint）详解

##### 一、什么是约束

> 约束英文： constraint
> 约束实际上就是表中数据的限制条件

#### 二、约束作用

> 表在设计的时候加入约束的目的就是为了保证表中的记录完整和有效

-  比如name 字段中要让其用户名不重复，这就需要添加约束。或者注册的时候添加邮箱。

#### 三、约束种类

- 非空约束(not null)
- 唯一性约束(unique)
- 主键约束(Primary Key) PK
- 外键约束(Foreign Key)FK
- 检查约束(目前MYSQL不支持、Oracle支持)

> 下面将逐一介绍以上约束

#### 四、非空约束

> 用 not null 约束的字段不能为 null值，必须给具体的数据

**创建表，给字段添加非空约束（创建用户表，用户名不能为空）**

```sql
	mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null
    -> );
Query OK, 0 rows affected (0.08 sec)

```

**如果没有插入name字段数据，则会报错**

```sql
mysql> insert into t_user (id) values(1);
ERROR 1364 (HY000): Field 'name' doesn't have a default value
```

#### 五、唯一性约束

> unique 约束的字段，具有唯一性，不可重复，但可以为null

**创建表，保证邮箱地址唯一(列级约束)**

```sql
mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null,
    -> email varchar(128) unique
    -> );
Query OK, 0 rows affected (0.03 sec)

```

**表级约束**

```sql
mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null,
    -> email varchar(128），
	-> unique(email)
    -> );

```

**表级约束可以给约束起名字(方便以后通过这个名字来删除这个约束)**

```sql
mysql> create table t_user(
    -> id int(10),
    -> name varchar(32) not null,
    -> email varchar(128),
    -> constraint t_user_email_unique unique(email)
    -> );
Query OK, 0 rows affected (0.06 sec)

```

> Todo:
>
> https://blog.csdn.net/w_linux/article/details/79655073

### 查询数据

#### 基本查询

```sql
SELECT * FROM <表名>
```

#### 条件查询

> SELECT语句可以通过`WHERE`条件来设定查询条件，查询结果是满足查询条件的记录。例如，要指定条件“分数在80分或以上的学生”，写成`WHERE`条件就是`SELECT * FROM students WHERE score >= 80`。

**条件表达式可以用**`<条件1> AND <条件2>`**表达满足条件1并且满足条件2**。

**第二种条件是**`<条件1> OR <条件2>`，**表示满足条件**1或者满足条件2。

**三种条件是**`NOT <条件>`，**表示**“**不符合该条件**”**的记录**。

**要组合三个或者更多的条件**，**就需要用小括号**`()`**表示如何进行条件运算**

如果不加括号，条件运算按照`NOT`、`AND`、`OR`的优先级进行，即`NOT`优先级最高，其次是`AND`，最后是`OR`。加上括号可以改变优先级

![image-20210416215323785](G:\Blog_Djk\Hexo\source\_posts\mysql\image-20210416215323785.png)

#### 投影查询

如果我们只希望返回某些列的数据，而不是所有列的数据，我们可以用`SELECT 列1, 列2, 列3 FROM ...`，让结果集仅包含指定列。这种操作称为投影查询。

> 使用`SELECT 列1, 列2, 列3 FROM ...`时，还可以给每一列起个别名，这样，结果集的列名就可以与原表的列名不同。它的语法是`SELECT 列1 别名1, 列2 别名2, 列3 别名3 FROM ...`。

#### 排序

我们使用SELECT查询时，细心的读者可能注意到，查询结果集通常是按照`id`排序的，也就是根据主键排序。这也是大部分数据库的做法。如果我们要根据其他条件排序怎么办？可以加上`ORDER BY`子句。例如按照成绩从低到高进行排序：

```sql
SELECT id, name, gender, score FROM students ORDER BY score;
```

如果要反过来，按照成绩从高到底排序，我们可以加上`DESC`表示“倒序”：

```sql
SELECT id, name, gender, score FROM students ORDER BY score DESC;
```

果`score`列有相同的数据，要进一步排序，可以继续添加列名。例如，使用`ORDER BY score DESC, gender`表示先按`score`列倒序，如果有相同分数的，再按`gender`列排序：

```sql\
-- 按score, gender排序:
SELECT id, name, gender, score FROM students ORDER BY score DESC, gender;
```

默认的排序规则是`ASC`：“升序”，即从小到大。`ASC`可以省略，即`ORDER BY score ASC`和`ORDER BY score`效果一样。

如果有`WHERE`子句，**那么`ORDER BY`子句要放到`WHERE`子句后面**。例如，查询一班的学生成绩，并按照倒序排序：

```sql
-- 带WHERE条件的ORDER BY:
SELECT id, name, gender, score
FROM students
WHERE class_id = 1
ORDER BY score DESC;
```

#### 通配符

![image-20210416223016219](G:\Blog_Djk\Hexo\source\_posts\mysql\image-20210416223016219.png)

#### SQL内置函数和计算

![image-20210416223344733](G:\Blog_Djk\Hexo\source\_posts\mysql\image-20210416223344733.png)