2021年12月30日

### 一、SQL简明总结

#### SQL简介

- SQL指结构化查询语言
- SQL使有能力访问数据库
- SQL是一种ANSI的标准计算机语言(注：ANSI，美国国家标准化组织)

#### SQL的作用

- 1、面向数据库指向查询
- 2、可从数据库取回数据
- 3、可在数据库中插入新的记录
- 4、可更新数据库中的数据
- 5、可从数据库删除记录
- 6、可创建数据库
- 7、可在数据库中创建新表
- 8、可在数据库中创建存储过程
- 9、可在数据库中创建视图
- 10、可以设置表、存储过程和视图的权限

#### SQL是一种标准

SQL是一门ANSI的标准计算机语言，用来访问和操作数据库系统。SQL语句用于取回和更新数据库中的数据。SQL可与数据库程序协同工作。比如MS Access、DB2、Informix、MS SQL Server、Oracle、Sybase以及其他数据库系统。

不幸地是，存在着很多不同版本的 SQL 语言，但是为了与 ANSI 标准相兼容，它们必须以相似的方式共同地来支持一些主要的关键词（比如 SELECT、UPDATE、DELETE、INSERT、WHERE 等等）。

**注释：**除了 SQL 标准之外，大部分 SQL 数据库程序都拥有它们自己的私有扩展！

#### RDBMS(关系型数据库管理系统)

RDBMS指的是关系型数据库管理系统。RDBMS是SQL的基础。同样也是索引现代数据库系统的基础。 比如 MS SQL Server, IBM DB2, Oracle, MySQL 以及 Microsoft Access。 

RDBMS中的数据存储在被称为 表 (tables)的数据库对象中。表是相关的数据项的集合，它是有列和行组成的。

#### 重要事项

1、SQL对大小写不敏感。

2、SQL语句后面的分号。（某些数据库系统要求在每条SQL命令的末端使用分号。“分号”是在数据库系统中分隔每条SQL语句的标准方法，可在对服务器的相同请求中指向一条以上的语句）

3、MS Access和SQL Server2000，可不用在末尾添加分号，不过某些数据库软件要求必须使用分号结束。

#### SQL（DML）和（DDL）

SQL分为两部分：

- 数据操作语言(DML)
- 数据定义语言(DDL)

SQL(结构化查询语言)是用于执行查询的语法。但是SQL语言也包含用于更新、插入和删除的语法

#### 数据操作语言(DML)

- SELECT 从数据库表中查询获取数据
- UPDATE 更新数据库表中的数据
- DELETE 从数据库表中删除数据
- INSERT INTO 向数据库表中插入数据

#### 数据定义语言(DDL)

- CREATE DATABASE --创建数据库
- ALTER DATABASE --修改数据库
- CREATE TABLE --创建新表
- ALTER TABLE --变更（改变）数据库表
- DROP TABLE --删除表
- CREATE INDEX --创建索引（搜索键）
- DROP INDEX --删除索引

#### SELECT

用于从表中选取数据，结果被存储在一个结果表中（被称为结果集）

```sql
--SELECT语法
SELECT 列名称 FROM 表名称;
--或
SELECT * FROM 表名称;
```

#### DISTINCT

在表中，可能会包含重复值，当使用关键词DISTINCT时，可用于返回唯一不同的值

```sql
--DISTINCT语法
SELECT DISTINCT 列名称 FROM 表名称;
```

#### WHERE

可有条件的从表中选取数据，可将WHERE子句添加到SELECT语句

```SQL
--WHERE语法
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
```

##### 运算符

| 操作符  |     描述     |
| :-----: | :----------: |
|    =    |     等于     |
|   <>    |    不等于    |
|    >    |     大于     |
|    <    |     小于     |
|   >=    |   大于等于   |
|   <=    |   小于等于   |
| BETWEEN | 在某个范围内 |
|  LIKE   | 搜索某种模式 |

==注意：在某些版本的SQL中，操作符<>可以写成 !=.==

#### AND

AND和OR可以在WHERE子句中把两个或多个条件结合起来。

1、如果第一个条件和第二个条件都成立，则AND运算符显示一条记录。

2、如果第一个条件和第二个条件中只要有一个成立，则OR运算符显示一条记录。

AND示例：

```SQL
--使用 AND 来显示所有姓为 "Carter" 并且名为 "Thomas" 的人
SELECT * FROM Persons WHERER FristName = 'Thomas' AND LastName = 'Carter';
```

OR示例

```SQL
--使用 OR 来显示所有姓为 "Carter" 或者名为 "Thomas" 的人
SELECT * FROM pERSONS WHERE FirstName = 'Thomas' OR LastName = 'Carter';
```

#### ORDER BY

ORDER BY语句用于更具指定的列对结果集进行排序，默认升序对结果进行排序。

关键字：

- DESC（降序）
- ASC（升序）

示例：

```SQL	
以字母顺序显示公司名称（Company），并以数字顺序显示顺序号（OrderNumber）
SELECT Company, OrderNumber FROM Orders ORDER BY Company, OrderNumber;
```

#### INSERT INTO

INSERT INTOy用于向表格中掺入新的行

```SQL
--INSERT INTO语法
INSERT INTO 表名称 VALUES(值1，指2，......);

--指定要插入的数据列
INSERT INTO table_name(列1， 列2，....) VALUES(值1， 值2，......);
```

#### UPDATE

UPDATE用于修改表中的数据。

```SQL
--UPDATE语法
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值;
```

示例：

```SQL
UPDATE Person SET Address = 'Zhongshan 23', City = 'NanJing' WHERE LastName = 'Wilson';
```

#### DELETE

DELETE用于删除表中的行

```SQL
--DELETE语法
DELETE FROM 表名称 WHERE 列名称 = 值;
```

示例：

```SQL
--Fred Wilson会被删除
DELETE FROM Person WHERE LastNmame = 'Wilson';
```

#### TOP

TOP用于规定要返回的记录的数目

==注意：对于用于千条记录的大型表来说，TOP子句是非常有用的。并非所有的数据库系统都支持TOP子句。==

##### SQL Server的语法

```SQL
SELECT TOP number | percent column_name(s) FROM table_name; 
```

==注意：MySQL和Oracle中的SQL SELECT TOP是等价的==

##### MySQL的语法

```SQL
SELECT column_name(s)
FROM table_name
LIMIT number;

--示例
SELECT *
FROM Persons
LIMIT 5;
```

##### Oralce的语法

```SQL
SELECT COLUMN_NAME(S)
FROM table_name
WHERE ROWNUM <= number;

--示例
SELECT *
FROM Persons
WHERE ROWNUM <= 5;
```

##### SQL TOP示例

```SQL
--希望从表头选取头两条记录
SELECT TOP 2 * FROM Persons;
```

SQL TOP PERCENT示例

```SQL
--希望从表中选取50%的记录
SELECT TOP 50 PERCENT * FROM Persons;
```

#### LIKE

LIKE操作符用于WHERE子句中搜索列中的指定模式

```SQL
--LIKE语法
SELECT colmun_name(s)
FROM table_name
WHERE column_name LIKE pattern;

--示例：从表中选取以“N”开始的城市里的人
SELECT * FROM Persons
WHERE City LIKE 'N%';
```

==注意：“%”可用于通配符（模式中缺少的字母）==

#### 通配符

在搜索数据库中的数据时，可使用SQL通配符，可以进行替代一个或多个字符，SQL通配符必须与LIKE运算符一起使用。

在SQL中，可使用以下的通配符：

|           通配符           |            描述            |
| :------------------------: | :------------------------: |
|             %              |     代表零个或多个字符     |
|             _              |       仅替代一个字符       |
|         [charlist]         |   字符列中的任何单一字符   |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

##### 使用%通配符

```SQL
--"Persons" 表中选取居住在以 "Ne" 开始的城市里的人
SELECT * FROM Persons
WHERE City LIKE 'Ne%';

--"Persons" 表中选取居住在包含 "lond" 的城市里的人
SELECT * FROM Persons
WHERE City LIKE '%lond%';
```

##### 使用_通配符

```SQL
--"Persons" 表中选取名字的第一个字符之后是 "eorge" 的人
SELECT * FROM Persons
WHERE FristName LIKE '_eorge';

--"Persons" 表中选取的这条记录的姓氏以 "C" 开头，然后是一个任意字符，然后是 "r"，然后是一个任意字符，然后是 "er"
SELECT * FROM Persons
WHERE LastName LIKE 'c_r_er';
```

