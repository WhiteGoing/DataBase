# MySQL

## 一、 基本使用

### 1. MySQL基本命令

####(1)　连接MySQL数据库 

```bash
# mysql [-h host_name] [-u user_name] [-p password]
# mysql -u root -p 
Enter password: mysql857025899
# 
```

#### (2) mysql基本命令

```mysql
mysql> help
```

#### (3) 库的操作

数据库服务器以数据库为一个个基本的管理对象，mysql提供了丰富的库操作命令，如下：

```mysql
1. 显示数据库列表
mysql> show databases;
2. 选择一个数据库(如：选择mysql)
mysql> use mysql
3. 查看一个数据库中的所有表
mysql> show tables;
```

实例：

```mysql
1. 构建公司数据库
mysql> create database company;

2. 创建员工信息表
mysql> create table worker(
	>	nid int not null, 
    >	name varchar(20) not null, 
    >	address varchar(20) not null, 
    >	salary float not null, 
    >	level int not null, 
    >	primary key(nid));
    
3. 插入基本数据
mysql> insert into worker values (100, 'tom', 'beijing', 2000.0, 0), 
	>	(101, 'jim', 'shanghai', 2000.0, 1), 
	>	(102, 'mali', 'shanghai', 3000.0, 2);
	
4. 查询全部数据
mysql> select * from worker;
+-----+------+----------+--------+-------+
| nid | name | address  | salary | level |
+-----+------+----------+--------+-------+
| 100 | tom  | beijing  |   2000 |     0 |
| 101 | jim  | shanghai |   2000 |     1 |
| 102 | mali | shanghai |   3000 |     2 |
+-----+------+----------+--------+-------+

5. 删除其中一条数据
mysql> delete from worker where nid=100;
mysql> select * from worker;
+-----+------+----------+--------+-------+
| nid | name | address  | salary | level |
+-----+------+----------+--------+-------+
| 101 | jim  | shanghai |   2000 |     1 |
| 102 | mali | shanghai |   3000 |     2 |
+-----+------+----------+--------+-------+

6. 更新其中一条记录
mysql> update worker set level=2, salary=3000.0 where nid=101;
mysql> select * from worker;
+-----+------+----------+--------+-------+
| nid | name | address  | salary | level |
+-----+------+----------+--------+-------+
| 101 | jim  | shanghai |   3000 |     2 |
| 102 | mali | shanghai |   3000 |     2 |
+-----+------+----------+--------+-------+

7. 删除数据库
（１）删除所有的数据表，SQL语句为：
	mysql> drop table worker;
（２）删除数据库，SQL语句为：
	mysql> drop database company;


```



##二、　数据库操作

## 1. SQL语言简介

SQL语言包括三个部分：

### (1) 数据定义语言(DDL)

用于定义和管理对象（数据库、数据表、视图等），语法有：create, drop, alter

### (2) 数据操作语言(DML)

操作数据库，语法有：select, insert, update, delete

###(3) 数据控制语言(DCL) 

用来管理数据库的语言，包含管理权限及数据更新，如：grank, revoke, commit, rollback语句



SQL中的数据类型主要分为一下５种：字符型、文本型、数值型、逻辑型、日期型

MySQL数据库中的注释：

(1) 以“＃”号开头直到行尾的所有内容都是注释

(2) 以“--”(注意"--"后面还有空格)号开头直到行尾的所有内容都是注释

(3) 以```“/*”```开始，以```“*/”```结尾的所有内容都是注释，可多行

## 2. 数据库操作

###(1) 创建数据库

```mysql
mysql> create database db_name
/*1. 名字可以由任意字母、数字、'_'或“$”组成，可以上述任意字符开头，但不允许单独由数字组成，易于数值混淆
　２．名称的长度限制为：数据库、表、列和索引的名称最多可由64个字符组成，而别名最多可达到256个字符。
　3.　不能使用MySQL的关键字作为数据库、表名。*/
```

### (2) 删除数据库

