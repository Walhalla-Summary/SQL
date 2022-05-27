2021年12月29日

### SQLServer简明总结

**数据操作类**

```sql
SELECT --查询   
INSERT --插入   
DELETE --删除   
UPDATE --更新
```

**数据定义类**

```sql
CREATE TABLE --创建表   
DROP TABLE --删除表   
ALTER TABLE --修改表结构    
CREATE INDEX --创建索引
DROP INDEX --删除索引  
CREATE VIEW --创建视图   
DROP VIEW --删除视图    
CREATE PROCEDURE --创建存储过程   
DROP PROCEDURE --删除存储过程
```

**统计函数**

```sql
AVG --求平均值   
MAX --求最大值   
MIN --求最小值   
COUNT --统计数目   
SUM --求和
```

**事务**

```sql
COMMIT --结束当前事务  
ROLLBACK --中止当前事务   
SET TRANSACTION --定义当前事务数据访问特征
```

**日期函数**

```sql
GetDate()--获取当时时间  
YEAR()--年份值  
MONTH()--月份值  
DAY()--日期值  
DATEADD( datepart, number,date)--在日期中添加或减去指定的时间间隔   

DATEDIFF(datepart ,startdate ,enddate)--函数返回两个指定日期之间的时间  
DATENAME(XX , Date )--函数以字符串的形式返回日期的指定部分  
DATEPART( datepart,date )--返回日期/时间的单独部分。
```

**游标**

```sql
DECLARE --为查询设定游标  
EXPLAN --为查询描述数据访问计划   
OPEN --检索查询结果打开一个游标  
FETCH --检索一行查询结果 
CLOSE --关闭游标  
PREPARE --为动态执行准备SQL 语句   
EXECUTE --动态地执行SQL 语句   
DESCRIBE --描述准备好的查询
```

![sqlserver](Images/sqlserver-1640682403131.jpg)

**上面介绍了基本语句关键词，在B/S开发框架中，应用了大量的数据库知识，下面我来看看数据库的一些常用和高级的sql语句。**

#### **常识**

1、创建数据库

```sql
CREATE DATABASE dbname
```

2、删除数据库

```sql
drop database dbname
```

3、备份

--- 创建 备份数据的 device

```sql
USE master

EXEC sp_addumpdevice 'disk', 'dbback', 'd:\sqlbackup\dbname.dat'
```

--- 开始 备份

```sql
BACKUP DATABASE pubs TO dbback
```

4、创建表

```sql
create table tabname(col1 type1 [not null][primary key],col2 type2 [not null],..)
```

复制表结构：

```sql
A：createtable newtable like oldtabe (复制表结构)

B：createtable newtable as select coloum1,coloum2,coloum3,… from oldtable definition only
```

5、删除表

```sql
drop table tablename
```

6、增加列

```sql
Alter table tablename add column columnname type
```

7、添加主键： 

```sql
Alter table tablename add primarykey(columnname)
```

   删除主键： 

```sql
Alter table tablename drop primary key(columnname)
```

8、创建索引：

```sql
create[unique] index indexname on tablename(columnname….)
```

   删除索引：

```sql
drop index indexname
```

注：索引是不可更改的，想更改必须删除重新建。

9、创建视图：

```sql
create view viewname as select statement
```

   删除视图：

```sql
drop view viewname
```

10、基本的sql语句集

插入：

```sql
insert into table(field1,field2) values(value1,value2)
```

删除：

```sql
delete from table where ...
```

更新：

```sql
update table set field=value where ...
```

选择：

```sql
select * from table where ...
```

查找：

```sql
select * from table where field like ’%value%’   ---模糊查找
```

总数：

```sql
select count(1) as totalcount from table
```

最大：

```sql
select max(field) as maxv from table
```

最小：

```sql
select min(field) as minv from table
```

求和：

```sql
select sum(field) as sumv from table
```

平均：

```sql
select avg(field) as avgv from table
```

11、三个逻辑运算符

A： UNION 并集运算符

```sql
UNION 多个表数据集合去重后结果表，带 ALL不去重复行，表的数据并集。
```