##### 使用[charlist]通配符

```SQL
--"Persons" 表中选取居住的城市以 "A" 或 "L" 或 "N" 开头的人
SELECT * FROM Persons
WHERE City LIKE '[ALN]%';

--"Persons" 表中选取居住的城市不以 "A" 或 "L" 或 "N" 开头的人
SELECT * FROM Persons
WHERE City LIKE '[!ALN]%';
```

#### IN

IN操作符运行在WHERE子句中规定多个值

```SQL
--IN操作符语法
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2,.....)

--示例
SELECT * FROM Persons
WHERE LastName IN ('Adams', 'Carter')
```

#### BETWEEN

BETWEEN操作符在WHERE子句中使用，作用是选取介于两个值之间的数据范围。

操作符BETWEEN ... AND或选取介于两个值之间的数据范围，值可为数值、文本或者日期。

```SQL
--BETWEEN语法
SELECT column_name(s)
FROM table_name
WHERE column_name
BETWEEN value1 AND value2;

--示例：显示介于 "Adams"（包括）和 "Carter"（不包括）之间的人
SELECT * FROM Persons
WHERE LastName
BETWEEN 'Adams' AND 'Carter';
```

#### Alias（别名）

通过使用SQL，可以为列名称和表名称指定别名（Alias）

```SQL
--表的Alias语法
SELECT column_name(s)
FROM table_name
AS alias_name;

--列的Alias语法
SELECT column_name AS alias_name FROM table_name;

--示例：使用表名称别名-"Persons" 和 "Product_Orders"。我们分别为它们指定别名 "p" 和 "po"
SELECT po.OrderID, p.LastName, P.FristName
FROM Persons AS p, Product_Order AS po
WHERE P.LastName = 'Adams' AND p.FirsrName = 'John';
```

#### JOIN

JOIN用于根据两个或多个表中的列之间的关系，从这些表中拆线呢数据。

##### JOIN和Key

如果需要得到完整的结果，需要先从两个或更多的表中获取结果。需要执行JOIN。

数据库中的表可通过键将彼此联系起来。主键（Primary Key）是一个列，在这个列中的每一行的值都是唯一的。在表中，每个主键的值都是唯一的。目的是在不重复每个表中的所有数据的情况下，将数据交叉捆绑在一起。

**Persons**表：

| Id_P | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

 注意，"Id_P" 列是 Persons 表中的的主键。这意味着没有两行能够拥有相同的 Id_P。即使两个人的姓名完全相同，Id_P 也可以区分 

**Order**表

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

注意，"Id_O" 列是 Orders 表中的的主键，同时，"Orders" 表中的 "Id_P" 列用于引用 "Persons" 表中的人，而无需使用他们的确切姓名。留意，"Id_P" 列把上面的两个表联系了起来。

##### 引用两个表

```SQL
SELECT Person.LastName, Persons.FristName, Orders.OrderNO
FROM Persons, Orders
WHERE Persons.Id_P = Orders.Id_P;
```

结果：

| LastName | FirstName | OrderNo |
| :------: | :-------: | :-----: |
|  Adams   |   John    |  22456  |
|  Adams   |   John    |  24562  |
|  Carter  |  Thomas   |  77895  |
|  Carter  |  Thomas   |  44678  |

##### 使用JOIN

使用关键字JOIN来从两个表中获取数据

```SQL
SELECT Person.LastName, Persons.FristName, Orders.OrderNO
FROM Persons
INNER JOIN Orders
ON Persons.Id_p = Orders.Id_p
ORDER BY Persons.LastName;
```

结果：

| LastName | FirstName | OrderNo |
| :------: | :-------: | :-----: |
|  Adams   |   John    |  22456  |
|  Adams   |   John    |  24562  |
|  Carter  |  Thomas   |  77895  |
|  Carter  |  Thomas   |  44678  |

##### 不同的SQL JOIN

- 1、INNER JOIN(内连接)。
- 2、JOIN：如果表中有至少一个匹配，则返回行。
- 3、LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行。
- 4、RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行。
- 5、FULL JOIN：只要其中一个表中存在匹配，就返回行。

#### INNER JOIN

在表中存在至少一个匹配时， INNER JOIN关键字返回行

```SQL
--INNER JOIN语法
SELECT column_name(s)
FROM table_name1
INNER JOIN table_name2
ON table_name1.column_name = table_name2_cloumn_name;
```

==注意：INNER JOIN 与 JOIN 是相同的。

 "Persons" 表 ：

| Id_P | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

 "Orders" 表 ：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

##### 内连接(INNER JOIN)

```SQL
--列出所有人的订购
SELECT Person.LastName, Person.FristName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id.P = Orders.Id_p
ORDER BY Persons.LastName;
```

结果：

| LastName | FirstName | OrderNo |
| :------: | :-------: | :-----: |
|  Adams   |   John    |  22456  |
|  Adams   |   John    |  24562  |
|  Carter  |  Thomas   |  77895  |
|  Carter  |  Thomas   |  44678  |

 INNER JOIN 关键字在表中存在至少一个匹配时返回行。如果 "Persons" 中的行在 "Orders" 中没有匹配，就不会列出这些行。 

#### LEFT JOIN 

从左表（table_name1）返回所有的行，即使在右表（table_name2）中没有匹配的行

```SQL
--LEFT JOIN语法
SELECT column_name(s)
FROM table_name1
LEFT JOIN table_name2
ON table_name1.column_name table_name2.column_name;
```

==注意：在某些数据库中，LEFT JOIN称为LEFT OUTER JOIN.==

 "Persons" 表 ：

| Id_P | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

 "Orders" 表 ：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

##### 左连接（LEFT JOIN）

```SQL
--列出所有的人。以及他们的订购·如果有的话
SELECT Persons.LastName, Persons.FristName, Orders.OrderNo
FROM Persons
LEFT JOIN Orders
ON Persons.Id_p = Orders.Id_p
ORDER BY Persons.LastName;
```

结果：

| LastName | FirstName | OrderNo |
| :------: | :-------: | :-----: |
|  Adams   |   John    |  22456  |
|  Adams   |   John    |  24562  |
|  Carter  |  Thomas   |  77895  |
|  Carter  |  Thomas   |  44678  |
|   Bush   |  George   |         |

 LEFT JOIN 关键字会从左表 (Persons) 那里返回所有的行，即使在右表 (Orders) 中没有匹配的行。 

#### RIGHT JOIN

从右表（table_name2）返回所有的行，即使在左表（table_name1）中没有匹配的行

```SQL
--RIGHT JOIN语法
SELECT column_name(s)
FROM table_name1
RIGHT JOIN table_name2
ON table_name1.column_name = table_name2.column_name;
```

==注意：在某些数据库中，RIGHT JOIN称为RIGHT OUTER JOIN.==

 "Persons" 表 ：

| Id_P | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

 "Orders" 表 ：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

##### 右连接（RIGHT JOIN）

```SQL
--列出所有的订单，以及订购它们的人，如果有的话
SELECT persons.LastName, Persons.FristName, Orders.OrderNO
FROM Persons
RIGHT JOIN Orders
ON Persons.Id_p = Orders.Id_p
ORDER BY Persons.LastName;
```

结果：

| LastName | FirstName | OrderNo |
| :------: | :-------: | :-----: |
|  Adams   |   John    |  22456  |
|  Adams   |   John    |  24562  |
|  Carter  |  Thomas   |  77895  |
|  Carter  |  Thomas   |  44678  |
|          |           |  34764  |

 RIGHT JOIN 关键字会从右表 (Orders) 那里返回所有的行，即使在左表 (Persons) 中没有匹配的行。 

#### FULL JOIN

只要其中某个表存在匹配，FULL JOIN就会返回行。

```SQL
--FULL JOIN语法
SELECT column_name(s)
FROM table_name1
FULL JOIN table_name2
ON table_name1.column_name = table_name2.column_name;
```

==注意：在某些数据库中，FULL JOIN称为FULL OUTER JOIN.==

"Persons" 表 ：

| Id_P | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

 "Orders" 表 ：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

##### 全连接（FULL JOIN）

```SQL
--列出所有的人，以及他们的订单，以及所有的订单，以及订购它们的人
SELECT Persons.LastName, Persons.FristName, Orders.OrderNO
FROM Persons
FULL JOIN Orders
ON Persons_Id_p = Orders.Id_p
ORDER BY Persons.LastName;
```