```mysql
mysql> drop database db_name
# 应该谨慎使用drop database语句，因为其是不可恢复的，建议删前先备份
```

## 3. 表的操作

###(1) 创建表

```mysql
# 1. 创建数据表的基本语法：
create table <表名>
(<列名>　<数据类型>[<列级完整性约束条件>]
 [, <列名>　<数据类型>[<列级完整性约束条件>] ]...
 [, 表级完整性约束条件] )
 
 # 2. MySQL中，创建表的定义如下：
 create [temporary] table [if not exists] tbl_name
 [(] like old_tbl_name [])];
 # temporary 参数可以用来创建临时表，在这些表与服务器的交互结束时会自动删除
```

### (2) 修改表

```mysql
# 1. 基本语法
alter table <表名>
[add <新列名> <数据类型> [完整性约束]]
[drop <完整性约束名>]
[alter column <列名> <数据类型>]
```

### (3) 删除表

```mysql
drop table table_name
# 如果不确定一个表是否存在，可以加上if exists语句，如下：
drop table if exists table_name
```

## 4. 记录的操作

### (1) 插入数据

```mysql
# 1. 基本语法
insert into <表名>
[(<属性名> [,<属性列2>...])]
values (<常量1> [, <常量2>]...)

# 如果按照表中的属性依次插入，则可以省略属性名的书写：
mysql> insert into worker values (100, 'tom', 'beijing', 2000.0, 0), 
	>	(101, 'jim', 'shanghai', 2000.0, 1), 
	>	(102, 'mali', 'shanghai', 3000.0, 2);

# 也可以如下：
mysql> insert into worker (nid, name, address) values (100, 'tom', 'beijing');

# 从另一个表选择数据插入：
mysql> insert into worker (nid, name, address) select nid, name, address from table_2;
```

### (2) 更新记录

```mysql
update <表名>
set <列名>=<表达式> [,<列名>=<表达式>]...
[where <条件>];

mysql> update student_info set stu_age=22 where stu_id=9028
```

### (3) 删除记录

```mysql
delete from <表名> [where <条件>] -- 注意，如果不加where，则整个表的数据都将被删除
```

## 5. 查询

```mysql
# 基本语法：
select [all|distinct] <目标列表达式> [, [目标列表达式]]...
from <表名或视图名>[, <表名或视图名>]...
[where <条件表达式>]
[group by <列名1> [having <条件表达式>]]
[order by <列名2> [asc|desc]]

# mysql:
SELECT
    [ALL | DISTINCT | DISTINCTROW ]
      [HIGH_PRIORITY]
      [STRAIGHT_JOIN]
      [SQL_SMALL_RESULT] [SQL_BIG_RESULT] [SQL_BUFFER_RESULT]
      [SQL_CACHE | SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS]
    select_expr [, select_expr ...]
    [FROM table_references
      [PARTITION partition_list]
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}
      [ASC | DESC], ... [WITH ROLLUP]]
    [HAVING where_condition]
    [WINDOW window_name AS (window_spec)
        [, window_name AS (window_spec)] ...]
    [ORDER BY {col_name | expr | position}
      [ASC | DESC], ...]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}]
    [INTO OUTFILE 'file_name'
        [CHARACTER SET charset_name]
        export_options
      | INTO DUMPFILE 'file_name'
      | INTO var_name [, var_name]]
    [FOR UPDATE | LOCK IN SHARE MODE]]
    [FOR {UPDATE | SHARE} [OF tbl_name [, tbl_name] ...] [NOWAIT | SKIP LOCKED] 
      | LOCK IN SHARE MODE]]
  
 mysql> select nid from worker where salary > 2000;
+-----+
| nid |
+-----+
| 101 |
| 102 |
+-----+     

```

## 6. 视图

###(1) 基本含义

视图是一个虚表，其内容由查询定义，同真实的表一样，视图包含一系列带有名称的列和行数据，且操作类似。但是，视图的行和列数据来自于查询时所引用的表，并且在引用视图时动态生成。

