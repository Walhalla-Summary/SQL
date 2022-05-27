2022年1月5日

派活第一天，只有一个需求，无任何相关操作，确实一脸懵逼，询问各位前辈，还是一脸懵逼，问了很多不懂的。。。。害



**目**    **录**

第一章    PL/SQL 程序设计简介... 4

§1.2  SQL与PL/SQL. 4

§1.2.1  什么是PL/SQL?. 4

§1.2.1  PL/SQL的好处... 4

§1.2.2 PL/SQL 可用的SQL语句... 5

§1.3  运行PL/SQL程序... 5

第二章  PL/SQL块结构和组成元素... 6

§2.1  PL/SQL块... 6

§2.2  PL/SQL结构... 6

§2.3  标识符... 6

§2.4  PL/SQL 变量类型... 7

§2.4.1 变量类型... 7

§2.4.2  复合类型... 9

§2.4.3 使用%ROWTYPE.. 11

§2.4.4 LOB类型*. 11

§2.4.5 Bind 变量... 11

§2.4.6 INDEX BY TABLES. 12

§2.4.7 数据类型的转换*. 13

§2.5  运算符和表达式(数据定义) 13

§2.5.1 关系运算符... 13

§2.5.2 一般运算符... 13

§2.5.3 逻辑运算符... 13

§2.6  变量赋值... 13

§2.6.1 字符及数字运算特点... 13

§2.6.2 BOOLEAN 赋值... 13

§2.6.3 数据库赋值... 13

§2.6.4 可转换的类型赋值... 13

§2.7  变量作用范围及可见性... 13

§2.8  注释... 13

§2.9  简单例子... 13

§2.9.1  简单数据插入例子... 13

§2.9.2  简单数据删除例子... 13

第三章 PL/SQL流程控制语句... 13

§3.1  条件语句... 13

§3.2  CASE 表达式... 13

§3.3  循环... 13

§3.3 标号和GOTO.. 13

§3.4 NULL 语句... 13

第四章 游标的使用... 13

§4.1 游标概念... 13

§4.1.1 处理显式游标... 13

§4.1.2 处理隐式游标... 13

§4.1.3 游标修改和删除操作... 13

第五章  异常错误处理... 13

§5.1 异常处理概念... 13

§5.1.1 预定义的异常处理... 13

§5.1.2 非预定义的异常处理... 13

§5.1.3 用户自定义的异常处理... 13

§5.1.4 用户定义的异常处理... 13

§5.2 异常错误传播... 13

§5.2.1 在执行部分引发异常错误... 13

§5.2.2 在声明部分引发异常错误... 13

§5.3 异常错误处理编程... 13

§5.4 在 PL/SQL 中使用 SQLCODE, SQLERRM... 13

第六章 存储函数和过程... 13

§6.1 引言... 13

§6.2 创建函数... 13

§6.3 存储过程... 13

§6.3.1 创建过程... 13

§6.3.2  调用存储过程... 13

§6.3.3 开发存储过程步骤... 13

§6.3.4 与过程相关数据字典... 13

第七章 包的创建和应用... 13

§7.1 引言... 13

§7.2 包的定义... 13

§7.3 包的开发步骤... 13

§7.4 包定义的说明... 13

§7.5 子程序重载... 13

§7.6 删除过程、函数和包... 13

§7.7 包的管理... 13

第八章 触发器... 13

§8.1 触发器类型... 13

§8.1.1 DML触发器... 13

§8.1.2 替代触发器... 13

§8.1.3 系统触发器... 13

§8.2 创建触发器... 13

§8.2.1 触发器触发次序... 13

§8.2.2 创建DML触发器... 13

§8.2.3 创建替代(Instead_of)触发器... 13

§8.2.3 创建系统事件触发器... 13

§8.2.4 系统触发器事件属性... 13

§8.2.5 使用触发器谓词... 13

§8.2.6 重新编译触发器... 13

§8.3 删除和使能触发器... 13

§8.4 触发器和数据字典... 13

§8.5  数据库触发器的应用举例... 13

 

**
**

# 第一章      PL/SQL 程序设计简介

 

PL /SQL是一种高级数据库程序设计语言，该语言专门用于在各种环境下对ORACLE数据库进行访问。由于该语言集成于数据库服务器中，所以PL/SQL代码可以对数据进行快速高效的处理。除此之外，可以在ORACLE数据库的某些客户端工具中，使用PL/SQL语言也是该语言的一个特点。本章的主要内容是讨论引入PL/SQL语言的必要性和该语言的主要特点，以及了解PL/SQL语言的重要性和数据库版本问题。还要介绍一些贯穿全书的更详细的高级概念，并在本章的最后就我们在本书案例中使用的数据库表的若干约定做一说明。

 

**本章主要重点：**

 

l PL/SQL概述

l PL/SQL块结构

l PL/SQL流程

l 运算符和表达式

l 游标

l 异常处理

l 数据库存储过程和函数

l 包

l 触发器

## §1.2  SQL与PL/SQL

### §1.2.1  什么是PL/SQL?

PL/SQL是 Procedure Language & Structured Query Language 的缩写。ORACLE的SQL是支持ANSI(American national Standards Institute)和ISO92 (International Standards Organization)标准的产品。PL/SQL是对SQL语言存储过程语言的扩展。从ORACLE6以后，ORACLE的RDBMS附带了PL/SQL。它现在已经成为一种过程处理语言，简称PL/SQL。目前的PL/SQL包括两部分，一部分是数据库引擎部分；另一部分是可嵌入到许多产品（如C语言，JAVA语言等）工具中的独立引擎。可以将这两部分称为：数据库PL/SQL和工具PL/SQL。两者的编程非常相似。都具有编程结构、语法和逻辑机制。工具PL/SQL另外还增加了用于支持工具（如ORACLE Forms）的句法，如：在窗体上设置按钮等。本章主要介绍数据库PL/SQL内容。

 

### §1.2.1  PL/SQL的好处

 

#### §1.2.1.1 有利于客户/服务器环境应用的运行

对于客户/服务器环境来说，真正的瓶颈是网络上。无论网络多快，只要客户端与服务器进行大量的数据交换。应用运行的效率自然就回受到影响。如果使用PL/SQL进行编程，将这种具有大量数据处理的应用放在服务器端来执行。自然就省去了数据在网上的传输时间。

 

#### §1.2.1.2 适合于客户环境

PL/SQL由于分为数据库PL/SQL部分和工具PL/SQL。对于客户端来说，PL/SQL可以嵌套到相应的工具中，客户端程序可以执行本地包含PL/SQL部分，也可以向服务发SQL命令或激活服务器端的PL/SQL程序运行。

 

 

### §1.2.2 PL/SQL 可用的SQL语句

  PL/SQL是ORACLE系统的核心语言，现在ORACLE的许多部件都是由PL/SQL写成。在PL/SQL中可以使用的SQL语句有：

 

INSERT，UPDATE，DELETE，SELECT INTO，COMMIT，ROLLBACK，SAVEPOINT。

 

**提示：在** **PL/SQL****中只能用** **SQL****语句中的** **DML** **部分，不能用** **DDL** **部分，如果要在****PL/SQL****中使用****DDL(****如****CREATE table** **等****)****的话，只能以动态的方式来使用。**

 

l ORACLE 的 PL/SQL 组件在对 PL/SQL 程序进行解释时，同时对在其所使用的表名、列名及数据类型进行检查。

l PL/SQL 可以在SQL*PLUS 中使用。

l PL/SQL 可以在高级语言中使用。

l PL/SQL可以 在ORACLE的 开发工具中使用。

l 其它开发工具也可以调用PL/SQL编写的过程和函数，如Power Builder 等都可以调用服务器端的PL/SQL过程。

## §1.3  运行PL/SQL程序

  PL/SQL程序的运行是通过ORACLE中的一个引擎来进行的。这个引擎可能在ORACLE的服务器端，也可能在 ORACLE 应用开发的客户端。引擎执行PL/SQL中的过程性语句，然后将SQL语句发送给数据库服务器来执行。再将结果返回给执行端。

 

 

**
**

# 第二章  PL/SQL块结构和组成元素

## §2.1  PL/SQL块

**PL/SQL**程序由三个块组成，即声明部分、执行部分、异常处理部分。

 

**PL/SQL****块的结构如下：**

 

**DECLARE** 

/* 声明部分: 在此声明PL/SQL用到的变量,类型及游标，以及局部的存储过程和函数 */

**BEGIN**

  /* 执行部分: 过程及SQL 语句 , 即程序的主要部分 */

**EXCEPTION**

  /* 执行异常部分: 错误处理 */

**END;**

 

其中 执行部分是必须的。

 

**PL/SQL****块可以分为三类：**

 

1. 无名块：动态构造，只能执行一次。
2. 子程序：存储在数据库中的存储过程、函数及包等。当在数据库上建立好后可以在其它程序中调用它们。
3. 触发器：当数据库发生操作时，会触发一些事件，从而自动执行相应的程序。

 

## §2.2  PL/SQL结构

l PL/SQL块中可以包含子块；

l 子块可以位于 PL/SQL中的任何部分；

l 子块也即PL/SQL中的一条命令；

 

## §2.3  标识符

PL/SQL程序设计中的标识符定义与SQL 的标识符定义的要求相同。要求和限制有：

l 标识符名不能超过30字符；

l 第一个字符必须为字母；

l 不分大小写；

l 不能用’-‘(减号);

l 不能是SQL保留字。

**提示****:** **一般不要把变量名声明与表中字段名完全一样****,****如果这样可能得到不正确的结果****.**

 

例如：下面的例子将会删除所有的纪录，而不是KING 的记录；

 

DECLARE

  Ename varchar2(20) :=’KING’;

BEGIN

​    DELETE FROM emp WHERE ename=ename;

END;

 

  变量命名在PL/SQL中有特别的讲究，建议在系统的设计阶段就要求所有编程人员共同遵守一定的要求，使得整个系统的文档在规范上达到要求。下面是建议的命名方法：

 

| 标识符            | 命名规则        | 例子            |
| ----------------- | --------------- | --------------- |
| 程序变量          | V_name          | V_name          |
| 程序常量          | C_Name          | C_company_name  |
| 游标变量          | Name_cursor     | Emp_cursor      |
| 异常标识          | E_name          | E_too_many      |
| 表类型            | Name_table_type | Emp_record_type |
| 表                | Name_table      | Emp             |
| 记录类型          | Name_record     | Emp_record      |
| SQL*Plus 替代变量 | P_name          | P_sal           |
| 绑定变量          | G_name          | G_year_sal      |

 

## §2.4  PL/SQL 变量类型

在前面的介绍中，有系统的数据类型，也可以自定义数据类型。下表是ORACLE类型和PL/SQL中的变量类型的合法使用列表：

 

### §2.4.1 变量类型

 

在ORACLE8i中可以使用的变量类型有：

| 类型           | 子类                                               | 说   明                                                      | 范  围                                   | ORACLE限制 |
| -------------- | -------------------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- | ---------- |
| CHAR           | CharacterStringRowidNchar                          | 定长字符串 民族语言字符集                                    | 0à32767可选,确省=1                       | 2000       |
| VARCHAR2       | Varchar, StringNVARCHAR2                           | 可变字符串民族语言字符集                                     | 0à327674000                              | 4000       |
| BINARY_INTEGER |                                                    | 带符号整数,为整数计算优化性能                                |                                          |            |
| NUMBER(p,s)    | Dec Double precisionIntegerIntNumericRealSmall int | 小数, NUMBER 的子类型高精度实数整数, NUMBER 的子类型整数, NUMBER 的子类型与NUMBER等价与NUMBER等价整数, 比 integer 小 |                                          |            |
| LONG           |                                                    | 变长字符串                                                   | 0->2147483647                            | 32,767字节 |
| DATE           |                                                    | 日期型                                                       | 公元前4712年1月1日至公元后4712年12月31日 |            |
| BOOLEAN        |                                                    | 布尔型                                                       | TRUE, FALSE,NULL                         | 不使用     |
| ROWID          |                                                    | 存放数据库行号                                               |                                          |            |
| UROWID         |                                                    | 通用行标识符，字符类型                                       |                                          |            |
|                |                                                    |                                                              |                                          |            |

 

例1.    插入一条记录并显示；

 

DECLARE

  Row_id UROWID;

  info  VARCHAR2(40);

BEGIN

​    INSERT INTO dept VALUES (90, ‘SERVICE’, ‘BEIJING’)

​     *RETURNING rowid, dname||’:’||to_char(deptno)||’:’||loc*

​           INTO row_id, info;

​    DBMS_OUTPUT.PUT_LINE(‘ROWID:’||row_id);

​    DBMS_OUTPUT.PUT_LINE(info);

END;

 

其中：RETURNING子句用于检索INSERT语句中所影响的数据行数，当INSERT语句使用VALUES 子句插入数据时，RETURNING 字句还可将列表达式、ROWID和REF值返回到输出变量中。在使用RETURNING 子句是应注意以下几点限制：

1．不能并行DML语句和远程对象一起使用；

2．不能检索LONG 类型信息；

3．当通过视图向基表中插入数据时，只能与单基表视图一起使用。

 

**例****2.** 修改一条记录并显示

 

DECLARE

  Row_id UROWID;

  info  VARCHAR2(40);