B： EXCEPT 不包含运算符

```sql
A表 EXCEPT B表，表示包括在A表中但不在B表中的行并去掉重复行的出结果表，带 ALL 不去除重复行。
```

C： INTERSECT 交集运算符（去重）

```sql
A表 INTERSECT B表， 表示A、B表公共部分并去掉重复行的结果表。带 ALL不去重复行。
```

12、内连接和外连接

A、left (outer) join：

左外连接(左连接)：左表数据全部保留，右表数据只保留连接条件过滤后的数据。

SQL: 

```sql
select A.a, a.b, a.c, b.c, b.d, b.f from A LEFT JOIN B ON A.a = B.c
```

B：full/cross (outer) join：

全外连接：两个连接表中的所有记录。

13、Order by 和 Group by:

Order by按照条件来进行正序和逆序排序。

根据group by中条件来分成若干组，然后进行统计，必须带分组统计函数：count,sum,max,min,avg等。

14、where 后 1=1，1=2，1<>1

```sql
“1=1” 是表示选择全部， “1=2”全部不选， “1<>1”全部不选
```

15：获取当前数据库中的所有用户表

```sql
select Name from sysobjects where xtype='u' and status>=0
```

16：获取某一个表的所有字段

```sql
select name from syscolumns where id=object_id('表名')

select name from syscolumns where id in (select id from sysobjects where type = 'u' and name = '表名')
```

两种方式的效果相同

17：查看当前数据库中所有存储过程

```sql
select name as 存储过程名称 from sysobjects wherextype='P'
```

18：查询某一个表的字段和数据类型

```sql
select column_name,data_type from information_schema.columns where table_name = '表名'
```

![sqlserver](https://www.hocode.com/images/sqlserver.jpg)

**下面为B/S开发框架数据库语句高级进阶知识分享**

#### 进阶

1、子查询(表名1：a 表名2：b)

```sql
select a,b,c from a where a IN (select d from b ) 或 select a,b,c from a where a IN (...)
```

2、between,between查询数据范围内的结果集，查询数据范围时包括了边界值,not between不在数据范围内的结果集。

```sql
select * from table where a between '值1' and '值2'

select * from table where a not between ‘数值1‘ and ‘数值2’
```

3、in，表是在数据范围内的结果集， not in 反之。

```sql
select * from table where a in (‘值1’,’值2’,’值3’,’值4’,’值5’)
```

4、两张关联表，删除表1中已经在表2中没有的信息

```sql
delete from table1 where not exists (select * from table2 where table1.field1=table2.field1 )
```

5、多表内连接查询公共数据：

```sql
select * from A join B on A.a=B.a join C on A.a=C.a where...
```

6、复制表(只复制表结构,源表名：a 新表名：b)

```sql
select * into b from a where 1<>1(仅用于SQL Server)

or select top 0 * into b from a
```

7、拷贝表(拷贝数据,源表名：a 目标表名：b) 

```sql
insert into b(a, b, c) select d,e,f from b;
```

8、跨数据库之间表的拷贝(具体数据使用绝对路径) 

```sql
insert into b(a, b, c) select d,e,f from bin ‘具体数据库’ where ...

例子：..from b in'"&Server.MapPath(".")&"\data.mdb"&"' where...
```

9、前n条记录

```sql
select top n * form table where...
```

10、删除表或者表数据

```sql
TRUNCATE TABLE tablename --清空表，不留痕迹   
Delete from TABLE tablename --仅仅删除数据    
drop tabel tablename --删除表，包括表结构
```

11、选择从第m到第n条记录的结果集

```sql
select top (n-m) * from (select top n * from tablename order by id asc) table order by id desc
```

12、随机选择记录

```sql
select newid()
```

13、随机取出n条数据

```sql
select top n * from tablename order by newid()
```

14、删除重复记录，请用查询分析器分析性能开销！

1)

```sql
delete from tablename where id not in (select max(id) from tablename group by column1,column2,column3...)
```

2)

```sql
select distinct * into temp from tablename;

delete from tablename;

insert into tablename select* from temp;
```