结果：


| LastName | FirstName | OrderNo |
| :------: | :-------: | :-----: |
|  Adams   |   John    |  22456  |
|  Adams   |   John    |  24562  |
|  Carter  |  Thomas   |  77895  |
|  Carter  |  Thomas   |  44678  |
|   Bush   |  George   |         |
|          |           |  34764  |

 FULL JOIN 关键字会从左表 (Persons) 和右表 (Orders) 那里返回所有的行。如果 "Persons" 中的行在表 "Orders" 中没有匹配，或者如果 "Orders" 中的行在表 "Persons" 中没有匹配，这些行同样会列出。 

#### UNION

UNION操作符用于合并两个或多个SELECT语句的结果集。

注意：UNION内部的SELECT语句必须拥有相同数量的列。列也必须有相似的数据类型，同时，每条SELECT语句中的列顺序必须相同。

```SQL
--UNION语法
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2;
```

==注意：默认地，UNION操作符选取不同的值，如果允许重复的值，请使用UNION ALL.==

#### UNION ALL

UNION结果集的列名总是等于UNION中的第一个SELECT语句中的列名。

```SQL
--列出所有在中国和美国的不同的雇员名
SELECT column_name(s) FROM table_name1
UNION ALL
SELECT column_name(s) FROM table_name2;
```

### Employees_China:

| E_ID |     E_Name     |
| :--: | :------------: |
|  01  |   Zhang, Hua   |
|  02  |   Wang, Wei    |
|  03  | Carter, Thomas |
|  04  |   Yang, Ming   |

### Employees_USA:

| E_ID |     E_Name     |
| :--: | :------------: |
|  01  |  Adams, John   |
|  02  |  Bush, George  |
|  03  | Carter, Thomas |
|  04  |  Gates, Bill   |

##### 使用UNION命令

```SQL
SELECT E_Name FROM Employees_China
UNION
SELECT E_Name FROM Employees_USA;
```

结果：

|     E_Name     |
| :------------: |
|   Zhang, Hua   |
|   Wang, Wei    |
| Carter, Thomas |
|   Yang, Ming   |
|  Adams, John   |
|  Bush, George  |
|  Gates, Bill   |

 **注释：**这个命令无法列出在中国和美国的所有雇员。在上面的例子中，我们有两个名字相同的雇员，他们当中只有一个人被列出来了。UNION 命令只会选取不同的值。 

##### 使用UNION ALL

UNION ALL命令和UNION命令几乎是等效的，不过UNION ALL命令列出所有的值。

```SQL
SQL Statement 1
UNION ALL
SQL Statement 2;
```

##### 使用UNION ALL命令

```SQL
--列出在中国和美国的所有的雇员
SELECT E_Name FROM Employees_China
UNION ALL
SELECT E_Name FROM Employees_USA;
```

结果：

|     E_Name     |
| :------------: |
|   Zhang, Hua   |
|   Wang, Wei    |
| Carter, Thomas |
|   Yang, Ming   |
|  Adams, John   |
|  Bush, George  |
| Carter, Thomas |
|  Gates, Bill   |

#### SELECT INTO

- 用于创建表的备份复件或者用于对记录进行存档。
- 从一个表中选取数据，然后把数据插入到另一个表中。

##### SELECT INTO

```SQL
--把所有的列插入新表
SELECT *
INTO new_table_name [IN externaldatabase]
FROM old_table_name;

--把希望的列插入新表
SELECT column_name(s)
INTO new_table_name [IN externaldatabase]
FROM OLD_TABLE_NAME;
```

##### 制作备份复件

```SQL
--制作“Persons”表的备份复件
SELECT *
INTO Persons_backup
FROM Persons;

--INTO子句可用于向两一个数据库中拷贝表
SELECT *
INTO Persons IN 'Backup.mdb'
FROM Persons;

--拷贝某些域或列，可在SELECT语句后列出
SELECT LastName, FirstName
INTO Person_backup
FROM Persons;
```

##### 带有WHERE子句

```SQL
--从 "Persons" 表中提取居住在 "Beijing" 的人的信息，创建了一个带有两个列的名为 "Persons_backup" 的表
SELECT LastName, FirstName
INTO Persons_backup
FROM Persons
WHERE City = 'BeiJing';
```

##### 被连接的表

```SQL
--创建一个名为 "Persons_Order_Backup" 的新表，其中包含了从 Persons 和 Orders 两个表中取得的信息
SELECT Persons.LastName, Orders.OrderNO
INTO Persons_Order_Backup
FROM Persons
INNER JOIN Orders
ON Persons.Id_p = Orders.Id_p;
```

#### CREATE DATABASE

用于创建数据库

```SQL
--CREATE DATABASE语法
CREATE DATABASE database_name;

--示例
CREATE DATABASE dsjprs_db;
```

#### CREATE TABLE

用于创建数据库中的表

```SQL
--CREATE TABLE语法
CREATE TABLE table_name(
    列名称1 数据类型，
    列名称2 数据类型，
    列名称3 数据类型，
    .......
);
```

 数据类型（data_type）规定了列可容纳何种数据类型。 SQL中最常用的数据类型 

|                         据类型                          |                             描述                             |
| :-----------------------------------------------------: | :----------------------------------------------------------: |
| integer(size)、int(size)、smallint(size)、tinyint(size) |           仅容纳整数。在括号内规定数字的最大位数。           |
|             decimal(size,d)numeric(size,d)              | 容纳带有小数的数字。"size" 规定数字的最大位数。"d" 规定小数点右侧的最大位数。 |
|                       char(size)                        | 容纳固定长度的字符串（可容纳字母、数字以及特殊字符）。在括号中规定字符串的长度。 |
|                      varchar(size)                      | 容纳可变长度的字符串（可容纳字母、数字以及特殊的字符）。在括号中规定字符串的最大长度。 |
|                     date(yyyymmdd)                      |                          容纳日期。                          |

示例：

```SQL
--如何创建名为 "Person" 的表。
--该表包含 5 个列，列名分别是："Id_P"、"LastName"、"FirstName"、"Address" 以及 "City"
CREATE TABLE Person(
	Id_p int,
    LastName varchar(225),
    FristName varchar(225),
    Address varchar(225),
    City varchar(225)
);
```

#### 约束（Constraints）

约束用于限制加入表的数据的类型。可以在创建表时规定约束（通过CREATE TABLE），或者在表创建之后也可以（通过ALTER TABLE语句）。

约束介绍：

- NOT NULL
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY
- CHECK
- DEFAULT

#### NOT NULL

NOT NULL约束强制不接受NULL的值。NOT NULL约束强制字段始终包含值。这意味着，如果不向指端添加值，就无法插入新记录或更新记录。

```SQL
--SQL语句强制“Id_P”列和“LastName”列接受NULL值
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225)
);
```

#### UNIQUE

UNIQUE约束唯一标识数据库表中的每条记录。UNIQUE和PRIMARY KEY约束均为列或列集合提供了唯一性的保证。PRIMARY KEY用于自动定义的UBIQUE约束，每个表可以有多个UNIQUE约束，但是每个表只能有一个PRIMARY KEY约束。

##### UNIQUE Constraint on CREATE TABLE

**MySQL**

```SQL
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225),
    UNIQUE (Id_p)
);
```

**SQL Server/Oracle/MS Access**

```sql
CREATE TABLE Persons(
	Id_p int NOT NULL UNIQUE,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225)
);
```

如果需要命名UNIQUE约束，以及多个列定义UNIQUE约束，则

**MySQL/SQL Server/Oracle/MS Access**

```SQL
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    Cirt varchar(225),
    CONSTRAINT uc_PersonID UNIQUE(Id_p, LastName)
);
```

##### UNIQUE Constraint on ALTER TABLE

当表已被创建，如需“Id_P”列创建UNIQUE约束

**MySQL/SQL Server/Oracle/MS Access**

```SQL
ALTER TABLE Person
ADD UNIQUE(Id_p);
```

如需命令UNIQUE约束，并定义多个列的UNIQUE约束

**MySQL/SQL Server/Oracle/MS Access**

```sql
ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE(Id_p, LastName);
```

##### 撤销UNIQUE约束

如需撤销UNIQUE约束

```SQL
--MySQL
ALTER TABLE Persons
DROP INDEX uc_PersonID;

--SQL Server / Oracle / MS Access
ALTER TABLE Persons
DROP CONSTRAINT uc_PersonsID;
```

