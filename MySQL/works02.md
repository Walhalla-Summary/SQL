2021年12月23日



## Oracle 详解

### 1、Oracle简介

 Oracle 是甲骨文公司开发的一款[关系型数据库](https://baike.baidu.com/item/关系型数据库/8999831?fr=aladdin)，它一款系统可移植性好、使用简单、功能强大的关系型数据库。它为各行业在各类环境下（服务器、虚拟机、微机环境下）可以快速搭建一种高效率、可靠性好、高吞吐量的数据库解决方案。 

### 2、Oracle版本

Oracle从1979开始发布Oracle2.0开始到现在Oracle12c，从开始的只是数据存储和查询到后来的分布式、RAC、网络计算、到现在的对云计算的支持，当中经历了很多变迁和计算的提升。

Oracle数据库分为个人版本、标准版1、标准版、企业版，区别：

标准版1（Standard Edition one）适用于1-2cpu的服务器，单机环境，适用于中小型用户入门级应用。

标准版（Standard    Edition）适用于1-4cpu的服务器，可以做双机热备和RAC，价格适中，适用于对数据库性能要求及安全性有进一步要求的大中型用户工作。

企业版（Enterprise    Edition） 适用于单机、双机、多CPU多节点集群等各种环境，功能齐全，适用于对数据库性能及可靠性有高要求的企业级用户应用。

个人版，只在windows平台上提供，不支持RAC之外的包含企业版所有功能。

### 3、Oracle平台支持

 2001年发布的Oracle9i之前，甲骨文公司把他们的数据库产品广泛的移植到了不同的平台上。截止甲骨文公司的Oracle10g/11g/12c都支持windows、Linux各大版本，包括X-86/64位系统。 

### 4、Oracle特点

[Oracle数据库](https://baike.baidu.com/item/Oracle数据库/3710800?fr=aladdin)具有完整的数据库管理功能、完备关系的产品以及具有分布式处理能力的数据库。

它对数据的可靠性、大量性、持久性、共享性提供了一套可靠的解决方案、而且可以轻松支持多用户、大事务量的事务处理。

它的优点就是可用性强、可扩展性强、数据安全性强、稳定性高，以及现阶段12C支持分布式数据处理。

它提供了一套严禁的逻辑结构、文件结构、相关恢复技术的解释和实现。

### 5、Oracle体系结构

Oracle数据库实际上是一个数据的物理储存系统，这其中包括数据文件（ora/dbf）、参数文件、控制文件、联机日志等。

**实例：**一个操作系统只有一个Oracle数据库，但是可以安装多个Oracle实例，一个Oracle实例对应着一系列的后台进程（Backguound Processes)和内存结构（Memory Structures)。

**数据文件：**Oracle数据文件是数据存储的物理单位，数据库的数据是存储在表空间中的。而一个表空间可以由一个或多个数据文件组成，一个数据文件只能属于一个表空间，一旦数据文件被加入到某个表空间后，就不能删除这个文件，如果要删除某个数据文件，只能删除其所属于的表空间才 行。

**表空间：**表空间是Oracle 对物理数据库数据文件（ora/dbf）的逻 辑映射。一个数据库在逻辑上被划分成一到若干个表空间，每个表空间由同一磁盘上的一个或多个数据文件（datafile）组成，一个数据文件只能属于一个表空间。

**oracle用户：**表当中的数据是有Oracle用户放入到表空间当中的，而这些表空间会随机的把数据放入到一个或者多个数据文件当中。oracle对表数据的管理是通过用户对表的管理去查询，而不是直接对数据文件或表空间进行查询。因为不同用户可以在同一个表空间上面建立相同的表名。但是通过不同的用户管理自己的表数据。

 **数据结构逻辑关系如下图：** 

  ![1640227498647](Images/1640227498647.png)

 **Oracle体系概要图如下：** 

![1640227538250](Images/1640227538250.png)

### 6、Oracle服务

1、OracleService+服务名（ORCL）:

该服务是Oracle数据库的基础，只有启动该服务才能正常使用Oracle数据库。

2、OracleOraDb11g_home1TNSlistener ：

该服务为Oracle客户端提供监听程序的服务，只有启动该服务，本地的客户端程序才能通过监听连接到数据库，和数据库进行交互。

3、Oracle ORCL VSS Writer Service：

Oracle卷映射拷贝写入服务，VSS(Volume Shadow Copy Service)能够让存储基础设备(比如磁盘，阵列等)创建高保真的时间点映像，即映射拷贝(shadow copy)。它可以在多卷或者单个卷上创建映射拷贝，同时不会影响到系统的性能。(非必须启动)

4、OracleMTSRecoveryService：

服务端控制。该服务允许数据库充当一个微软事务服务器MTS、COM/COM+对象和分布式环境下的事务的资源管理器。(非必须启动)

5、 OracleOraDb11g_home1ClrAgent：

Oracle数据库 .NET扩展服务的一部分。 (非必须启动)

6、 OracleJobSchedulerORCL：

Oracle作业调度(定时器)服务，ORCL是Oracle实例标识。(非必须启动)

```scala
提示：

在使用第三方客户端连接Oracle数据库时，OracleOraDb11g_home1TNSlistener 服务必须启动，才能连接到远程数据库！
```

### 7、数据库启动与关闭

 OracleService服务启动后，即可以操作数据库了，默认情况下Oracle数据库是启动状态，可以通过客户端SQLPLUS使用sys用户进行登录，通过命令行关闭Oracle数据库，命令如下： 

```sql
shutdown immediate
```

 重新启动Oracle数据库和实例，命令如下： 

```sql
startup open
```

### 8、Oracle用户

oracle用户的概念对于Oracle数据库至关重要，在现实环境当中一个服务器一般只会安装一个Oracle实例，一个Oracle用户代表着一个用户群，他们通过该用户登录数据库，进行数据库对象的创建、查询等开发。

每一个用户对应着该用户下的N多对象，因此，在实际项目开发过程中，不同的项目组使用不同的Oracle用户进行开发，不相互干扰。也可以理解为一个Oracle用户既是一个业务模块，这些用户群构成一个完整的业务系统，不同模块间的关联可以通过Oracle用户的权限来控制，来获取其它业务模块的数据和操作其它业务模块的某些对象。

#### Oracle用户创建

```sql
--Create the user
Create user student --用户名
	indentified by "123456" --用户密码
	default tablespace USERS --表空间名
	temporary tableSpace temp --临时表空间名
	profile DEFAULT --数据文件（默认数据文件）
	account unlock; --账户是否解锁（lock;锁定、unlock解锁）
```

 通过上面语句，可以创建一个student用户，但是该用户现在还不能登录数据库，因为它没有登录数据库权限，最少他需要一个create session系统权限才能登录数据库。 

#### 用户权限

Oracle数据库用户权限分为：系统权限和对象权限两种。

系统权限：比如：create session可以和数据库进行连接权限、create table、create view 等具有创建数据库对象权限。

对象权限：比如：对表中数据进行增删改查操作，拥有数据库对象权限的用户可以对所拥有的对象进行相应的操作。

#### 数据库角色

oracle数据库角色是若干系统权限的集合，给Oracle用户进行授数据库角色，就是等于赋予该用户若干数据库系统权限。常用的数据库角色如下：

CONNECT角色：connect角色是Oracle用户的基本角色，connect权限代表着用户可以和Oracle服务器进行连接，建立session（会 话）。

RESOURCE角色：resouce角色是开发过程中常用的角色。 RESOURCE给用户提供了可以创建自己的对象，包括：表、视图、序列、过程、触发器、索引、包、类型等。

DBA角色：DBA角色是管理数据库管理员该有的角色。它拥护系统了所有权限，和给其他用户授权的权限。SYSTEM用户就具有DBA权限。

因此，在实际开发过程当中可以根据需求，把某个角色或系统权限赋予某个用户。授权语句如下：

```sql
提示：

系统权限只能通过DBA用户授权，对象权限有拥有该对象权限的对象授权（不一定是本身对象）！用户不能自己给自己授权！
```

语法：授权

```sql
--GRANT 对象权限 on 对 TO 用户
grant select, insert, update on JSQUSER to STUDENT;

--GRANT 系统权限 to 用户
grant select any table to STUDENT;

--GRANT 角色 TO 用户
grant connect to STUDENT; --授权connect角色
grant resource to STUDENT; --授予resource角色
```

语法：取消用户权限

```sql
--Revoke 对象权限 on 对象 from 用户
remoke select, insert, update, delete on JSUSER from STUDENT;

--Revoke 系统权限 from 用户
revoke select ant table from Student;

--Revoke 角色(role) from 用户
revoke resource from STUDENT;
```

语法：Oracle用户的其他操作

```sql
--修改用户信息
alter user STUDENT;
	identified by ****** -- 修改密码
	account lock; -- 修改用户处于锁定状态或者解锁状态(LOCK|UNLOCK)
```

### SQL语句介绍