BEGIN

​    UPDATE dept SET deptno=80 WHERE DNAME=‘SERVICE’

​       RETURNING rowid, dname||’:’||to_char(deptno)||’:’||loc

​           INTO row_id, info;

​    DBMS_OUTPUT.PUT_LINE(‘ROWID:’||row_id);

​    DBMS_OUTPUT.PUT_LINE(info);

END;

 

其中：RETURNING子句用于检索被修改行信息：当UPDATE语句修改单行数据时，RETURNING 子句可以检索被修改行的ROWID和REF值，以及行中被修改列的列表达式，并可将他们存储到PL/SQL变量或复合变量中；当UPDATE语句修改多行数据时，RETURNING 子句可以将被修改行的ROWID和REF值，以及列表达式值返回到复合变量数组中。在UPDATE中使用RETURNING 子句的限制与INSERT语句中对RETURNING子句的限制相同。

 

**例****3.** 删除一条记录并显示

 

DECLARE

  Row_id UROWID;

  info  VARCHAR2(40);

BEGIN

​    DELETE dept WHERE DNAME=‘SERVICE’

​       RETURNING rowid, dname||’:’||to_char(deptno)||’:’||loc

​           INTO row_id, info;

​    DBMS_OUTPUT.PUT_LINE(‘ROWID:’||row_id);

​    DBMS_OUTPUT.PUT_LINE(info);

END;

 

其中：RETURNING子句用于检索被修改行信息：当UPDATE语句修改单行数据时，RETURNING 子句可以检索被修改行的ROWID和REF值，以及行中被修改列的列表达式，并可将他们存储到PL/SQL变量或复合变量中；当UPDATE语句修改多行数据时，RETURNING 子句可以将被修改行的ROWID和REF值，以及列表达式值返回到复合变量数组中。在UPDATE中使用RETURNING 子句的限制与INSERT语句中对RETURNING子句的限制相同。

 

### §2.4.2  复合类型

  ORACLE 在 PL/SQL 中除了提供象前面介绍的各种类型外,还提供一种称为复合类型的类型---记录和表.

 

#### §2.4.2.1 记录类型

记录类型是把逻辑相关的数据作为一个单元存储起来，它必须包括至少一个标量型或RECORD 数据类型的成员，称作PL/SQL RECORD 的域(FIELD)，其作用是存放互不相同但逻辑相关的信息。

 

**定义记录类型语法如下****:**

 

TYPE record_type IS RECORD(

  Field1 type1 [NOT NULL] [:= exp1 ],

  Field2 type2 [NOT NULL] [:= exp2 ],

  . . .  . . .

  Fieldn typen [NOT NULL] [:= expn ] ) ;

 

**例****4** **：**

 

DECLARE

  TYPE test_rec IS RECORD(

​     Code VARCHAR2(10),

​     Name VARCHAR2(30) NOT NULL :=’a book’);

  V_book test_rec;

BEGIN

  V_book.code :=’123’;

  V_book.name :=’C++ Programming’;

  DBMS_OUTPUT.PUT_LINE(v_book.code||v_book.name);

END;

 

   可以用 SELECT语句对记录变量进行赋值,只要保证记录字段与查询结果列表中的字段相配即可。

 

#### §2.4.2.2 使用%TYPE

定义一个变量，其数据类型与已经定义的某个数据变量的类型相同，或者与数据库表的某个列的数据类型相同，这时可以使用%TYPE。

使用%TYPE特性的优点在于：

l 所引用的数据库列的数据类型可以不必知道；

l 所引用的数据库列的数据类型可以实时改变。

 

**例****5****：**

DECLARE

  -- 用 %TYPE 类型定义与表相配的字段

  TYPE t_Record IS RECORD(

​      T_no emp.empno%TYPE,

​      T_name emp.ename%TYPE,

​      T_sal emp.sal%TYPE );

  -- 声明接收数据的变量

  v_emp t_Record;

BEGIN

  SELECT empno, ename, sal INTO v_emp FROM emp WHERE empno=7788;

  DBMS_OUTPUT.PUT_LINE

(TO_CHAR(v_emp.t_no)||v_emp.t_name||TO_CHAR(v_emp.t_sal));

END;

 

**例****6****：**

DECLARE

  v_empno emp.empno%TYPE :=&empno;

  Type r_record is record (

​    v_name  emp.ename%TYPE,

​    v_sal   emp.sal%TYPE,

​    v_date   emp.hiredate%TYPE);

  Rec r_record;

BEGIN

  SELECT ename, sal, hiredate INTO Rec FROM emp WHERE empno=v_empno;

  DBMS_OUTPUT.PUT_LINE(Rec.v_name||'---'||Rec.v_sal||'--'||Rec.v_date);

END;

 

### §2.4.3 使用%ROWTYPE

PL/SQL 提供%ROWTYPE操作符, 返回一个记录类型, 其数据类型和数据库表的数据结构相一致。

使用%ROWTYPE特性的优点在于：

l 所引用的数据库中列的个数和数据类型可以不必知道；

l 所引用的数据库中列的个数和数据类型可以实时改变。

 

**例****7****：**

DECLARE

  v_empno emp.empno%TYPE :=&empno;

  rec emp%ROWTYPE;

BEGIN

  SELECT * INTO rec FROM emp WHERE empno=v_empno;

  DBMS_OUTPUT.PUT_LINE('姓名:'||rec.ename||'工资:'||rec.sal||'工作时间:'||rec.hiredate);

END;

 

### §2.4.4 LOB类型*

  ORACLE提供了LOB (Large OBject)类型，用于存储大的数据对象的类型。ORACLE目前主要支持BFILE, BLOB, CLOB 及 NCLOB 类型。

 

**BFILE (Movie)**

  存放大的二进制数据对象，这些数据文件不放在数据库里，而是放在操作系统的某个目录里，数据库的表里只存放文件的目录。

 

**BLOB(Photo)**

  存储大的二进制数据类型。变量存储大的二进制对象的位置。大二进制对象的大小<=4GB。

 

**CLOB(Book)**

  存储大的字符数据类型。每个变量存储大字符对象的位置，该位置指到大字符数据块。大字符对象的大小<=4GB。

 

**NCLOB**

  存储大的NCHAR字符数据类型。每个变量存储大字符对象的位置，该位置指到大字符数据块。大字符对象的大小<=4GB。

 

### §2.4.5 Bind 变量

绑定变量是在主机环境中定义的变量。在PL/SQL 程序中可以使用绑定变量作为他们将要使用的其它变量。为了在PL/SQL 环境中声明绑定变量，使用命令VARIABLE。例如：

VARIABLE return_code NUMBER

VARIABLE return_msg VARCHAR2(20)

 

可以通过SQL*Plus命令中的PRINT 显示绑定变量的值。例如：

PRINT return_code

PRINT return_msg

 

**例****7****：**

 

VARIABLE result NUMBER

 

BEGIN

​    SELECT (sal*12)+nvl(comm, 0) INTO :result FROM emp WHERE empno=7788;

END;

 

PRINT result

 

### §2.4.6 INDEX BY TABLES

 

包括两个基本成分:

．数据处理类型为BINARY_INTEGER主键;

．标量或记录数据类型的列．

 

TYPE type_name IS TABLE OF

​    {column_type | variable%TYPE | table.column%TYPE } [NOT NULL] | table%ROWTYPE

​    [ INDEX BY BINARY_INTEGER];

 

| 方法      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| EXISTS(n) | Return TRUE if the nth element in a PL/SQL table exists;     |
| COUNT     | Returns the number of elements that a PL/SQL table currently contains; |
| FIRSTLAST | Return the first and last (smallest and lastest) index numbers in a PL/SQL table. Returns NULL if the PL/SQL table is empty. |
| PRIOR(n)  | Returns the index number that precedes index n in a PL/SQL table; |
| NEXT(N)   | Returns the index number that succeeds index n in a PL/SQL table; |
| TRIM      | TRIM removes one element from the end of a PL/SQL table.TRIM(n) removes n element from the end of a PL/SQL table. |
| DELETE    | DELETE removes all elements from a PL/SQL table.DELETE(n) removes the nth elements from a PL/SQL table.DELETE(m, n) removes all elements in the range m to n from a PL/SQL table. |

 

**例****8****：**

 

DECLARE

​    TYPE dept_table_type IS TABLE OF

​       dept%ROWTYPE INDEX BY BINARY_INTEGER;

​    my_dname_table dept_table_type;

​    v_count number(2) :=4;

BEGIN

​    FOR int IN 1 .. v_count LOOP

​       SELECT * INTO my_dname_table(int) FROM dept WHERE deptno=int*10;

​    END LOOP;

​    FOR int IN my_dname_table.FIRST .. my_dname_table.LAST LOOP

​       DBMS_OUTPUT.PUT_LINE(‘Department number: ‘||my_dname_table(int).deptno);

​       DBMS_OUTPUT.PUT_LINE(‘Department name: ‘|| my_dname_table(int).dname);

​    END LOOP;

END;

 

 

### §2.4.7 数据类型的转换*

 

*隐式类型转换*

|              | **BIN_INT** | **CHAR** | **DATE** | **LONG** | **NUMBER** | **PLS_INT** | **UROWID** | **VARCHAR2** |
| ------------ | ----------- | -------- | -------- | -------- | ---------- | ----------- | ---------- | ------------ |
| **BIN_INT**  |            |          |         |          |            |             |           |              |
| **CHAR**     |             |         |          |          |            |             |            |              |
| **DATE**     |            |          |         |          |           |            |           |              |
| **LONG**     |            |          |         |         |           |            |           |              |
| **NUMBER**   |             |          |         |          |           |             |           |              |
| **RAW**      |            |          |         |          |           |            |           |              |
| **UROWID**   |            |          |         |         |           |            |           |              |
| **VARCHAR2** |             |          |          |          |            |             |            |             |

 

 

## §2.5  运算符和表达式(数据定义)

### §2.5.1 关系运算符

 

| 运算符            | **意义**   |
| ----------------- | ---------- |
| =                 | 等于       |
| <> , != , ~= , ^= | 不等于     |
| <                 | 小于       |
| >                 | 大于       |
| <=                | 小于或等于 |
| >=                | 大于或等于 |

 

 

### §2.5.2 一般运算符

 

| 运算符 | **意义**   |
| ------ | ---------- |
| +      | 加号       |
| -      | 减号       |
| *      | 乘号       |
| /      | 除号       |
| :=     | 赋值号     |
| =>     | 关系号     |
| ..     | 范围运算符 |
| \|\|   | 字符连接符 |

 

### §2.5.3 逻辑运算符

 

| 运算符  | **意义**                   |
| ------- | -------------------------- |
| IS NULL | 是空值                     |
| BETWEEN | 介于两者之间               |
| IN      | 在一列值中间               |
| AND     | 逻辑与                     |
| OR      | 逻辑或                     |
| NOT     | 取返,如IS NOT NULL, NOT IN |

 

## §2.6  变量赋值

在PL/SQL编程中，变量赋值是一个值得注意的地方，它的语法如下：

  variable := expression ;

  variable 是一个PL/SQL变量, expression 是一个PL/SQL 表达式.

 

### §2.6.1 字符及数字运算特点

 

空值加数字仍是空值：NULL + < 数字> = NULL

 

空值加（连接）字符，结果为字符：NULL || <字符串> = < 字符串>

 

### §2.6.2 BOOLEAN 赋值

 

布尔值只有TRUE, FALSE及 NULL 三个值。如：

 

DECLARE

done BOOLEAN;

/* the following statements are legal: */

BEGIN

done := FALSE;

WHILE NOT done LOOP

Null;

END LOOP;

END;

 

### §2.6.3 数据库赋值

 

  数据库赋值是通过 SELECT语句来完成的，每次执行 SELECT语句就赋值一次，一般要求被赋值的变量与SELECT中的列名要一一对应。如：

**例****9****：**

 

DECLARE

emp_id   emp.empno%TYPE :=7788;

emp_name emp.ename%TYPE;

wages   emp.sal%TYPE;

BEGIN

SELECT ename, NVL(sal,0) + NVL(comm,0) INTO emp_name, wages

FROM emp WHERE empno = emp_id;

Dbms_output.put_line(emp_name||’----‘||to_char(wages));

END;

 

**提示：不能将****SELECT****语句中的列赋值给布尔变量。**

 

### §2.6.4 可转换的类型赋值

 

l **CHAR** **转换为** **NUMBER****：**

使用 TO_NUMBER 函数来完成字符到数字的转换，如：

v_total := TO_NUMBER(‘100.0’) + sal;

 

l **NUMBER** **转换为****CHAR****：**

  使用 TO_CHAR函数可以实现数字到字符的转换，如：

v_comm := TO_CHAR(‘123.45’) || ’元’ ;

 

l **字符转换为日期：**

使用 TO_DATE函数可以实现 字符到日期的转换，如：

v_date := TO_DATE('2001.07.03','yyyy.mm.dd');

 

l **日期转换为字符**

使用 TO_CHAR函数可以实现日期到字符的转换，如：

v_to_day := TO_CHAR(SYSDATE, 'yyyy.mm.dd hh24:mi:ss') ;

 

## §2.7  变量作用范围及可见性