使用视图的原因：安全性；使复杂的操作易于理解和使用；

###(2) 视图的语法

MySQL在处理视图时有两种算法，即：MERGE和TEMPTABLE。在执行CREATE VIEW语句时，可以指定使用哪种算法。MERGE指在涉及到视图的操作时，将对视图的操作根据视图的定义进行展开，有点类似与C语言的宏定义。

```mysql
#创建
CREATE [OR REPLACE] [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
VIEW view_name [{column_list}] #column_list可以将select语句的列名进行修改，且列数必须相等。
AS select_statement
[WITH [CASCADED | LOCAL] CHECK OPTION]

#删除
DROP VIEW [IF EXISTS]
		view_name [, view_name] ...
[RESTRICT | CASCADE]
```

视图定义服从一下限制：

1. SELECT语句不能包含FROM子句中的子查询、不能应用系统或用户变量、不能引用预处理语句参数
2. 在存储子程序内，定义不能引用子程序参数或局部变量
3. 在定义中应用的表格或视图必须存在，但在创建视图后，可以舍弃这些表格或视图。
4. 定义中不能引用TEMPORARY表，不能创建TEMPORARY视图。
5. 不能将触发程序与视图关联在一起。

在视图的定义中可以使用ORDER BY语句，但是如果被选择的视图中具有自己的ORDER BY，它将被忽略。

### (3)视图的使用

通过对视图看到的数据进行修改，相应的基本表数据也会发生变化，同时若基本表的数据发生变化，这种变化也会自动反映到视图中。

规则：

1. 视图必须唯一命名
2. 在MySQL中视图的数量没有限制
3. 创建视图必须从管理员那里获取必要的权限
4. 视图支持嵌套，即视图的视图
5. 视图不能索引，也不能关联触发器或默认值
6. 视图可以和表同时使用

##7. 触发器操作

触发器是一种特殊的存储过程，它在插入、删除或修改特定表中的数据时触发执行。***要在两张表上实现***。

### (1) MySQL定义

```mysql
CREATE
    [DEFINER = { user | CURRENT_USER }]
    TRIGGER trigger_name
    trigger_time trigger_event
    ON tbl_name FOR EACH ROW
    [trigger_order]
    trigger_body
    
trigger_time: { BEFORE | AFTER }

trigger_event: { INSERT | UPDATE | DELETE }
# insert: insert or load data or replace
# update: update
# delete: delete or replace

trigger_order: { FOLLOWS | PRECEDES } other_trigger_name

# 在执行对个语句时，可以使用BEGIN...END复合语句。
mysql> create trigger level_up after insert on worker
    -> for each row 
    -> begin
    -> update worker_2 set level = 3 where level = 2;
    -> delete from worker_2 where level = 0;
    -> end
    
    
mysql> create trigger also_insert before insert on worker for each row insert into finary values (new.nid, new.level);
```



##8. 存储过程、存储函数

存储过程：是一组为了完成特定功能的SQL语句集，经编译存储在数据库中。

```mysql
create procedure sp_name ([proc_parameter[,...]]) #指定数据库时使用db_name.sp_name
[characteristic ...]
routine_body

# 在存储过程中声明局部变量，作用范围在begin...end之间：
declare var_name[,...] type [default value]

mysql->declare counter int default 0;
set counter = counter + 1;

# 在存储过程中，set语句一般用于声明子程序内的变量或者全局服务器变量
set var_name = expr [, var_name = expr] ....
```



存储函数与存储过程相对应，调用用call语句，区别（？）

```mysql
create function sp_name ([func_parameter[,...]])
	returns type   # 指定返回值类型
	[characteristic ...]
	routine_body   # 包含return value
```



##9. 索引

索引是对数据库表中一列或多列的值进行排序的一种结构。

创建：

```mysql
create [unique | fulltext | spatial] index index_name
[using index_type]
on table_name (index_col_name , ...)
```