SQL语句可以对Oracle进行对象创建、删除，数据的插入、删除、更新，以及[数据库的管理](http://www.oraclejsq.com/article/010100133.html)等操作，SQL是一个结构化的的查询语言（Structured Query Language ），不仅仅适用于ORACLE数据库，再其它的数据也适用。

在 Oracle 开发中，客户端把 SQL 语句发送给服务器，服务器对 SQL 语句进行编译、执行，把执行的结果返回给客户端。常用的SQL语句大致可以分为五类：

数据定义语言（DDL），包括 CREATE（创建）命令、 ALTER（修改）命令、 DROP（删除）命令等。

数据操纵语言（DML），包括 INSERT（插入）命令、 UPDATE（更新）命令、 DELETE（删除）命令、 SELECT … FOR UPDATE（查询）等。

数据查询语言（DQL），包括基本查询语句、 Order By 子句、 Group By 子句等。

事务控制语言（TCL），包括 COMMIT（提交）命令、 SAVEPOINT（保存点）命令、ROLLBACK（回滚）命令。   

数据控制语言（DCL）， GRANT（授权）命令、 REVOKE（撤销）命令。

#### 案例所需表结构

![1640229252600](Images/1640229252600.png)

 表结构执行脚本： 

```sql
-- Create table 创建表
create table STUINFO
(
  stuid      VARCHAR2(11) not null,
  stuname    VARCHAR2(50) not null,
  sex        CHAR(1) not null,
  age        NUMBER(2) not null,
  classno    VARCHAR2(7) not null,
  stuaddress VARCHAR2(100) default '地址未录入',
  grade      CHAR(4) not null,
  enroldate  DATE,
  idnumber   VARCHAR2(18) default '身份证未采集' not null
)
tablespace USERS
  pctfree 10
  initrans 1
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
-- Add comments to the table 
comment on table STUINFO
  is '学生信息表';
-- Add comments to the columns 
comment on column STUINFO.stuid
  is '学号';
comment on column STUINFO.stuname
  is '学生姓名';
comment on column STUINFO.sex
  is '学生性别';
comment on column STUINFO.age
  is '学生年龄';
comment on column STUINFO.classno
  is '学生班级号';
comment on column STUINFO.stuaddress
  is '学生住址';
comment on column STUINFO.grade
  is '年级';
comment on column STUINFO.enroldate
  is '入学时间';
comment on column STUINFO.idnumber
  is '身份证号';
-- Create/Recreate primary, unique and foreign key constraints 
alter table STUINFO
  add constraint PK_STUINFO primary key (STUID)
  using index 
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
  
  -- Create table
create table CLASS
(
  classno        VARCHAR2(7) not null,
  classname      VARCHAR2(50),
  monitorid      VARCHAR2(11),
  monitorname    VARCHAR2(50),
  headmasterid   VARCHAR2(8),
  headmastername VARCHAR2(50),
  classaddress   VARCHAR2(50),
  enterdate      DATE
)
tablespace USERS
  pctfree 10
  initrans 1
  maxtrans 255
  storage
  (
    initial 64K
    minextents 1
    maxextents unlimited
  );
-- Add comments to the table 
comment on table CLASS
  is '班级信息表';
-- Add comments to the columns 
comment on column CLASS.classno
  is '班级号';
comment on column CLASS.classname
  is '班级名称';
comment on column CLASS.monitorid
  is '班长学号';
comment on column CLASS.monitorname
  is '班长姓名';
comment on column CLASS.headmasterid
  is '班主任教师号';
comment on column CLASS.headmastername
  is '班主任姓名';
comment on column CLASS.classaddress
  is '班级地址';
comment on column CLASS.enterdate
  is '录入时间';
-- Create/Recreate primary, unique and foreign key constraints 
alter table CLASS
  add constraint PK_CLASS primary key (CLASSNO)
  using index 
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255;


-- Create table
create table COURSE
(
  courseid   VARCHAR2(9) not null,
  schyear    VARCHAR2(4),
  term       VARCHAR2(4),
  coursename VARCHAR2(100)
)
tablespace USERS
  pctfree 10
  initrans 1
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
-- Add comments to the table 
comment on table COURSE
  is '课程表';
-- Add comments to the columns 
comment on column COURSE.courseid
  is '课程id';
comment on column COURSE.schyear
  is '学年';
comment on column COURSE.term
  is '学期';
comment on column COURSE.coursename
  is '课程名称';
-- Create/Recreate primary, unique and foreign key constraints 
alter table COURSE
  add constraint PK_COURSE primary key (COURSEID)
  using index 
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
  
  -- Create table
create table STUCOURSE
(
  selectid   VARCHAR2(18) not null,
  stuid      VARCHAR2(11),
  courseid   VARCHAR2(9),
  schyear    VARCHAR2(4),
  term       VARCHAR2(4),
  redo       VARCHAR2(1),
  selectdate DATE
)
tablespace USERS
  pctfree 10
  initrans 1
  maxtrans 255
  storage
  (
    initial 64K
    minextents 1
    maxextents unlimited
  );
-- Add comments to the table 
comment on table STUCOURSE
  is '学生选课表';
-- Add comments to the columns 
comment on column STUCOURSE.selectid
  is '选课id';
comment on column STUCOURSE.stuid
  is '学号';
comment on column STUCOURSE.courseid
  is '课程id';
comment on column STUCOURSE.schyear
  is '年度';
comment on column STUCOURSE.term
  is '学期';
comment on column STUCOURSE.redo
  is '是否重修';
comment on column STUCOURSE.selectdate
  is '选课时间';
-- Create/Recreate primary, unique and foreign key constraints 
alter table STUCOURSE
  add constraint PK_STUCOURSE primary key (SELECTID)
  using index 
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255;


-- Create table
create table SCORE
(
  scoreid  VARCHAR2(18) not null,
  stuid    VARCHAR2(11),
  courseid VARCHAR2(9),
  score    NUMBER,
  scdate   DATE
)
tablespace USERS
  pctfree 10
  initrans 1
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
-- Add comments to the table 
comment on table SCORE
  is '学生成绩表';
-- Add comments to the columns 
comment on column SCORE.scoreid
  is '学生成绩id';
comment on column SCORE.stuid
  is '学生学号';
comment on column SCORE.courseid
  is '课程id(年度+上下学期+课程序列)';
comment on column SCORE.score
  is '成绩';
comment on column SCORE.scdate
  is '成绩录入时间';
-- Create/Recreate primary, unique and foreign key constraints 
alter table SCORE
  add constraint PK_SCORE primary key (SCOREID)
  using index 
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
```

#### Oracle建表（Create table）

 Oracle表是Oracle数据库的核心，是存储数据的逻辑基础。Oracle表是一个二维的数据结构，有列字段和对应列的数据构成一个数据存储的结构。可以简单看成行和列的二维表，列代表着Oracle字段（column），行代表着一行数据（即一条数据记录）。 

#### Oracle字段数据类型

|     数据类型     |                           类型解释                           |
| :--------------: | :----------------------------------------------------------: |
| VARCHAR2(length) | 字符串类型：存储可变的长度的字符串，length:是字符串的最大长度，默认不填的时候是1，最大长度不超过4000。 |
|   CHAR(length)   | 字符串类型：存储固定长度的字符串，length:字符串的固定长度大小，默认是1，最大长度不超过2000。 |
|   NUMBER(a,b)    | 数值类型：存储数值类型，可以存整数，也可以存浮点型。a代表数值的最大位数：包含小数位和小数点，b代表小数的位数。例子：number(6,2)，输入123.12345，实际存入：123.12 。 |
|       DATA       | 时间类型：存储的是日期和时间，包括年、月、日、时、分、秒。例子：内置函数sysdate获取的就是DATA类型 |
|    TIMESTAMP     | 时间类型：存储的不仅是日期和时间，还包含了时区。例子：内置函数systimestamp获取的就是timestamp类型 |
|       CLOB       | 大字段类型：存储的是大的文本，比如：非结构化的txt文本，字段大于4000长度的字符串。 |
|       BLOB       | 二进制类型：存储的是二进制对象，比如图片、视频、声音等转换过来的二进制对象 |

#### **create table语句**

 Oracle数据库建表是通过create table命令来执行的。

 **案例1：创建stuinfo（学生信息表）** 

```sql
-- Create table
create table STUDENT.stuinfo
(
  stuid      varchar2(11) not null,--学号：'S'+班号（7位数）+学生序号（3位数）(1)
  stuname    varchar2(50) not null,--学生姓名
  sex        char(1) not null,--性别
  age        number(2) not null,--年龄
  classno    varchar2(7) not null,--班号：'C'+年级（4位数）+班级序号（2位数）
  stuaddress varchar2(100) default '地址未录入',--地址 (2)
  grade      char(4) not null,--年级
  enroldate  date,--入学时间
  idnumber   varchar2(18) default '身份证未采集' not null--身份证
)
tablespace USERS --(3)
  storage
  (
    initial 64K
    minextents 1
    maxextents unlimited
  );
-- Add comments to the table 
comment on table STUDENT.stuinfo --(4)
  is '学生信息表';
-- Add comments to the columns 
comment on column STUDENT.stuinfo.stuid -- (5)
  is '学号';
comment on column STUDENT.stuinfo.stuname
  is '学生姓名';
comment on column STUDENT.stuinfo.sex
  is '学生性别';
comment on column STUDENT.stuinfo.age
  is '学生年龄';
comment on column STUDENT.stuinfo.classno
  is '学生班级号';
comment on column STUDENT.stuinfo.stuaddress
  is '学生住址';
comment on column STUDENT.stuinfo.grade
  is '年级';
comment on column STUDENT.stuinfo.enroldate
  is '入学时间';
comment on column STUDENT.stuinfo.idnumber
  is '身份证号';
```

代码解析：

（1）处： not null 表示学号字段（stuid）不能为空。

（2）处：default 表示字段stuaddress不填时候会默认填入‘地址未录入’值。

（3）处：表示表stuinfo存储的表空间是users，storage表示存储参数：区段(extent)一次扩展64k，最小区段数为1，最大的区段数不限制。

（4）处：comment on table 是给表名进行注释。

（5）处：comment on column 是给表字段进行注释。

 通过上面crate table命令创建了stuinfo学生信息表后，还可以给表添加相应的约束来保证表数据的准确性。

比如：学生的年龄不能存在大龄的岁数，可能是错误数据、性别不能填入不是1（男）、2（女）之外的数据等。 

 **案例2：stuinfo（学生信息表）添加约束** 

```sql
-- Create/Recreate primary, unique and foreign key constraints 
alter table STUDENT.STUINFO
  add constraint pk_stuinfo_stuid primary key (STUID);
  --把stuid当做主键，主键字段的数据必须是唯一性的（学号是唯一的）
  
-- Create/Recreate check constraints 
alter table STUDENT.STUINFO
  add constraint ch_stuinfo_age
  check (age>0 and age<=50);--给字段年龄age添加约束，学生的年龄只能0-50岁之内的
  
alter table STUDENT.STUINFO
  add constraint ch_stuinfo_sex
  check (sex='1' or sex='2');
  
alter table STUDENT.STUINFO
  add constraint ch_stuinfo_GRADE
  check (grade>='1900' and grade<='2999');
```

#### Oracle查询（select）

**简单查询是利用SELECT命令从表中进行提取数据，SELECT命令结构如下： **

select命令结构：

```sql
select *|列名|表达式 from 表名 where 条件 order by 列名
```

 案例1：查询学生信息表（stuinfo）中“李四”同学的基本信息： 

```sql
select t.* 
	from STUDENT.STUINFO t 
	where t.stuname = '李四';
```

 案例2：查询“李四”同学的学号、班级、年级和地址： 

```sql
select t.stuid,t.classno,t.stuaddress,t.grade 
	from STUDENT.STUINFO t 
	where t.stuname = '李四';
```

 案例3：查询班级“C201801”所有同学信息，按年龄进行升序展示： 

```sql
select t.*  
	from STUDENT.STUINFO t 
	where t.classno = 'C201801' 
	ORDER BY T.AGE ASC
```

语法解析：

1、“t”代表stuinfo的别名。

2、 "*" 代表所有字段。

3、表达式可以是函数（列名）、常数、连接词“||”等组成的表达式。

4、where子语句是查询语句的条件。

5、order by :查询结果按某个字段进行排序，默认是升序，desc是降序。

#### 备份查询数据

 Oracle进行表数据备份时，可以利用create table（建表）的方式对select查询的结果进行快速备份。 

 备份查询数据命令结构： 

```sql
create table 表名 as select 语句
```

 案例 4：备份学生信息表（stuinfo）的数据： 

```sql
create table student.stuinfo_2018 as select * 
	from student.stuinfo ;

select * from student.stuinfo_2018;
```

#### Oracle插入（insert into）

 Oracle对表数据的插入是使用insert命令来执行的。 

 insert 命令结构： 

```sql
insert into 表名（列名1,列名2,列名3.....）values(值1,值2,值3.....);
```

语法解析：

1、列名可以省略，当列名不填时，默认的是表中的所有列，列的顺序是按照建表的顺序进行排列的。

2、列名的数量和值的数量要一致，并且值的类型要和列的类型一一对应。

3、当表当中某些字段设置了某些约束的情况下，必须按照字段的约束来进行该值的插入，例如：学生信息表（STUINFO）当中设置有主键（主键字段是STUID）,因此该字段必须具有唯一性，不能和原有的数据重复。age、stuname、calassno等字段是必填字段，因此是必须有值的。

 案例1：向学生信息表（stuinfo）插入一条数据： 

```sql
insert into STUDENT.STUINFO (STUID, STUNAME, SEX, AGE, CLASSNO, STUADDRESS, GRADE, ENROLDATE, IDNUMBER)
values ('SC201801005', '龙七', '1', 26, 'C201801', '福建省厦门市XXX号', '2018',to_date('01-09-2018', 'dd-mm-yyyy'),'3503021992XXXXXXXX');

select * 
	from student.stuinfo t 
	where t.stuid='SC201801005';
```

 案例2：向学生信息表（stuinfo）插入重复数据： 

```sql
insert into STUDENT.STUINFO (STUID, STUNAME, SEX, AGE, CLASSNO, STUADDRESS, GRADE, ENROLDATE, IDNUMBER)
values ('SC201801005', '龙七', '1', 26, 'C201801', '福建省厦门市XXX号', '2018',to_date('01-09-2018', 'dd-mm-yyyy'),'3503021992XXXXXXXX');
```

#### insert插入一个select的结果集

 在 Oracle 中，一个 INSERT 命令可以把一个select结果集一次性插入到一张表中。 

 语法结构如下： 

```sql
INSERT INTO 表 SELECT 子句，
```

 案例3：备份的表stuinfo_2018的数据一次插入表stuinfo当中： 

```sql
delete  from 
	student.stuinfo t 
	where t.stuid in (
        	select b.stuid 
        	from student.stuinfo_2018 b 
    );

insert into 
	student.stuinfo 
	select * 
		from 
		student.stuinfo_2018;

select * from student.stuinfo;
```

 数据操纵语言（DML）包括 INSERT（插入）命令、 UPDATE（更新）命令、 DELETE（删除）命令、 SELECT … FOR UPDATE（查询）等。只有提交（commit）后才能持久化到数据库。 

#### Oracle更新（update）

 Oracle对表数据的更新是使用update命令来执行的。 

 update命令结构： 

```sql
update 表名 set 列名1=值1,列名2=值2,列名3=值3..... where 条件
```

 案例1、更新学生“张三”的年龄和身份证信息： 

```sql
update student.stuinfo t
   set t.age = '24', t.idnumber = '3503021994XXXXXXXX'
 where t.stuname = '张三';
commit;
select * from student.stuinfo t where t.stuname='张三';
```

 update 利用另外一张表关联更新本表数据的命令结构如下： 

```sql
update 表1 set 列名=（select 列名 from 表2 where 表1.列名=表2.列名） 
       where exists (select 1 from 表2 where 表1.列名=表2.列名)
```

 案例2、利用备份表stuinfo_2018更新回学生“张三”的年龄和身份证： 

```sql
update student.stuinfo t
   set (age, idnumber) =
       (select age, idnumber from student.stuinfo_2018 b where b.stuid = t.stuid)
 where exists (select 1
          from student.stuinfo_2018 b
         where b.stuid = t.stuid
           and b.stuname = '张三');
           
select *from student.stuinfo t where t.stuname='张三';
```

#### Oracle删除（delete）

 Oracle中对表数据的删除是利用delete命令进行的。 

 delete命令结构： 

```sql
delete from 表名 where 条件
```

命令解析：

1、当delete from不加where条件时，表示是把表中的数据全部删除。

 案例1、删除学生信息表（stuinfo）中学生“张三”的数据： 

```sql
delete  from stuinfo t where t.stuname='张三';
```

#### truncate命令

 truncate命令也是数据删除命令，他是直接把Oracle表数据一次删除的命令，truncate命令是一个DDL命令，不同于delete是DML命令。 

 truncate命令结构： 

```sql
truncate table 表名；truncate table 表名;
```

 案例2、删除学生信息备份表（stuinfo_2018）: 

```sql
truncate table stuinfo_2018;
```

 truncate和delete都能删除表中的数据，区别： 

1、TRUNCATE 是 DDL 命令，命令执行完就提交，删除的数据不能恢复； DELETE 命令是 DML 命令，命令执行完需提交后才能生效，删除后的数据可以通过日志文件恢复。

2、如果表中的数据量较大，TRUNCATE的速度比DELETE速度快很多。

3、truncate删除将重新设置表索引的初始大小，而delete不能。

4、delete能够触发表上相关的delete触发器，而truncate则不会触发。

5、delete删除的原理是一次一条从表中删除数据，并将删除操作当做事物记录在数据库的日志当中，以便进行数据回滚。而truncate是一次性进行数据页的删除，因此执行速度快，但是不能回滚。

总结：truncate命令是属于DDL命令，一次性删除表中所有数据，并且数据不能恢复，在实际开发过程当中truncate命令慎用。

#### Oracle运算符

 Oracle运算符包括算术运算符、关系运算符和逻辑运算符。 

 **案例展示所需表结构如下 :**

![1640234090604](Images/1640234090604.png)

#### Oracle算术运算符

 Oracle算术运算符包括+、-、*、/四个，其中/获得的结果是浮点数。 

 案例1、求2018年上学期数学的平均成绩。 

```sql
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

#### Oracle关系运算符

 Oracle关系运算符在where条件语句当中经常使用到，常用的关系如下： 

| 符号 | 解释 |   符号   |     解释     |
| :--: | :--: | :------: | :----------: |
|  =   | 等于 | <>或者!= |    不等于    |
|  >   | 大于 |    >=    | 大于或者等于 |
|  <   | 小于 |    <=    | 小于或者等于 |

#### Oracle逻辑运算符

 Oracle的逻辑运算符有三个：AND、OR、NOT。 

 案例2、查看2018年上学期数学成绩在85-95分之间的同学： 

```sql
select a.*, b.coursename, c.stuname
  from score a, course b, stuinfo c
 where a.courseid = b.courseid
   and a.stuid = c.stuid
   and a.score >= '85'
   and a.score <= '95'
```

#### Oracle字符串连接符||

 Oracle中利用字符串连接符||（即双竖线）来连接查询结果。 

 案例1、字符串连接符||： 

```sql
select 
'姓名：' || c.stuname || ', 课程：' || b.coursename || ', 成绩：' || a.score || '分。' as sxcj
  from score a, course b, stuinfo c
 where a.courseid = b.courseid
   and a.stuid = c.stuid
```

#### Oracle DISTINCT

 Oracle DISTINCT关键字的作用可以对Oracle查询结果进行重复数据的消除。具体的做法参考案例： 

 DISTINCT语法结构: 

```sql
SELECT DISTINCT 列1,列2,列3... from 表名;
```

语法解析：

1、当关键字DISTINCT后面只有一个列1时，表示的是单个字段查询结果的不重复数据，当后面跟着多个列值时，表示的是多个字段组成的查询结果的所有唯一值，进行的是多个字段的分组消除。

 案例1、查询学生成绩表中课程“数学(2018上学期)”的所有出现的成绩，不重复： 

```sql
select distinct b.coursename, t.score
  from score t, course b
 where t.courseid = b.courseid
   and t.courseid = 'R20180101';
```

#### Oracle 条件查询

 Oracle条件查询时经常使用=、IN、LIKE、BETWEEN...AND来作为条件查询的操作符。在Oracle select 查询中where条件经常使用到这几个操作符。下列案例所需表结构参考： 

#### =操作符

在条件查询语句中“=”表示列值等于一个固定值所查询出的结果。

 案例1、查询学生成绩表“score”中课程id为“R20180101”，成绩为“85”分的同学信息。 

```sql
select t.stuid,
       t.courseid,
       t.score,
       b.stuname,
       b.sex,
       b.age,
       b.classno,
       b.grade
  from score t, stuinfo b
 where t.stuid = b.stuid
   and t.courseid = 'R20180101'
   and t.score = '85'
```

#### IN操作符

在 Where 子句中可以使用 IN 操作符来查询其列值在指定的列表中的查询结果。

 案例2、查询学生成绩表“score”中课程id为“R20180101”，成绩为“79”、“85”、“89”分的同学信息。 

```sql
--利用逻辑运算符or 和条件"=" 查询
select t.stuid,
       t.courseid,
       t.score,
       b.stuname,
       b.sex,
       b.age,
       b.classno,
       b.grade
  from score t, stuinfo b
 where t.stuid = b.stuid
   and t.courseid = 'R20180101'
   and (t.score = '85' or t.score ='89' or t.score ='79');
-- 利用Oracle操作符”IN“查询  
select t.stuid,
       t.courseid,
       t.score,
       b.stuname,
       b.sex,
       b.age,
       b.classno,
       b.grade
  from score t, stuinfo b
 where t.stuid = b.stuid
   and t.courseid = 'R20180101'
   and t.score in ('85','89','79');
```

#### BETWEEN...AND

在 WHERE 子句中，可以使用 BETWEEN...AND 操作符来查询列值包含在指定区间内的查询结果 。

案例3、查询学生成绩表“score”中课程id为“R20180101”，成绩在70-95之间的学生信息。

```sql
select t.stuid,
       t.courseid,
       t.score,
       b.stuname,
       b.sex,
       b.age,
       b.classno,
       b.grade
  from score t, stuinfo b
 where t.stuid = b.stuid
   and t.courseid = 'R20180101'
   and  t.score between '70' and '95'
```

#### LIKE模糊查询

在Oracle条件查询where条件之中，当遇到查询值不清楚时，可以利用模糊查询LIKE关键字进行where条件的模糊查询。LIKE 关键字通过字符匹配检索出所需要的数据行。字符匹配操作可以使用通配符“%”和“_” :

1、%：表示零个或者多个任意字符。

2、_：代表一个任意字符。

3、\：指转义字符，“\%”在字符串中表示一个字符“%”。

 案例4、查询学生基本信息表“STUINFO”中姓“张”的学生基本信息： 

```sql
select * from STUINFO t where t.stuname like '张%';
```

案例5、查询学生基本信息表“STUINFO”中姓“张”的，并且姓名长度是两个字的学生基本信息：

```sql
select * from STUINFO t where t.stuname like '张_';
```

#### Oracle集合运算

Oracle集合运算就是把多个查询结果组合成一个查询结果，oralce的集合运算包括：INTERSECT(交集)、UINION ALL(交集重复)、UINION(交集不重复)、MINUS(补集)。

1、INTERSECT(交集)，返回两个查询共有的记录。

2、UNION ALL(并集重复)，返回各个查询的所有记录，包括重复记录。

3、UNION(并集不重复)，返回各个查询的所有记录，不包括重复记录 （重复的记录只取一条）。

4、MINUS(补集)，返回第一个查询检索出的记录减去第二个查询检索出的记录之后剩余的记录。 

当使用Oracle集合运算时，要注意每个独立查询的字段名的列名尽量一致（列名不同时，取第一个查询的列名）、列的数据类型、列的个数要一致，不然会报错。

 表数据如下： 

![1640234983219](Images/1640234983219.png)

INTERSECT(交集)：

```sql
select * from stuinfo 
intersect
select * from stuinfo_2018;
```

UNION ALL(并集重复)

```sql
select * from stuinfo 
union all
select * from stuinfo_2018;
```

UNION(并集不重复)

```sql
select * from stuinfo 
union 
select * from stuinfo_2018;
```

MINUS(补集)

```sql
select * from stuinfo 
minus
select * from stuinfo_2018;
```

#### Oracle连接查询

 Oracle连接查询，包含内关联(inner jion )和外关联(outer join)，其中外关联又分为左外关联（left outer join）、右外关联（right outer join）和全外关联（full outer join）其中外关联可以使用（+）来表示。 

#### 内连接

Oracle内连接：两张表通过某个字段进行内关联，查询结果是通过该字段按关系运算符匹配出的数据行。其中可以包括：

1、等值连接：在连接条件中使用等于号(=)运算符比较被连接列的列值，其查询结果中列出被连接表中的所有列。

2、不等连接：在连接条件使用除等于运算符以外的其它比较运算符比较被连接的列的列值，这些关系运算符包括>、>=、<=、!>、!<、<>。

案例1、查询学生信息表（stuinfo）的学生信息，关联查询该学生的班级信息（class）。

代码如下：

```sql
select a.stuid,
       a.stuname,
       a.classno,
       b.classno,
       b.classname,
       b.monitorid,
       b.monitorname,
       b.classaddress
  from stuinfo a, class b
 where a.classno = b.classno;
```

#### 外连接

外连接，返回到查询结果集合中的不仅包含符合连接条件的行，而且还包括左表(左外连接或左连接))、右表(右外连接或右连接)或两个边接表(全外连接)中的所有数据行。

1、left join(左联接)等价于（left outer join）返回包括左表中的所有记录和右表中联结字段相等的记录。

2、right join(右联接)等价于（right outer join）返回包括右表中的所有记录和左表中联结字段相等的记录。

3.、full join （全连接）等价于（full outer join）查询结果等于左外连接和右外连接的和。

下面案例利用学生信息表（stuinfo）和之前的备份表（stuinfo_2018）做案例解析：

stuinfo表数据：

![1640235149609](Images/1640235149609.png)

案例2、left join(左联接）

代码：

```sql
--左外连接（stuinfo表中数据都存在,stuinfo_2018不在stuinfo中存在的学生相关字段为null值）
select a.*, b.stuid, b.stuname
  from stuinfo a
  left join stuinfo_2018 b
    on a.stuid = b.stuid;
--左外连接（利用（+）在右边）另外一种写法
select a.*, b.stuid, b.stuname
  from stuinfo a,stuinfo_2018 b 
  where a.stuid=b.stuid(+);
```

![1640235200461](Images/1640235200461.png)

案例3、right join（右连接）

代码：

```sql
--右外连接（stuinfo_2018表中数据都存在,stuinfo不在stuinfo_2018存在的学生相关字段为null值）
select a.*, b.stuid, b.stuname
  from stuinfo a
  right join stuinfo_2018 b
    on a.stuid = b.stuid;
--右外连接（利用（+）在左边）另外一种写法
select a.*, b.stuid, b.stuname
  from stuinfo a,stuinfo_2018 b 
  where a.stuid(+)=b.stuid;
```

![1640235229566](Images/1640235229566.png)

案例4、full join（全外连接）

代码：

```sql
 --(全外连接（stuinfo、stuinfo_2018表中数据都存在,
 --stuinfo不在stuinfo_2018存在的学生相关字段为null值,
 --stuinfo_2018不在stuinfo存在的学生相关字段为null值）
select a.*, b.stuid, b.stuname
  from stuinfo a
  full join stuinfo_2018 b
    on a.stuid = b.stuid;
```

![1640235253989](Images/1640235253989.png)

#### **Oracle伪列**

Oracle的伪列是Oracle表在存储的过程中或查询的过程中，表会有一些附加列，称为伪列。伪列就像表中的字段一样，但是表中并不存储。伪列只能查询，不能增删改。Oracle的伪列有：rowid、rownum。

#### ORACLE ROWID

Oracle表中的每一行在数据文件中都有一个物理地址， ROWID 伪列返回的就是该行的物理地址。使用 ROWID 可以快速的定位表中的某一行。 ROWID 值可以唯一的标识表中的一行。通过Oracle select 查询出来的ROWID，返回的就是该行数据的物理地址。

ROWID代码：

```sql
select t.*,t.rowid from stuinfo t ;
select t.*,t.rowid from stuinfo t where t.rowid='AAAShjAAEAAAAEFAAD';
```

#### ORACLE ROWNUM

ORACLE ROWNUM表示的Oracle查询结果集的顺序，ROWNUM为每个查询结果集的行标识一个行号，第一行返回1，第二行返回2，依次顺序递增。

ROWNUM 与 ROWID 不同， ROWID 是插入记录时生成， ROWNUM 是查询数据时生成。ROWID 标识的是行的物理地址。 ROWNUM 标识的是查询结果中的行的次序。

ROWNUM代码：

```sql
select t.stuid,t.stuname,t.sex,t.classno,t.stuaddress ,rownum  from stuinfo t ;
```

 ROWNUM经常用来限制查询的结果返回的行数，求前几行或前几名的数据。 

案例1、返回学生信息表中（stuinfo）中学生年龄最低的前四位同学。

代码：

```sql
select * from (select t.stuid, t.stuname, t.sex, t.classno, t.stuaddress, t.age, rownum
  from stuinfo t
 order by t.age asc) where rownum <=4;
```

#### Oracle 函数

Oracle SQL语句中经常使用到Oracle自带的函数，这些函数丰富了SQL的语言功能，为Oracle SQL提供了更多的操作性。Oracle函数可以接受零个或者多个输入参数，并返回一个输出结果。 Oracle 数据库中主要使用两种类型的函数：

1、单行函数：对每一个函数应用在表的记录中时，只能输入一行中的列值作为输入参数(或常数)，并且返回一个结果。

例如1：MOD(X,Y) 是求余函数，返回的X除以Y的余数，其中X和Y可以是列值，也可以是常数。

例如2：TO_CHAR(X,'YYYYMMDD')是时间类型转字符串的函数，其中X可以是行中某一时间类型（date）的列，也可以是一个时间类型的常数。

常用的单行函数大致以下几类：

字符串函数：对字符串进行操作，例如：TO_CHAR()、SUBSTR()、DECODE()等等。

数值函数：对数值进行计算或操作，返回一个数字。例如：ABS()、MOD()、ROUND()等等。

转换函数：将一种数据类型转换成另外一种类型：例如：TO_CHAR()、TO_NUMBER()、TO_DATE()等等。

日期函数：对时间和日期进行操作的函数。例如：TRUNC()、SYSDATE()、ADD_MONTHS()等等。

2、聚合函数：聚合函数同时可以对多行数据进行操作，并返回一个结果。比如 SUM(x)返回结果集中 x 列的总合。

#### Oracle字符型函数

 Oracle字符型函数是单行函数当中的一种，是用来处理字符串类型的函数，通过接收字符串参数，然后经过操作返回字符串结果的函数。 

 常用的函数如下表： 

| **函数 **                | **说明 **                                                    | **案例 **                                                    | **结果 **      |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------- |
| ASCII(X)                 | 求字符X的ASCII码                                             | select ASCII('A') FROM DUAL;                                 | 65             |
| CHR(X)                   | 求ASCII码对应的字符                                          | select CHR(65) FROM DUAL;                                    | 'A'            |
| LENGTH(X)                | 求字符串X的长度                                              | select LENGTH('ORACLE技术圈')from DUAL;                      | 9              |
| CONCATA(X,Y)             | 返回连接两个字符串X和Y的结果                                 | select CONCAT('ORACLE','技术圈') from DUAL;                  | ORACLE技术圈   |
| INSTR(X,Y[,START])       | 查找字符串X中字符串Y的位置，可以指定从Start位置开始搜索，不填默认从头开始 | SELECT INSTR('ORACLE技术圈','技术') FROM DUAL;               | 7              |
| LOWER(X)                 | 把字符串X中大写字母转换为小写                                | SELECT LOWER('ORACLE技术圈') FROM DUAL;                      | oracle技术圈   |
| UPPER(X)                 | 把字符串X中小写字母转换为大写                                | SELECT UPPER('Oracle技术圈') FROM DUAL;                      | ORACLE技术圈   |
| INITCAP(X)               | 把字符串X中所有单词首字母转换为大写，其余小写。              | SELECT INITCAP('ORACLE is good ') FROM DUAL;                 | Oracle Is Good |
| LTRIM(X[,Y])             | 去掉字符串X左边的Y字符串，Y不填时，默认的是字符串X左边去空格 | SELECT LTRIM('--ORACLE技术圈','-') FROM DUAL;                | ORACLE技术圈   |
| RTRIM(X[,Y])             | 去掉字符串X右边的Y字符串，Y不填时，默认的是字符串X右边去空格 | SELECT RTRIM('ORACLE技术圈--','-') FROM DUAL;                | ORACLE技术圈   |
| TRIM(X[,Y])              | 去掉字符串X两边的Y字符串，Y不填时，默认的是字符串X左右去空格 | SELECT TRIM('--ORACLE技术圈--','-') FROM DUAL;               | ORACLE技术圈   |
| REPLACE(X,old,new）      | 查找字符串X中old字符，并利用new字符替换                      | SELECT REPLACE('ORACLE技术圈','技术圈','技术交流') FROM DUAL; | ORACLE技术交流 |
| SUBSTR(X,start[,length]) | 截取字符串X，从start位置（其中start是从1开始）开始截取长度为length的字符串，length不填默认为截取到字符串X末尾 | SELECT SUBSTR('ORACLE技术圈',1,6) FROM DUAL;                 | ORACLE         |
| RPAD(X,length[,Y])       | 对字符串X进行右补字符Y使字符串长度达到length长度             | SELECT RPAD('ORACLE',9,'-') from DUAL;                       | ORACLE---      |
| LPAD(X,length[,Y])       | 对字符串X进行左补字符Y使字符串长度达到length长度             | SELECT LPAD('ORACLE',9,'-') from DUAL;                       | ---ORACLE      |

#### Oracle日期型函数

 Oracle日期类型函数是操作日期、时间类型的相关数据，返回日期时间类型或数字类型结果，常用的函数有：SYSDATE()、ADD_MONTHS（）、LAST_DAY（）、TRUNC()、ROUND()等等。 

#### 系统日期、时间函数

**SYSDATE函数：**该函数没有参数，可以得到系统的当前时间。

案例代码：

```sql
select to_char(sysdate,'yyyy-mm-dd hh24:mi:ss') from dual;
```

**SYSTIMESTAMP函数：**该函数没有参数，可以得到系统的当前时间，该时间包含时区信息，精确到微秒。

案例代码：

```sql
select systimestamp from dual;
```

#### 数据库时区函数：

**DBTIMEZONE函数：**该函数没有输入参数，返回数据库时区。

案例代码：

```sql
select dbtimezone from dual;
```

#### 给日期加上指定的月份函数：

**ADD_MONTHS（r,n）函数：**该函数返回在指定日期r上加上一个月份数n后的日期。其中

r：指定的日期。

n：要增加的月份数，如果N为负数，则表示减去的月份数。

案例代码：

```sql
select to_char(add_months(to_date('2018-11-12','yyyy-mm-dd'),1),'yyyy-mm-dd'),
       to_char(add_months(to_date('2018-10-31','yyyy-mm-dd'),1),'yyyy-mm-dd'),
       to_char(add_months(to_date('2018-09-30','yyyy-mm-dd'),1),'yyyy-mm-dd')        
  from dual;
```

结果：（如果指定的日期是月份的最后一天，返回的也是新的月份的最后一天，如果新的月份比指定的月份日期少，将会自动调回有效日期）

#### 月份最后一天函数:

**LAST_DAY(r)函数：**返回指定r日期的当前月份的最后一天日期。

案例代码：

```sql
 select last_day(sysdate) from dual;
```

#### 指定日期后一周的日期函数:

**NEXT_DAY(r,c)函数：**返回指定R日期的后一周的与r日期字符（c：表示星期几）对应的日期。

案例代码：

```sql
 select next_day(to_date('2018-11-12','yyyy-mm-dd'),'星期四') from dual;
```

#### 返回指定日期中特定部分的函数：

**EXTRACT（time）函数：**返回指定time时间当中的年、月、日、分等日期部分。

案例代码：

```sql
select  extract( year from timestamp '2018-11-12 15:36:01') as year,
        extract( month from timestamp '2018-11-12 15:36:01') as month,        
        extract( day from timestamp '2018-11-12 15:36:01') as day,  
        extract( minute from timestamp '2018-11-12 15:36:01') as minute,
        extract( second from timestamp '2018-11-12 15:36:01') as second
 from dual;
```

#### 返回两个日期间的月份数

**MONTHS_BETWEEN(r1,r2)函数：**该函数返回r1日期和r2日期直接的月份。当r1>r2时，返回的是正数，假如r1和r2是不同月的同一天，则返回的是整数，否则返回的小数。当r1<r2时，返回的是负数。

案例代码：

```sql
select months_between(to_date('2018-11-12', 'yyyy-mm-dd'),
                      to_date('2017-11-12', 'yyyy-mm-dd')) as zs, --整数
       months_between(to_date('2018-11-12', 'yyyy-mm-dd'),
                      to_date('2017-10-11', 'yyyy-mm-dd')) as xs, --小数
       months_between(to_date('2017-11-12', 'yyyy-mm-dd'),
                      to_date('2018-10-12', 'yyyy-mm-dd')) as fs --负数
  from dual;
```

#### 日期截取函数

**ROUND（r[,f]）函数：**将日期r按f的格式进行四舍五入。如果f不填，则四舍五入到最近的一天。

案例代码：

```sql
select sysdate, --当前时间
       round(sysdate, 'yyyy') as year, --按年
       round(sysdate, 'mm') as month, --按月
       round(sysdate, 'dd') as day, --按天
       round(sysdate) as mr_day, --默认不填按天
       round(sysdate, 'hh24') as hour --按小时
  from dual;
```

**TRUNC（r[,f]）函数：**将日期r按f的格式进行截取。如果f不填，则截取到当前的日期。

案例代码：

```sql
select sysdate, --当前时间
       trunc(sysdate, 'yyyy') as year, --按年
       trunc(sysdate, 'mm') as month, --按月
       trunc(sysdate, 'dd') as day, --按天
       trunc(sysdate) as mr_day, --默认不填按天
       trunc(sysdate, 'hh24') as hour --按小时
  from dual;
```

#### Oracle数值型函数

 Oracle数值型函数可以是输入一个数值，并返回一个数值的函数，经常用到函数如下表： 

| **函数 **    | **解释 **                                                    | **案例 **                                                    | **结果 **        |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------- |
| ABS(X)       | 求数值X的绝对值                                              | select abs(-9) from dual;                                    | 9                |
| COS(X)       | 求数值X的余弦                                                | select cos(1) from dual;                                     | 0.54030230586814 |
| ACOS(X)      | 求数值X的反余弦                                              | select acos(1) from dual;                                    | 0                |
| CEIL(X)      | 求大于或等于数值X的最小值                                    | select ceil(7.8) from dual;                                  | 8                |
| FLOOR(X)     | 求小于或等于数值X的最大值                                    | select floor(7.8) from dual;                                 | 7                |
| log(x,y)     | 求x为底y的对数                                               | select log(2,8) from dual;                                   | 3                |
| mod(x,y)     | 求x除以y的余数                                               | select mod(13,4) from dual;                                  | 1                |
| power(x,y)   | 求x的y次幂                                                   | select power(2,4) from dual;                                 | 16               |
| sqrt(x)      | 求x的平方根                                                  | select sqrt(16) from dual;                                   | 4                |
| round(x[,y]) | 求数值x在y位进行四舍五入。y不填时，默认为y=0;当y>0时，是四舍五入到小数点右边y位。当y<0时，是四舍五入到小数点左边\|y\|位。 | select round(7.816, 2), round(7.816), round(76.816, -1)  from dual; | 7.82 / 8 / 80    |
| trunc(x[,y]) | 求数值x在y位进行直接截取y不填时，默认为y=0;当y>0时，是截取到小数点右边y位。当y<0时，是截取到小数点左边\|y\|位。 | select trunc(7.816, 2), trunc(7.816), trunc(76.816, -1)  from dual; | 7.81 / 7 / 70    |

#### Oracle转换函数

 Oracle转换函数是进行不同数据类型转换的函数，是我们平常数据库开发过程当中用的最多的内置函数。常用的函数有to_char()、to_number()、to_date()等等。详细分析如下表： 

| **函数 **                    | **解释 **                                                    | **案例 **                                                    | **结果 **                               |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------------- |
| asciistr(x)                  | 把字符串x转换为数据库字符集对应的ASCII值                     | select asciistr('Oracle技术圈')  from dual;                  | Oracle\6280\672F\5708                   |
| bin_to_num(x1[x2...])        | 把二进制数值转换为对应的十进制数值                           | select bin_to_num(1,0,0) from dual;                          | 4                                       |
| cast(x as type)              | 数据类型转换函数，该函数可以把x转换为对应的type的数据类型，基本上用于数字，字符，时间类型安装数据库规则进行互转， | select cast('123' as number) num,cast(123 as varchar2(3)) as ch,cast(to_date('20181112','yyyymmdd') as varchar2(12)) as time  from dual; | 123/'123'/12-11月-18(三列值，用"/"隔开) |
| convert(x,d_chset[,r_chset]) | 字符串在字符集间的转换函数，对字符串x按照原字符集r_chset转换为目标字符集d_chset，当r_chset不填时，默认选择数据库服务器字符集。 | select CONVERT('oracle技术圈','US7ASCII','ZHS16GBK') from dual; | oracle???                               |
| to_char(x[,f])               | 把字符串或时间类型x按格式f进行格式化转换为字符串。           | select to_char(123.46,'999.9') from dual; select to_char(sysdate,'yyyy-mm-dd') from dual; | 123.52018-11-13                         |
| to_date(x[,f])               | 可以把字符串x按照格式f进行格式化转换为时间类型结果。         | select to_date('2018-11-13','yyyy-mm-dd') from dual;         | 2018/11/13                              |
| to_number(x[,f])             | 可以把字符串x按照格式f进行格式化转换为数值类型结果。         | select to_number('123.74','999.99') from dual                | 123.74                                  |

 **提醒：**其中数值的格式f可以参考下表： 

| **参数 ** | **示例 ** | **说明 **                |
| --------- | --------- | ------------------------ |
| 9         | 999       | 指定位置返回数字         |
| .         | 99.9      | 指定小数点的位置         |
| ，        | 99,9      | 指定位置返回一个逗号     |
| $         | $99.9     | 指定开头返回一个美元符号 |
| EEEE      | 9.99EEEE  | 指定科学计数法           |

#### Oracle聚合函数

 Oracle聚合函数同时可以对多行数据进行操作，并返回一个结果。比如经常用来计算一些分组数据的总和和平均值之类，常用函数有AVG()、SUM()、MIN()、MAX()等等。 

#### AVG函数

AVG([distinct ] expr)：该函数可以求列或列组成的表达式expr的平均值，返回的是数值类型。其中 distinct是可选参数，表示是否去掉重复行。

**案例1、求学生信息表（stuinfo）中学生的平均年龄，代码如下：**

```sql
select * from stuinfo;
select avg(t.age) from stuinfo t;
```

使用该函数和其他聚合函数时，都可以和where条件语句和分组GROUP BY 查询组合使用，得到特定的结果。

**案例2,、按照班级求各班学生的平均年龄（其中年龄大于等于30岁的不计入在内）。代码：**

```sql
select classno, avg(t.age)
  from stuinfo t
 where t.age < 30
 group by t.classno;
```

#### COUNT函数

count（*|[distinct]expr）函数可以用来计算查询结果的条数或行数。函数中必须指定列名或者表达式expr，不然就要全选使用*号。

**案例3、查询学生信息表中所有的学生的个数。代码如下：**

```sql
select count(*) from stuinfo;
```

#### MAX/MIN函数

MAX([distinct] expr)、MIN([distinct] expr)函数可以返回指定列或列组成的表达式expr中的最大值或最小值。该函数也通常和where条件、group by分组结合在一起使用。

**案例4、求学生信息表中年龄最大的学生的年龄：**

```sql
select max(age) from stuinfo;
```

#### SUM函数

SUM([distinct] expr)函数可以对指定列或列组成的表达式expr进行求和，假如不使用分组group by ,那就是按照整表作为一个分组。

**案例5、正好利用sum函数求和乘以人数进行求学生的平均年龄**

```sql
select classno, sum(age), count(*), sum(age) / count(*), avg(age)
  from stuinfo t
 where t.age < 30
 group by t.classno;
```

#### Oracle子查询

Oracle子查询就是嵌套查询，他把select 查询的结果作为另外一个select、update或delete语句的条件，它的本质就是where条件查询中的一个条件表达式。其中我们数据库开发过程中，子查询可以根据查询结果的行数的多少，可以区分为单行子查询和多行子查询。

1、单行子查询：向外部返回的结果为空或者返回一行。

2、多行子查询：向外部返回的结果为空、一行、或者多行。

#### Oracle单行子查询

  Oracle单行子查询是利用where条件“=”关联查询结果的，如果单行子查询返回多行会报单行子查询不能返回多行的数据库错误，下面利用案例讲解子查询。

**案例1**、查询学生信息表（stuinfo）和班级表(class)中班级为“信息科学2班（18）”的所有学生信息

```sqlite
select *
  from stuinfo t
 where t.classno in (select b.classno
                       from class b
                      where b.classname = '信息科学2班（18）');

/*虽然在这利用内关联也可以查出结果，
  而且效率更好，但是在一些没有关联关
  系的时候可以利用子查询 */
select t.*
  from stuinfo t, class b
 where t.classno = b.classno
   and b.classname = '信息科学2班（18）';
```

#### Oracle多行子查询

Oracle多行子查询则需要利用IN关键字来接收子查询的多行结果。也可以用量化关键字ANY、ALL和关系运算符>、>=、=、<、<=来组合使用。

ANY关键字：表示子查询结果当中的任意一个。假如：>ANY(子查询)，表示：只要大于子查询当中的任意一个值，这个条件就满足。

ALL关键字：表示子查询中的所有结果。假如：>ALL(子查询)，表示：必须大于子查询当中的所有结果才能满足这个条件。

**案例2**、查询班级表中所有班级的学生信息。代码如下：

```sql
select * from stuinfo t where t.classno in (select b.classno from class b);
```

**案例3**、ANY/ALL关键字案例展示，代码如下：

```sql
--年龄只要大于当中子查询的最小值26岁即可
select * from stuinfo t where t.age>any(26,27,28);
--年龄必须大于子查询当中的最大值28岁才可以
select * from stuinfo t where t.age>all(26,27,28);
```

#### Oracle synonym 同义词

Oracle synonym 同义词是数据库当前用户通过给另外一个用户的对象创建一个别名，然后可以通过对别名进行查询和操作，等价于直接操作该数据库对象。Oracle同义词常常是给表、视图、函数、过程、包等制定别名，可以通过CREATE 命令进行创建、ALTER 命令进行修改、DROP 命令执行删除操作。

Oracle synonym 同义词按照访问权限分为私有同义词、公有同义词。

私有同义词：私有同义词只能当前用户可以访问，前提：当前用户具有create synonym 权限。

公有同义词：公有同义词只能具有DBA用户才能进行创建，所有用户都可以访问的。

**语法结构：**

```sql
CREATE [OR REPLACE] [PUBLIC] SYSNONYM [当前用户.]synonym_name

FOR [其他用户.]object_name;
```

**解析：**

1、create [or replace] 命令create建表命令一样，当当前用户下同义词对象名已经存在的时候，就会删除原来的同义词，用新的同义词替代上。

2、[public]：创建的是公有同义词，在实际开发过程中比较少用，因为创建就代表着任何用户都可以通过自己用户访问操作该对象，一般我们访问其他用户对象时，需要该用户进行授权给我们。

3、用户名.object_name：oralce用户对象的权限都是自己用户进行管理的，需要其他用户的某个对象的操作权限，只能通过对象拥有者（用户）进行授权给当前用户。或者当前用户具有系统管理员权限（DBA），即可通过用户名.object_name操作该对象。

案例分析：

在jsq_copy用户下也创建了一张学生信息表（stuinfo），该信息表只存在一个学生信息“张三丰”。由于我们当前用户student用户不具有jsq_copy.stuino的权限，因此要需要该用户授权，然后才能访问。代码如下：

```sql
--未授权之前查询（提示表不存在,没有操作权限）
select * from jsq_copy.stuinfo;

--登录jsq_copy用户进行授权
conn  jsq_copy/123456;
grant all on stuinfo to student;

--授权后再次查询该表数据
conn student/123456;
select * from jsq_copy.stuinfo;
```

现在为jsq_copy.stuinfo创建同义词stuinfo_copy，然后通过当前用户student直接操作同义词stuinfo_copy查询jsq_copy.stuinfo表数据。代码如下：

```sql
create synonym stuinfo_copy for jsq_copy.stuinfo;
```

**同义词删除**

​    同义词删除只能通过同义词拥有者的用户或者具有DBA权限的用户才能删除。

**语法结构：**

```sql
DROP [PUBLIC] SYNONYM [用户.]sysnonym_name;
```

#### Oracle序列

Oracle序列Sequence是用来生成连续的整数数据的对象，它经常用来作为业务中无规则的主键。Oracle序列可以是升序列也可以是降序列。

**创建Oracle序列的语法结构如下：**

```sql
CREATE SEQUENCE sequence_name
[MAXVALUE num|NOMAXVALUE]
[MINVALUE num|NOMINVALUE]
[START WITH num]
[INCREMENT BY increment]
[CYCLE|NOCYCLE]
[CACHE num|NOCACHE]
```

**语法解析：**

1、MAXVALUE/MINVALUE：指定的是序列的最大值和最小值。

2、NOMAXVALUE/NOMINVALUE：不指定序列的最大值和最小值，使用系统的默认选项，升序的最大值：10^27次方，降序是-1。升序最小值：1，降序的最小值：-10^26。

3、START WITH：指定从某一个整数开始，升序默认是1，降序默认是-1。

4、CYCLE | NOCYCLE:表示序列达到最大值或者最小值的时候，是否重新开始。CYCLE：重新开始，NOCYCLE：不重新开始。

5、CACHE：使用 CACHE 选项时，该序列会根据序列规则预生成一组序列号。保留在内存中，当使用下一个序列号时，可以更快的响应。当内存中的序列号用完时，系统再生成一组新的序列号，并保存在缓存中，这样可以提高生成序列号的效率 。

6、NOCACHE：不预先在内存中生成序列号

#### Oracle视图

oracle视图可以理解为数据库中一张虚拟的表，他是通过一张或者多张基表进行关联查询后组成一个虚拟的逻辑表。查询视图，本质上是对表进行关联查询。

视图的本身是不包含任何数据，只是一个查询结果，当基表的数据发生变化时，视图里面的数据也会跟着发生变化。我们经常在实际开发过程中遇到的视图可以大概分为三种：单表视图、多表关联视图、视图中含有子视图。

#### 视图的作用和优势

既然视图在实际开发过程当中被广泛使用到，它到底有哪些作用和优势呢？

**1、使数据简单化**：可以将复杂的查询创建成视图，提供给他人使用，他人就不需要去理解其中复杂性的业务关系或逻辑关系。这样对视图的使用人员来说，就简化了数据的，屏蔽了数据的复杂性。

**2、表结构设计的补充：**系统刚刚开始设计时，大部分程序是直接访问表结构的数据的，但是随着业务的变化、系统的更新等，造成了某些表结构的不适用，这时候去修改表结构对系统的影响太大，开发成本较高，这个时候可以创建视图来对表结构的设计进行补充，降低开发成本。程序可以直接通过查询视图得到想要的数据。

**3、增加安全性：**视图可以把表中指定的字段展示给用户，而不必把表中所有字段一起展示给用户。在实际开发中，视图经常作为数据的提供方式，设置为只读权限提供给第三方人员进行查询使用。

#### 创建视图

创建视图的语法结构如下：

```sql
CREATE [OR REPLACE]  VIEW view_name
AS
SELECT 查询
[WITH READ ONLY CONSTRAINT]
```

解释：

1、OR REPLACE：如果视图已经存在，则替换旧视图。

2、WITH READ ONLY：默认不填的，用户是可以通过视图对基表执行增删改操作，但是有很多在基表上的限制（比如：基表中某列不能为空，但是该列没有出现在视图中，则不能通过视图执行 insert 操作，或者基表设置了某些约束，这时候插入视图或者修改视图的值，有可能会报错）， WITH READ ONLY 说明视图是只读视图，不能通过该视图进行增删改操作。但是在现实开发中，基本上不通过视图对表中的数据进行增删改操作。 

**案例1、**利用学生信息表（stuinfo）、班级表（class）关联创建视图，只提供一些学生基本信息和班级信息（剔除学生一些敏感信息：如身份证，家庭地址等）。代码如下：

```sql
create view vw_stuinfo as 
select a.stuid,--学号
       a.stuname,--学生姓名
       a.grade,--年级
       a.sex,--性别（1:男、2:女）
       a.age,--年龄
       b.classname,--班级
       b.monitorname,--班长
       b.headmastername--班主任
  from stuinfo a, class b
 where a.classno = b.classno;
select * from vw_stuinfo;
```

#### Oracle索引

Oracle索引（index）最大的作用是用来优化数据库查询的效率，提升数据库的查询性能。就好比书的目录一样，可以通过目录来直接定位所需内容存在的页数，大大提高检索效率。

Oracle数据库中如果某列出现在查询的条件中，而该列的数据是无序的，查询时只能从第一行开始一行一行的匹配。创建索引就是对某些特定列中的数据进行排序或归类，生成独立的索引表。在某列上创建索引后，如果该列出现在查询条件中，Oracle 会自动的引用该索引，先从索引表中查询出符合条件记录的 ROWID，由于 ROWID 是记录的物理地址，因此可以根据 ROWID 快速的定位到具体的记录，当表中的数据非常多时，引用索引带来的查询效率非常可观 。

#### 何时建立索引

既然都知道建立索引有利于查询速率的提升，那是不是所有字段都可以加上索引。这是万万不行的，建立索引不仅仅要浪费空间来存储索引表，当数据量较少时，直接查询数据比经过查询索引表再定位到表数据的速度更快。索引可以提高查询的效率，但是在数据增删改时需要更新索引，因此索引对增删改时会有负面影响。所以要根据实际情况， 考虑好再建立索引。

那何时建立索引，下面大概介绍几点，其余的得在实际应用和开发过程中，酌情考虑：

1、Oracle 数据库会为表的主键和包含唯一约束的列自动创建索引，所以在建立唯一约束时，可以考虑该列是否必要建立。是否经常要作为查询条件。

2、如果某个表的数据量较大（十几二十万以上），某列经常作为where的查询条件，并且检索的出来的行数经常是小于总表的5%，那该列可以考虑建立索引。

3、对于两表连接的字段，应该考虑建立索引。如果经常在某表的一个字段进行Order By 则也经过进行索引。

4、不应该在小表上建立索引。上面也说过，小表之间查询的数据会比建立索引的查询速度更快，但是在某些字段，如性别：只有男、女和未知三种数据时，可以考虑位图索引，可以增加查询效率。

5、经常进行DML操作，即经常进行增删改的操作的表，创建表索引时就要权衡一下，因为建索引会导致进行DML操作时速度变慢。所以可以根据实际情况，选择某些字段建立索引，而不能盲目乱建。

#### 索引的类别

适当的使用索引可以提高数据检索速度，那Oracle有哪些类型的索引呢？

**1、b-tree索引：**Oracle数据中最常见的索引，就是b-tree索引，create index创建的normal就是b-tree索引，没有特殊的必须应用在哪些数据上。

**2、bitmap位图索引：**位图索引经常应用于列数据只有几个枚举值的情况，比如上面说到过的性别字段，或者我们经常开发中应用的代码字段。这个时候使用bitmap位图索引，查询效率将会最快。

**3、函数索引：**比如经常对某个字段做查询的时候经常是带函数操作的，那么此时建一个函数索引就有价值了。例如：trim（列名）或者substr(列名)等等字符串操作函数，这个时候可以建立函数索引来提升这种查询效率。

**4、hash索引：**hash索引可能是访问数据库中数据的最快方法，但它也有自身的缺点。创建hash索引必须使用hash集群，相当于定义了一个hash集群键，通过这个集群键来告诉oracle来存储表。因此，需要在创建HASH集群的时候指定这个值。存储数据时，所有相关集群键的行都存储在一个数据块当中，所以只要定位到hash键，就能快速定位查询到数据的物理位置。

**5、reverse反向索引：**这个索引不经常使用到，但是在特定的情况下，是使用该索引可以达到意想不到的效果。如：某一列的值为{10000,10001,10021,10121,11000,....}，假如通过b-tree索引，大部分都密集分布在某一个叶子节点上，但是通过反向处理后的值将变成{00001,10001,12001,12101,00011,...}，很明显的发现他们的值变得比较随机，可以比较平均的分部在各个叶子节点上，而不是之前全部集中在某一个叶子节点上，这样子就可大大提高检索的效率。

**6、分区索引和分区表的全局索引：**这两个索引是应用在分区表上面的，前者的分区索引是对分区表内的单个分区进行数据索引，后者是对分区表的全表进行全局索引。分区表的介绍，可以后期再做单独详解，这里就不累述了。

#### 索引的创建

**语法结构：**

```sql
create[unique]|[bitmap] index index_name --UNIQUE表示唯一索引、BITMAP位图索引
on table_name(column1,column2...|[express])--express表示函数索引
[tablespace tab_name] --tablespace表示索引存储的表空间
[pctfree n1]    --索引块的空闲空间n1
[storage         --存储块的空间
 (
    initial 64K  --初始64k
    next 1M
    minextents 1
    maxextents unlimited

)];
```

**语法解析：**

1、UNIQUE:指定索引列上的值必须是唯一的。称为唯一索引，BITMAP表示位图索引。

2、index_name：指定索引名。

3、tabl_name：指定要为哪个表创建索引。

4、column_name：指定要对哪个列创建索引。我们也可以对多列创建索引，这种索引称为组合索引。也可以是函数表达式，这种就是函数索引。

**修改索引：**

1、重命名索引：

```sql
alter index index_old rename to index_new;--重新命名索引
```

2、合并索引、重新构造索引：我们索引建好后，经过很长一段时间的使用，索引表中存储的空间会产生一些碎片，导致索引的查询效率会有所下降，这个时候可以合并索引，原理是按照索引规则重新分类存储一下，或者也可以选择删除索引重新构造索引。

```sql
alter index index_name coalesce;--合并索引
alter index index_name rebuild;--重新构造
```

**删除索引：**

```sql
drop index index_name;
```

**查看索引：**

```sql
select t.INDEX_NAME,--索引名字
       t.index_type,--索引类型
       t.TABLESPACE_NAME,--表空间
       t.status,--状态
       t.UNIQUENESS--是否唯一索引
  from all_indexes T 
  where  t.INDEX_NAME='index_name';
```

**案例分析：**

**案例1、**学生信息表（stuinfo）创建的时候就对学号（stuid）设置了主键（PK_STUINFO），当我们学生信息表数据量大的情况下，我们明显发现班号（classno）需要一个索引，不仅仅是用来关联班级信息表（class）、而且经常作为查询条件，因此创建脚本如下：

```
create index STUDENT.IDX_STUINFO_CLASSNO on STUDENT.STUINFO (CLASSNO)
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
```

**案例2、**对于学生信息我们经常用性别作为统计条件进行对学生信息进行统计，因此我们可以在性别（sex）建立一个位图索引进行查询优化。代码如下：

```sql
create bitmap index STUDENT.IDX_STUINFO_SEX on STUDENT.STUINFO (SEX)
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
```

查询一下三种索引的状态：

```sql
select t.INDEX_NAME,
       t.index_type,
       t.TABLESPACE_NAME,
       t.status,
       t.UNIQUENESS
  from all_indexes T
  where t.TABLE_NAME='STUINFO'
  AND T.OWNER='STUDENT'
```

#### Oracle分区详解和创建

Oracle在实际业务生产环境中，经常会遇到随着业务量的逐渐增加，表中的数据行数的增多，Oracle对表的管理和性能的影响也随之增大。对表中数据的查询、表的备份的时间将大大提高，以及遇到特定情况下，要对表中数据进行恢复，也随之数据量的增大而花费更多的时间。这个时候，Oracle数据库提供了分区这个机制，通过把一个表中的行进行划分，归为几部分。可以减少大数据量表的管理和性能问题。利用这种分区方式把表数据进行划分的机制称为表分区，各个分区称为分区表。

Oracle分区对于大型表（大数据量）非常有用，分区的作用主要有：

1、改善大型表的查询性能，因为可以通过查询对应分区表中对应的数据，而不需要查询整个表。

2、表更容易管理，因为分区表的数据存储在各个分区中，所以可以按照分区建，来管理对应分区当中的数据，可以按照分区加载和删除其中的数据，比在不分区情况下，更容易管理数据。以及在特定的事故情况下，通过备份好的分区，可以快速恢复对应分区当中的数据，也不需要对全表数据进行恢复。

#### Oracle创建分区

既然，Oracle分区有如此好处，我们在这里通过一个例子来讲解如何创建分区。在我们的学生信息系统案例当中，学生成绩表（SCORE）会随着学生的增多和课程的增多，表中的数据量会越来越大，所以可以考虑创建分区表来解决这个问题。

Oracle分区也是通过create table命令组成，但是对表进行分区时，得考虑一个字段作为分区建，通常按值的范围来划分分区，所以这里考虑使用成绩的录入时间进行分区。具体代码如下：

```sql
-- Create table
create table STUDENT.SCORE
(
  scoreid  VARCHAR2(18) not null,
  stuid    VARCHAR2(11),
  courseid VARCHAR2(9),
  score    NUMBER,
  scdate   DATE
)
partition by range(scdate)(
partition p_score_2018 values less than (TO_DATE('2019-01-01 00:00:00','yyyy-mm-ddhh24:mi:ss'))
 TABLESPACE TS_2018,
partition p_score_2019 values less than (TO_DATE('2020-01-01 00:00:00','yyyy-mm-ddhh24:mi:ss'))
 TABLESPACE TS_2019,
partition p_score_2020 values less than (MAXVALUE)
 TABLESPACE TS_2020
);
-- Add comments to the table 
comment on table STUDENT.SCORE
  is '学生成绩表';
-- Add comments to the columns 
comment on column STUDENT.SCORE.scoreid
  is '学生成绩id';
comment on column STUDENT.SCORE.stuid
  is '学生学号';
comment on column STUDENT.SCORE.courseid
  is '课程id(年度+上下学期+课程序列)';
comment on column STUDENT.SCORE.score
  is '成绩';
comment on column STUDENT.SCORE.scdate
  is '成绩录入时间';
-- Create/Recreate primary, unique and foreign key constraints 
alter table STUDENT.SCORE
  add constraint PK_SCORE primary key (SCOREID)
  using index 
  tablespace USERS
  pctfree 10
  initrans 2
  maxtrans 255
  storage
  (
    initial 64K
    next 1M
    minextents 1
    maxextents unlimited
  );
```

这里使用命令partition by range对成绩的录入日期（scdate）进行分区，如录入日期小于2019年的会被放入分区p_score_2018当中，2019年数据会被放入p_score_2019这个分区当中，大于2019年数据都会被放入到p_score_2020这个分区当中。

这里不必为最后一个分区指定最大值，maxvalue关键字会告诉Oracle使用这个分区来存储前面几个分区当中不能存储的数据。

上面实例展示的是Oracle按照值的范围进行分区，Oracle还支出散列分区，通过某一个字段，把表中的数据散列在各个分区中。可以通过关键字partition by hash，可以把分区散列到不同的表空间当中。

Oracle还支持列表分区（partition by list），它是通过按照指定分区建的值归并到各个分区，其实这里学生成绩表也可以考虑按照课程进行列表分区。

总结：Oracle分区对大型表（数据量大）有重大的性能提升，所以在表结构设计时，需要提前按照相关业务需求进行相应的改进。

#### Oracle如何在分区表上创建索引

 在实际生产环境中，为了进一步的优化大型表（大数据量集）的查询效率，这个时候得考虑在分区表上某个字段创建索引。分区表的索引和普通表的索引本质上是一样的，都是利用空间换取时间的方式，通过存储索引块来增加查询效率。但是有不同地方是，Oracle分区表索引可以分为局部（分区）索引和全局索引之分。 

#### 区索引

所为的分区索引指的是在子分区当中按照某个字段建立索引，例如，上一章创建的学生成绩表中（score）,可以对学生学号创建local索引，即分区索引。代码如下：

```sql
create index idx_score_stuid on student.score(stuid)
local
(
partition idx_score_stuid_1 tablespace TS_2018,
partition idx_score_stuid_2 tablespace TS_2019,
partition idx_score_stuid_3 tablespace TS_2020
)
```

请注意local关键字。在这个create index命令中没有指定范围，而是由local 关键字告诉Oracle为score表的每一个分区创建一个单独的索引，因此，每一个表分区对应着一个索引分区。每一个索引分区存储在不同的表空间上，可以大大提高I/O和查询效率。

通过查询数据字典dba_ind_partitions可以查看刚刚创建的分区索引，如下图：

![1640236694588](Images/1640236694588.png)

#### 全局索引

Oracle分区表也可以创建全局索引，全局索引和普通表的索引一样，是对整表的数据进行创建索引。例如，可以对学生成绩表的（score）的课程ID（COURSEID）创建全局索引，具体代码如下：

```sql
create index STUDENT.IDX_SCORE_COURSEID 
on STUDENT.SCORE (courseid)
global;
```

这里，虽然分区索引比全局索引更容易管理，而且在分区当中查询效率更高，但是全局索引在全表进行唯一性检索时的速度可能会比局部索引更快，因为全局检索唯一性时，需要跨区。

**注意：**不能为子分区创建全局索引。

#### Oracle merge into命令

Oracle merge into命令，顾名思义就是“有则更新，无则插入”，这个也是merge into 命令的核心思想，在实际开发过程中，我们会经常遇到这种通过两表互相关联匹配更新其中一个表的某些字段的业务，有时还要处理不匹配的情况下的业务。这个时候你会发现随着表的数据量增加，类似这种业务场景的执行效率会比较慢，那是因为你需要多次重复查询两表中的数据，而通过merge into命令，只需要一次关联即可完成“有则更新，无则插入”的业务场景，大大提高语句的执行效率。

merge into命令的语法结构如下：

```sql
merge into A 
using B 
on (A.id = B.id)
when matched then
  update set A.col=B.col
when not matched then
  insert 语句;
```

语法解析：利用B表通过A.id=B.id的条件来匹配A表，当满足条件时，可以对A表进行更新，当不满足条件时，可以利用inert语句插入相关数据。

 例子：利用merge into命令从学生表（stuinfo）更新学生备份表（stuinfo_2018）的年龄，当备份表中找不到学生信息时插入新的学生信息，先看下两张表的数据： 

![1640236866662](Images/1640236866662.png)

具体代码如下：

```sql
merge into student.stuinfo_2018 A --
using student.stuinfo B 
on (A.stuid = B.stuid)
when matched then
  update set A.age=B.age
when not matched then
  insert (a.STUID,a.STUNAME,a.SEX,a.AGE,a.CLASSNO,a.STUADDRESS,a.GRADE,a.ENROLDATE,a.IDNUMBER
) values(b.STUID,b.STUNAME,b.SEX,b.AGE,b.CLASSNO,b.STUADDRESS,b.GRADE,b.ENROLDATE,b.IDNUMBER);
```

再看下备份表的数据，发现已经按照意愿添加了新的学生和变更了学生的年龄。如下：

![1640236900998](Images/1640236900998.png)

#### Oracle物化视图

Oracle物化视图可以理解为用来存储数据表的副本或者聚集，物化视图可以用来复制一个表的全部数据或者部分数据，也可以复制多表关联查询的结果集。然后按照指定的时间间隔内自动更新副本数据的刷新。本文将介绍物化视图常用的场景和创建方法，以及刷新策略。

物化视图是基于select查询结果的数据副本，简单来讲就是数据的复制表，但是它可以按照特定的刷新策略刷新复制表中的数据。常用来：

1、物化视图经常用来当做远程数据表的本地化，可以用来做数据同步用。

2、也经常用来做本地单表或多表数据的汇总，这样子，可以定时把汇总数据更新到复制表，用来做决策分析用。

3、也可以用来做复杂视图的物化作用，把这种数据不经常实时更新的视图，物化成物理表，然后在物化表上建相应的索引，大大提高查询效率。

物化视图在创建时，可以指定刷新（refresh interval）的间隔来执行定时刷新物化表的数据。也可以利用基于事务的刷新，通过主表变化的行数实时来更新物化表。

具体的如何创建物化视图，下回再讲解，或自行搜索。

#### Oracle分析函数_开窗函数详解

Oracle分析函数是Oracle系统自带函数中的一种，是Oracle专门用来解决具有复杂统计需求的函数，它可以对数据进行分组然后基于组中数据进行分析统计，最后在每组数据集中的每一行中返回这个统计值。

Oracle分析函数不同于分组统计（group by），group by只能按照分组字段返回一个固定的统计值，但是不能在原来的数据行上带上这个统计值，而Oracle分析函数正是Oracle专门解决这类统计需求所开发出来的函数。

Oracle分析函数都会带上一个开窗函数over（），所以常把两者结合一起讲解。

**Oracle分析函数的语法结构：**

```sql
select table.column, 
Analysis_function()OVER(
[partition by 字段]
[order by 字段 [windos]]
) as 统计值
from table
```

语法解析：

  1、Analysis_function：指定分析函数名，常用的分析函数有sum、max、first_value、last_value、rank、row_number等等。

  2、over()：开窗函数名，partition by指定进行数据分组的字段，order by指定进行排序的字段，windos指定数据窗口（即指定分析函数要操作的行数），使用的语法形式大概如下：

```sql
over(partition by xxx order by yyy rows between zzz)
```

下面就通过几个案例来讲解一下几个常用的分析函数。

  first_value：返回组中数据窗口的第一个值。

  last_value：返回组中数据窗口的最后一个值。

  max：返回组中的最大值

  min：返回组中的最小值

  下面利用学生选课系统当中的学生成绩表的数据来做案例讲解，原始数据如下：

![1640237011218](Images/1640237011218.png)

例1、利用min、max分别取出不同课程当中的学生成绩的最高值和最低值。  

  需求：在原始数据上附带上每门课的最高成绩和最低成绩。

  代码如下：

```sql
select c.stuname,
       b.coursename,
       t.score,
       --获取组中成绩最大值
       max(t.score) over(partition by t.courseid) as score_max,
       --获取组中成绩最小值
       min(t.score) over(partition by t.courseid) as score_min,
       --分组窗口的第一个值 (指定窗口为组中第一行到末尾行)
       first_value(t.score) over(partition by t.courseid 
       order by t.score desc ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) as score_first,
       --分组窗口的最后一个值(指定窗口为组中第一行到末尾行)
       last_value(t.score) over(partition by t.courseid 
       order by t.score desc ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) as score_last,
       
       --分组窗口的第一个值 （不指定窗口）
       first_value(t.score) over(partition by t.courseid order by t.score desc ) as score_first_1,
       --分组窗口的最后一个值（不指定窗口）
       last_value(t.score) over(partition by t.courseid order by t.score desc ) as score_last_1
        
  from STUDENT.SCORE t, student.course b, student.stuinfo c
 where t.courseid = b.courseid
   and t.stuid = c.stuid
```

  结果如下：

![1640237041283](Images/1640237041283.png)

通过数据，可以发现：

1、min和max分析函数是直接获取组中的最小值和最大值。

2、first_value和last_value是返回窗口的第一行和最后一行数据，由于我们通过成绩字段对分组内的数据进行了降序排序，所以也可以达到在一定的窗口内获取最大值和最小值的功能。

3、排序不指定窗口时，就是按照组内的第一行到当前行作为窗口，然后取出窗口的第一行和最后一行。

4、窗口子语句当中的第一行是 unbounded preceding，当前行是 current row，最后一行是 unbounded following，所以正是利用窗口范围是第一行到最后一行，得到同一课程内的最大成绩和最小成绩。

ROW_NUMBER/RANK：根据开窗函数中排序的字段返回在组内的有序的偏移量，即可得到在组内的位置。

  案例2、利用row_number、rank获取学生课程成绩的排名，具体代码如下：

```sql
select c.stuname,
       b.coursename,
       t.score,
       --组内排名
       row_number() over(partition by t.courseid order by t.score desc) as "row_number排名",
       --组内排名
       rank() over(partition by t.courseid order by t.score desc) as "rank排名"

  from STUDENT.SCORE t, student.course b, student.stuinfo c
 where t.courseid = b.courseid
   and t.stuid = c.stuid
```

 结果如下： 

![1640237098316](Images/1640237098316.png)

 通过数据可以看出：

1、ROW_NUMBER函数排名是返回一个唯一的值，当碰到相同数据时，排名按照记录集中记录的顺序依次递增。

2、rank函数返回一个唯一的值，但是当碰到相同的数据时，此时所有相同数据的排名是一样的，同时会在最后一条相同记录和下一条不同记录的排名之间空出排名。比如数学成绩都是84分的两个人并列第二名，但是“张三丰”同学就是直接是第四名。

3、经常会利用row_number函数的排名机制（排名的唯一性）来过滤重复数据，即按照某一个特定的排序条件，通过获取排名为1的数据来获取重复数据当中最新的数据值。

#### 总结

  Oracle分析函数还有很多，使用方式上和以上的几个函数类似，都是通过开窗函数进行分组，然后通过特定字段的排序，从而获取函数的统计值附加在数据行后面

#### Oracle行转列（PIVOT）

 在实际业务开发环境中，经常会遇到要对查询的数据集进行行转列的需求。那么Oracle是如何一一实现的呢？

#### Oracle行转列

  Oracle行转列就是把某一个字段的值作为唯一值，然后另外一个字段的行值转换成它的列值。这里依然利用我们系统的学生成绩表作为例子，成绩表记录（行）当中对应着每一个科目的每一个学生的成绩，那要做出一个报表是每个学生的所有科目作为一列展示出学生的成绩信息。案例数据如下：

![1640237286347](Images/1640237286347.png)

 1、首先肯定想到的是利用Oracle分组（group by）应该可以实现，实现代码如下： 

```sql
select c.stuname,
       --利用分组聚合函数
       sum(decode(b.coursename, '英语(2018上学期)', t.score, 0)) as "英语(2018上学期)",
       sum(decode(b.coursename, '数学(2018上学期)', t.score, 0)) as "英语(2018上学期)",
       sum(decode(b.coursename, '语文(2018上学期)', t.score, 0)) as "英语(2018上学期)"
  from STUDENT.SCORE t, student.course b, student.stuinfo c
 where t.courseid = b.courseid
   and t.stuid = c.stuid
 group by c.stuname
```

 利用group by对学生进行分组，然后利用decode对对应的课程的成绩值进行转换，然后再求和即可得到该门成绩的结果值，结果如下： 

![1640237348127](Images/1640237348127.png)

2、Oracle11g之后提供了自带函数PIVOT可以完美解决这个行转列的需求，具体语法结构如下：

```sql
SELECT * FROM （数据查询集）
PIVOT 
(
 SUM(Score/*行转列后 列的值*/) FOR 
 coursename/*需要行转列的列*/ IN (转换后列的值)
)
```

  具体代码如下：

```sql
select * from  (select c.stuname,
       b.coursename,
       t.score
  from STUDENT.SCORE t, student.course b, student.stuinfo c
 where t.courseid = b.courseid
   and t.stuid = c.stuid )  /*数据源*/
PIVOT 
(
 SUM(score/*行转列后 列的值*/) 
 FOR coursename/*需要行转列的列*/ IN ('英语(2018上学期)' as 英语,'数学(2018上学期)' as 数学,'语文(2018上学期)' as 语文 )
) ;
```

![1640237396610](Images/1640237396610.png)

#### Oracle列转行_unpivot

在实际业务开发环境中，经常会遇到要对查询的数据集进行列转行的需求。那么Oracle是如何实现的呢?

#### Oracle列转行

Oracle列转行就是把一行当中的列的字段按照行的唯一值转换成多行数据。 比如上文Oracle行转列中的学生成绩表的基础数据是一个学生的一个科目成绩对应着是一条记录。然后进行了行转列后变成一个学生对应着每列（数学、英语、语文）科目的成绩是一条记录。那么本文就是要把之前转换后的学生成绩表（备份表score_copy）再次进行列转行，转换为原始数据。案例数据如下：

![1640237471497](Images/1640237471497.png)

![1640237499508](Images/1640237499508.png)

1、利用union all 进行拼接，可以完美的把对应的列转为行记录，具体代码如下：

```sql
select t.stuname, '英语' as coursename ,t.英语 as score  from SCORE_COPY t
union all
select t.stuname, '数学' as coursename ,t.数学 as score  from SCORE_COPY t
union all
select t.stuname, '语文' as coursename ,t.语文 as score  from SCORE_COPY t
```

![1640237530715](Images/1640237530715.png)

2、利用Oracle自带的列转行函数unpivot也可以完美解决该问题，具体语法结构如下：

```sql
select 字段 from 数据集
unpivot（自定义列名/*列的值*/ for 自定义列名 in（列名））
```

  实现代码如下：

```sql
select stuname, coursename ,score from
score_copy  t
unpivot
(score for coursename in (英语,数学,语文))
```

![1640237574685](Images/1640237574685.png)

#### Oracle创建物化视图

 通过Oracle物化视图章节，已经了解到Oracle物化视图的作用和创建原理，本节通过实例详细讲解Oracle是如何创建物化视图的 

#### 创建物化视图语法：

**语法：**

```
create materialized view view_name
refresh [fast|complete|force]
[
on [commit|demand] |
start with (start_time) next (next_time)
]
AS select 查询语句;
```

**语法解析：**

1、create materialized view是创建物化视图的命令关键字。view_name指的是要创建物化视图的名字。

2、refresh 是指定物化视图数据刷新的模式：

force：这个是默认的刷新方式，Oracle会自动判断该如何进行数据刷新，如果满足快速刷新的条件，就进行fast刷新，不满足就进行全量刷新。

complete:这个是全量刷新数据，当要刷新数据时，会删除物化表中的所有数据，然后物化视图中的查询语句重新生成数据。

fast:采用增量的方式进行数据的刷新。通过主表的视图日志和上次刷新数据进行比对，然后增量更新物化后的数据表。

3、on[comit|demand]，指的是选择物化视图数据刷新的模式。

on commit指的是基表的数据有提交的时候触发刷新物化视图，使得物化视图中的数据和基本的数据是一致性的。

on demand指定是物化视图数据刷新的另外一种方式，仅在需要更新数据时才刷新物化视图中的数据。一般配合 start with 参数按照特定的时间计划，按计划更新数据，比如每天晚上12点或每周更新一次物化视图中的数据。

 **给一个子查询创建一下物化视图提高它的查询效率，子查询如下：** 

![1640237655926](Images/1640237655926.png)

创建物化视图，创建脚本如下：

```sql
 --创建物化视图需要权限
 grant create materialized view to student;  
 
 create materialized view student.mv_stuinfo 
 refresh force
 on demand
 start with sysdate next to_date(concat(to_char(sysdate+1,'dd-mm-yyyy'),'01:00:00'),'dd-mm-yyyy hh24:mi:ss') 
 as 
select t1.stuid, t1.stuname, t1.sex, t1.age, t2.classno, t2.classname
  from student.stuinfo t1, student.class t2
 where t1.classno = t2.classno;
```

创建好后，直接查询物化视图，可以发现已经有数据了，这时你可以随意在物化视图上加索引，进一步提高查询效率。

![1640237684695](Images/1640237684695.png)