在PL/SQL编程中，如果在变量的定义上没有做到统一的话，可能会隐藏一些危险的错误，这样的原因主要是变量的作用范围所致。与其它高级语言类似，PL/SQL的变量作用范围特点是：

l 变量的作用范围是在你所引用的程序单元（块、子程序、包）内。即从声明变量开始到该块的结束。

l 一个变量（标识）只能在你所引用的块内是可见的。

l 当一个变量超出了作用范围，PL/SQL引擎就释放用来存放该变量的空间（因为它可能不用了）。

l 在子块中重新定义该变量后，它的作用仅在该块内。

 

**例****10****：**

DECLARE

  Emess char(80);

BEGIN

 

  DECLARE

   V1 NUMBER(4);

  BEGIN

   SELECT empno INTO v1 FROM emp WHERE LOWER(job)=’president’;

​     DBMS_OUTPUT.PUT_LINE(V1);

  EXCEPTION

   When TOO_MANY_ROWS THEN

​     DBMS_OUTPUT.PUT_LINE (‘More than one president’);

  END;

 

  DECLARE

   V1 NUMBER(4);

  BEGIN

   SELECT empno INTO v1 FROM emp WHERE LOWER(job)=’manager’;

  EXCEPTION

   When TOO_MANY_ROWS THEN

​     DBMS_OUTPUT.PUT_LINE (‘More than one manager’);

  END;

 

EXCEPTION

  When others THEN

   Emess:=substr(SQLERRM,1,80);

   DBMS_OUTPUT.PUT_LINE (emess);

END;

## §2.8  注释

  在PL/SQL里，可以使用两种符号来写注释，即：

l 使用双 ‘-‘ ( 减号) 加注释

PL/SQL允许用 – 来写注释，它的作用范围是只能在一行有效。如：

V_Sal NUMBER(12,2); -- 工资变量。

 

l 使用 /*  */ 来加一行或多行注释，如：

/***********************************************/

/* 文件名： statistcs_sal.sql      */

/***********************************************/

 

**提示：被解释存放在数据库中的** **PL/SQL** **程序，一般系统自动将程序头部的注释去掉。只有在** **PROCEDURE** **之后的注释才被保留；另外程序中的空行也自动被去掉。**

## §2.9  简单例子

### §2.9.1  简单数据插入例子

 

**例****11****：**

/* 本例子仅是一个简单的插入，不是实际应用。 */

DECLARE

v_ename  VARCHAR2(20) := ‘Bill’;

v_sal    NUMBER(7,2) :=1234.56;

v_deptno  NUMBER(2) := 10;

v_empno  NUMBER(4) := 8888;

BEGIN

INSERT INTO emp ( empno, ename, JOB, sal, deptno , hiredate ) 

VALUES ( v_empno, v_ename, ‘Manager’, v_sal, v_deptno,

TO_DATE(’1954.06.09’,’yyyy.mm.dd’) );

COMMIT;

END;

 

### §2.9.2  简单数据删除例子

**例****12****：**

/* 本例子仅是一个简单的删除例子，不是实际应用。 */

 DECLARE

v_empno  number(4) := 8888;

BEGIN

DELETE FROM emp WHERE empno=v_empno;

COMMIT;

END;

 

**
**

# 第三章 PL/SQL流程控制语句

 

介绍PL/SQL的流程控制语句, 包括如下三类:

l 控制语句: IF 语句

l 循环语句: LOOP语句, EXIT语句

l 顺序语句: GOTO语句, NULL语句

## §3.1  条件语句

IF <布尔表达式> THEN

PL/SQL 和 SQL语句

END IF;

 

IF <布尔表达式> THEN

PL/SQL 和 SQL语句

ELSE

其它语句

END IF;

 

IF <布尔表达式> THEN

PL/SQL 和 SQL语句

ELSIF < 其它布尔表达式> THEN

其它语句

ELSIF < 其它布尔表达式> THEN

其它语句

ELSE

其它语句

END IF;

 

**提示****: ELSIF** **不能写成** **ELSEIF**

 

**例****1:**

DECLARE

  v_empno emp.empno%TYPE :=&empno;

  V_salary emp.sal%TYPE;

  V_comment VARCHAR2(35);

BEGIN

  SELECT sal INTO v_salary FROM emp WHERE empno=v_empno;

  IF v_salary<1500 THEN

​    V_comment:= ‘Fairly less’;

  ELSIF v_salary <3000 THEN

   V_comment:= ‘A little more’;

  ELSE

   V_comment:= ‘Lots of salary’;

  END IF;

  DBMS_OUTPUT.PUT_LINE(V_comment);

END;

 

## §3.2  CASE 表达式

CASE selector

​    WHEN expression1 THEN result1

​    WHEN expression2 THEN result2

 

​    WHEN expressionN THEN resultN

​    [ ELSE resultN+1]

END;

 

**例****2:**

 

DECLARE

​    V_grade char(1) := UPPER(‘&p_grade’);

​    V_appraisal VARCHAR2(20);

BEGIN

​    V_appraisal :=

​    CASE v_grade

​       WHEN ‘A’ THEN ‘Excellent’

​       WHEN ‘B’ THEN ‘Very Good’

​       WHEN ‘C’ THEN ‘Good’

​       ELSE ‘No such grade’

​    END;

​    DBMS_OUTPUT.PUT_LINE(‘Grade:‘||v_grade||’ Appraisal: ‘|| v_appraisal);

END;

 

 

## §3.3  循环

 **1.** **简单循环**

LOOP

   要执行的语句;

   EXIT WHEN <条件语句>    /*条件满足，退出循环语句*/

END LOOP;

 

**例** **3.**

DECLARE

  int NUMBER(2) :=0;

BEGIN

  LOOP

​    int := int + 1;

   DBMS_OUTPUT.PUT_LINE('int 的当前值为:'||int);

​    EXIT WHEN int =10;

  END LOOP;

END;

 

**2. WHILE** **循环**

 

WHILE <布尔表达式> LOOP

  要执行的语句;

END LOOP;

 

**例****4.**

DECLARE

x NUMBER;

BEGIN

  x:= 1;

  WHILE x<10 LOOP

   DBMS_OUTPUT.PUT_LINE('X的当前值为:'||x);

​    x:= x+1;

  END LOOP;

END;

 

**3.** **数字式循环**

FOR 循环计数器 IN [ REVERSE ] 下限 .. 上限 LOOP

 要执行的语句;

END LOOP;

每循环一次，循环变量自动加1；使用关键字REVERSE，循环变量自动减1。跟在IN REVERSE 后面的数字必须是从小到大的顺序，而且必须是整数，不能是变量或表达式。可以使用EXIT 退出循环。

 

**例****5.**

BEGIN

  FOR int  in 1..10 LOOP

​    DBMS_OUTPUT.PUT_LINE('int 的当前值为: '||int);

  END LOOP;

END;

 

**例** **6.**

CREATE TABLE temp_table(num_col NUMBER);

 

DECLARE

V_counter NUMBER := 10;

BEGIN

  INSERT INTO temp_table(num_col) VALUES (v_counter );

  FOR v_counter IN 20 .. 25 LOOP

​    INSERT INTO temp_table (num_col ) VALUES ( v_counter );

  END LOOP;

  INSERT INTO temp_table(num_col) VALUES (v_counter );

  FOR v_counter IN REVERSE 20 .. 25 LOOP

​    INSERT INTO temp_table (num_col ) VALUES ( v_counter );

  END LOOP;

END ;

 

DROP TABLE temp_table;

## §3.3 标号和GOTO

PL/SQL中GOTO语句是无条件跳转到指定的标号去的意思。语法如下：

 

**GOTO  label;**

 **. . . . . .**

<<label>>　/*标号是用<<　>>括起来的标识符 */

 

**例****7:**

DECLARE

  V_counter NUMBER := 1;

BEGIN

  LOOP

   DBMS_OUTPUT.PUT_LINE('V_counter的当前值为:'||V_counter);

 V_counter := v_counter + 1;

 IF v_counter > 10 THEN

   GOTO l_ENDofLOOP;

 END IF;

  END LOOP;

 <<l_ENDofLOOP>>

   DBMS_OUTPUT.PUT_LINE('V_counter的当前值为:'||V_counter);

END ;

## §3.4 NULL 语句

在PL/SQL 程序中，可以用 null 语句来说明“不用做任何事情”的意思，相当于一个占位符，可以使某些语句变得有意义，提高程序的可读性。如：

DECLARE

. . .

BEGIN

…

IF v_num IS NULL THEN

GOTO print1;

END IF;

…

<<print1>>

NULL; -- 不需要处理任何数据。

END;

 

**
**

# 第四章 游标的使用

  在 PL/SQL 程序中，对于处理多行记录的事务经常使用游标来实现。

## §4.1 游标概念

 为了处理 SQL 语句，ORACLE 必须分配一片叫上下文( context area )的区域来处理所必需的信息，其中包括要处理的行的数目，一个指向语句被分析以后的表示形式的指针以及查询的活动集(active set)。

 游标是一个指向上下文的句柄( handle)或指针。通过游标，PL/SQL可以控制上下文区和处理语句时上下文区会发生些什么事情。

​    对于不同的SQL语句，游标的使用情况不同：

| SQL语句              | 游标           |
| -------------------- | -------------- |
| 非查询语句           | 隐式的         |
| 结果是单行的查询语句 | 隐式的或显示的 |
| 结果是多行的查询语句 | 显示的         |

 

### §4.1.1 处理显式游标

 

1. **1.** **显式游标处理**

显式游标处理需四个 PL/SQL步骤:

l **定义游标：**就是定义一个游标名，以及与其相对应的SELECT 语句。

格式：

CURSOR cursor_name[(parameter[, parameter]…)] IS select_statement;

​    游标参数只能为输入参数，其格式为：

​       parameter_name [IN] datatype [{:= | DEFAULT} expression]

​    在指定数据类型时，不能使用长度约束。如NUMBER(4)、CHAR(10) 等都是错误的。

l **打开游标：**就是执行游标所对应的SELECT 语句，将其查询结果放入工作区，并且指针指向工作区的首部，标识游标结果集合。如果游标查询语句中带有FOR UPDATE选项，OPEN 语句还将锁定数据库表中游标结果集合对应的数据行。

格式：

OPEN cursor_name[([parameter =>] value[, [parameter =>] value]…)];

在向游标传递参数时，可以使用与函数参数相同的传值方法，即位置表示法和名称表示   法。PL/SQL 程序不能用OPEN 语句重复打开一个游标。

l **提取游标数据：**就是检索结果集合中的数据行，放入指定的输出变量中。

格式：

FETCH cursor_name INTO {variable_list | record_variable };

l 对该记录进行处理；

l 继续处理，直到活动集合中没有记录；

l **关闭游标：**当提取和处理完游标结果集合数据后，应及时关闭游标，以释放该游标所占用的系统资源，并使该游标的工作区变成无效，不能再使用FETCH 语句取其中数据。关闭后的游标可以使用OPEN 语句重新打开。

格式：

CLOSE cursor_name;

**注：定义的游标不能有****INTO** **子句。**

 

**例****1.** 游标参数的传递方法。

DECLARE

​    DeptRec dept%ROWTYPE;

​    Dept_name dept.dname%TYPE;

​    Dept_loc dept.loc%TYPE;

​    CURSOR c1 IS

SELECT dname, loc FROM dept WHERE deptno <= 30;

​    CURSOR c2(dept_no NUMBER DEFAULT 10) IS

​       SELECT dname, loc FROM dept WHERE deptno <= dept_no;

​    CURSOR c3(dept_no NUMBER DEFAULT 10) IS

​       SELECT * FROM dept WHERE deptno <=dept_no;

BEGIN

​    OPEN c1;

​    LOOP

​       FETCH c1 INTO dept_name, dept_loc;

​       EXIT WHEN c1%NOTFOUND;

​       DBMS_OUTPUT.PUT_LINE(dept_name||’---‘||dept_loc);

​    END LOOP;

​    CLOSE c1;

 

​    OPEN c2;

​    LOOP

​       FETCH c2 INTO dept_name, dept_loc;

​       EXIT WHEN c2%NOTFOUND;

​       DBMS_OUTPUT.PUT_LINE(dept_name||’---‘||dept_loc);

​    END LOOP;

​    CLOSE c2;

 

​    OPEN c3(dept_no =>20);

​    LOOP

​       FETCH c3 INTO deptrec;

​       EXIT WHEN c3%NOTFOUND;

​       DBMS_OUTPUT.PUT_LINE(deptrec.deptno||’---‘||deptrec.dname

||’---‘||deptrec.loc);

​    END LOOP;

​    CLOSE c3;

END;

 

**2.****游标属性**

 %FOUND    布尔型属性，当最近一次读记录时成功返回,则值为TRUE；

 %NOTFOUND  布尔型属性，与%FOUND相反；

 %ISOPEN    布尔型属性，当游标已打开时返回 TRUE；

 %ROWCOUNT  数字型属性，返回已从游标中读取的记录数。

 

**例****2****：**给工资低于1200 的员工增加工资50。

DECLARE

  v_empno emp.empno%TYPE;

  v_sal   emp.sal%TYPE;

  CURSOR c IS SELECT empno, sal FROM emp;

BEGIN

  OPEN c;

  LOOP

   FETCH c INTO v_empno, v_sal;