#### PRIMARY KEY

PRIMARY KEY约束唯一标识数据库表中的每条记录。主键必须包含唯一的值。主键列不能包含NULL值。每个表都应用于有一个主键，并且每个表只能有一个主键。

##### PRIMARY KEY Constraint on CREATE TABLE

  在 "Persons" 表创建时在 "Id_P" 列创建 PRIMARY KEY 约束 

```SQL
--MySQL
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225),
    PRIMARY KEY(Id_p)
);
--SQL Server/Oracle/MS Access
CREATE TABLE Persons(
	Id_p int NOT NULL PRIMARY KEY,
    LastName varchar(225),
    FristName varchar(225),
    Address varchar(225),
    Address varchar(225),
    City varchar(225)
);
```

如果需要命名PRIMARY KEY约束，以及为多个列定义PRIMARY KEY约束

```SQL
--MySQL/SQL Server/Oracle/MS Access
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225),
    CONSTRAINT pk_PersonID PRIMARY KEY(Id_p, LastName)
);
```

##### PRIMARY KEY Constraint on ALTER TABLE

如果表已存在的情况下为“Id_p”列创建PRIMARY KEY约束

```SQL
--MySQL/SQL Server/Oracle/MS Access
ALTER TABLE Persons
add primary key (Id_p);
```

 如果需要命名 PRIMARY KEY 约束，以及为多个列定义 PRIMARY KEY 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
ALTER TABLE Persons
ADD CONSTRAINT pk_PersonID PRIMARY KEY(Id_p, LastName);
```

==注意：如果使用ALTER TABLE语句添加主键，必须把主键声明为不包含NULL值（在表首次创建时）==

##### 撤销PRIMARY KEY约束

如需撤销PRIMARY KEY约束

```SQL
--MySQL
ALTER TABLE Persons
DROP PRIMARY KEY;

--SQL Server/Oralce/MS Access
ALTER TABLE Person
DROP CONSTRAINT pk_PersonID;
```

#### FOREIGN KEY

一个表中的FOREIGN KEY指向拎一个表中的PRIMARY KEY。

"Persons" 表：

| Id_P | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

"Orders" 表：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |

注意：

"Orders" 中的 "Id_P" 列指向 "Persons" 表中的 "Id_P" 列。

"Persons" 表中的 "Id_P" 列是 "Persons" 表中的 PRIMARY KEY。

"Orders" 表中的 "Id_P" 列是 "Orders" 表中的 FOREIGN KEY。

FOREIGN KEY 约束用于预防破坏表之间连接的动作。

FOREIGN KEY 约束也能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一。

##### FOREIGN KEY Constraint on CREATE TABLE

  "Orders" 表创建时为 "Id_P" 列创建 FOREIGN KEY 

```SQL
--MySQL
CREATE TABLE Orders(
	Id_O int NOT NULL;
    OrderNo int NOT NULL,
    Id_p int,
    PRIMARY KEY (Id_O),
    FOREIGN KEY (Id_O) REFERENCES Persons(Id_p)
);

--SQL Server/Oracle/MS Access
CREATE TABLE oRDERS(
	Id_O int NOT NULL PRIMARY KEY,
    OrderNo int NUO NULL,
    Id_p int FOREIGN KEY REFERENCES Persons(Id_p)
);
```

 如果需要命名 FOREIGN KEY 约束，以及为多个列定义 FOREIGN KEY 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
CREATE TABLE Orders(
	Id_O int NOT NULL,
    OrderNo int NOT NULL,
    Id_p int,
    PRIMARY KEY (Id_O),
    CONSTRAINT fk_PerOrders FOREIGN KEY (Id_p),
    REFERENCES pERSON(Id_p)
);
```

##### FOREIGN KEY Constraint on ALTER TABLE

  "Orders" 表已存在的情况下为 "Id_P" 列创建 FOREIGN KEY 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
ALTER TABLE Orders
ADD FOREIGN KEY (Id_p)
REFERENCES Persons(Id_p)
```

 如果需要命名 FOREIGN KEY 约束，以及为多个列定义 FOREIGN KEY 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
ALTER TABLES Orders
ADD CONSTRAINT fk_PerOrders
FOREIGN KEY (Id_p) REFERENCES Persons(Id_p);
```

##### 撤销FOREIGN KEY约束

如需撤销FOREIGN KEY约束

```SQL
--MySQL
ALTER TABLE Orders
DROP FOREIGN KEY fk_PerOrders;

--SQL Server / Oracle/MS Access
ALTER TABLE Orders
DROP CONSTRAINT fk_PerOrders;
```

#### CHECK

CHECK约束用于限制列中的值的范围。如果多单个列定义CHECK约束，那么该列只允许特定的值。如果多一个表定义CHECK约束，那么此约束会在特定的列对值进行限制。

##### CHECK Constraint on CREATE TABLE

QL 在 "Persons" 表创建时为 "Id_P" 列创建 CHECK 约束。CHECK 约束规定 "Id_P" 列必须只包含大于 0 的整数。

```SQL
--MySQL
CREATE TABLE Persons
(
    Id_P int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255),
    CHECK (Id_P>0)
);
```

```SQL
--SQL Server / Oracle / MS Access
CREATE TABLE Persons
(
    Id_P int NOT NULL CHECK (Id_P>0),
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

 如果需要命名 CHECK 约束，以及为多个列定义 CHECK 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225),
    CONSTRAINT chk_Person CHECK (Id_P > 0 AND City = 'Sandnes')
);
```

##### CHECK Constraint on ALTER TABLE

 如果在表已存在的情况下为 "Id_P" 列创建 CHECK 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
ALTER TABLE Persons
ADD CHECK(Id_p > 0);
```

 如果需要命名 CHECK 约束，以及为多个列定义 CHECK 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
ALTER TABLE Persons
ADD CONSTRAINT chk_Person CHECK (Id_p > 0 AND City = 'Sandnes');
```

##### 撤销CHECK约束

 如需撤销 CHECK 约束 

```SQL
--SQL Server/Oracle/MS Access
ALTER TABLE Persons
DROP CONSTRAINT chk_Person;

--MySQL
ALTER TABLE Persons
DROP CHECK chk_Person;
```

#### DEFALUT

DEFAULT约束用于向列中插入默认值。如果没有规定其值，那么就会将默认值添加到所有的新记录。

##### DEFAULR Constrsint on CREATE TABLE

在 "Persons" 表创建时为 "City" 列创建 DEFAULT 约束 

```SQL
--MySQL/SQL Server/Oracle/MS Access
CREATE TABLE Persons(
	Id_p int NOT NULL,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225) DEFAULT 'Sandnes'
);
```

使用类似GETDATE()函数，DEFAULT约束也可以用于插入系统值

```SQL
CREATE TABLE Orders(
	Id_O int NOT NULL,
    OrderNo int NOT NULL,
    Id_p int,
    OrderDate date DEFAULT GETDATE()
);
```

##### DEFAULT Constraint on ALTER TABLE

 如果在表已存在的情况下为 "City" 列创建 DEFAULT 约束 

```SQL
--MySQL
ALTER TABLE Persons
ALTER City SET DEFAULT 'SANDNES';

--SQL Server/Oracle/MS Access
ALTER TABLE Persons
ALTER COLUMN City SET DEFAULT 'SANDNES';
```

##### 撤销约束

如需撤销DEFAULT约束

```SQL
--MySQL
ALTER TABLE Persons
ALTER City DROP DEFAULT;

--SQL Server/Oracle/MS Access
ALTER TABLE Persons
ALTER COLUMN City DROP DEFALUT;
```

#### CREATE INDEX

用于在表中创建索引。在不读取整个表的情况下，索引使数据库应用程序可以更快的查找数据。

##### 索引

可在表中创建索引，以便更加高效地查询数据。用户无法看到所有，它们只能被用来加速搜索、查询。

==注意：更新一个包含所有的表需要比更新一个没有索引的表更多的时间。这是由于索引本身也需要更新。因此，理想的做法是仅仅在常常被索引的列（以及表）上面创建索引。==

```SQL
--CREATE INDEX语法
CREATE INDEX index_name
ON table_name (column_name);

--注释：“column_name”规定需要索引的列



--CREATE UNIQUE INDEX语法
--在表上创建一个唯一的索引，唯一的索引意味着两行不饿能拥有相同的索引值。
CREATE UNIQUE INDEX index_name
ON table_name (column_name);
```

