2021年12月24日

### Oracle踩坑记录

之前安装的是Oracle21版本，想想不靠谱，索性卸载了。。。。。。。。。

安装Oracle19c版本，踩坑记录

Oracle用户创建后，需要另外指定或者删除已存在的Oracle用户，其次删除Oracle服务，和相关文件，通过cmd，打开regedit注册表，进行删除Oracle相关文件信息

期间踩坑 Oracle configure assistant安装失败，Oracle已经指定现有目录或用户。

Oracle电子书





### Oracle相关学习

#### select 语句

```sql
select 
	column_1,
	column_2,
	.....
from
	table_name;
```

#### Order By子句

```sql
select
	column_1,
	column_2,
	column_3,
	.....
from
	table_name
ORDER BY
	column_1 [ASC | DESC] [NULLS FRIST | NULLS LAST],
	column_1 [ASC | DESC] [NULLS FRIST | NULLS LAST],
```

#### Distinct子句

```sql
select DISTINCT
	column_1
from
	table_name;
	
--例子
select 
	*,
	count(distinct name)
from
	table 
	group by name; 
```

#### Where子句

```sql
select
	column_1,
	column_2,
	....
from
	table_name
where
	serch_condition
order by
	column_1,
	column_2;
```

#### and子句

```sql
--例子_1
select 
	order_id, costomer_id, status, TO_CHAR(order_date, 'YYYY-MM-DD') as order_date
from 
	orders
where
	status = 'Pending' AND customer_id = 2
order by 
	order_date;
	
--例子_2
select
	order_id
	customer_id,
	status,
	TO_CHAR(order_date, 'YYYY-MM-DD') as order_date
from 
	orders
where
	status = 'Shipped'
	and salesman_id = 60
	and EXTRACT(YEAR from order_date) = 2017
order by
	order_date;
```

#### or子句

```sql
--例子_1
select
	order_id,
	customer_id,
	status,
	TO_CHAR(order_date, 'YYYY-MM-DD') as order_date
from
	orders
where
	status = 'Pending'
	or status = 'Canceled'
order by
	order_date desc;
--例子_2
select
	order_id,
	customer_id,
	status,
	salesman_id
	TO_CHAR(order_date, 'YYYY-MM-DD') as order
from
	orders
where
	salesman_id = 60
	or salesman_id = 61
	or salesman_id = 62
order by
	order_date desc;
```

#### fetch子句

```sql
--一下查询语句仅仅能在oracle 12c 以上版本进行执行
--获取前N行记录的示例
select
	product_name,
	quantity
from
	inventories
inner join products
	using(product_id)
order by
	quantity desc
fetch next 5 rows only;

--with ties示例
select
	product_name,
	quantity
from
	inventories
	inner json products
	using(product_id)
order by
	quantity desc
fetch next 10 rows with ties;

--以百分比限制返回行的示例
select
	product_name,
	quantity
from
	invertories
	inner json products
	using
order by
	quantity desc
fetch frist 1 percent rows only;
```

#### in子句

```sql
expression [NOT] IN (v1, v2, .....)
--或者
expression [NOT] IN (subquery)

--例子
select 
	order_id,
	customer_id,
	status,
	salesman_id,
from
	orders
where
	salesman_id IN (54, 55, 56)
order by
	order_id;
	
--例子2
select 
	order_id,
	customer_id,
	status,
	salesman_id
from
	orders
where
	status NOT IN('Shipped', Cannceled)
order by
	order_id;
```

#### between子句

```sql
expression [NOT] between low and high
value >= low and value <= high

--例子
select
	produce_name,
	standard_cost
from
	products
where
	standard_cost between 500 and 600
order by
	standard_cost;
	
--例子2
select
	product_name,
	standard_cost
from
	products
where
	standard_cost not between 500 and 600
order by
	product_name;
	
--例子3
select
	order_id,
	customer_id,
	status,
	order_date
from
	orders
where
	order_date between date '2021-12-21' and date '2021-12-26'
order by
	order_date
```

#### like子句