​    EXIT WHEN C%NOTFOUND;

   IF v_sal<=1200 THEN

​      UPDATE emp SET sal=sal+50 WHERE empno=v_empno;

​       DBMS_OUTPUT.PUT_LINE('编码为'||v_empno||'工资已更新!');

END IF;

DBMS_OUTPUT.PUT_LINE('记录数:'||C%ROWCOUNT);

  END LOOP;

  CLOSE c;

END;

 

**3.** **游标的****FOR****循环**

  PL/SQL语言提供了游标FOR循环语句，自动执行游标的OPEN、FETCH、CLOSE语句和循环语句的功能；当进入循环时，游标FOR循环语句自动打开游标，并提取第一行游标数据，当程序处理完当前所提取的数据而进入下一次循环时，游标FOR循环语句自动提取下一行数据供程序处理，当提取完结果集合中的所有数据行后结束循环，并自动关闭游标。

格式：

​    FOR index_variable IN cursor_name[value[, value]…] LOOP

​       -- 游标数据处理代码

​    END LOOP;

其中：

​    index_variable为游标FOR 循环语句隐含声明的索引变量，该变量为记录变量，其结构与游标查询语句返回的结构集合的结构相同。在程序中可以通过引用该索引记录变量元素来读取所提取的游标数据，index_variable中各元素的名称与游标查询语句选择列表中所制定的列名相同。如果在游标查询语句的选择列表中存在计算列，则必须为这些计算列指定别名后才能通过游标FOR 循环语句中的索引变量来访问这些列数据。

**注：不要在程序中对游标进行人工操作；不要在程序中定义用于控制****FOR** **循环的记录。**

 

**例****3****：**

DECLARE

  CURSOR c_sal IS SELECT empno, ename, sal FROM emp ;

BEGIN

--隐含打开游标

  FOR v_sal IN c_sal LOOP

  --隐含执行一个FETCH语句

​       DBMS_OUTPUT.PUT_LINE( to_char(v_sal.empno)||’---‘||

v_sal.ename||’---‘||to_char(v_sal.sal)) ;

  --隐含监测c_sal%NOTFOUND

  END LOOP;

--隐含关闭游标

END;

 

**例****4****：**当所声明的游标带有参数时，通过游标FOR 循环语句为游标传递参数。

DECLARE

​    CURSOR c1(dept_no NUMBER DEFAULT 10) IS

​       SELECT dname, loc FROM dept WHERE deptno <= dept_no;

BEGIN

​    DBMS_OUTPUT.PUT_LINE(‘dept_no参数值为30：’);

​    FOR c1_rec IN c1(30) LOOP

​       DBMS_OUTPUT.PUT_LINE(c1_rec.dname||’---‘||c1_rec.loc);

​    END LOOP;

 

​    DBMS_OUTPUT.PUT_LINE(CHR(10)||’使用默认的dept_no参数值10：’);

​    FOR c1_rec IN c1 LOOP

​       DBMS_OUTPUT.PUT_LINE(c1_rec.dname||’---‘||c1_rec.loc);

​    END LOOP;

END;

 

**例****5****：**PL/SQL还允许在游标FOR循环语句中使用子查询来实现游标的功能。

BEGIN

​    FOR c1_rec IN (SELECT dname, loc FROM dept) LOOP

​       DBMS_OUTPUT.PUT_LINE(c1_rec.dname||’---‘||c1_rec.loc);

​    END LOOP;

END;

 

### §4.1.2 处理隐式游标

显式游标主要是用于对查询语句的处理，尤其是在查询结果为多条记录的情况下；而对于非查询语句，如修改、删除操作，则由ORACLE 系统自动地为这些操作设置游标并创建其工作区，这些由系统隐含创建的游标称为隐式游标，隐式游标的名字为SQL，这是由ORACLE 系统定义的。对于隐式游标的操作，如定义、打开、取值及关闭操作，都由ORACLE 系统自动地完成，无需用户进行处理。用户只能通过隐式游标的相关属性，来完成相应的操作。在隐式游标的工作区中，所存放的数据是与用户自定义的显示游标无关的、最新处理的一条SQL 语句所包含的数据。

格式调用为： SQL%

 

注：INSERT, UPDATE, DELETE, SELECT 语句中不必明确定义游标。

 

**隐式游标属性**

 SQL%FOUND    布尔型属性,当最近一次读记录时成功返回，则值为true；

 SQL%NOTFOUND  布尔型属性,与%found相反；

 SQL %ROWCOUNT 数字型属性, 返回已从游标中读取得记录数；

 SQL %ISOPEN  布尔型属性, 取值总是FALSE。SQL命令执行完毕立即关闭隐式游标。

 

**例****6:** 删除EMP 表中某部门的所有员工，如果该部门中已没有员工，则在DEPT 表中删除该部门。

DECLARE

V_deptno emp.deptno%TYPE :=&p_deptno;

BEGIN

​    DELETE FROM emp WHERE deptno=v_deptno;

​    IF SQL%NOTFOUND THEN

​       DELETE FROM dept WHERE deptno=v_deptno;

​    END IF;

END;

 

 

### §4.1.3 游标修改和删除操作

游标修改和删除操作是指在游标定位下，修改或删除表中指定的数据行。这时，要求游标查询语句中必须使用FOR UPDATE选项，以便在打开游标时锁定游标结果集合在表中对应数据行的所有列和部分列。

为了对正在处理(查询)的行不被另外的用户改动，ORACLE 提供一个 FOR UPDATE 子句来对所选择的行进行锁住。该需求迫使ORACLE锁定游标结果集合的行，可以防止其他事务处理更新或删除相同的行，直到您的事务处理提交或回退为止。

语法：

**SELECT . . . FROM … FOR UPDATE [OF column[, column]…] [NOWAIT]**

 

  如果另一个会话已对活动集中的行加了锁，那么SELECT FOR UPDATE操作一直等待到其它的会话释放这些锁后才继续自己的操作，对于这种情况，当加上NOWAIT子句时，如果这些行真的被另一个会话锁定，则OPEN立即返回并给出：

ORA-0054 ：resource busy and acquire with nowait specified.

 

  如果使用 FOR UPDATE 声明游标，则可在DELETE和UPDATE 语句中使用WHERE CURRENT OF cursor_name子句，修改或删除游标结果集合当前行对应的数据库表中的数据行。

 

**例****7****：**从EMP表中查询某部门的员工情况，将其工资最低定为 1500；

 

DECLARE

V_deptno emp.deptno%TYPE :=&p_deptno;

​    CURSOR emp_cursor IS SELECT empno, sal

FROM emp WHERE deptno=v_deptno FOR UPDATE OF sal NOWAIT;

BEGIN

​    FOR emp_record IN emp_cursor LOOP

IF emp_record.sal < 1500 THEN

​    UPDATE emp SET sal=1500 WHERE CURRENT OF emp_cursor;

END IF;

​    END LOOP;

--   COMMIT;

END;

 

**
**

# 第五章   异常错误处理

  一个优秀的程序都应该能够正确处理各种出错情况，并尽可能从错误中恢复。ORACLE 提供异常情况(EXCEPTION)和异常处理(EXCEPTION HANDLER)来实现错误处理。

## §5.1 异常处理概念

异常情况处理(EXCEPTION)是用来处理正常执行过程中未预料的事件,程序块的异常处理预定义的错误和自定义错误,由于PL/SQL程序块一旦产生异常而没有指出如何处理时,程序就会自动终止整个程序运行.

有三种类型的异常错误：

1． 预定义 ( Predefined )错误

ORACLE预定义的异常情况大约有24个。对这种异常情况的处理，无需在程序中定义，由ORACLE自动将其引发。

2． 非预定义 ( Predefined )错误

即其他标准的ORACLE错误。对这种异常情况的处理，需要用户在程序中定义，然后由ORACLE自动将其引发。

3． 用户定义(User_define) 错误

程序执行过程中，出现编程人员认为的非正常情况。对这种异常情况的处理，需要用户在程序中定义，然后显式地在程序中将其引发。

 

异常处理部分一般放在 PL/SQL 程序体的后半部,结构为:

EXCEPTION

  WHEN first_exception THEN  <code to handle first exception >

  WHEN second_exception THEN  <code to handle second exception >

  WHEN OTHERS THEN <code to handle others exception >

END;

异常处理可以按任意次序排列,但 OTHERS 必须放在最后.

 

### §5.1.1 预定义的异常处理

预定义说明的部分 ORACLE 异常错误

| 错误号   | 异常错误信息名称        | 说明                                                         |
| -------- | ----------------------- | ------------------------------------------------------------ |
| ORA-0001 | Dup_val_on_index        | 试图破坏一个唯一性限制                                       |
| ORA-0051 | Timeout-on-resource     | 在等待资源时发生超时                                         |
| ORA-0061 | Transaction-backed-out  | 由于发生死锁事务被撤消                                       |
| ORA-1001 | Invalid-CURSOR          | 试图使用一个无效的游标                                       |
| ORA-1012 | Not-logged-on           | 没有连接到ORACLE                                             |
| ORA-1017 | Login-denied            | 无效的用户名/口令                                            |
| ORA-1403 | No_data_found           | SELECT INTO没有找到数据                                      |
| ORA-1422 | Too_many_rows           | SELECT INTO 返回多行                                         |
| ORA-1476 | Zero-divide             | 试图被零除                                                   |
| ORA-1722 | Invalid-NUMBER          | 转换一个数字失败                                             |
| ORA-6500 | Storage-error           | 内存不够引发的内部错误                                       |
| ORA-6501 | Program-error           | 内部错误                                                     |
| ORA-6502 | Value-error             | 转换或截断错误                                               |
| ORA-6504 | Rowtype-mismatch        | 缩主游标变量与 PL/SQL变量有不兼容行类型                      |
| ORA-6511 | CURSOR-already-OPEN     | 试图打开一个已存在的游标                                     |
| ORA-6530 | Access-INTO-null        | 试图为null 对象的属性赋值                                    |
| ORA-6531 | Collection-is-null      | 试图将Exists 以外的集合( collection)方法应用于一个null pl/sql 表上或varray上 |
| ORA-6532 | Subscript-outside-limit | 对嵌套或varray索引得引用超出声明范围以外                     |
| ORA-6533 | Subscript-beyond-count  | 对嵌套或varray 索引得引用大于集合中元素的个数.               |

  

对这种异常情况的处理，只需在PL/SQL块的异常处理部分，直接引用相应的异常情况名，并对其完成相应的异常错误处理即可。

 

**例****1****：**更新指定员工工资，如工资小于1500，则加100；

 

DECLARE

  v_empno emp.empno%TYPE :=&empno;

  v_sal  emp.sal%TYPE;

BEGIN

  SELECT sal INTO v_sal FROM emp WHERE empno=v_empno;

  IF v_sal<=1500 THEN

​     UPDATE emp SET sal=sal+100 WHERE empno=v_empno;

​    DBMS_OUTPUT.PUT_LINE('编码为'||v_empno||'员工工资已更新!');

  ELSE

DBMS_OUTPUT.PUT_LINE('编码为'||v_empno||'员工工资已经超过规定值!');

  END IF;

EXCEPTION

  WHEN NO_DATA_FOUND THEN

   DBMS_OUTPUT.PUT_LINE('数据库中没有编码为'||v_empno||'的员工');

  WHEN TOO_MANY_ROWS THEN

   DBMS_OUTPUT.PUT_LINE('程序运行错误!请使用游标');

  WHEN OTHERS THEN

​    DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END;

 

### §5.1.2 非预定义的异常处理

   

对于这类异常情况的处理，首先必须对非定义的ORACLE错误进行定义。步骤如下：

1. 在PL/SQL 块的定义部分定义异常情况：

<异常情况> EXCEPTION;

 

1. 将其定义好的异常情况，与标准的ORACLE错误联系起来，使用EXCEPTION_INIT语句：

PRAGMA EXCEPTION_INIT(<异常情况>, <错误代码>)；

 

1. 在PL/SQL 块的异常情况处理部分对异常情况做出相应的处理。

 

**例****2****：**删除指定部门的记录信息，以确保该部门没有员工。

 

INSERT INTO dept VALUES(50, ‘FINANCE’, ‘CHICAGO’);

 

DECLARE

  v_deptno dept.deptno%TYPE :=&deptno;

  e_deptno_remaining EXCEPTION;

  PRAGMA EXCEPTION_INIT(e_deptno_remaining, -2292);

  /* -2292 是违反一致性约束的错误代码 */

BEGIN

  DELETE FROM dept WHERE deptno=v_deptno;

EXCEPTION

  WHEN e_deptno_remaining THEN

   DBMS_OUTPUT.PUT_LINE('违反数据完整性约束!');

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END;

 

### §5.1.3 用户自定义的异常处理

当与一个异常错误相关的错误出现时，就会隐含触发该异常错误。用户定义的异常错误是通过显式使用 RAISE 语句来触发。当引发一个异常错误时，控制就转向到 EXCEPTION块异常错误部分，执行错误处理代码。

 

​    对于这类异常情况的处理，步骤如下：

1． 在PL/SQL 块的定义部分定义异常情况：

<异常情况> EXCEPTION;

 

2． RAISE <异常情况>；

 