##### CREATE INDEX示例

 创建一个简单的索引，名为 "PersonIndex"，在 Person 表的 LastName 列 

```SQL
CREATE INDEX PersonIndex
ON Person(LastName);
```

 以*降序*索引某个列中的值，您可以在列名称之后添加保留字 *DESC* 

```SQL
CREATE TABLE PersonIndex
ON Person (LastName DESC)
```

 索引不止一个列，可以在括号中列出这些列的名称，用逗号隔开 

```SQL
CREATE INDEX PersonIndex
ON Person (LastName, FristName);
```

#### DROP

使用DROP语句，可以进行撤销索引、表以及数据库。

##### DROP INDEX

删除表格中的索引。



```SQL
--用于 Microsoft SQLJet (以及 Microsoft Access) 的语法
DROP INDEX index_name ON table_name;

--用于 MS SQL Server 的语法
DROP INDEX table_name.index_name;

--用于 IBM DB2 和 Oracle 语法
DROP INDEX index_name;

--用于 MySQL 的语法
ALTER TABLE table_name DROP INDEX index_name;
```

##### DROP TABLE

同于删除表（表结构、属性以及所有也会被删除）

```SQL
--语法
DROP TBLE 表名称;
```

##### DROP DATABASE

用于删除数据库

```SQL
AAADROP DTBSE 数据库名称;
```

##### TRUNCATE TABLE

如果仅仅需要除去表内的数据，但并不删除表本身，需要使用TRUNCATE（仅仅删除表格中的数据）

```SQL
TRUNCATE TABLE 表名称;
```

#### ALTER TABLE

用于在已有的表添加、修改或删除列。

```SQL
--ALTER TABLE语法
ALTER TABLE table_name
ADD column_name datatype;
```

要删除表中的列。

```SQL
ALTER TABLE table_name
DROP COLUMN column_name;
```

==注意：某些数据库系统不允许这种在数据库表中删除列的方式（DROP COLUMN column_name）.==

要改变表中列的数据类型

```SQL
ALTER TABLE table_name
ALTER COLUMN column_name datatype
```

Persons 表:

|  Id  | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

##### ALTER TABLE示例

 在表 "Persons" 中添加一个名为 "Birthday" 的新列 

```SQL
ALTER TABLE Persons
ADD Brithday date;
```

 注意，新列 "Birthday" 的类型是 date，可以存放日期。数据类型规定列中可以存放的数据的类型 。

新的 "Persons" 表类似这样：

|  Id  | LastName | FirstName |    Address     |   City   | Birthday |
| :--: | :------: | :-------: | :------------: | :------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |          |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |          |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |          |

##### 改变数据类型示例

 改变 "Persons" 表中 "Birthday" 列的数据类型。 

```SQL
ALTER TABLE Persons
ALTER COLUMN Birthday year;
```

 注意，"Birthday" 列的数据类型是 year，可以存放 2 位或 4 位格式的年份。 

##### DROP COLUMN 示例

删除 "Person" 表中的 "Birthday" 列：

```SQL
ALTER TABLE Person
DROP COLUMN Birthday
```

Persons 表会成为这样:

|  Id  | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

#### AUTO INCREMENT

会在新记录插入表中时生成·一个唯一的数字。通常希望在每次插入新记录时，自动地创建主键字段的值。

##### 用于MySQL的语法

 "Persons" 表中的 "P_Id" 列定义为 auto-increment 主键 

```SQL
CREATE TABLE Person(
	p_Id int NOT NULL AUTO_INCREMENT,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225),
    PRIMARY KEY (p_Id)
);
```

MySQL 使用 AUTO_INCREMENT 关键字来执行 auto-increment 任务。默认地，AUTO_INCREMENT 的开始值是 1，每条新记录递增 1。

 让 AUTO_INCREMENT 序列以其他的值起始 

```SQL
ALTER TABLE Persons AUTO_INCREMENT = 100;
```

 在 "Persons" 表中插入新记录，不必为 "P_Id" 列规定值（会自动添加一个唯一的值） 

```SQL
INSERT INTO Persons(FirstName, LastName) VALUES('Bill', 'Gates');
```

 SQL 语句会在 "Persons" 表中插入一条新记录。"P_Id" 会被赋予一个唯一的值。"FirstName" 会被设置为 "Bill"，"LastName" 列会被设置为 "Gates"。 

##### 用于SQL Server的语法

  "Persons" 表中的 "P_Id" 列定义为 auto-increment 主键 。

```SQL
CREATE TABLE Persons(
	p_Id int PARMARY KEY IDENTITY,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225)
);
```

MS SQL 使用 IDENTITY 关键字来执行 auto-increment 任务。默认地，IDENTITY 的开始值是 1，每条新记录递增 1。



规定 "P_Id" 列以 20 起始且递增 10，请把 identity 改为 IDENTITY(20,10)，要在 "Persons" 表中插入新记录，不必为 "P_Id" 列规定值（会自动添加一个唯一的值）

```SQL
INSERT INTO Persons (FirstName,LastName)VALUES ('Bill','Gates');
```

##### 用于Access的语法

 "Persons" 表中的 "P_Id" 列定义为 auto-increment 主键 。

```SQL
CREATE TABLE Persons(
	p_Id int PRIMARY KEY AUTO_INCREMENT,
    LastName varchar(225) NOT NULL,
    FristName varchar(225),
    Address varchar(225),
    City varchar(225)
);
```

MS Access 使用 AUTOINCREMENT 关键字来执行 auto-increment 任务。默认地，AUTOINCREMENT 的开始值是 1，每条新记录递增 1。



规定 "P_Id" 列以 20 起始且递增 10，请把 autoincrement 改为 AUTOINCREMENT(20,10)，要在 "Persons" 表中插入新记录，我们不必为 "P_Id" 列规定值（会自动添加一个唯一的值）

```SQL
INSERT INTO Persons (FirstName,LastName) VALUES ('Bill','Gates')
```

 SQL 语句会在 "Persons" 表中插入一条新记录。"P_Id" 会被赋予一个唯一的值。"FirstName" 会被设置为 "Bill"，"LastName" 列会被设置为 "Gates"。 

##### 用于Oracle的语法

在Oracle中，代码稍微复杂一点。必须通过sequence对创建AUTO_INCREMENT（该对象生成数字序列）

```SQL
CREATE SEQUENCE seq_person
MINVALUE 1
START WITH 1
INCREMENT BY 1
CACHE 10;
```

 创建名为 seq_person 的序列对象，它以 1 起始且以 1 递增。该对象缓存 10 个值以提高性能。CACHE 选项规定了为了提高访问速度要存储多少个序列值。 



 在 "Persons" 表中插入新记录，必须使用 nextval 函数（该函数从 seq_person 序列中取回下一个值） 

```SQL
INSERT INTO Persons (P_Id,FirstName,LastName)
VALUES (seq_person.nextval,'Lars','Monsen');
```

 SQL 语句会在 "Persons" 表中插入一条新记录。"P_Id" 的赋值是来自 seq_person 序列的下一个数字。"FirstName" 会被设置为 "Bill"，"LastName" 列会被设置为 "Gates"。 

#### CREATE VIEW

视图是可视化的表。在SQL中，视图是基于SQL语句的结果集的可视化表。视图包含行和列。就像一个真是的表。视图中的字段就是一个或多个数据库中真实的字段。可以向视图添加SQL函数、WHERE以及JOIN语句，可以提交数据，就行这些来自某单一的表。

==注意：数据库的设计和结构不会受到视图中的函数、WHERE或JOIN语句的影响。==

```SQL
--CREATE VIEW语法
CREATE VIEW view_name 
AS
SELECT column_name(s)
FROM table_name
WHERE condition;
```

==注意：视图总是显示最近的数据。每当用户查询视图时，数据库引擎通过使用SQL舆来重建数据。==

##### 更新视图

```SQL
--更新视图语法
SQL CREATE OR REPLACE VIEW Syntax
CREATE OR REPLACE VIEW view_name AS
SELECT column_name(s) 
FROM table_name
WHERE condition;
```

##### 撤销视图

通过DROP VIEW命令来删除视图

```SQL
SQL DROP VIEW Syntax
DROP VIEW view_name;
```

#### Date函数

当处理日期时，最难的任务恐怕时确保所插入的日期的格式，与数据库中的日期列的格式相匹配。只要数据包含的只是日期部分，运行拆线呢就不会出现问题。但是，如果涉及时间，情况就会变得复杂。