```sql
expression [NOT] like pattern [escape escape_characters]

--例子1
select
	fristname,
	last_name,
	phone
from
	constacts
where
	last_name lis 'St%'
order by
	last_name;

--例子2
select
	frist_name,
	last_name,
	phone
from
	contacts
where
	last_name like '%er'
order by
	last_name;
```

#### Oracle事务特性

## 事务特性

SQL92标准对数据库事务的特点进行如下定义：

**原子性(Atomicity)：**一个事务里面所有包含的SQL语句都是一个整体，是不可分割的，要么不做，要么都做。

**一致性(Consistency)：**事务开始时，数据库中的数据是一致的，事务结束时，数据库的数据也应该是一致的。

**隔离性(Isolation)：**数据库允许多个并发事务同时对其中的数据进行读写和修改的能力，隔离性可以防止事务在并发执行时，由于他们的操作命令交叉执行而导致的数据不一致状态。

**持久性 (Durability) :** 当事务结束后，它对数据库中的影响是永久的，即便系统遇到故障的情况下，数据也不会丢失。

一组SQL语句操作要成为事务，数据库管理系统必须保证这组操作的原子性（Atomicity）、一致性（consistency）、隔离性（Isolation）和持久性（Durability），这就是ACID特性。

#### Commit语法（提交事务）

```sql
commit [work] [comment clause] [write clause] [force clause]

--commit语句示例
commit;
commit work write wait immediate;

--添加备注
commit comment 'This is the comment the transaction';
--sql
--或者
commit work comment 'This is the comment for the transaction';

--强制
commit force '22.14.67';
commit work force '22.14.67';
```

#### rollback(事务回滚)

```sql
rollback [work] [TO[savepint] savepoint_name | force 'String'];
--rollback语法示例
rollback;
rollback work;

--savepoint
rollback to savepoint savepoint1;
rollback work to savepoint1;

--force
rollback force '22.14.67';
rollback work force '22.14.67';
```

#### set transaction语法(设置事务)

```sql
set transaction [read only | read write]
	[isloatton level [serialize | read commited]]
	[user rollback segment 'segment_name']
	[name 'transaction_name']
	

--set transaction示例
--只读
set transaction read only name 'ro_example';
-- 此示例会将事务设置为只读，并为其分配“RO_example”的名称。

--读写
set transaction read write name 'RW——example';

--use rollback segment示例
declare
	l_name varchar2(100);
	l_age number;
	l_sex varchar2(2);
begin
 -- 为保证set transaction是事务的第一条语句，先使用commit或rollback来结束掉前面可能存在的事务
 commit;
 --使用name给事务命名
 set transaction read only name "查询报表";
 select 
 	name
 	into l_name
 from
 	student
 where
 	student_id = 1001;
 select
 	age
 	into l_age
 from
 	student
 where
 	student_id = 1001;
 select 
 	sex
 	into l_sex
 from
 	student
 where
 	student_id = 1001;
```

#### locak table(锁表)

```sql
lock table tables in lock_mode mode [wait [, integer] | nowit];
--参数
--tables：用逗号分隔的表格列表。
--lock_mode：它是以下值之一：

--lock table示例
lock table suppliers in share mode nowait;

```

| lock_mode           | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| ROW SHARE           | 允许同时访问表，但阻止用户锁定整个表以进行独占访问。         |
| ROW EXCLUSIVE       | 允许对表进行并发访问，但阻止用户以独占访问方式锁定整个表并以共享方式锁定表。 |
| SHARE UPDATE        | 允许同时访问表，但阻止用户锁定整个表以进行独占访问。         |
| SHARE               | 允许并发查询，但用户无法更新锁定的表。                       |
| SHARE ROW EXCLUSIVE | 用户可以查看表中的记录，但是无法更新表或锁定`SHARE`表中的表。 |
| EXCLUSIVE           | 允许查询锁定的表格，但不能进行其他活动。                     |

WAIT：它指定数据库将等待(达到指定整数的特定秒数)以获取 DML 锁定。

NOWAIT：它指定数据库不应该等待释放锁

#### 外键创建