3． 在PL/SQL 块的异常情况处理部分对异常情况做出相应的处理。

 

**例****3****：**更新指定员工工资，增加100；

 

DECLARE

  v_empno emp.empno%TYPE :=&empno;

  no_result EXCEPTION;

BEGIN

  UPDATE emp SET sal=sal+100 WHERE empno=v_empno;

  IF SQL%NOTFOUND THEN

​    RAISE no_result;

  END IF;

EXCEPTION

  WHEN no_result THEN

   DBMS_OUTPUT.PUT_LINE('你的数据更新语句失败了!');

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END;

 

### §5.1.4 用户定义的异常处理

调用DBMS_STANDARD(ORACLE提供的包)包所定义的RAISE_APPLICATION_ERROR过程，可以重新定义异常错误消息，它为应用程序提供了一种与ORACLE交互的方法。

 

RAISE_APPLICATION_ERROR 的语法如下：

RAISE_APPLICATION_ERROR(error_number,error_message,[keep_errors] ) ;

 

这里的error_number 是从 –20,000 到 –20,999 之间的参数，

  error_message 是相应的提示信息(< 2048 字节)，

keep_errors 为可选，如果keep_errors =TRUE ,则新错误将被添加到已经引发的错误列表中。如果keep_errors=FALSE(缺省),则新错误将替换当前的错误列表。

 

**例****4****：**创建一个函数get_salary, 该函数检索指定部门的工资总和，其中定义了-20991和-20992号错误，分别处理参数为空和非法部门代码两种错误：

 

CREATE TABLE errlog(

​    Errcode NUMBER,

​    Errtext CHAR(40));

 

CREATE OR REPLACE FUNCTION get_salary (p_deptno NUMBER)

​    RETURN NUMBER AS

​    V_sal NUMBER;

BEGIN

​    IF p_deptno IS NULL THEN

​       RAISE_APPLICATION_ERROR(-20991, ’部门代码为空’);

​    ELSIF p_deptno<0 THEN

​       RAISE_APPLICATION_ERROR(-20992, ’无效的部门代码’);

​    ELSE

​       SELECT SUM(sal) INTO v_sal FROM EMP WHERE deptno=p_deptno;

​       RETURN V_sal;

​    END IF;

END;

 

DECLARE

​    V_salary NUMBER(7,2);

​    V_sqlcode NUMBER;

​    V_sqlerr VARCHAR2(512);

​    Null_deptno EXCEPTION;

​    Invalid_deptno EXCEPTION;

​    PRAGMA EXCEPTION_INIT(null_deptno,-20991);

​    PRAGMA EXCEPTION_INIT(invalid_deptno, -20992);

BEGIN

​    V_salary :=get_salary(10);

​    DBMS_OUTPUT.PUT_LINE(’10号部门工资：’||TO_CHAR(V_salary));

 

​    BEGIN

​       V_salary :=get_salary(-10);

​    EXCEPTION

​       WHEN invalid_deptno THEN

​           V_sqlcode :=SQLCODE;

​           V_sqlerr :=SQLERRM;

​           INSERT INTO errlog(errcode, errtext) VALUES(v_sqlcode, v_sqlerr);

​           COMMIT;

​    END inner1;

 

​    V_salary :=get_salary(20);

​    DBMS_OUTPUT.PUT_LINE(’20号部门工资：’||TO_CHAR(V_salary));

 

​    BEGIN

​       V_salary :=get_salary(NULL);

​    END inner2;

 

​    V_salary :=get_salary(30);

​    DBMS_OUTPUT.PUT_LINE(’30号部门工资：’||TO_CHAR(V_salary));

 

​    EXCEPTION

​       WHEN null_deptno THEN

​           V_sqlcode :=SQLCODE;

​           V_sqlerr :=SQLERRM;

​           INSERT INTO errlog(errcode, errtext) VALUES(v_sqlcode, v_sqlerr);

​           COMMIT;

​    WHEN OTHERS THEN

DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END outer;

 

## §5.2 异常错误传播

  由于异常错误可以在声明部分和执行部分以及异常错误部分出现，因而在不同部分引发的异常错误也不一样。

 

### §5.2.1 在执行部分引发异常错误

  当一个异常错误在执行部分引发时，有下列情况：

l 如果当前块对该异常错误设置了处理，则执行它并成功完成该块的执行，然后控制转给包含块。

l 如果没有对当前块异常错误设置定义处理器，则通过在包含块中引发它来传播异常错误。然后对该包含块执行步骤1)。

 

### §5.2.2 在声明部分引发异常错误

  如果在声明部分引起异常情况，即在声明部分出现错误，那么该错误就能影响到其它的块。比如在有如下的PL/SQL程序：

 

DECLARE

Abc number(3):=’abc’;

其它语句

BEGIN

其它语句

EXCEPTION

WHEN OTHERS THEN

其它语句

END;

 

例子中，由于Abc number(3)=’abc’; 出错，尽管在EXCEPTION中说明了WHEN OTHERS THEN语句，但WHEN OTHERS THEN也不会被执行。 但是如果在该错误语句块的外部有一个异常错误，则该错误能被抓住，如：

 

BEGIN

DECLARE

Abc number(3):=’abc’;

其它语句

  BEGIN

其它语句

  EXCEPTION

WHEN OTHERS THEN

其它语句

END;

EXCEPTION

WHEN OTHERS THEN

其它语句

END;

## §5.3 异常错误处理编程

  在一般的应用处理中，建议程序人员要用异常处理，因为如果程序中不声明任何异常处理，则在程序运行出错时，程序就被终止，并且也不提示任何信息。下面是使用系统提供的异常来编程的例子。

## §5.4 在 PL/SQL 中使用 SQLCODE, SQLERRM

  由于ORACLE 的错信息最大长度是512字节，为了得到完整的错误提示信息，我们可用 SQLERRM和 SUBSTR 函数一起得到错误提示信息。

 

SQLCODE 返回错误代码数字.

SQLERRM 返回错误信息.

 

如: SQLCODE=+100 è SQLERRM=’no_data_found ‘

  SQLCODE=0   è SQLERRM=’normal, successfual completion’

**例****5.** 将ORACLE错误代码及其信息存入错误代码表

CREATE TABLE errors (errnum NUMBER(4), errmsg VARCHAR2(100));

 

DECLARE

  err_msg VARCHAR2(100);

BEGIN

  /* 得到所有 ORACLE 错误信息 */

  FOR err_num IN -100 .. 0 LOOP

   err_msg := SQLERRM(err_num);

   INSERT INTO errors VALUES(err_num, err_msg);

  END LOOP;

END;

 

DROP TABLE errors;

 

**例****6.** 查询ORACLE错误代码；

BEGIN

  INSERT INTO emp(empno, ename, hiredate, deptno)

​       VALUES(2222, ‘Jerry’, SYSDATE, 20);

  DBMS_OUTPUT.PUT_LINE('插入数据记录成功!');

  INSERT INTO emp(empno, ename, hiredate, deptno)

​       VALUES(2222, ‘Jerry’, SYSDATE, 20);

  DBMS_OUTPUT.PUT_LINE('插入数据记录成功!');

EXCEPTION

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE(SQLCODE||’---‘||SQLERRM);

END;

 

 

**
**

# 第六章 存储函数和过程

## §6.1  引言

ORACLE 提供可以把PL/SQL 程序存储在数据库中，并可以在任何地方来运行它。这样就叫存储过程或函数。过程和函数统称为PL/SQL子程序，他们是被命名的PL/SQL块，均存储在数据库中，并通过输入、输出参数或输入/输出参数与其调用者交换信息。过程和函数的唯一区别是函数总向调用者返回数据，而过程则不返回数据。在本节中，主要介绍：

1． 创建存储过程和函数。

2． 正确使用系统级的异常处理和用户定义的异常处理。

3． 建立和管理存储过程和函数。

## §6.2 创建函数

**1.** **建立内嵌函数**

语法如下：

CREATE [OR REPLACE] FUNCTION function_name