##### MySQL Date函数

  MySQL 中最重要的内建日期函数 

|     函数      |                描述                 |
| :-----------: | :---------------------------------: |
|     NOW()     |        返回当前的日期和时间         |
|   CURDATE()   |           返回当前的日期            |
|   CURTIME()   |           返回当前的时间            |
|    DATE()     | 提取日期或日期/时间表达式的日期部分 |
|   EXTRACT()   |      返回日期/时间按的单独部分      |
|  DATE_ADD()   |      给日期添加指定的时间间隔       |
|  DATE_SUB()   |      从日期减去指定的时间间隔       |
|  DATEDIFF()   |       返回两个日期之间的天数        |
| DATE_FORMAT() |      用不同的格式显示日期/时间      |

##### SQL Server Date函数

SQL Server 中最重要的内建日期函数 

|    函数    |               描述               |
| :--------: | :------------------------------: |
| GETDATE()  |        返回当前日期和时间        |
| DATEPART() |     返回日期/时间的单独部分      |
| DATEADD()  | 在日期中添加或减去指定的时间间隔 |
| DATEDIFF() |      返回两个日期之间的时间      |
| CONVERT()  |    用不同的格式显示日期/时间     |

##### SQL Date数据类型

MySQL 使用下列数据类型在数据库中存储日期或日期/时间值：

- DATE - 格式 YYYY-MM-DD
- DATETIME - 格式: YYYY-MM-DD HH:MM:SS
- TIMESTAMP - 格式: YYYY-MM-DD HH:MM:SS
- YEAR - 格式 YYYY 或 YY

SQL Server 使用下列数据类型在数据库中存储日期或日期/时间值：

- DATE - 格式 YYYY-MM-DD
- DATETIME - 格式: YYYY-MM-DD HH:MM:SS
- SMALLDATETIME - 格式: YYYY-MM-DD HH:MM:SS
- TIMESTAMP - 格式: 唯一的数字

#### NULL

NULL值是遗漏的未知数据。默认地，表的列可以存放NULL值。SQL NULL值，如果表中的某个列是可选的，那么我们可以在不向该列添加值的情况下插入新记录或更新已有的记录。这意味着该字段可以以NULL值保存。NULL值的处理方式与其他值不同。NULL用作位置的或不适用的值的占位符。

==注意：无法比较NULL和0；它们是不等价的。==

##### SQL IS NULL

如何仅仅选取在 "Address" 列中带有 NULL 值的记录呢？必须使用 IS NULL 操作符

```SQL
SELECT LastName, FristName, Address FROM Persons
WHERE Address IS NULL;
--提示：始终使用IS NULL 来查找NULL值
```

##### SQL IS NOT  NULL

如何选取在 "Address" 列中不带有 NULL 值的记录呢？必须使用 IS NOT NULL 操作符

```SQL
SELECT LastName, FristName, Address FROM Persons
WHERE Address IS NOT NULL;
```

#### NULL函数

##### SQL ISNULL()、NVL()、IFNULL() 和 COALESCE() 函数

 "Products" 表：

| P_Id | ProductName | UnitPrice | UnitsInStock | UnitsOnOrder |
| :--: | :---------: | :-------: | :----------: | :----------: |
|  1   |  computer   |    699    |      25      |      15      |
|  2   |   printer   |    365    |      36      |              |
|  3   |  telephone  |    280    |     159      |      57      |

 假如 "UnitsOnOrder" 是可选的，而且可以包含 NULL 值。 

使用如下 SELECT 语句：

```SQL
SELECT ProductName,UnitPrice*(UnitsInStock+UnitsOnOrder)
FROM Products
```

在上面的例子中，如果有 "UnitsOnOrder" 值是 NULL，那么结果是 NULL。微软的 ISNULL() 函数用于规定如何处理 NULL 值。NVL(), IFNULL() 和 COALESCE() 函数也可以达到相同的结果。在这里，希望 NULL 值为 0。下面，如果 "UnitsOnOrder" 是 NULL，则不利于计算，因此如果值是 NULL 则 ISNULL() 返回 0。

##### SQL Server/MS Access

```SQL
SELECT ProductName, UnitPrice*(UnitsInStock + ISNULL(UnitsOnOrder, 0)) 
FROM Products;
```

##### Oracle

Oracle没有ISNULL（）函数。不过可以使用NVL（）函数达到相同的结果。

```SQL
SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
FROM Products;
```

##### MySQL

MySQL也拥有类似ISNULL（）函数，不过与微软的ISNULL（）函数有点不同。在MySQL中，可以使用IFNULL（）函数。

```SQL
SELECT ProductName,UnitPrice*(UnitsInStock+IFNULL(UnitsOnOrder,0))
FROM Products;
```

 或者使用 COALESCE() 函数 

```SQL
SELECT ProductName,UnitPrice*(UnitsInStock+COALESCE(UnitsOnOrder,0))
FROM Products;
```

#### SQL数据类型

##### MySQL 数据类型

在 MySQL 中，有三种主要的类型：文本、数字和日期/时间类型。

**Text 类型：**

|     数据类型     |                             描述                             |
| :--------------: | :----------------------------------------------------------: |
|    CHAR(size)    | 保存固定长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的长度。最多 255 个字符。 |
|  VARCHAR(size)   | 保存可变长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的最大长度。最多 255 个字符。注释：如果值的长度大于 255，则被转换为 TEXT 类型。 |
|     TINYTEXT     |             存放最大长度为 255 个字符的字符串。              |
|       TEXT       |            存放最大长度为 65,535 个字符的字符串。            |
|       BLOB       | 用于 BLOBs (Binary Large OBjects)。存放最多 65,535 字节的数据。 |
|    MEDIUMTEXT    |          存放最大长度为 16,777,215 个字符的字符串。          |
|    MEDIUMBLOB    | 用于 BLOBs (Binary Large OBjects)。存放最多 16,777,215 字节的数据。 |
|     LONGTEXT     |        存放最大长度为 4,294,967,295 个字符的字符串。         |
|     LONGBLOB     | 用于 BLOBs (Binary Large OBjects)。存放最多 4,294,967,295 字节的数据。 |
| ENUM(x,y,z,etc.) | 允许你输入可能值的列表。可以在 ENUM 列表中列出最大 65535 个值。如果列表中不存在插入的值，则插入空值。注释：这些值是按照你输入的顺序存储的。可以按照此格式输入可能的值：ENUM('X','Y','Z') |
|       SET        | 与 ENUM 类似，SET 最多只能包含 64 个列表项，不过 SET 可存储一个以上的值。 |

**Number 类型：**

|    数据类型     |                             描述                             |
| :-------------: | :----------------------------------------------------------: |
|  TINYINT(size)  |  -128 到 127 常规。0 到 255 无符号*。在括号中规定最大位数。  |
| SMALLINT(size)  | -32768 到 32767 常规。0 到 65535 无符号*。在括号中规定最大位数。 |
| MEDIUMINT(size) | -8388608 到 8388607 普通。0 to 16777215 无符号*。在括号中规定最大位数。 |
|    INT(size)    | -2147483648 到 2147483647 常规。0 到 4294967295 无符号*。在括号中规定最大位数。 |
|  BIGINT(size)   | -9223372036854775808 到 9223372036854775807 常规。0 到 18446744073709551615 无符号*。在括号中规定最大位数。 |
|  FLOAT(size,d)  | 带有浮动小数点的小数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。 |
| DOUBLE(size,d)  | 带有浮动小数点的大数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。 |
| DECIMAL(size,d) |       作为字符串存储的 DOUBLE 类型，允许固定的小数点。       |

这些整数类型拥有额外的选项 UNSIGNED。通常，整数可以是负数或正数。如果添加 UNSIGNED 属性，那么范围将从 0 开始，而不是某个负数。

**Date 类型：**

|  数据类型   |                             描述                             |
| :---------: | :----------------------------------------------------------: |
|   DATE()    | 日期。格式：YYYY-MM-DD注释：支持的范围是从 '1000-01-01' 到 '9999-12-31' |
| DATETIME()  | *日期和时间的组合。格式：YYYY-MM-DD HH:MM:SS注释：支持的范围是从 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59' |
| TIMESTAMP() | *时间戳。TIMESTAMP 值使用 Unix 纪元('1970-01-01 00:00:00' UTC) 至今的描述来存储。格式：YYYY-MM-DD HH:MM:SS注释：支持的范围是从 '1970-01-01 00:00:01' UTC 到 '2038-01-09 03:14:07' UTC |
|   TIME()    | 时间。格式：HH:MM:SS 注释：支持的范围是从 '-838:59:59' 到 '838:59:59' |
|   YEAR()    | 2 位或 4 位格式的年。注释：4 位格式所允许的值：1901 到 2155。2 位格式所允许的值：70 到 69，表示从 1970 到 2069。 |