```sql
--使用create table语句创建
create table table_name
(
	column1 datetype null/not null,
    column2 datetype null/not null,
    ....
    constraint fk_column
    	foreign key (column1, column2, column_n)
    	references parent_table (column1, column2,..column_n)
);

--示例
create table supplier(
	supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    contact_name varchar2(50),
    constraint supplier_pk primary key (supplier_id)
);
create table produces(
	product_id numeric(10) not null,
    supplier_id numeric(10) not null,
    constraint fk_supplier
    	foreign key (supplier_id)
    	references (supplier_id)
);

--创建一个具有多个字段的外键
create table suplier(
	supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    contact_name varchar2(50),
    constraint supplier_pk primary key (supplier_id, supplier_name)
);
create table products(
	product_id numeric(10) not null,
    supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    constraint fk_supplier_comp
    	foreign key (supplier_id, supplier_name)
    	references supplier(supplier_id, supplier_name)
);

--使用alter table语句创建
--在alter table语句中创建外键的语法是
alter table table_name
add constraint constraint_name
	foreign key (column1, column2,..column_n)
	references parent_table (column1,...column_n)

--示例
alter table products
add constraint fk_supplier
	foregn key (supplier_id)
	references supplier(supplier_id);
```

#### 级联删除外键

```sql
--使用create table语句定义级联删除
create table table_name(
	column1 datatype null/not null,
    column2 datetype null/not null,
    ....
    
    constraint fk_column
    	foreign key (column1, column2, .. column_n)
    	references parent_table (column1, column2, column_n)
    	on delete cascade
);

--示例
create table supplier(
	supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    contact_name varchar2(50),
    constraint supplier_pk primary key (supplier_id)
);
create table products(
	product_id numeric(10) not null,
    supplier_id numeric(10) not null,
    constraint fk_supplier
    	foreign key (supplier_id)
    	references supplier(supplier_id)
);

--可以创建一个具有多个字段的外键(带级联删除)，如下所示：
create table supplier(
	supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    contact_name vatchar2(50),
    constraint supplier_pk primary key (supplier_id, supplier_name)
);
create table products(
	product_id numeric(10) not null,
    supplier_id numeric(10) not null,
    supplier_name varcahr2(50) not null,
    constraint fk_supplier_comp
    	foreign key (supplier_id, supplier_name)
    	references supplier(supplier_id, supplier_name)
    on delete cascade
);

--使用alter table语句定义级联删除
alter talbe table_name
add sontraint constraint_name
	foreign key (column1, column2, .. column_n)
	references parent_table (column1, column2,..column_n)
	on delete cascade;
--示例
alter table products
add constraint fk_supplier
	foreign key (supplier_id)
	references supplier(supplier_id)
	on delete cascade;
```

#### 怎么删除外键

```sql
--可以使用alter table语句来对外键进行删除
--语法
alter table "表名" drop constraint "主键名"
--或
alter table "表名" drop primary key

--示例
create table supplier(
	supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    contact_name varchar(50),
    constraint supplier_pk primary key (supplier_id)
);
create table products(
	product_id numeric(10) not null,
    supplier_id numeric(10) not null,
    constraint fk_supplier
    foreign key (supplier_id)
    references supplier(supplier_id)
);
```

#### 怎么禁用外键

```sql
--在Oracle中，禁用外键可以使用以下语法
alter table table_name
disable constraint constraint_name;

--示例
create table supplier(
	supplier_id numeric(10) not null,
    supplier_name varchar2(50) not null,
    contact_name varchar2(50),
    constraint supplier+pk primary key (supplier_id)
);
create table products(
	product_id numeric(10) not null,
    supplier_id numeric(10) not null,
    constraint fk_supplier
    	foreign key (supplier_id)
    	references supplier(supplier_id)
);

--如果想禁用这个外键，可以执行以下命令
alter table products
disable constraint fk_supplier;
```

#### 启用外键

```sql
--外键启用语法
alter table table_name
enable constraint constraint_name;

--示例
alter table products
enable constraint fk_supplier;
```

#### Ascii()函数

```sql
--Ascii()函数语法
ASCII(single_character)

--single_character：指定的字符来检索NUMBER代码。 如果输入多个字符，则ASCII函数将返回第一个字符的值，并忽略第一个字符后的所有字符。

--示例
ASCII('t')
Result: 116

ASCII('T')
Result: 84

ASCII('T2')
Result: 84
```