15、case when then使用

```sql
select type,(case columnname when 'xx' then 'oo' when 'xxx' then 'ooo' else 'over' end) FROM tablename
```



### MySQL

#### 引言

[B/S开发框架](https://www.hocode.com/) 中MySQL和SQL Server从语法和语句上都比较的相似的，懂SQL Server的童鞋学起MySQL是很容易，不过对数据库没有功底的童鞋也务气磊，三尺冰冻非一日之寒，只要用心学也不那么的难，学习地址[SqlServer基本语法和语句大全_B/S开发框架](https://www.hocode.com/OrgTec/DB/0006.html)，在B/S开发框架中是支持SQL Server和MySQL的，可以根据项目情况选择，下面根据经验总结下MySQL的常用语法和语句。

![B/S开发框架_mysql](Images/mysql.jpg)

#### 语法

新建表

```sql
CREATE TABLE table_name (column_name column_type);
```

添加字段

```sql
alter table table_name add column column_name column_type； 
```

删除表

```sql
drop table table_name;
```

插入数据

```sql
insert into table_name (field01, field02) values (1， ’first’);
```

创建索引

```sql
index index_name on table_name (col_name[(length)]，... ) 
```

B/S开发框架改变表结构，如包括改变字段名

```sql
alter table table_name alter_spec [， alter_spec ...] 
```

删除数据对象，如删除表或索引

```sql
drop table table_name ;
drop index Index_name;
```

插入数据

```sql
insert [into] table_name [(column(s))]  values (expression(s)) 
```

删除数据

```sql
delete from table_name where search_condition 
```

修改数据

```sql
table_name set column_name=value where ...; 
```

查询数据

```sql
SELECT [STRAIGHT_JOIN] [SQL_SMALL_RESULT] [SQL_BIG_RESULT] [HIGH_PRIORITY] [DISTINCT | DISTINCTROW | ALL]  
```

列出表清单 

```sql
show tables;  
```

列出表中的字段清单 

```sql
show columns from table_name; 
```

统计函数

```sql
sum (exepression) 计算和
avg (exepression) 计算平均值
count (exepression) 进行简单的计数
count (*) 统计记录数
max (exepression) 求最大值
min (exepression) 求最小值
```

#### 常用语句及举例

B/S开发框架里我们以产品数据模型的数据库表操作为例为大家说明

**创建表**

```sql
CREATE TABLE tb_Product(
	Id int NOT NULL AUTO_INCREMENT,
	CatalogID int NULL,
	Code varchar(500) NOT NULL,
	Name varchar(500) NOT NULL,
	Description varchar(500) NOT NULL,
	StoreID int NOT NULL,
	Used bit NOT NULL,
	CreateAt datetime NULL,
	CreateBy varchar(500) NULL,
	ModifyAt datetime NULL,
	ModifyBy varchar(500) NULL,
  CONSTRAINT PRIMARY KEY (Id),
  CONSTRAINT `FK_tb_Product_CatalogID` FOREIGN KEY (`CatalogID`) REFERENCES `tb_Catalog` (`Id`),
  CONSTRAINT `FK_tb_Product_StoreID` FOREIGN KEY (`StoreID`) REFERENCES `tb_Store` (`Id`)

) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8 ;
CONSTRAINT PRIMARY KEY (Id)：创建主键
CONSTRAINT `FK_tb_Product_CatalogID` FOREIGN KEY (`CatalogID`) REFERENCES `tb_Catalog` (`Id`)：创建外键
```

为编号创建非聚集索引

```sql
CREATE INDEX `IX_tb_Product_Code` ON `tb_Product` (`Code` ASC);
```

插入数据

```sql
insert tb_Product(CatalogID,Code,Name,Description,StoreID,Used) values(1,'P001','产品1','',1,0)
```

**查询数据**

```sql
select * from tb_Product where id=1
```

```java
void doSomething(Shape shape){
    shape.erase();
    shape.draw();
}
Circle circle = new Circle();
Triangle triangle = new Triangle();
Line line = new Line();
doSomething(circle);
```