[(argment [ { IN| IN OUT }] type,

​       argment [ { IN | OUT | IN OUT } ] type]

RETURN return_type

{ IS | AS }

<类型.变量的说明>

BEGIN

FUNCTION_body

EXCEPTION

其它语句

END;

 

 

**例1.**    获取某部门的工资总和：

 

CREATE OR REPLACE FUNCTION get_salary(

​    Dept_no NUMBER,

​    Emp_count OUT NUMBER)

​    RETURN NUMBER IS

​    V_sum NUMBER;

BEGIN

​    SELECT SUM(sal), count(*) INTO V_sum, emp_count

​       FROM emp WHERE deptno=dept_no;

​    RETURN v_sum;

EXCEPTION

  WHEN NO_DATA_FOUND THEN

   DBMS_OUTPUT.PUT_LINE('你需要的数据不存在!');

  WHEN TOO_MANY_ROWS THEN

   DBMS_OUTPUT.PUT_LINE('程序运行错误!请使用游标');

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END get_salary;



**2.** **内嵌函数的调用**

函数声明时所定义的参数称为形式参数，应用程序调用时为函数传递的参数称为实际参数。应用程序在调用函数时，可以使用以下三种方法向函数传递参数：

 

**第一种参数传递格式称为位置表示法，格式为：**

​    argument_value1[,argument_value2 …]

 

**例****2****：**计算某部门的工资总和：

 

DECLARE

​    V_num NUMBER;

​    V_sum NUMBER;

BEGIN

​    V_sum :=get_salary(30, v_num);

​    DBMS_OUTPUT.PUT_LINE(’30号部门工资总和：’||v_sum||’，人数：’||v_num);

END;

 

**第二种参数传递格式称为名称表示法，格式为：**

​    argument => parameter [,…]

其中：argument 为形式参数，它必须与函数定义时所声明的形式参数名称相同。Parameter 为实际参数。

在这种格式中，形势参数与实际参数成对出现，相互间关系唯一确定，所以参数的顺序可以任意排列。

**例****3****：**计算某部门的工资总和：

 

DECLARE

​    V_num NUMBER;

​    V_sum NUMBER;

BEGIN

​    V_sum :=get_salary(emp_count => v_num, dept_no => 30);

​    DBMS_OUTPUT.PUT_LINE(’30号部门工资总和：’||v_sum||’，人数：’||v_num);

END;

 

**第三种参数传递格式称为混合表示法：**

即在调用一个函数时，同时使用位置表示法和名称表示法为函数传递参数。采用这种参数传递方法时，使用位置表示法所传递的参数必须放在名称表示法所传递的参数前面。也就是说，无论函数具有多少个参数，只要其中有一个参数使用名称表示法，其后所有的参数都必须使用名称表示法。

 

**例****4****：**

CREATE OR REPLACE FUNCTION demo_fun(

​    Name VARCHAR2,

​    Age INTEGER,

​    Sex VARCHAR2)

​    RETURN VARCHAR2

AS

​    V_var VARCHAR2(32);

BEGIN

​    V_var := name||’：‘||TO_CHAR(age)||’岁，’||sex;

​    RETURN v_var;

END;

 

DECLARE

​    Var VARCHAR(32);

BEGIN

​    Var := demo_fun(‘user1’, 30, sex => ‘男’);

​    DBMS_OUTPUT.PUT_LINE(var);

 

​    Var := demo_fun(‘user2’, age => 40, sex => ‘男’);

​    DBMS_OUTPUT.PUT_LINE(var);

 

​    Var := demo_fun(‘user3’, sex => ‘女’, age => 20);

​    DBMS_OUTPUT.PUT_LINE(var);

END;

 

无论采用哪一种参数传递方法，实际参数和形式参数之间的数据传递只有两种方法：传址法和传值法。所谓传址法是指在调用函数时，将实际参数的地址指针传递给形式参数，使形式参数和实际参数指向内存中的同一区域，从而实现参数数据的传递。这种方法又称作参照法，即形式参数参照实际参数数据。输入参数均采用传址法传递数据。

​    传值法是指将实际参数的数据拷贝到形式参数，而不是传递实际参数的地址。默认时，输出参数和输入/输出参数均采用传值法。在函数调用时，ORACLE将实际参数数据拷贝到输入/输出参数，而当函数正常运行退出时，又将输出形式参数和输入/输出形式参数数据拷贝到实际参数变量中。

 

**3.** **参数默认值**

在CREATE OR REPLACE FUNCTION 语句中声明函数参数时可以使用DEFAULT关键字为输入参数指定默认值。

 

**例****5****：**

CREATE OR REPLACE FUNCTION demo_fun(

​    Name VARCHAR2,

​    Age INTEGER,

​    Sex VARCHAR2 DEFAULT ‘男’)

​    RETURN VARCHAR2

AS

​    V_var VARCHAR2(32);

BEGIN

​    V_var := name||’：‘||TO_CHAR(age)||’岁，’||sex;

​    RETURN v_var;

END;

 

具有默认值的函数创建后，在函数调用时，如果没有为具有默认值的参数提供实际参数值，函数将使用该参数的默认值。但当调用者为默认参数提供实际参数时，函数将使用实际参数值。在创建函数时，只能为输入参数设置默认值，而不能为输入/输出参数设置默认值。

DECLARE

​    Var VARCHAR(32);

BEGIN

​    Var := demo_fun(‘user1’, 30);

​    DBMS_OUTPUT.PUT_LINE(var);

 

​    Var := demo_fun(‘user2’, age => 40);

​    DBMS_OUTPUT.PUT_LINE(var);

 

​    Var := demo_fun(‘user3’, sex => ‘女’, age => 20);

​    DBMS_OUTPUT.PUT_LINE(var);

END;

## §6.3  存储过程

### §6.3.1  创建过程

 

**建立存储过程**

  在 ORACLE SERVER上建立存储过程,可以被多个应用程序调用,可以向存储过程传递参数,也可以向存储过程传回参数.

 

**创建过程语法****:**

CREATE [OR REPLACE] PROCEDURE Procedure_name

[ (argment [ { IN | IN OUT }] Type,

   argment [ { IN | OUT | IN OUT } ] Type ]

{ IS | AS }

<类型.变量的说明>

BEGIN

<执行部分>

EXCEPTION

<可选的异常错误处理程序>

END;

 

**例****6****．**用户连接登记记录；

 

CREATE table logtable (userid VARCHAR2(10), logdate date);

 

CREATE OR REPLACE PROCEDURE logexecution IS

BEGIN

  INSERT INTO logtable (userid, logdate) VALUES (USER, SYSDATE);

END;

 

**例****7****．**删除指定员工记录；

 

CREATE OR REPLACE PROCEDURE DelEmp(v_empno IN emp.empno%TYPE) AS

No_result EXCEPTION;

BEGIN

  DELETE FROM emp WHERE empno=v_empno;

  IF SQL%NOTFOUND THEN

​    RAISE no_result;

  END IF;

  DBMS_OUTPUT.PUT_LINE('编码为'||v_empno||'的员工已被除名!');

EXCEPTION

  WHEN no_result THEN

   DBMS_OUTPUT.PUT_LINE('你需要的数据不存在!');

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END DelEmp;

 

 

### §6.3.2  调用存储过程

 

  存储过程建立完成后，只要通过授权，用户就可以在SQLPLUS 、ORACLE开发工具或第三方开发工具中来调用运行。ORACLE 使用EXECUTE 语句来实现对存储过程的调用：

EXEC[UTE]  Procedure_name( parameter1, parameter2…);

 

**例****8****：**

EXECUTE logexecution;

 

 

**例****9****．**计算指定部门的工资总和，并统计其中的职工数量。

 

CREATE OR REPLACE PROCEDURE proc_demo(

​    Dept_no NUMBER DEFAULT 10,

​    Sal_sum OUT NUMBER,

​    Emp_count OUT NUMBER)

IS

BEGIN

​    SELECT SUM(sal), COUNT(*) INTO sal_sum, emp_count

FROM emp WHERE deptno=dept_no;

EXCEPTION

  WHEN NO_DATA_FOUND THEN

   DBMS_OUTPUT.PUT_LINE('你需要的数据不存在!');

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END proc_demo;

 

调用方法:

 DECLARE

V_num NUMBER;

V_sum NUMBER(8, 2);

BEGIN

​    Proc_demo(30, v_sum, v_num);

DBMS_OUTPUT.PUT_LINE('30号部门工资总和：'||v_sum||’，人数：’||v_num);

​    Proc_demo(sal_sum => v_sum, emp_count => v_num);

DBMS_OUTPUT.PUT_LINE('10号部门工资总和：'||v_sum||’，人数：’||v_num);

END;

 

​    在PL/SQL 程序中还可以在块内建立本地函数和过程，这些函数和过程不存储在数据库中，但可以在创建它们的PL/SQL 程序中被重复调用。本地函数和过程在PL/SQL 块的声明部分定义，它们的语法格式与存储函数和过程相同，但不能使用CREATE OR REPLACE 关键字。

 

**例****10****：**建立本地过程，用于计算指定部门的工资总和，并统计其中的职工数量；

 

DECLARE

V_num NUMBER;

V_sum NUMBER(8, 2);

PROCEDURE proc_demo(

​       Dept_no NUMBER DEFAULT 10,

​       Sal_sum OUT NUMBER,

​       Emp_count OUT NUMBER)

IS

BEGIN

​       SELECT SUM(sal), COUNT(*) INTO sal_sum, emp_count

FROM emp WHERE deptno=dept_no;

EXCEPTION

  WHEN NO_DATA_FOUND THEN

   DBMS_OUTPUT.PUT_LINE('你需要的数据不存在!');

  WHEN OTHERS THEN

   DBMS_OUTPUT.PUT_LINE('发生其它错误!');

END proc_demo;

BEGIN

​    Proc_demo(30, v_sum, v_num);

DBMS_OUTPUT.PUT_LINE('30号部门工资总和：'||v_sum||’，人数：’||v_num);

​    Proc_demo(sal_sum => v_sum, emp_count => v_num);

DBMS_OUTPUT.PUT_LINE('10号部门工资总和：'||v_sum||’，人数：’||v_num);

END;

 

### §6.3.3  开发存储过程步骤

  开发存储过程、函数、包及触发器的步骤如下：

 

#### §6.3.3.1  使用文字编辑处理软件编辑存储过程源码

  使用文字编辑处理软件编辑存储过程源码，要用类似WORD 文字处理软件进行编辑时，要将源码存为文本格式。

 

#### §6.3.3.2  在SQLPLUS或用调试工具将存储过程程序进行解释

  在SQLPLUS或用调试工具将存储过程程序进行解释；

  在SQL>下调试，可用START 或GET 等ORACLE命令来启动解释。如：

SQL>START c:\stat1.sql

  如果使用调式工具，可直接编辑和点击相应的按钮即可生成存储过程。

 

#### §6.3.3.3  调试源码直到正确

  我们不能保证所写的存储过程达到一次就正确。所以这里的调式是每个程序员必须进行的工作之一。在SQLPLUS下来调式主要用的方法是：

l 使用 SHOW ERROR命令来提示源码的错误位置；

l 使用 user_errors 数据字典来查看各存储过程的错误位置。

 

#### §6.3.3.4  授权执行权给相关的用户或角色

如果调式正确的存储过程没有进行授权，那就只有建立者本人才可以运行。所以作为应用系统的一部分的存储过程也必须进行授权才能达到要求。在SQL*PLUS下可以用GRANT命令来进行存储过程的运行授权。

 

**GRANT****语法：**

GRANT system_privilege | role

TO user | role | PUBLIC [WITH ADMIN OPTION]

 

GRANT object_privilege | ALL ON schema.object

TO user | role | PUBLIC [WITH GRANT OPTION]

 

**例子：**

 

CREATE OR REPLACE PUBLIC SYNONYM dbms_job FOR dbms_job

 

GRANT EXECUTE ON dbms_job TO PUBLIC WITH GRANT OPTION

 

### §6.3.4  与过程相关数据字典

 

USER_SOURCE, ALL_SOURCE, DBA_SOURCE, USER_ERRORS

 

相关的权限:

CREATE ANY PROCEDURE

DROP ANY PROCEDURE

 

在SQL*PLUS 中，可以用DESCRIBE 命令查看过程的名字及其参数表。

 

DESCRIBE Procedure_name;

 

DROP PROCEDURE logexecution;

DROP PROCEDURE delemp;

DROP PROCEDURE proc_demo;

DROP FUNCTION demo_fun;

DROP FUNCTION get_salary;

**
**

# 第七章  包的创建和应用

## §7.1  引言

  包是一组相关过程、函数、变量、常量和游标等PL/SQL程序设计元素的组合，它具有面向对象程序设计语言的特点，是对这些PL/SQL 程序设计元素的封装。包类似于C++和JAVA语言中的类，其中变量相当于类中的成员变量，过程和函数相当于类方法。把相关的模块归类成为包，可使开发人员利用面向对象的方法进行存储过程的开发，从而提高系统性能。

​    与类相同，包中的程序元素也分为公用元素和私用元素两种，这两种元素的区别是他们允许访问的程序范围不同，即它们的作用域不同。公用元素不仅可以被包中的函数、过程所调用，也可以被包外的PL/SQL程序访问，而私有元素只能被包内的函数和过程序所访问。

​    在PL/SQL程序设计中，使用包不仅可以使程序设计模块化，对外隐藏包内所使用的信息（通过使用私用变量），而写可以提高程序的执行效率。因为，当程序首次调用包内函数或过程时，ORACLE将整个包调入内存，当再次访问包内元素时，ORACLE直接从内存中读取，而不需要进行磁盘I/O操作，从而使程序执行效率得到提高。

  一个包由两个分开的部分组成：

  包定义（PACKAGE）：包定义部分声明包内数据类型、变量、常量、游标、子程序和异常错误处理等元素，这些元素为包的公有元素。

  包主体（PACKAGE BODY）：包主体则是包定义部分的具体实现，它定义了包定义部分所声明的游标和子程序，在包主体中还可以声明包的私有元素。

  包定义和包主体分开编译，并作为两部分分开的对象存放在数据库字典中，详见数据字典user_source, all_source, dba_source.

## §7.2  包的定义

**包定义的语法如下：**

**创建包定义****:**

CREATE [OR REPLACE] PACKAGE package_name

[AUTHID {CURRENT_USER | DEFINER}]

{IS | AS}

[公有数据类型定义[公有数据类型定义]…]

[公有游标声明[公有游标声明]…]

[公有变量、常量声明[公有变量、常量声明]…]

[公有子程序声明[公有子程序声明]…]

END [package_name];

其中：AUTHID CURRENT_USER和AUTHID DEFINER选项说明应用程序在调用函数时所使用的权限模式，它们与CREATE FUNCTION语句中invoker_right_clause子句的作用相同。

 

**创建包主体****:**

CREATE [OR REPLACE] PACKAGE BODY package_name

{IS | AS}

[私有数据类型定义[私有数据类型定义]…]

[私有变量、常量声明[私有变量、常量声明]…]

[私有子程序声明和定义[私有子程序声明和定义]…]

[公有游标定义[公有游标定义]…]

[公有子程序定义[公有子程序定义]…]

BEGIN

PL/SQL 语句

END [package_name];

其中：在包主体定义公有程序时，它们必须与包定义中所声明子程序的格式完全一致。

## §7.3  包的开发步骤

  与开发存储过程类似，包的开发需要几个步骤：

1． 将每个存储过程调式正确；

2． 用文本编辑软件将各个存储过程和函数集成在一起；

3． 按照包的定义要求将集成的文本的前面加上包定义；

4． 按照包的定义要求将集成的文本的前面加上包主体；

5． 使用SQLPLUS或开发工具进行调式。

## §7.4  包定义的说明

**例****1:**创建的包为demo_pack, 该包中包含一个记录变量DeptRec、两个函数和一个过程。

CREATE OR REPLACE PACKAGE demo_pack

IS

​    DeptRec dept%ROWTYPE;

​    V_sqlcode NUMBER;

​    V_sqlerr VARCHAR2(2048);

​    FUNCTION add_dept(

dept_no NUMBER, dept_name VARCHAR2, location VARCHAR2)

​    RETURN NUMBER;

​    FUNCTION remove_dept(dept_no NUMBER)

​       RETURN NUMBER;

​    PROCEDURE query_dept(dept_no IN NUMBER);

END demo_pack;

 

包主体的创建方法，它实现上面所声明的包定义，并在包主体中声明一个私有变量flag和一个私有函数check_dept，由于在add_dept和remove_dept等函数中需要调用check_dpet函数，所以，在定义check_dept 函数之前首先对该函数进行声明，这种声明方法称作前向声明。

CREATE OR REPLACE PACKAGE BODY demo_pack

​    IS

​    Flag INTEGER;

FUNCTION check_dept(dept_no NUMBER)

​       RETURN INTEGER;

 

FUNCTION add_dept(dept_no NUMBER, dept_name VARCHAR2, location VARCHAR2)

​    RETURN NUMBER

​    IS

BEGIN

​    IF check_dept(dept_no)=0 THEN

​       INSERT INTO dept VALUES(dept_no, dept_name, location);

​       RETURN 1;

​    ELSE

​       RETURN 0;

​    END IF;

EXCEPTION

​    WHEN OTHERS THEN

​       V_sqlcode := SQLCODE;

​       V_sqlerr := SQLERRM;

​       RETURN -1;

END add_dept;

 

FUNCTION remove_dept(dept_no NUMBER)

​    RETURN NUMBER

​    IS

BEGIN

​    V_sqlcode := 0;

​    V_sqlerr := NULL;

​    IF check_dept(dept_no) = 1 THEN

​       DELETE FROM dept WHERE deptno=dept_no;

​       RETURN 1;

​    ELSE

​       RETURN 0;

​    END IF;

EXCEPTION

​    WHEN OTHERS THEN

​       V_sqlcode := SQLCODE;

​       V_sqlerr := SQLERRM;

​       RETURN -1;

END remove_dept;

 

PROCEDURE query_dept(dept_no IN NUMBER)

​    IS

BEGIN

​    IF check_dept(dept_no) =1 THEN

​       SELECT * INTO DeptRec FROM dept WHERE deptno=dept_no;

​    END IF;

END query_dept;

 

FUNCTION check_dept(dept_no NUMBER)

​    RETURN INTEGER

​    IS

BEGIN

​    SELECT COUNT(*) INTO flag FROM dept WHERE deptno=dept_no;

​    IF flag > 0 THEN

​       Flag := 1;

​    END IF;

​    RETURN flag;

END check_dept;

 

BEGIN

​    V_sqlcode := NULL;

​    V_sqlerr := NULL;

END demo_pack;

 

对包内共有元素的调用格式为：包名.元素名称

调用demo_pack包内函数对dept表进行插入、查询和修改操作，并通过demo_pack包中的记录变量DeptRec 显示所查询到的数据库信息：

DECLARE

​    Var NUMBER;

BEGIN

​    Var := demo_pack.add_dept(90,’Administration’, ‘Beijing’);

​    IF var =-1 THEN

​       DBMS_OUTPUT.PUT_LINE(demo_pack.v_sqlerr);

​    ELSIF var =0 THEN

​       DBMS_OUTPUT.PUT_LINE(‘该部门记录已经存在！’);

ELSE

​       DBMS_OUTPUT.PUT_LINE(‘添加记录成功！’);

​       Demo_pack.query_dept(90);

​       DBMS_OUTPUT.PUT_LINE(demo_pack.DeptRec.deptno||’---‘||

demo_pack.DeptRec.dname||’---‘||demo_pack.DeptRec.loc);

​       var := demo_pack.remove_dept(90);

​       IF var =-1 THEN

​           DBMS_OUTPUT.PUT_LINE(demo_pack.v_sqlerr);

​       ELSE

​           DBMS_OUTPUT.PUT_LINE(‘删除记录成功！’);

​       END IF;

​    END IF;

END;

 

 

**例****2:** 创建包emp_package

 

CREATE OR REPLACE PACKAGE emp_package

​    IS

​    TYPE emp_table_type IS TABLE OF emp%ROWTYPE

INDEX BY BINARY_INTEGER;

​    PROCEDURE read_emp_table (p_emp_table OUT emp_table_type);

END emp_package;

 

CREATE OR REPLACE PACKAGE BODY emp_package

​    IS

​    PROCEDURE read_emp_table (p_emp_table OUT emp_table_type)

​    IS

​    I BINARY_INTEGER := 0;

​    BEGIN

​       FOR emp_record IN ( SELECT * FROM emp ) LOOP

​           P_emp_table(i) := emp_record;

​           I := I + 1;

​       END LOOP;

​    END read_emp_table;

END emp_package;

 

DECLARE

​    E_table emp_package.emp_table_type;

BEGIN

​    Emp_package.read_emp_table(e_table);

​    FOR I IN e_table.FIRST .. e_table.LAST LOOP

​       DBMS_OUTPUT.PUT_LINE(e_table(i).empno||’ ‘||e_table(i).ename);

​    END LOOP;

END;

 

## §7.5  子程序重载

PL/SQL 允许对包内子程序和本地子程序进行重载。所谓重载时指两个或多个子程序有相同的名称，但拥有不同的参数变量、参数顺序或参数数据类型。

例：

CREATE OR REPLACE PACKAGE demo_pack1

IS

​    DeptRec dept%ROWTYPE;

​    V_sqlcode NUMBER;

​    V_sqlerr VARCHAR2(2048);

​    FUNCTION query_dept(dept_no IN NUMBER)

​       RETURN INTEGER;

​    FUNCTION query_dept(dept_no IN VARCHAR2)

​       RETURN INTEGER;

END demo_pack1;

 

CREATE OR REPLACE PACKAGE BODY demo_pack1

​    IS

FUNCTION check_dept(dept_no NUMBER)

​    RETURN INTEGER

IS

​    Flag INTEGER;

BEGIN

​    SELECT COUNT(*) INTO flag FROM dept WHERE deptno=dept_no;

​    IF flag > 0 THEN

​       RETURN 1;

​    ELSE

​       RETURN 0;

​    END IF;

END check_dept;

 

FUNCTION check_dept(dept_no VARCHAR2)

​    RETURN INTEGER

IS

​    Flag INTEGER;

BEGIN

​    SELECT COUNT(*) INTO flag FROM dept WHERE deptno=dept_no;

​    IF flag > 0 THEN

​       RETURN 1;

​    ELSE

​       RETURN 0;

​    END IF;

END check_dept;

 

FUNCTION query_dept(dept_no IN NUMBER)

​    RETURN INTEGER

IS

BEGIN

​    IF check_dept(dept_no) =1 THEN

​       SELECT * INTO DeptRec FROM dept WHERE deptno=dept_no;

​       RETURN 1;

​    ELSE

​       RETURN 0;

​    END IF;

END query_dept;

 

FUNCTION query_dept(dept_no IN VARCHAR2)

​    RETURN INTEGER

IS

BEGIN

​    IF check_dept(dept_no) =1 THEN

​       SELECT * INTO DeptRec FROM dept WHERE deptno=dept_no;

​       RETURN 1;

​    ELSE

​       RETURN 0;

​    END IF;

END query_dept;

 

END demo_pack1;

 

## §7.6  删除过程、函数和包

**1****．删除过程**

我们可以DROP PROCEDURE命令对不需要的过程进行删除，语法如下：

DROP PROCEDURE [user.]Procudure_name;

 

**2****．删除函数**

我们可以DROP FUNCTION 命令对不需要的函数进行删除，语法如下：

DROP FUNCTION [user.]Function_name;

 

**3****．删除包**

我们可以 DROP PACKAGE 命令对不需要的包进行删除，语法如下：

DROP PACKAGE [BODY] [user.]package_name;

 

DROP PROCEDURE OpenCurType;

DROP PACKAGE demo_pack;

DROP PACKAGE emp_package;

## §7.7  包的管理

DBA_SOURCE, USER_SOURCE, USER_ERRORS, DBA-OBJECTS

 

**
**

# 第八章 触发器

 触发器是许多关系数据库系统都提供的一项技术。在ORACLE系统里，触发器类似过程和函数，都有声明，执行和异常处理过程的PL/SQL块。

## §8.1  触发器类型

  触发器在数据库里以独立的对象存储，它与存储过程不同的是，存储过程通过其它程序来启动运行或直接启动运行，而触发器是由一个事件来启动运行。即触发器是当某个事件发生时自动地隐式运行。并且，触发器不能接收参数。所以运行触发器就叫触发或点火（firing）。ORACLE事件指的是对数据库的表进行的INSERT、UPDATE及DELETE操作或对视图进行类似的操作。ORACLE将触发器的功能扩展到了触发ORACLE，如数据库的启动与关闭等。

 

### §8.1.1 DML触发器

  ORACLE可以在DML语句进行触发，可以在DML操作前或操作后进行触发，并且可以对每个行或语句操作上进行触发。

 

### §8.1.2 替代触发器

  由于在ORACLE里，不能直接对由两个以上的表建立的视图进行操作。所以给出了替代触发器。它就是ORACLE 8专门为进行视图操作的一种处理方法。

 

### §8.1.3 系统触发器

ORACLE 8i 提供了第三种类型的触发器叫系统触发器。它可以在ORACLE数据库系统的事件中进行触发，如ORACLE系统的启动与关闭等。

 

触发器组成: 

l 触发事件：即在何种情况下触发TRIGGER; 例如：INSERT, UPDATE, DELETE。

l 触发时间：即该TRIGGER 是在触发事件发生之前（BEFORE）还是之后(AFTER)触发，也就是触发事件和该TRIGGER 的操作顺序。

l 触发器本身：即该TRIGGER 被触发之后的目的和意图，正是触发器本身要做的事情。 例如：PL/SQL 块。

l 触发频率：说明触发器内定义的动作被执行的次数。即语句级(STATEMENT)触发器和行级(ROW)触发器。

语句级(STATEMENT)触发器：是指当某触发事件发生时，该触发器只执行一次；

行级(ROW)触发器：是指当某触发事件发生时，对受到该操作影响的每一行数据，触发器都单独执行一次。

## §8.2  创建触发器

**创建触发器的一般语法是****:**

 

CREATE [OR REPLACE] TRIGGER trigger_name

{BEFORE | AFTER | INSTEAD OF}

{INSERT | DELETE | UPDATE [OF column [, column …]]}

ON {[schema.] table_name | [schema.] view_name}

[REFERENCING {OLD [AS] old | NEW [AS] new| PARENT as parent}]

[FOR EACH ROW ]

[WHEN condition]

trigger_body;

其中：

BEFORE 和AFTER指出触发器的触发时序分别为前触发和后触发方式，前触发是在执行触发事件之前触发当前所创建的触发器，后触发是在执行触发事件之后触发当前所创建的触发器。

​    INSTEAD OF 选项使ORACLE激活触发器，而不执行触发事件。只能对视图和对象视图建立INSTEAD OF触发器，而不能对表、模式和数据库建立INSTEAD OF 触发器。

​    FOR EACH ROW选项说明触发器为行触发器。行触发器和语句触发器的区别表现在：行触发器要求当一个DML语句操走影响数据库中的多行数据时，对于其中的每个数据行，只要它们符合触发约束条件，均激活一次触发器；而语句触发器将整个语句操作作为触发事件，当它符合约束条件时，激活一次触发器。当省略FOR EACH ROW 选项时，BEFORE 和AFTER 触发器为语句触发器，而INSTEAD OF 触发器则为行触发器。

​    REFERENCING 子句说明相关名称，在行触发器的PL/SQL块和WHEN 子句中可以使用相关名称参照当前的新、旧列值，默认的相关名称分别为OLD和NEW。触发器的PL/SQL块中应用相关名称时，必须在它们之前加冒号(:)，但在WHEN子句中则不能加冒号。

WHEN 子句说明触发约束条件。Condition 为一个逻辑表达时，其中必须包含相关名称，而不能包含查询语句，也不能调用PL/SQL 函数。WHEN 子句指定的触发约束条件只能用在BEFORE 和AFTER 行触发器中，不能用在INSTEAD OF 行触发器和其它类型的触发器中。

  当一个基表被修改( INSERT, UPDATE, DELETE)时要执行的存储过程，执行时根据其所依附的基表改动而自动触发，因此与应用程序无关，用数据库触发器可以保证数据的一致性和完整性。

 

每张表最多可建立12 种类型的触发器，它们是:

BEFORE INSERT

BEFORE INSERT FOR EACH ROW

AFTER INSERT

AFTER INSERT FOR EACH ROW

 

BEFORE UPDATE

BEFORE UPDATE FOR EACH ROW

AFTER UPDATE

AFTER UPDATE FOR EACH ROW

 

BEFORE DELETE

BEFORE DELETE FOR EACH ROW

AFTER DELETE

AFTER DELETE FOR EACH ROW

 

### §8.2.1 触发器触发次序

1. 执行 BEFORE语句级触发器;
2. 对与受语句影响的每一行：

l 执行 BEFORE行级触发器

l 执行 DML语句

l 执行 AFTER行级触发器 

1. 执行 AFTER语句级触发器

 

### §8.2.2 创建DML触发器

  触发器名与过程名和包的名字不一样，它是单独的名字空间，因而触发器名可以和表或过程有相同的名字，但在一个模式中触发器名不能相同。

 

**触发器的限制**

l CREATE TRIGGER语句文本的字符长度不能超过32KB；

l 触发器体内的SELECT 语句只能为SELECT … INTO …结构，或者为定义游标所使用的SELECT 语句。

l 触发器中不能使用数据库事务控制语句 COMMIT; ROLLBACK, SVAEPOINT 语句；

l 由触发器所调用的过程或函数也不能使用数据库事务控制语句；

l 触发器中不能使用LONG, LONG RAW 类型；

l 触发器内可以参照LOB 类型列的列值，但不能通过 :NEW 修改LOB列中的数据；

l 触发器所访问的表受到表的约束限制，即后面的“变化表”。

 

问题：当触发器被触发时，要使用被插入、更新或删除的记录中的列值，有时要使用操作前、    后列的值.

实现:  :new 修饰符访问操作完成后列的值

​    :old 修饰符访问操作完成前列的值

 

| 特性 | INSERT | UPDATE | DELETE |
| ---- | ------ | ------ | ------ |
| OLD  | NULL   | 有效   | 有效   |
| NEW  | 有效   | 有效   | NULL   |

 

**例****1:** 建立一个触发器, 当职工表 emp 表被删除一条记录时，把被删除记录写到职工表删除日志表中去。

CREATE TABLE emp_his AS SELECT * FROM EMP WHERE 1=2;

 

CREATE OR REPLACE TRIGGER del_emp

  BEFORE DELETE ON scott.emp FOR EACH ROW

BEGIN

  --  将修改前数据插入到日志记录表 del_emp ,以供监督使用。

  INSERT INTO emp_his(deptno , empno, ename , job ,mgr , sal , comm , hiredate )

​    VALUES( :old.deptno, :old.empno, :old.ename , :old.job,

​        :old.mgr, :old.sal, :old.comm, :old.hiredate );

END;

 

DELETE emp WHERE empno=7788;

 

DROP TABLE emp_his;

DROP TRIGGER del_emp;

 

### §8.2.3 创建替代(Instead_of)触发器

  INSTEAD_OF 用于对视图的DML触发，由于视图有可能是由多个表进行联结(join)而成，因而并非是所有的联结都是可更新的。但可以按照所需的方式执行更新，例如下面情况：

 

CREATE OR REPLACE VIEW emp_view AS

SELECT deptno, count(*) total_employeer, sum(sal) total_salary

FROM emp GROUP BY deptno;

 

在此视图中直接删除是非法：

SQL>DELETE FROM emp_view WHERE deptno=10;

DELETE FROM emp_view WHERE deptno=10

​      *

ERROR 位于第 1 行:

ORA-01732: 此视图的数据操纵操作非法

 

但是我们可以创建INSTEAD_OF触发器来为 DELETE 操作执行所需的处理，即删除EMP表中所有基准行：

 

CREATE OR REPLACE TRIGGER emp_view_delete

  INSTEAD OF DELETE ON emp_view FOR EACH ROW

BEGIN

  DELETE FROM emp WHERE deptno= :old.deptno;

END emp_view_delete;

 

DELETE FROM emp_view WHERE deptno=10;

 

DROP TRIGGER emp_view_delete;

DROP VIEW emp_view;

 

### §8.2.3 创建系统事件触发器

  ORACLE8i提供的系统事件触发器可以在DDL或数据库系统上被触发。DDL指的是数据定义语言，如CREATE 、ALTER及DROP 等。而数据库系统事件包括数据库服务器的启动或关闭，用户的登录与退出、数据库服务错误等。创建系统触发器的语法如下：

 

CREATE OR REPLACE TRIGGER [sachema.] trigger_name

  {BEFORE|AFTER} {ddl_event_list|database_event_list}

  ON { DATABASE | [schema.] SCHEMA }

  [ WHEN_clause]

  trigger_body;

其中: ddl_event_list：一个或多个DDL 事件，事件间用 OR 分开；

   database_event_list：一个或多个数据库事件，事件间用 OR 分开；

​    系统事件触发器既可以建立在一个模式上，又可以建立在整个数据库上。当建立在模式之上时，只有模式所指定用户的DDL操作和它们所导致的错误才激活触发器；当建立在数据库之上时，该数据库所有用户的DDL操作和他们所导致的错误，以及数据库的启动和关闭均可激活触发器。要在数据库之上建立触发器时，要求用户具有ADMINISTER DATABASE TRIGGER权限。

 

下面给出系统触发器的种类和事件出现的时机（前或后）：

| 事件                  | 允许的时机 | 说明                 |
| --------------------- | ---------- | -------------------- |
| 启动STARTUP           | 之后       | 实例启动时激活       |
| 关闭SHUTDOWN          | 之前       | 实例正常关闭时激活   |
| 服务器错误SERVERERROR | 之后       | 只要有错误就激活     |
| 登录LOGON             | 之后       | 成功登录后激活       |
| 注销LOGOFF            | 之前       | 开始注销时激活       |
| 创建CREATE            | 之前，之后 | 在创建之前或之后激活 |
| 撤消DROP              | 之前，之后 | 在撤消之前或之后激活 |
| 变更ALTER             | 之前，之后 | 在变更之前或之后激活 |

 

  系统触发器可以在数据库级（database）或模式（schema）级进行定义。数据库级触发器在任何事件都激活触发器，即触发对象为整个数据库中所有用户产生的每个指定事件；而模式触发器只有在指定的模式所产生的的触发事件发生时才触发，默认时为当前用户模式。

 

### §8.2.4 系统触发器事件属性

 

| 事件属性\事件 | Startup/Shutdown | Servererror | Logon/Logoff | DDL   | DML   |
| ------------- | ---------------- | ----------- | ------------ | ----- | ----- |
| 事件名称      | ****            | ****       | ****        | **** | **** |
| 数据库名称    | ****            |             |              |       |       |
| 数据库实例号  | ****            |             |              |       |       |
| 错误号        |                  | ****       |              |       |       |
| 用户名        |                  |             | ****        |       |       |
| 模式对象类型  |                  |             |              | **** |       |
| 模式对象名称  |                  |             |              | **** |       |
| 列            |                  |             |              |       | **** |

 

除DML语句的列属性外，其余事件属性值可通过调用ORACLE定义的事件属性函数来读取。

| 函数名称                   | 数据类型       | 说  明                                                       |
| -------------------------- | -------------- | ------------------------------------------------------------ |
| Sysevent                   | VARCHAR2（20） | 激活触发器的事件名称                                         |
| Instance_num               | NUMBER         | 数据库实例名                                                 |
| Database_name              | VARCHAR2（50） | 数据库名称                                                   |
| Server_error(posi)         | NUMBER         | 错误信息栈中posi指定位置中的错误号                           |
| Is_servererror(err_number) | BOOLEAN        | 检查err_number指定的错误号是否在错误信息栈中，如果在则返回TRUE，否则返回FALSE。在触发器内调用此函数可以判断是否发生指定的错误。 |
| Login_user                 | VARCHAR2(30)   | 登陆或注销的用户名称                                         |
| Dictionary_obj_type        | VARCHAR2(20)   | DDL语句所操作的数据库对象类型                                |
| Dictionary_obj_name        | VARCHAR2(30)   | DDL语句所操作的数据库对象名称                                |
| Dictionary_obj_owner       | VARCHAR2(30)   | DDL语句所操作的数据库对象所有者名称                          |
| Des_encrypted_password     | VARCHAR2(2)    | 正在创建或修改的经过DES算法加密的用户口令                    |

 

 

### §8.2.5 使用触发器谓词

  ORACLE 提供三个参数INSERTING, UPDATING, DELETING 用于判断触发了哪些操作。

| 谓词      | 行为                                             |
| --------- | ------------------------------------------------ |
| INSERTING | 如果触发语句是 INSERT 语句，则为TRUE,否则为FALSE |
| UPDATING  | 如果触发语句是 UPDATE语句，则为TRUE,否则为FALSE  |
| DELETING  | 如果触发语句是 DELETE 语句，则为TRUE,否则为FALSE |

 

### §8.2.6 重新编译触发器

如果在触发器内调用其它函数或过程，当这些函数或过程被删除或修改后，触发器的状态将被标识为无效。当DML语句激活一个无效触发器时，ORACLE将重新编译触发器代码，如果编译时发现错误，这将导致DML语句执行失败。

在PL/SQL程序中可以调用ALTER TRIGGER语句重新编译已经创建的触发器，格式为：

​    ALTER TRIGGER [schema.] trigger_name COMPILE [ DEBUG]

其中：DEBUG 选项要器编译器生成PL/SQL 程序条使其所使用的调试代码。

## §8.3  删除和使能触发器

l **删除触发器：**

DROP TRIGGER trigger_name;

 

当删除其他用户模式中的触发器名称，需要具有DROP ANY TRIGGER系统权限，当删除建立在数据库上的触发器时，用户需要具有ADMINISTER DATABASE TRIGGER系统权限。

此外，当删除表或视图时，建立在这些对象上的触发器也随之删除。

 

l **使能触发器**

数据库TRIGGER 的状态：

有效状态(ENABLE)：当触发事件发生时，处于有效状态的数据库触发器TRIGGER 将被触发。

无效状态(DISABLE)：当触发事件发生时，处于无效状态的数据库触发器TRIGGER 将不会被触发，此时就跟没有这个数据库触发器(TRIGGER) 一样。

数据库TRIGGER的这两种状态可以互相转换。格式为：

ALTER TIGGER trigger_name [DISABLE | ENABLE ];

例：ALTER TRIGGER emp_view_delete DISABLE;

   

​    ALTER TRIGGER语句一次只能改变一个触发器的状态，而ALTER TABLE语句则一次能够改变与指定表相关的所有触发器的使用状态。格式为：

​    ALTER TABLE [schema.]table_name {ENABLE|DISABLE} ALL TRIGGERS;

 

例：使表EMP 上的所有TRIGGER 失效：

ALTER TABLE emp DISABLE ALL TRIGGERS; 

## §8.4 触发器和数据字典

相关数据字典：USER_TRIGGERS、ALL_TRIGGERS、DBA_TRIGGERS

 

COL trigger_name FORMAT A10

COL trigger_type FORMAT A10

COL triggering_event FORMAT A10

COL table_owner FORMAT A10

COL base_object_type FORMAT A10

COL referencing_names FORMAT A10

COL status FORMAT A10

COL action_type FORMAT A10

 

SELECT TRIGGER_NAME, TRIGGER_TYPE, TRIGGERING_EVENT,

​    TABLE_OWNER, BASE_OBJECT_TYPE, REFERENCING_NAMES,

​    STATUS, ACTION_TYPE

​    FROM user_triggers;

 

## §8.5  数据库触发器的应用举例

**例****5****：**利用ORACLE事件属性函数，创建一个系统事件触发器。首先创建一个事件日志表eventlog，由它存储用户在当前数据库中所创建的数据库对象，以及用户的登陆和注销、数据库的启动和关闭等事件，之后创建trig_ddl、trig_before和trig_after触发器，它们调用事件属性函数将各个事件记录到eventlog数据表中。

由于在PL/SQL块中不能直接调用DDL语句，所以，利用ORACLE内置包DBMS_UTILITY中的EXEC_DDL_STATEMENT过程，由它执行DDL语句创建触发器。

 

BEGIN

​    -- 创建用于记录事件日志的数据表

​    DBMS_UTILITY.EXEC_DDL_STATEMENT(‘

​       CREATE TABLE eventlog(

​           Eventname VARCHAR2(20) NOT NULL,

​           Eventdate date default sysdate,

​           Inst_num NUMBER NULL,

​           Db_name VARCHAR2(50) NULL,

​           Srv_error NUMBER NULL,

​           Username VARCHAR2(30) NULL,

​           Obj_type VARCHAR2(20) NULL,

​           Obj_name VARCHAR2(30) NULL,

​           Obj_owner VARCHAR2(30) NULL

​       )

​    ‘);

 

​    -- 创建DDL触发器trig4_ddl

​    DBMS_UTILITY.EXEC_DDL_STATEMENT(‘

​       CREATE OR REPLACE TRIGGER trig_ddl

​           AFTER CREATE OR ALTER OR DROP

ON DATABASE

​       DECLARE

​           Event VARCHAR2(20);

​           Typ VARCHAR2(20);

​           Name VARCHAR2(30);

​           Owner VARCHAR2(30);

​       BEGIN

​           -- 读取DDL事件属性

​           Event := SYSEVENT;

​           Typ := DICTIONARY_OBJ_TYPE;

​           Name := DICTIONARY_OBJ_NAME;

​           Owner := DICTIONARY_OBJ_OWNER;

​           -- 将事件属性插入到事件日志表中

​           INSERT INTO scott.eventlog(eventname, obj_type, obj_name, obj_owner)

​              VALUES(event, typ, name, owner);

​       END;

​    ‘);

 

​    -- 创建LOGON、STARTUP和SERVERERROR 事件触发器

​    DBMS_UTILITY.EXEC_DDL_STATEMENT(‘

​       CREATE OR REPLACE TRIGGER trig_after

​           AFTER LOGON OR STARTUP OR SERVERERROR

ON DATABASE

​       DECLARE

​           Event VARCHAR2(20);

​           Instance NUMBER;

​           Err_num NUMBER;

​           Dbname VARCHAR2(50);

​           User VARCHAR2(30);

​       BEGIN

​           Event := SYSEVENT;

​           IF event = ‘’LOGON’’ THEN

​              User := LOGIN_USER;

​              INSERT INTO eventlog(eventname, username)

​                  VALUES(event, user);

​           ELSIF event = ‘’SERVERERROR’’ THEN

​              Err_num := SERVER_ERROR(1);

​              INSERT INTO eventlog(eventname, srv_error)

​                  VALUES(event, err_num);

​           ELSE

​              Instance := INSTANCE_NUM;

​              Dbname := DATABASE_NAME;

​              INSERT INTO eventlog(eventname, inst_num, db_name)

​                  VALUES(event, instance, dbname);

​           END IF;

​       END;

​    ‘);

 

​    -- 创建LOGOFF和SHUTDOWN 事件触发器

​    DBMS_UTILITY.EXEC_DDL_STATEMENT(‘

​       CREATE OR REPLACE TRIGGER trig_before

​           BEFORE LOGOFF OR SHUTDOWN

ON DATABASE

​       DECLARE

​           Event VARCHAR2(20);

​           Instance NUMBER;

​           Dbname VARCHAR2(50);

​           User VARCHAR2(30);

​       BEGIN

​           Event := SYSEVENT;

​           IF event = ‘’LOGOFF’’ THEN

​              User := LOGIN_USER;

​              INSERT INTO eventlog(eventname, username)

​                  VALUES(event, user);

​           ELSE

​              Instance := INSTANCE_NUM;

​              Dbname := DATABASE_NAME;

​              INSERT INTO eventlog(eventname, inst_num, db_name)

​                  VALUES(event, instance, dbname);

​           END IF;

​        END;

​    ‘);

END;

 

CREATE TABLE mydata(mydate NUMBER);

CONNECT SCOTT/TIGER

 

COL eventname FORMAT A10

COL eventdate FORMAT A12

COL username FORMAT A10

COL obj_type FORMAT A15

COL obj_name FORMAT A15

COL obj_owner FORMAT A10

SELECT eventname, eventdate, obj_type, obj_name, obj_owner, username, Srv_error

​    FROM eventlog;

 

DROP TRIGGER trig_ddl;

DROP TRIGGER trig_before;

DROP TRIGGER trig_after;

DROP TABLE eventlog;

 