即便 DATETIME 和 TIMESTAMP 返回相同的格式，它们的工作方式很不同。在 INSERT 或 UPDATE 查询中，TIMESTAMP 自动把自身设置为当前的日期和时间。TIMESTAMP 也接受不同的格式，比如YYYYMMDDHHMMSS、YYMMDDHHMMSS、YYYYMMDD 或 YYMMDD。

##### SQL Server 数据类型

**Character 字符串：**

|   数据类型   |                     描述                      | 存储 |
| :----------: | :-------------------------------------------: | :--: |
|   char(n)    |     固定长度的字符串。最多 8,000 个字符。     |  n   |
|  varchar(n)  |     可变长度的字符串。最多 8,000 个字符。     |      |
| varchar(max) | 可变长度的字符串。最多 1,073,741,824 个字符。 |      |
|     text     |     可变长度的字符串。最多 2GB 字符数据。     |      |

**Unicode 字符串：**

|   数据类型    |                        描述                        | 存储 |
| :-----------: | :------------------------------------------------: | :--: |
|   nchar(n)    |    固定长度的 Unicode 数据。最多 4,000 个字符。    |      |
|  nvarchar(n)  |    可变长度的 Unicode 数据。最多 4,000 个字符。    |      |
| nvarchar(max) | 可变长度的 Unicode 数据。最多 536,870,912 个字符。 |      |
|     ntext     |    可变长度的 Unicode 数据。最多 2GB 字符数据。    |      |

B**inary 类型：**

|    数据类型    |                  描述                   | 存储 |
| :------------: | :-------------------------------------: | :--- |
|      bit       |            允许 0、1 或 NULL            |      |
|   binary(n)    | 固定长度的二进制数据。最多 8,000 字节。 |      |
|  varbinary(n)  | 可变长度的二进制数据。最多 8,000 字节。 |      |
| varbinary(max) |  可变长度的二进制数据。最多 2GB 字节。  |      |
|     image      |    可变长度的二进制数据。最多 2GB。     |      |

**Number 类型：**

|   数据类型   |                             描述                             |    存储     |
| :----------: | :----------------------------------------------------------: | :---------: |
|   tinyint    |                 允许从 0 到 255 的所有数字。                 |   1 字节    |
|   smallint   |            允许从 -32,768 到 32,767 的所有数字。             |   2 字节    |
|     int      |     允许从 -2,147,483,648 到 2,147,483,647 的所有数字。      |   4 字节    |
|    bigint    | 允许介于 -9,223,372,036,854,775,808 和 9,223,372,036,854,775,807 之间的所有数字。 |   8 字节    |
| decimal(p,s) | 固定精度和比例的数字。允许从 -10^38 +1 到 10^38 -1 之间的数字。p 参数指示可以存储的最大位数（小数点左侧和右侧）。p 必须是 1 到 38 之间的值。默认是 18。s 参数指示小数点右侧存储的最大位数。s 必须是 0 到 p 之间的值。默认是 0。 |  5-17 字节  |
| numeric(p,s) | 固定精度和比例的数字。允许从 -10^38 +1 到 10^38 -1 之间的数字。p 参数指示可以存储的最大位数（小数点左侧和右侧）。p 必须是 1 到 38 之间的值。默认是 18。s 参数指示小数点右侧存储的最大位数。s 必须是 0 到 p 之间的值。默认是 0。 |  5-17 字节  |
|  smallmoney  |     介于 -214,748.3648 和 214,748.3647 之间的货币数据。      |   4 字节    |
|    money     | 介于 -922,337,203,685,477.5808 和 922,337,203,685,477.5807 之间的货币数据。 |   8 字节    |
|   float(n)   | 从 -1.79E + 308 到 1.79E + 308 的浮动精度数字数据。 参数 n 指示该字段保存 4 字节还是 8 字节。float(24) 保存 4 字节，而 float(53) 保存 8 字节。n 的默认值是 53。 | 4 或 8 字节 |
|     real     |      从 -3.40E + 38 到 3.40E + 38 的浮动精度数字数据。       |   4 字节    |

**Date 类型：**

|    数据类型    |                             描述                             |    存储    |
| :------------: | :----------------------------------------------------------: | :--------: |
|    datetime    | 从 1753 年 1 月 1 日 到 9999 年 12 月 31 日，精度为 3.33 毫秒。 |  8 bytes   |
|   datetime2    | 从 1753 年 1 月 1 日 到 9999 年 12 月 31 日，精度为 100 纳秒。 | 6-8 bytes  |
| smalldatetime  |  从 1900 年 1 月 1 日 到 2079 年 6 月 6 日，精度为 1 分钟。  |  4 bytes   |
|      date      |  仅存储日期。从 0001 年 1 月 1 日 到 9999 年 12 月 31 日。   |  3 bytes   |
|      time      |                仅存储时间。精度为 100 纳秒。                 | 3-5 bytes  |
| datetimeoffset |              与 datetime2 相同，外加时区偏移。               | 8-10 bytes |
|   timestamp    | 存储唯一的数字，每当创建或修改某行时，该数字会更新。timestamp 基于内部时钟，不对应真实时间。每个表只能有一个 timestamp 变量。 |            |

**其他数据类型：**

|     数据类型     |                             描述                             |
| :--------------: | :----------------------------------------------------------: |
|   sql_variant    | 存储最多 8,000 字节不同数据类型的数据，除了 text、ntext 以及 timestamp。 |
| uniqueidentifier |                   存储全局标识符 (GUID)。                    |
|       xml        |               存储 XML 格式化数据。最多 2GB。                |
|      cursor      |              存储对用于数据库操作的指针的引用。              |
|      table       |                   存储结果集，供稍后处理。                   |

##### Microsoft Access 数据类型

|   数据类型    |                             描述                             |   存储   |
| :-----------: | :----------------------------------------------------------: | :------: |
|     Text      |        用于文本或文本与数字的组合。最多 255 个字符。         |          |
|     Memo      | Memo 用于更大数量的文本。最多存储 65,536 个字符。注释：无法对 memo 字段进行排序。不过它们是可搜索的。 |          |
|     Byte      |                    允许 0 到 255 的数字。                    |  1 字节  |
|    Integer    |           允许介于 -32,768 到 32,767 之间的数字。            |  2 字节  |
|     Long      |   允许介于 -2,147,483,648 与 2,147,483,647 之间的全部数字    |  4 字节  |
|    Single     |                 单精度浮点。处理大多数小数。                 |  4 字节  |
|    Double     |                 双精度浮点。处理大多数小数。                 |  8 字节  |
|   Currency    | 用于货币。支持 15 位的元，外加 4 位小数。提示：您可以选择使用哪个国家的货币。 |  8 字节  |
|  AutoNumber   |    AutoNumber 字段自动为每条记录分配数字，通常从 1 开始。    |  4 字节  |
|   Date/Time   |                        用于日期和时间                        |  8 字节  |
|    Yes/No     | 逻辑字段，可以显示为 Yes/No、True/False 或 On/Off。在代码中，使用常量 True 和 False （等价于 1 和 0）注释：Yes/No 字段中不允许 Null 值 |  1 比特  |
|  Ole Object   | 可以存储图片、音频、视频或其他 BLOBs (Binary Large OBjects)  | 最多 1GB |
|   Hyperlink   |              包含指向其他文件的链接，包括网页。              |          |
| Lookup Wizard |       允许你创建一个可从下列列表中进行选择的选项列表。       |  4 字节  |

#### SQL 服务器-RDBMS

##### DBMS-数据库管理系统（Database Management System）

数据库管理系统是一种可以访问数据库中数据的计算机程序。DBMS可以在数据库中提取、修改或者存储信息。不同的DBMS提供了不同的函数用于查询。提交以及修改数据。

##### RDBMS-关系型数据库管理系统（Relationnal Database Management Systen）