#### Asciistr()函数

```sql
--Asciistr()函数语法
ASCIISTR(string)
--string：任何字符集中的字符串，希望将其转换为数据库字符集中的ASCII字符串。

--示例
ASCIISTR('A B C Ä Ê')
Result: 'A B C 0C4 0CA'

ASCIISTR('A B C Õ Ø')
Result: 'A B C 0D5 0D8'

ASCIISTR('A B C Ä Ê Í Õ Ø')
Result: 'A B C 0C4 0CA 0CD 0D5 0D
```

#### Chr()函数

```sql
--Chr()函数语法
CHR( number_code )
--number_code：用于检索对应字符的NUMBER代码。

--示例
CHR(116)
Result: 't'

CHR(84)
Result: 'T'
```

#### Compose()函数

```sql
--Compose()函数语法
COMPOSE( string )
--string：用于创建Unicode字符串的输入值。 它可以是char，varchar2，nchar，nvarchar2，clob或nclob。

--示例
COMPOSE('o' || unistr('\0308') )
Result: ö

COMPOSE('a' || unistr('\0302') )
Result: â

COMPOSE('e' || unistr('\0301') )
Result: é
```

| Unistring值       | 结果字符    |
| ----------------- | ----------- |
| `unistr('\0300')` | 重音符(`)   |
| `unistr('\0301')` | 锐音符(‘)   |
| `unistr('\0302')` | (`^`)       |
| `unistr('\0303')` | `~`         |
| `unistr('\0308')` | 变音符(`¨`) |

#### Concat()函数

```sql
--CONCAT()函数语法
CONCAT( string1, string2 )

--string1：第一个要连接的字符串。
--string2：第二个要连接的字符串。

--示例
CONCAT('Oraok', '.com')
-- Result: 'Oraok.com'

CONCAT('a', 'b')
-- Result: 'ab'

--在Oracle中，CONCAT函数将只允许您将两个值连接在一起。如果需要连接多个值，那么可以嵌套多个CONCAT函数调用。
SELECT CONCAT(CONCAT('A', 'B'),'C')
FROM dual;
-- Result: 'ABC'

SELECT CONCAT(CONCAT(CONCAT('A', 'B'),'C'),'D')
FROM dual;
- Result: 'ABCD'

--连接单引号
SELECT CONCAT('Let''s', ' learn Oracle')
FROM dual;
-- Result: Let's learn Oracle
```

#### || 连接运算符

```sql
--|| 运算符语法
string1 || string2 [ || string_n ]
--string1： 第一个要连接的字符串。
--string2：第二个要连接的字符串。
--string_n：可选项，第 n 个要连接的字符串

--示例
'oraok' || '.com'

'a' || 'b' || 'c' || 'd'
--结果为：
'oraok.com'

'abcd'

--案例：
select '姓名：' || c.stuname || ', 课程：' || b.coursename || ', 成绩：' || a.score || '分数' as sxcj
from
 	score a, course b, stuinfo c
where 
 	a.courseid = b.courseid
   and 
   a.stuid = c.stuid
   
 --连接空格字符
SELECT 'Dave' || ' ' || 'Anderson'
FROM dual;
-- Result: 'Dave Anderson'
```

#### Convert()函数

```sql
--在 Oracle 中，Convert() 函数可以将字符串从一个字符集转换为另一个字符集 
--Convert() 函数语法
CONVERT( string1, char_set_to [, char_set_from] )

--string1：要转换的字符串。
--char_set_to：要转换为的字符集。
--char_set_from：可选的，要从中转换的字符集。

--示例
SELECT CONVERT('Ä Ê Í Õ Ø A B C D E ', 'US7ASCII', 'WE8ISO8859P1') 
   FROM DUAL; 

CONVERT('ÄÊÍÕØABCDE' 
--------------------- 
A E I ? ? A B C D E ? 
```

## 返回值

CONVERT 函数返回特定字符集中的字符串值。 可用的字符集是：

| 字符集       | 描述                          |
| ------------ | ----------------------------- |
| US7ASCII     | 美国 7 位 ASCII 字符集        |
| WE8DEC       | 西欧 8 位字符集               |
| WE8HP        | 惠普西欧 Laserjet 8 位字符集  |
| F7DEC        | DEC 法语 7 位字符集           |
| WE8EBCDIC500 | IBM 西欧 EBCDIC 代码第 500 页 |
| WE8PC850     | IBM PC 代码第 850 页          |
| WE8ISO8859P1 | ISO 8859-1 西欧 8 位字符      |

#### Dump()函数

```sql
--Dump()函数语法
DUMP( expression [, return_format] [, start_position] [, length] )

--expression：要分析的表达式。

--return_format：决定了返回值的格式，该参数可以是以下任何值：

     ● 8 ：八进制符号

     ● 10 ：十进制符号

     ● 16 ：十六进制符号

     ● 17 ：单个字符

     ● 1008 ：带字符集名称的八进制符号

     ● 1010 ：带字符集名称的十进制符号

     ● 1016 ：带字符集名称的十六进制符号

     ● 1017 ：带字符集名称的单个字符

--start_position ：可选的，要返回的内部表示的起始位置。
--length ：可选的，要返回的内部表示的长度。

--示例
DUMP('Tech')
-- Result: 'Typ=96 Len=4: 84,101,99,104'

DUMP('Tech', 10)
-- Result: 'Typ=96 Len=4: 84,101,99,104'

DUMP('Tech', 16)
-- Result: 'Typ=96 Len=4: 54,65,63,68'

DUMP('Tech', 1016)
-- Result: 'Typ=96 Len=4 CharacterSet=US7ASCII: 54,65,63,68'

DUMP('Tech', 1017)
-- Result: 'Typ=96 Len=4 CharacterSet=US7ASCII: T,e,c,h'
```

#### Initcap()函数

```sql
--Initcap()函数语法
INITCAP( string1 )

--string1 ：字符串参数，其中每个单词中的第一个字符将转换为大写字母，其余所有字符转换为小写字母。

--示例
INITCAP('tech on the oraok');
-- Result: 'Tech On The Oraok'

INITCAP('GEORGE BURNS');
-- Result: 'George Burns'
```

#### 运算符

```sql
--Oracle 算术运算符包括+、-、*、/四个，其中/获得的结果是浮点数。
--案例1、求2018年上学期数学的平均成绩。
select a.*, b.coursename, c.stuname
  from score a, course b, stuinfo c
 where a.courseid = b.courseid
   and a.stuid = c.stuid;
 
select b.coursename, sum(a.score) / count(1)
  from score a, course b
 where a.courseid = b.courseid
   and a.courseid = 'R20180101'
 group by b.coursename;
```

## Oracle关系运算符

Oracle 关系运算符在 `where` 条件语句当中经常使用到，常用的关系如下：

| 符号 | 解释 | 符号     | 解释         |
| ---- | ---- | -------- | ------------ |
| =    | 等于 | <>或者!= | 不等于       |
| >    | 大于 | >=       | 大于或者等于 |
| <    | 小于 | <=       | 小于或者等于 |

## Oracle逻辑运算符

Oracle 的逻辑运算符有三个：`AND`、`OR`、`NOT`。

案例2、查看2018年上学期数学成绩在85-95分之间的同学：

```sql
select a.*,b.coursename,c.stuname
    from score a,course b,stuinfo c
where a.courseid=b.courseid
    and a.stuid=c.stuid and a.score>='85'and a.score<='95'
```

```java
public class Demo{
    public static void main(String[] args){
        int i, j;
        int count = 0;
        for (i = 0; i < 100; i++){
            for (j = i; j < i; j ++){
                if (i % 2 == 0 && j % 4 == 0){
                   System.out,println(i + "i" + j + 'j');
                    count++;
                }
            }
        }
        System.out.println("count和为：" + count);
    }
}
```

```python
def sum(a, b):
    return a + b
def div(a, b):
    return a ? b
def cal(a ,b):
    return a % b
def add(a, b):
    a += b
```