关系型数据库管理系统（RDBMS）也是一种数据库管理系统，其数据库是根据数据间的关系来组织和访问数据的。20世纪70年代初。IBM公司发明了RDBMS。RDBMS是SQL的基础， 也是所有现代数据库系统诸如 Oracle、SQL Server、IBM DB2、Sybase、MySQL 以及 Microsoft Access 的基础。 

### SQL函数

SQL拥有很多可用于计数和计算的内建函数

#### 函数的语法

```SQL
--内建SQL函数的语法
SELECT function(列) FROM 表;
```

#### 函数的类型

在SQL中，基本的函数类型和种类有若干种。函数的基本类型为：

- Aggregate函数
- Scalar函数

#### 合计函数（Aggregate functions）

 Aggregate 函数的操作面向一系列的值，并返回一个单一的值。 

 **注释：**如果在 SELECT 语句的项目列表中的众多其它表达式中使用 SELECT 语句，则这个 SELECT 必须使用 GROUP BY 语句！ 

##### "Persons" table (在大部分的例子中使用过)

|      Name      | Age  |
| :------------: | :--: |
|  Adams, John   |  38  |
|  Bush, George  |  33  |
| Carter, Thomas |  28  |

##### MS Access 中的合计函数

|      函数      |               描述               |
| :------------: | :------------------------------: |
|  AVG(column)   |         返回某列的平均值         |
| COUNT(column)  | 返回某列的行数（不包括 NULL 值） |
|    COUNT(*)    |           返回被选行数           |
| FIRST(column)  |  返回在指定的域中第一个记录的值  |
|  LAST(column)  | 返回在指定的域中最后一个记录的值 |
|  MAX(column)   |         返回某列的最高值         |
|  MIN(column)   |         返回某列的最低值         |
| STDEV(column)  |                                  |
| STDEVP(column) |                                  |
|  SUM(column)   |          返回某列的总和          |
|  VAR(column)   |                                  |
|  VARP(column)  |                                  |

##### 在 SQL Server 中的合计函数

|          函数          |                           描述                           |
| :--------------------: | :------------------------------------------------------: |
|      AVG(column)       |                     返回某列的平均值                     |
|    BINARY_CHECKSUM     |                                                          |
|        CHECKSUM        |                                                          |
|      CHECKSUM_AGG      |                                                          |
|     COUNT(column)      |              返回某列的行数（不包括NULL值）              |
|        COUNT(*)        |                       返回被选行数                       |
| COUNT(DISTINCT column) |                    返回相异结果的数目                    |
|     FIRST(column)      |  返回在指定的域中第一个记录的值（SQLServer2000 不支持）  |
|      LAST(column)      | 返回在指定的域中最后一个记录的值（SQLServer2000 不支持） |
|       MAX(column       |                     返回某列的最高值                     |
|      MIN(column)       |                     返回某列的最低值                     |
|     STDEV(column)      |                                                          |
|     STDEVP(column)     |                                                          |
|      SUM(column)       |                      返回某列的总和                      |
|      VAR(column)       |                                                          |
|      VARP(column)      |                                                          |

#### Scalar 函数

Scalar 函数的操作面向某个单一的值，并返回基于输入值的一个单一的值。

##### MS Access 中的 Scalar 函数

|          函数           |                  描述                  |
| :---------------------: | :------------------------------------: |
|        UCASE(c)         |           将某个域转换为大写           |
|        LCASE(c)         |           将某个域转换为小写           |
|   MID(c,start[,end])    |          从某个文本域提取字符          |
|         LEN(c)          |          返回某个文本域的长度          |
|      INSTR(c,char)      |  返回在某个文本域中指定字符的数值位置  |
| LEFT(c,number_of_char)  |    返回某个被请求的文本域的左侧部分    |
| RIGHT(c,number_of_char) |    返回某个被请求的文本域的右侧部分    |
|    ROUND(c,decimals)    | 对某个数值域进行指定小数位数的四舍五入 |
|        MOD(x,y)         |           返回除法操作的余数           |
|          NOW()          |           返回当前的系统日期           |
|    FORMAT(c,format)     |          改变某个域的显示方式          |
| DATEDIFF(d,date1,date2) |            用于执行日期计算            |

#### AVG()

AVG()函数返回值列的平均值。NULL值不包括在计算中。

```SQL
--AVG()语法
SELECT ACG(column_name) FROM table_name;
```

#### COUNT()

COUNT()函数返回指定条件的行数。COUNT(column_name)函数返回指定列的值的数目（NULL不计入）。

```SQL
--COUNT(column_name)语法
SELECT COUNT(column_name) FROM table_name;
```

##### COUNT(*)语法

函数返回表中的记录数。

```SQL
SELECT COUNT(*) FROM table_name;
```

##### COUNT(DISTINCT column_name)语法

函数返回指定列的不同值的数目。

```SQL
SELECT COUNT(DISTINCT column_name) FROM table_name;
```

==**注释：**COUNT(DISTINCT) 适用于 ORACLE 和 Microsoft SQL Server，但是无法用于 Microsoft Access.==

#### FIRST()

FIRST()函数返回指定的字段中第一个记录的值。

提示：可使用ORDER BY语句对记录进行排序。

```SQL
--FIRDT()语法
SELECT FIRST(column_name) FROM table_name;
```

#### LAST()

LAST()函数返回指定的字段中最后一个记录的值。

提示：可使用ORDER BY语句对记录进行排序。

```SQL
--LAST()语法
SELECT LAST(column_name) FROM table_name;
```

#### MAX()

MAX()函数返回一列中的最大值。NULL值不包括在计算中。

```SQL
--MAX()语法
SELECT MAX(column_name) FROM table_name;
```

==注释：MIN和MAX也可用于文本列，以获得按字母顺序排列的最高或者最低值。==

#### MIN()

 MIN 函数返回一列中的最小值。NULL 值不包括在计算中。 

```SQL
--MIN() 语法
SELECT MIN(column_name) FROM table_name
```

==**注释：**MIN 和 MAX 也可用于文本列，以获得按字母顺序排列的最高或最低值。==

#### SUM()

SUM函数返回数值列的总数（总额）

```SQL
--SUM()语法
SELECT SUM(column_name) FROM table_name;
```

#### GROUP BY

合计函数（比如SUM）常常需要添加GROUP BY语句

GROUP BY语句用于结合合计函数，根据一个或多个列对结果集进行分组。

```SQL
--GROUP BY语法
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```

#### HAVING

在SQL中增加HAVING子句的原因是，WHERE关键字无法与合计函数一起使用。

```SQL	
--HAVING语法
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
HAVING aggregate_function(column_name) operator value;
```

#### UCASE()

UCASE()函数把字段的值转换为大写。

```SQL
--UCASE()语法
SELECT UCASE(column_name) FROM table_name;
```

#### LCASE()

LCASE()函数把字段的值转换为小写。

```SQL
--LCASE()语法
SELECT LCASE(column_name) FROM table_name;
```

#### MID()

MID()函数用于从文本字段中提取字符。

```SQL
--MID()语法
SELECT MID(column_name, start[, length]) FROM table_name;
```

|    参数     |                            描述                             |
| :---------: | :---------------------------------------------------------: |
| column_name |                  必需。要提取字符的字段。                   |
|    start    |             必需。规定开始位置（起始值是 1）。              |
|   length    | 可选。要返回的字符数。如果省略，则 MID() 函数返回剩余文本。 |

#### LEN()

LEN()函数返回文本字段中值的长度。

```SQL
--LEN()语法
SELECT LEN(column_name) FROM table_name;
```

#### ROUND()函数

ROUND()函数用于把数值字段舍入为指定的小数位数。

```SQL
--ROUND()语法
SELECT ROUND(column_name, dicimals) FROM table_name;
```

|    参数     |             描述             |
| :---------: | :--------------------------: |
| column_name |     必需。要舍入的字段。     |
|  decimals   | 必需。规定要返回的小数位数。 |

#### NOW()

NOW()函数返回当前的日期和时间。

提示：如果在使用SQL Server数据库，请使用getdate()函数来获取当前的日期和时间。

```SQL
--NOW()语法
SELECT NOW() FROM table_name;
```

#### FORMAT()

FORMAT()函数用于对字段的显示进行格式化。

```SQL
--FORMAT()语法
SELECT FROMAT(column_name, fromat) FROM table_name;
```

|    参数     |          描述          |
| :---------: | :--------------------: |
| column_name | 必需。要格式化的字段。 |
|   format    |    必需。规定格式。    |