### PL/SQL

#### PL/SQL简介

PL/SQL不是一个独立的编程语言，它是Oracle编程环境中的工具。SQL * Plus 是一个互动工具，可以正在命令提示符下输入SQL和PL/SQL语句，将输入命令发送到数据库进行处理。语句处理之后将结果发回，并在屏幕上打印出来。

启动SQL * Plus

```SQL
sqlplus " / as sysdba"
```

#### PL/SQL基本语法

PL/SQL是块结构语言，PL/SQL程序划分成几个部分，并在每个部分中写入逻辑代码块。

每个块由3个子部分组成：

- 声明部分：以关键字DECLARE开头。这是一个可选部分，并定义了程序中要使用的所有变量、游标、子程序和其他元素。
- 可执行命令部分：在关键字BEGIN和END之间，这是一个强制性部分。由程序的可执行PL/SQL语句组成、至少有一个可执行代码行，可以只是一个NULL命名，标识不执行任何操作。
- 异常处理部分：以关键字EXCEPTION开头。这是一个可选部分，其包含处理程序中错误的异常。

每个PL/SQL语句以分号(;)结尾。使用BEGIN和END可以将PL/SQL块嵌套在其他PL/SQL块中。

```SQL
--PL/SQL块的基本结构
DECLARE
	<declarations section>
BEGIN
	<executable command(s)>
EXCEPTION
	<exception handing>
END;

--Hello World示例
DECLARE
	message varchar2(20) := "Hello World";
BEGIN
	dbms_output.put_line(message);
END;
```

END; 行标识PL/SQL块的结尾。要从SQL命令运行代码，需要在代码的最后一行之后输入/字符。

执行结果：

```SQL
Hello World

PL/SQL prodedure successfully completed.
```

##### PL/SQL标识符

PL/SQL标识符是常量、变量、异常、过程、游标和保留字、标识符包括一个字母，可以选地后跟多个字母，数字、美元符号、下环线和数字符号，不得超过30个字符。

默认情况下，标识符不区分大小写。例如：可以使用integer或者INTEGER来标识数值。不饿能使用保留关键字作为标识符。

##### PL/SQL分隔符

分隔符是具有特殊含义地符号。以下是PL/SQL中地分隔列表：


|                |                            |
| :------------: | :------------------------: |
|     分隔符     |            描述            |
|   +、-、*、/   | 加法、减法/负、乘法、除法  |
|       %        |          属性绑定          |
|                |        字符串分隔符        |
|       .        |         组件选择符         |
|      (,)       |     表达式或列表分隔符     |
|       ：       |       主机变量指示符       |
|       ，       |         项目分隔符         |
|       “        |      引用标识符分隔符      |
|       @        |       远程访问指示符       |
|       ;        |      声明或语句终止符      |
|       :=       |         赋值运算符         |
|       =>       |         关联运算符         |
|      \|\|      |         连接运算符         |
|       **       |         指数运算符         |
|     <<, >>     |   标签分隔符(开始和结束)   |
|     /*, */     | 多行注释分隔符(开始和结束) |
|       --       |       单行注释指示符       |
|       ..       |         范围运算符         |
|  <, >, <=, >=  |         关系运算符         |
| <>, `=, ~=, ^= |  不同版本地”不等于“运算符  |

##### PL/SQL注释

程序注释可以在编写的PL/SQL代码中包含的说明性文字，并帮助其他人阅读源码。所有编程语言都允许某种形式的注释。

PL/SQL支持单行和多行注释。注释中的所有字符都被PL/SQL编译器忽略。PL/SQL单行注释以分隔符开头 -- (双连字符)，多行注释由 /* 和 */括起来。

```SQL
--PL/SQL注释
DECLARE
	-- variable declaration
	message varchar2(20) := "Hello World";
BEGIN
	/*
	 * PL/SQL executable statement(s)
	 */
	 dbms_output.put_line(message);
END;
/
--开始执行...........
```

##### PL/SQL程序单元

PL/SQL单元是以下任何一个：

- PL/SQL块
- 函数
- 包
- 包体
- 过程
- 触发器
- 类型
- 类型体

#### PL/SQL数据类型

PL/SQL变量、常量和参数必须具有有效的数据类型，它指定存储格式，约束和有效的值范围。

**标量(SCALAR)类型**：它没有内部组件的单个值，例如：NUMBER, DATE 或BOOLEAN等

**大对象(LOB)类型**：指向与其他数据项（例如：文本、图形图像、视频剪辑和声音波形）分开存储的大对象的指针。

**复合类型**：具有可单独访问的内部组件的数据向。例如：集合和记录

**引用类型**：指向其他数据项

##### PL/SQL标量数据类型和子类型

PL/SQL标量数据类型和子类型分为以下几类：



|      |          |                                  |
| :--: | :------: | :------------------------------: |
| 序号 |   类型   |               描述               |
|  1   |   数字   |        执行算数运算的数值        |
|  2   |   字符   | 标识单个字符或字符串的字母数字值 |
|  3   |   布尔   |       执行逻辑运算的逻辑值       |
|  4   | 日期时间 |       用于表示日期和时间值       |

PL/SQL提供了数据类型的子类型。例如：NUMBER数据类型具有一个叫INTEGER的子类型。可以使用PL./SQL程序中的子类型将数据类型与其他程序中的数据类型兼容，同时将PL/SQL代码嵌入到另一个程序中(如Java程序)。

##### PL/SQL数值数据类型和子类型

列出了PL/SQL预定义的数子数据类型及其子类型：

|      |                      |                                                              |
| :--: | :------------------: | :----------------------------------------------------------: |
| 序号 |         类型         |                             描述                             |
|  1   |     PLS_INTEGER      | 带符号整数：`-2,147,483,648`至`2,147,483,647`，以`32`位表示  |
|  2   |    BINARY_INTEGER    | 带符号整数：`-2,147,483,648`至`2,147,483,647`，以`32`位表示  |
|  3   |     BINARY_FLOAT     |                  单精度`IEEE 754`格式浮点数                  |
|  4   |    BINARY_DOUBLE     |                  双精度`IEEE 754`格式浮点数                  |
|  5   | NUMBER(prec, scale)  | 在`1E-130`到(但不包括)`1.0E126`范围内的绝对值的定点或浮点数。`NUMBER`变量也可以表示`0` |
|  6   |   DEC(prec, scale)   |         ANSI特定定点类型，最大精度为`38`位十进制数字         |
|  7   | DECIMAL(prec, scale) |         IBM具体定点类型，最大精度为`38`位十进制数字          |
|  8   | NUMERIC(pre, secale) |               浮点型，最大精度为`38`位十进制数               |
|  9   |   DOUBLE PRECISION   | ANSI特定浮点类型，最大精度为`126`位二进制数字(大约38位十进制数字) |
|  10  |        FLOAT         | ANSI和IBM特定浮点类型，最大精度为`126`位二进制数字(大约`38`位十进制数字) |
|  11  |         INT          |          ANSI特定整数类型，最大精度为`38`位十进制数          |
|  12  |       INTEGER        |          ANSI特定整数类型，最大精度为`38`位十进制数          |
|  13  |       SMALLINT       |       ANSI和IBM特定整数类型，最大精度为`38`位十进制数        |
|  14  |         REAL         |        浮点型，最大精度为`63`位二进制数字(约十八位数)        |

示例：

```SQL
DECLARE
	num1 INTEGER;
	num2 REAL;
	num3 DOUBLE PRECISION;
BEGIN
	null;
END;
/
```

##### PL/SQL字符数据类型和子类型

PL/SQL预定义字符数据类型机器子类型：

|      |           |                                                              |
| :--: | :-------: | :----------------------------------------------------------: |
| 序号 |   类型    |                             描述                             |
|  1   |   CHAR    |            固定长度字符串，最大大小为`32,767`字节            |
|  2   | VARCHAR2  |            最大大小为`32,767`字节的可变长度字符串            |
|  3   |    RAW    | 最大大小为`32,767`字节的可变长度二进制或字节字符串，不由PL/SQL解释 |
|  4   |   NCHAR   |         固定长度的国家字符串，最大大小为`32,767`字节         |
|  5   | NVARCHAR2 |         可变长度的国家字符串，最大大小为`32,767`字节         |
|  6   |   LONG    |            最大长度为`32,760`字节的可变长度字符串            |
|  7   | LONG RAW  | 最大大小为`32,760`字节的可变长度二进制或字节字符串，不由PL/SQL解释 |
|  8   |   ROWID   |               物理行标识符，普通表中的行的地址               |
|  9   |  UROWID   |            通用行标识符(物理，逻辑或外部行标识符)            |

##### PL/SQL布尔数据类型

BOOLEAN数据类型存储逻辑运算中的逻辑值。逻辑值为布尔值：TRUE、FALSE以及NULL值。但是，SQL没有类似于BOOLEAN的数据类型。因此布尔值不能用于：

- SQL语句
- 内置SQL函数(例如：TO_CHAR)
- 从SQL语句调用PL/SQL函数

##### PL/SQL日期时间和间隔类型

DATE数据类型用于存储笃定长度的数据日期时间，其包括自午夜以来以秒为单位的时间。有效期为公元前4712年1月1日至公园9999年12月31日。

默认日期格式由Oracle初始化参数NLS_DATE_FORMATE设置。例如，默认值可能是”DD-MM-YY“,其中包括一个月的两位数字。月份名称的缩写以及年份的最后两位数字。例如：01-OCT-12

每个DATE类型的数据值包括世纪、年、月、日、时、分、秒，下表显示每个字段的有效值：



|                   |                                                         |                                                |
| :---------------: | :-----------------------------------------------------: | :--------------------------------------------: |
|      字段名       |                    有效的日期时间值                     |                   有效间隔值                   |
|       YEAR        |             `-4712`至`9999`(不包括第`0`年)              |                  任意非零整数                  |
|       MONTH       |                       `01` ~ `12`                       |                  `01` ~ `11`                   |
|        DAY        | `01`至`31`(限于`MONTH`和`YEAR`的值，根据本地日历的规则) |                  任何非零整数                  |
|       HOUR        |                       `00` ~ `23`                       |                  `00` ~ `23`                   |
|      MINUTE       |                       `00` ~ `59`                       |                  `00` ~ `59`                   |
|      SECOND       |      `00` ~ `59.9(n)`，其中`9(n)`是时间分秒的精度       | `00` ~ `59.9(n)`，其中`9(n)`是间隔分数秒的精度 |
|   TIMEZONE_HOUR   |             `-12`至`14`(范围适应夏令时更改)             |                     不适用                     |
| `TIMEZONE_MINUTE` |                       `00` ~ `59`                       |                     不适用                     |
|  TIMEZONE_REGION  |          在动态性能视图`V$TIMEZONE_NAMES`找到           |                     不适用                     |
|   TIMEZONE_ABBR   |          在动态性能视图`V$TIMEZONE_NAMES`找到           |                     不适用                     |

##### PL/SQL大对象(LOB)数据类型

大对象(LOB)数据类型指的是大数据项，如文本、图形图像、视频剪辑和声音波形。LOB数据类型允许对数据进行搞笑、随机、分段访问。以下是预定义的PL/SQL LOB数据类型：

|          |                                                    |                           |
| :------: | :------------------------------------------------: | :-----------------------: |
| 数据类型 |                        描述                        |           大小            |
|  BFILE   | 用于在数据库外的操作系统文件中存储大型二进制对象。 | 取决于系统，但不得超过4GB |
|   BLOB   |         用于在数据库中存储的大型二进制对象         |      `8TB`至`128TB`       |
|   CLOB   |            用于在数据库中存储大字符数据            |      `8TB`至`128TB`       |
|  NCLOB   |         用于在数据库中存储大块`NCHAR`数据          |      `8TB`至`128TB`       |

##### PL/SQL用户定义的子类型

子类型是另一种数据类型的子集，它称为基本类型。子类型具有与基本类型相同的操作，但只有基本类型有效值的子集。

PL/SQL预定义包STANDARD中的几个子类型。例如：PL/SQL预定义子类型CHARACTER和INTEGER

```SQL
SUBTYPE CHARACTER IS CHAR;
SUBTYPE INTEGER IS NUMBER(38, 0);
```

可定义和使用自己的子类型。

```SQL
--如何定义和使用用户定义的子类型
DECLARE 
   SUBTYPE name IS char(20); 
   SUBTYPE message IS varchar2(100); 
   salutation name; 
   greetings message; 
BEGIN 
   salutation := 'Reader '; 
   greetings := 'Welcome to the World of PL/SQL'; 
   dbms_output.put_line('Hello ' || salutation || greetings); 
END; 
/	
```

##### PL/SQL中的NULL

PL/SQL中的NULL值标识丢失或未知数据，它们不是整数、字符串或任何其他特定数据类型。

注意：NULL与空数据字符串或字符值\0不同。可以将一个null值分配给其他变量，但不能等同于任何东西，包括其自身(null)。

#### PL/SQL变量

PL/SQL中的变量，一个变量只不过是在程序中可以操纵的存储区域的名称。PL/SQL中每个变量都有一个指定的数据类型，其决定了变量内存的大小和布局。可以存储在存储器中的值的范围以及可应用于该变量的一组操作。

PL/SQL变量的名称由可选的字母、数字、美元($)符号，下划线和数字符号组成，不能超过30个字符。默认情况下，变量名不区分大小写。不饿能将保留的PL/SQL关键字用作变量名称。

PL/SQL变量语言允许定义各种类型的变量，如：日期时间数据类型、记录、集合等。

##### PL/SQL变量声明

必须在声明部分或包中声明PL/SQL变量作为全局变量。当声明一个变量时，PL/SQL为变量的值分配内存，并且存储位置由变量名称标识

声明变量的语法：

```SQL
variable_name [CONSTRANT] datatype [NOT NULL] [:= | DEFAULT INITIAL_VALUE]
```

variable_name是PL/SQL中的有效标识符，datatype必须是有效的PL/SQL数据类型或任何用户定义的数据类型。

```SQL
sales number(10, 2);
pi CONSTANT bouble precision := 3.1415;
name varchar2(25);
address varchar2(100);
```

当使用数据提供大小，比例或精度限制时，称为约束声明。有约束声明比无约束声明需要更少的内存。

```SQL
sales number(10, 2);
name vaechar2(25);
address varchar2(100);
```

##### PL/SQL变量初始化

无论何时声明一个变量，PL/SQL都会为变量分配一个默认值NULL。如果要是有NULL值的值初始化变量，则可以声明期间使用以下任意一种作法：

- DEFAULT 关键字
- 分配运算符

```SQL
conter binary_integer := 0;
greetings varchar2(20) DEFAULT 'Have a Good Day';
```

还可以使用`NOT NULL`约束指定变量不应该具有`NULL`值。 如果使用`NOT NULL`约束，则必须为变量显式分配初始值。

 初始化变量是一个很好的编程实践，否则有时程序会产生意想不到的结果。 

```SQL
DECLARE 
   a integer := 10; 
   b integer := 20; 
   c integer; 
   f real; 
BEGIN 
   c := a + b; 
   dbms_output.put_line('Value of c: ' || c); 
   f := 70.0/3.0; 
   dbms_output.put_line('Value of f: ' || f); 
END; 
/
```

##### PL/SQL变量作用域

PL/SQL允许块的嵌套，即每个成型快可以包含另一个内部快。如果在内部快中声明一个变量，则外部块不可访问内部变量。但是，如果一个变量声明并且可以被外部块访问，那么所有嵌套的内部快都可以访问该变量。

变量由两种类型的范围：

- 局部变量：内部快中声明的变量，外部快不可访问
- 全局变量：在最外部块或包中声明的变量

演示局部变量和全局变量的用法：

```SQL
DECLARE
	--Global variables
	num1 number := 95;
	num2 number := 85;
BEGIN  
   dbms_output.put_line('Outer Variable num1: ' || num1); 
   dbms_output.put_line('Outer Variable num2: ' || num2); 
   DECLARE  
      -- Local variables 
      num1 number := 195;  
      num2 number := 185;  
   BEGIN  
      dbms_output.put_line('Inner Variable num1: ' || num1); 
      dbms_output.put_line('Inner Variable num2: ' || num2); 
   END;  
END;
/
```

##### SQL查询结果分配给PL/SQL变量

可使用SQL的SECELT INTO语句将值分配给PL/SQL变量。对于SELECT列表中的每个项目，INTO列表必须有一个对应的类型兼容变量。

创建一个名为CUSTOMERS的表

```SQL
CREATE TABLE CUSTOMERS(
	ID INT NOT NULL,
    NAME VARCHAR(20) NOT NULL,
    AGE INT NOT NULL,
    ADDRESS CHAR(25),
    SALARY DECIMAL(18, 2),
    PRIMARY KEY (ID)
);
```

 向`CUSTOMERS`表中插入一些数据记录 

```SQL
INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY) 
VALUES (1, 'Ramesh', 32, 'Ahmedabad', 2000.00 );  

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY) 
VALUES (2, 'Khilan', 25, 'Delhi', 1500.00 );  

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY) 
VALUES (3, 'kaushik', 23, 'Kota', 2000.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY) 
VALUES (4, 'Chaitali', 25, 'Mumbai', 6500.00 ); 

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY) 
VALUES (5, 'Hardik', 27, 'Bhopal', 8500.00 );  

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY) 
VALUES (6, 'Komal', 22, 'MP', 4500.00 );
```

 使用SQL的`SELECT INTO`子句将上表中的值分配给PL/SQL变量 

```SQL
DECLARE 
   c_id customers.id%type := 1; 
   c_name  customerS.No.ame%type; 
   c_addr customers.address%type; 
   c_sal  customers.salary%type; 
BEGIN 
   SELECT name, address, salary INTO c_name, c_addr, c_sal 
   FROM customers 
   WHERE id = c_id;  
   dbms_output.put_line 
   ('Customer ' ||c_name || ' from ' || c_addr || ' earns ' || c_sal); 
END; 
/
```

#### PL/SQL常量和文字

常量在声明时指定值，并且在程序中不会更改。常量声明需要指定其名称，数据类型和值，并为其分配存储空间。声明也可以增加NOT NULL约束。

##### 声明常数

使用CONSTANT关键字声明常量。需要初始值，不允许在声明后更改该值。

示例：声明的常量PI

```SQL
PI CONSTANT NUMBER := 3.141592654;
DECLARE
	--CONSTANT DECLARATION
	pi constant number := 3.141592654;
	--other declarations
	radius number(5, 2);
	dia number(5, 2);
	cricumference number(7, 2);
	area number(10, 2);
BEGIN
	--PROCESSING
	radius := 9.5;  
	dia := radius * 2;  
    circumference := 2.0 * pi * radius; 
    area := pi * radius * radius; 
    -- output 
    dbms_output.put_line('半径: ' || radius); 
    dbms_output.put_line('直径: ' || dia); 
    dbms_output.put_line('圆周: ' || circumference); 
    dbms_output.put_line('面积: ' || area); 
END; 
/
```

输出：

```SQL
半径: 9.5 
直径: 19 
圆周: 59.69 
面积: 283.53  

Pl/SQL procedure successfully completed.
```

##### PL/SQL文字

声明常数

使用`CONSTANT`关键字声明常量。它需要初始值，不允许在声明后更改该值。下面示例中声明的常量：`PI`，详细代码如下 -

```sql
PI CONSTANT NUMBER := 3.141592654; 
DECLARE 
   -- constant declaration 
   pi constant number := 3.141592654; 
   -- other declarations 
   radius number(5,2);  
   dia number(5,2);  
   circumference number(7, 2); 
   area number (10, 2); 
BEGIN  
   -- processing 
   radius := 9.5;  
   dia := radius * 2;  
   circumference := 2.0 * pi * radius; 
   area := pi * radius * radius; 
   -- output 
   dbms_output.put_line('半径: ' || radius); 
   dbms_output.put_line('直径: ' || dia); 
   dbms_output.put_line('圆周: ' || circumference); 
   dbms_output.put_line('面积: ' || area); 
END; 
/
SQL
```

当上述代码在SQL提示符下执行时，它会产生以下结果 -

```shell
半径: 9.5 
直径: 19 
圆周: 59.69 
面积: 283.53  

Pl/SQL procedure successfully completed.
Shell
```

##### PL/SQL文字

文字是一个不由标识符表示的显式数字，字符，字符串或布尔值。 例如，`TRUE`，`7788`，`NULL`，`'yiibai tutorials'`分别是`Boolean`，`number`或`string`类型的文字。 PL/SQL，文字区分大小写。

PL/SQL支持以下几种文字：

- 数字文字
- 字符文字
- 字符串文字
- 布尔文字
- 日期和时间文字

 提供了所有这些类别的文字值的示例 ：

| 序号 |    文字类型    |                             示例                             |
| :--: | :------------: | :----------------------------------------------------------: |
|  1   |    数字文字    | `2346`,`050 78 -14 0 +32767`,`6.6667 0.0 -12.0 3.14159 +7800.00`,`6E5 1.0E-8 3.14159e0 -1E38 -9.5e-3` |
|  2   |    字符文字    |           `'A'`, `'%'`, `'9'`, `' '`, `'z'`, `'('`           |
|  3   |   字符串文字   |              `'Hello, world!'`,`'Yiibai Point'`              |
|  4   |    布尔文字    |                   `TRUE`, `FALSE`, `NULL`                    |
|  5   | 日期和时间文字 |            `'1998-08-25'`,`'2017-10-02 12:01:01'`            |

 在字符串文字中嵌入单引号，请将两个单引号放在一起，如以下程序所示：  

```SQL
DECLARE 
   message  varchar2(30):= 'What''s yiibai.com!'; 
BEGIN 
   dbms_output.put_line(message); 
END; 
/
```

#### PL/SQL运算符

运算符是一个符号，告诉编译器执行指定的数学或逻辑操作。PL/SQL语言中有丰富的内置运算符。

运算符有以下类型：

- 算术运算符
- 关系运算符
- 比较运算符
- 逻辑运算符
- 字符串运算符

##### 算术运算符

| 运算符 |                  描述                  |      示例       |
| :----: | :------------------------------------: | :-------------: |
|   +    |             两个操作数相加             |   A + B = 15    |
|   -    |        从第一个减去第二个操作数        |    A - B = 5    |
|   *    |            将两个操作数相乘            |   A * B = 50    |
|   /    |        从第一个除以第二个操作数        |    A / B = 2    |
|   **   | 指数运算符，提出一个操作数到其他的幂值 | A ** B = 100000 |

算术运算符示例：

```SQL
BEGIN  
   dbms_output.put_line( 10 + 5); 
   dbms_output.put_line( 10 - 5); 
   dbms_output.put_line( 10 * 5); 
   dbms_output.put_line( 10 / 5); 
   dbms_output.put_line( 10 ** 5); 
END; 
/
--输出
15 
5 
50 
2 
100000  

PL/SQL procedure successfully completed.
```

##### 关系运算符

关系运算符比较两个表达式或值，返回一个布尔结果。

|     运算符      |                             描述                             |        示例        |
| :-------------: | :----------------------------------------------------------: | :----------------: |
|        =        |       检查两个操作数的值是否相等，如果是，则条件成立。       |    (A = B)为假     |
| `!=`,`<>`，`~=` |  检查两个操作数的值是否相等，如果两个值不相等则条件成为真。  |    (A != B)为真    |
|        >        | 检查左操作数的值是否大于右操作数的值，如果是，则条件成为真。 |    (A > B) 为假    |
|        <        | 检查左操作数的值是否小于右操作数的值，如果是，则条件成为真。 | (A < B) 条件为真。 |
|       \>=       | 检查左操作数的值是否大于或等于右操作数的值，如果是，则条件成为真。 |   (A >= B) 为假    |
|       <=        | 检查左操作数的值是否小于或等于右操作数的值，如果是，则条件成为真。 |   (A <= B) 为真    |

关系运算符示例：

```SQL
DECLARE 
   a number (2) := 21; 
   b number (2) := 10; 
BEGIN 
   IF (a = b) then 
      dbms_output.put_line('Line 1 - a is equal to b'); 
   ELSE 
      dbms_output.put_line('Line 1 - a is not equal to b'); 
   END IF;  
   IF (a < b) then 
      dbms_output.put_line('Line 2 - a is less than b'); 
   ELSE 
      dbms_output.put_line('Line 2 - a is not less than b'); 
   END IF; 

   IF ( a > b ) THEN 
      dbms_output.put_line('Line 3 - a is greater than b'); 
   ELSE 
      dbms_output.put_line('Line 3 - a is not greater than b'); 
   END IF;  
   -- Lets change value of a and b 
   a := 5; 
   b := 20; 
   IF ( a <= b ) THEN 
      dbms_output.put_line('Line 4 - a is either equal or less than b'); 
   END IF; 
   IF ( b >= a ) THEN 
      dbms_output.put_line('Line 5 - b is either equal or greater than a'); 
   END IF;
   IF ( a <> b ) THEN 
      dbms_output.put_line('Line 6 - a is not equal to b'); 
   ELSE 
      dbms_output.put_line('Line 6 - a is equal to b'); 
   END IF;  
END; 
/

--输出
Line 1 - a is not equal to b 
Line 2 - a is not less than b 
Line 3 - a is greater than b 
Line 4 - a is either equal or less than b 
Line 5 - b is either equal or greater than a 
Line 6 - a is not equal to b  

PL/SQL procedure successfully completed
```

##### 比较运算符

比较运算符用于将一个表达式与另一个表达式作比较，结果始终为TRUE、FALSE或NULL。

| 运算符  |                             描述                             |                             示例                             |
| :-----: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|  LIKE   | `LIKE`运算符将字符，字符串或`CLOB`值与模式进行比较，如果值与模式匹配，则返回`TRUE`，否则返回`FALSE` | 如果`'Zara Ali'` `LIKE 'Z％A_i'`返回一个布尔值`true`，而`'Nuha Ali' LIKE'Z％A_i'`返回一个布尔值。 |
| BETWEEN | `BETWEEN`运算符测试值是否在指定范围内。`x BETWEEN a AND b`表示`x >= a`和`x <= b`。 | 如果`x = 10`，那么在`5`到`20`之间则`x`返回`true`，`x`在`5`和`10`之间则`x`返回true，但是`x`在`11`和`20`之间返回`false`。 |
|   IN    | `IN`运算符测试集成员数据。 `x IN(set)`表示`x`等于集合中的任何成员数据。 | 如果`x ='m'`，则在`('a'，'b'，'c')`中`x`返回`false`，而在`('m'，'n'，'o')`中`x`返回`true`。 |
| IS NULL | `IS NULL`运算符如果其操作数为`NULL`返回值为`TRUE`，如果不为`NULL`则返回`FALSE`。 涉及`NULL`值的比较总是产生`NULL`。 |           如果`x ='m'`，则`is null'`返回`false` 。           |

LIKE运算符示例： 这里使用一个小的过程`procedure()`来显示`LIKE`运算符的功能 

```SQL
DECLARE 
PROCEDURE compare (value  varchar2,  pattern varchar2 ) is 
BEGIN 
   IF value LIKE pattern THEN 
      dbms_output.put_line ('True'); 
   ELSE 
      dbms_output.put_line ('False'); 
   END IF; 
END;  
BEGIN 
   compare('Zara Ali', 'Z%A_i'); 
   compare('Nuha Ali', 'Z%A_i'); 
END; 
/

--输出
True 
False  

PL/SQL procedure successfully completed.
```

BETWEEN运算符示例：

```SQL
DECLARE 
   x number(2) := 10; 
BEGIN 
   IF (x between 5 and 20) THEN 
      dbms_output.put_line('True'); 
   ELSE 
      dbms_output.put_line('False'); 
   END IF; 

   IF (x BETWEEN 5 AND 10) THEN 
      dbms_output.put_line('True'); 
   ELSE 
      dbms_output.put_line('False'); 
   END IF; 

   IF (x BETWEEN 11 AND 20) THEN 
      dbms_output.put_line('True'); 
   ELSE 
      dbms_output.put_line('False'); 
   END IF; 
END; 
/

--输出
True 
True 
False 

PL/SQL procedure successfully completed.
```

IN和IS NULL运算符：

```SQL
ECLARE 
   letter varchar2(1) := 'm'; 
BEGIN 
   IF (letter in ('a', 'b', 'c')) THEN 
      dbms_output.put_line('True'); 
   ELSE 
      dbms_output.put_line('False'); 
   END IF; 

   IF (letter in ('m', 'n', 'o')) THEN 
       dbms_output.put_line('True'); 
   ELSE 
      dbms_output.put_line('False'); 
   END IF; 

   IF (letter is null) THEN 
    dbms_output.put_line('True'); 
   ELSE 
      dbms_output.put_line('False'); 
   END IF; 
END; 
/

--输出
False
True
False

PL/SQL procedure successfully completed.
```

##### 逻辑运算符

运算符使用布尔运算符并产生布尔运算结果，假设变量A = TRUE， 变量 B = FALSE

| 运算符 |                             描述                             |        示例        |
| :----: | :----------------------------------------------------------: | :----------------: |
|  and   |       逻辑与运算符。如果两个操作数都为真，则条件成立。       |   (A and B) 为假   |
|   or   | 逻辑或运算符。如果两个操作数中的任何一个为真，则条件成为真。 |    (A or B)是真    |
|  not   | 逻辑非运算符。用于反转其操作数的逻辑状态。如果条件为真，则逻辑NOT运算符将使其为`false`。 | (not A)结果为FALSE |

逻辑运算符示例：

```SQL
DECLARE 
   a boolean := true; 
   b boolean := false; 
BEGIN 
   IF (a AND b) THEN 
      dbms_output.put_line('Line 1 - Condition is true'); 
   END IF; 
   IF (a OR b) THEN 
      dbms_output.put_line('Line 2 - Condition is true'); 
   END IF; 
   IF (NOT a) THEN 
      dbms_output.put_line('Line 3 - a is not true'); 
   ELSE 
      dbms_output.put_line('Line 3 - a is true'); 
   END IF; 
   IF (NOT b) THEN 
      dbms_output.put_line('Line 4 - b is not true'); 
   ELSE 
      dbms_output.put_line('Line 4 - b is true'); 
   END IF; 
END;
/

--输出
Line 2 - Condition is true 
Line 3 - a is true 
Line 4 - b is not true  

PL/SQL procedure successfully completed.
```

##### 运算符优先级别

运算符优先级决定表达式中术语的分组。这会影响表达式的评估求值顺序。某些运算符的优先级高于其他运算符; 例如，乘法运算符的优先级高于加法运算符。

例如，`x = 7 + 3 * 2`; 这里，求值结果`x`的值为`13`，而不是`20`，因为运算符 `*`的优先级高于`+`，所以它首先被乘以`3 * 2`，然后再加上`7`。

优先级最高的运算符出现在表的顶部，最底层的运算符出现在底部。在一个表达式中，将首先评估求值较高优先级的运算符。

运算符的优先级如下：`=`，`<`，`>`，`<=`，`>=`，`<>`，`！=`，`〜=`，`^=`，`IS NULL`，`LIKE`，`BETWEEN`，`IN`。

|    运算符    |   操作描述   |
| :----------: | :----------: |
|   `*`, `/`   | 指数幂运算符 |
|   `+`, `-`   | 标识符，负数 |
|   `*`, `/`   |  乘法，除法  |
| `+`, `-`, ΙΙ | 加，减，连接 |
|     NOT      |   逻辑否定   |
|     AND      |     AND      |
|      OR      | 包含(逻辑或) |

运算符优先级示例：

```SQL
DECLARE 
   a number(2) := 20; 
   b number(2) := 10; 
   c number(2) := 15; 
   d number(2) := 5; 
   e number(2) ; 
BEGIN 
   e := (a + b) * c / d;      -- ( 30 * 15 ) / 5 
   dbms_output.put_line('Value of (a + b) * c / d is : '|| e );  
   e := ((a + b) * c) / d;   -- (30 * 15 ) / 5 
   dbms_output.put_line('Value of ((a + b) * c) / d is  : ' ||  e );  
   e := (a + b) * (c / d);   -- (30) * (15/5) 
   dbms_output.put_line('Value of (a + b) * (c / d) is  : '||  e );  
   e := a + (b * c) / d;     --  20 + (150/5) 
   dbms_output.put_line('Value of a + (b * c) / d is  : ' ||  e ); 
END; 
/

--输出
Value of (a + b) * c / d is : 90 
Value of ((a + b) * c) / d is  : 90 
Value of (a + b) * (c / d) is  : 90 
Value of a + (b * c) / d is  : 50  

PL/SQL procedure successfully completed.
```

#### PL/SQL条件控制

决策结构要求程序员指定要由程序评估或测试一个或多个条件，以及如果条件为真(true)，则执行对应的语句块，以及可选地，如果执行其他语句条件被确定为假(fasle)。

大多数编程语言中的典型条件(即决策)结构的一般形式：
![1640934645557](Images/1640934645557.png)

PL/SQL编程语言提供以下类型的决策语句：

| 编号 |        语句        |                             说明                             |
| :--: | :----------------: | :----------------------------------------------------------: |
|  1   |    if-then语句     | `IF`语句将条件与关键字`THEN`和`END IF`包含语句序列相关联。如果条件为`true`，则语句将被执行，如果条件为`false`或`NULL`，则`IF`语句不会执行任何操作。 |
|  2   |  if-then-else语句  | `IF`语句添加了关键字`ELSE`，后跟一个备选的语句序列。如果条件为`false`或`NULL`，则只有备选的语句序列被执行。它只执行语句序列中的任一个。 |
|  3   | if-then-elsif语句  |                   它允许选择几种备选方案。                   |
|  4   |      case语句      | 像`IF`语句一样，`CASE`语句选择要执行的一个语句序列。但是，要选择序列，`CASE`语句使用选择器而非多个布尔表达式。选择器是一个表达式，它的值用于选择几种备选方案之一。 |
|  5   |    搜索CASE语句    | 被搜索CASE语句没有选择器，它的`WHEN`子句将包含产生布尔值的搜索条件。 |
|  6   | 嵌套if-then-el语句 | 可以在一个`IF-THEN`或`IF-THEN-ELSIF`语句中使用另一个`IF-THEN`或`IF-THEN-ELSIF`语句。 |

##### IF-THEN

`if-then`语句是`IF`控制语句中最简单的形式，经常用于决策和更改程序执行的控制流程。

`IF`语句将条件与关键字`THEN`和`END IF`所包含的语句序列相关联。如果条件为`TRUE`，则语句将被执行，如果条件为`FALSE`或`NULL`，则`IF`语句块不会执行任何操作。

语法：

```SQL
--IF-THEN语句的语法
IF condition THEN
	S;
END IF;
```

 `condition`是布尔或关系条件，`S`是简单或复合语句。 以下是`IF-THEN`语句的一个例子 

```SQL
IF (a <= 20) THEN
	c := c + 1;
END IF;
```

如果布尔表达式条件求值为`true`，则`if`语句中的代码块将被执行。如果布尔表达式求值为`false`，则`if`语句结束后的第一组代码(在结束结束`if`之后)将被执行。

流程图：

![1640935097347](Images/1640935097347.png)

示例1：理解上面的执行流程 

```SQL
DECLARE 
   a number(2) := 10; 
BEGIN 
   a:= 10; 
  -- check the boolean condition using if statement  
   IF( a < 20 ) THEN 
      -- if condition is true then print the following   
      dbms_output.put_line('a is less than 20 ' ); 
   END IF; 
   dbms_output.put_line('value of a is : ' || a); 
END; 
/

--输出
a is less than 20 
value of a is : 10  

PL/SQL procedure successfully completed.
```

示例2： 创建了一个表和几个记录，参考以下语句操作上述表和数据  

```SQL
DECLARE 
   c_id customers.id%type := 1; 
   c_sal  customers.salary%type; 
BEGIN 
   SELECT  salary  
   INTO  c_sal 
   FROM customers 
   WHERE id = c_id; 
   IF (c_sal <= 2000) THEN 
      UPDATE customers  
      SET salary =  salary + 1000 
         WHERE id = c_id; 
      dbms_output.put_line ('Salary updated'); 
   END IF; 
END; 
/

--输出
Salary updated  

PL/SQL procedure successfully completed.
```

##### IF-THEN-ELSE

`IF-THEN`语句的序列之后的`ELSE`语句的可选序列，`ELSE`语句块在`IF`条件为`FALSE`时执行。

语法：

```SQL
--IF-THEN-ELSE语句的语法
IF condition THEN
	S1;
ELSE
	S2;
END IF;
```

其中，`S1`和`S2`是不同的语句序列。 在`IF-THEN-ELSE`语句中，当测试条件为`TRUE`时，执行语句`S1`并跳过`S2`; 当测试条件为`FALSE`时，则跨过`S1`并执行语句`S2`中的语句块。

```SQL
IF color = red THEN 
  dbms_output.put_line('You have chosen a red car') 
ELSE 
  dbms_output.put_line('Please choose a color for your car'); 
END IF;
/
```

 如果布尔表达式条件求值为真，则将执行`if-then`代码块，否则将执行`else`代码块。 

流程图：
![1640935340168](Images/1640935340168.png)

示例：

```SQL
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   a number(3) := 100; 
BEGIN 
   -- check the boolean condition using if statement  
   IF( a < 20 ) THEN 
      -- if condition is true then print the following   
      dbms_output.put_line('a is less than 20 ' ); 
   ELSE 
      dbms_output.put_line('a is not less than 20 ' ); 
   END IF; 
   dbms_output.put_line('value of a is : ' || a); 
END; 
/
```

##### IF-THEN-ELSIF

在PL/SQL中，`IF-THEN-ELSIF`语句允许在多种选择之间进行选择。`IF-THEN`语句后面可以有一个可选的`ELSIF ... ELSE`语句。 `ELSIF`子句可用于添加附加条件。

使用`IF-THEN-ELSIF`语句时需要注意几点。

- 需要看清楚，它是`ELSIF`，并不是`ELSEIF`。
- `IF-THEN`语句可以有零个或一个`ELSE`，它必须在`ELSIF`之后。
- `IF-THEN`语句可以有零或多个`ELSIF`，它们必须在`ELSE`之前。
- 一旦有一个`ELSIF`条件测试成功，其余的`ELSIF`或`ELSE`都不会再被测试。

语法：

```SQL
--PL/SQL编程语言中的IF-THEN-ELSIF语句的语法
IF(boolean_expression 1)THEN  
   S1; -- Executes when the boolean expression 1 is true  
ELSIF( boolean_expression 2) THEN 
   S2;  -- Executes when the boolean expression 2 is true  
ELSIF( boolean_expression 3) THEN 
   S3; -- Executes when the boolean expression 3 is true  
ELSE  
   S4; -- executes when the none of the above condition is true  
END IF;
/
```

示例：

```SQL
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   a number(3) := 100; 
BEGIN 
   IF ( a = 10 ) THEN 
      dbms_output.put_line('Value of a is 10' ); 
   ELSIF ( a = 20 ) THEN 
      dbms_output.put_line('Value of a is 20' ); 
   ELSIF ( a = 30 ) THEN 
      dbms_output.put_line('Value of a is 30' ); 
   ELSE 
       dbms_output.put_line('None of the values is matching'); 
   END IF; 
   dbms_output.put_line('Exact value of a is: '|| a );  
END; 
/
```

##### CASE 				 				 				 			

像`IF`语句一样，`CASE`语句选择要执行的一个语句序列。 但是，要选择序列，`CASE`语句使用选择器而不是多个布尔表达式。选择器是一个表达式，其值用于选择几种替代方法之一。

语法：

```SQL
--PL/SQL中的case语句的语法
CASE selector 
   WHEN 'value1' THEN S1; 
   WHEN 'value2' THEN S2; 
   WHEN 'value3' THEN S3; 
   ... 
   ELSE Sn;  -- default case 
END CASE;
/
```

流程图：

![1640935570164](Images/1640935570164.png)

示例：

```SQL
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   grade char(1) := 'A'; 
BEGIN 
   CASE grade 
      when 'A' then dbms_output.put_line('Excellent'); 
      when 'B' then dbms_output.put_line('Very good'); 
      when 'C' then dbms_output.put_line('Well done'); 
      when 'D' then dbms_output.put_line('You passed'); 
      when 'F' then dbms_output.put_line('Better try again'); 
      else dbms_output.put_line('No such grade'); 
   END CASE; 
END; 
/
```

##### 搜索CASE	 				 				 				 			

可搜索的`CASE`语句没有选择器，语句中的`WHEN`子句包含给出布尔值的搜索条件。

语法：

```SQL
--PL/SQL中可搜索的case语句的语法
CASE 
   WHEN selector = 'value1' THEN S1; 
   WHEN selector = 'value2' THEN S2; 
   WHEN selector = 'value3' THEN S3; 
   ... 
   ELSE Sn;  -- default case 
END CASE;
/
```

流程图：

![1640935693811](Images/1640935693811.png)

示例：

```SQL
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   grade char(1) := 'B'; 
BEGIN 
   case  
      when grade = 'A' then dbms_output.put_line('Excellent'); 
      when grade = 'B' then dbms_output.put_line('Very good'); 
      when grade = 'C' then dbms_output.put_line('Well done'); 
      when grade = 'D' then dbms_output.put_line('You passed'); 
      when grade = 'F' then dbms_output.put_line('Better try again'); 
      else dbms_output.put_line('No such grade'); 
   end case; 
END; 
/
```

##### 嵌套IF-THEN-ELSE

在PL/SQL编程中嵌套`IF-ELSE`语句总是合法的，也就是说可以在一个`IF`或`ELSE IF`语句中使用另一个`IF`或`ELSE IF`语句。

语法：

```SQL
--PL/SQL中嵌套IF-ELSE语句的语法
IF( boolean_expression 1)THEN 
   -- executes when the boolean expression 1 is true  
   IF(boolean_expression 2) THEN 
      -- executes when the boolean expression 2 is true  
      sequence-of-statements; 
   END IF; 
ELSE 
   -- executes when the boolean expression 1 is not true 
   else-statements; 
END IF;
/
```

示例：

```SQL
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   a number(3) := 100; 
   b number(3) := 200; 
BEGIN 
   -- check the boolean condition  
   IF( a = 100 ) THEN 
   -- if condition is true then check the following  
      IF( b = 200 ) THEN 
      -- if condition is true then print the following  
      dbms_output.put_line('Value of a is 100 and b is 200' ); 
      END IF; 
   END IF; 
   dbms_output.put_line('Exact value of a is : ' || a ); 
   dbms_output.put_line('Exact value of b is : ' || b ); 
END; 
/
```

#### PL/SQL循环

当需要执行一段代码多次时，可能会出现以下这种情况：一般来说，语句依次执行，首先执行函数中第一个语句，然后执行第二个语句，依次类推。

编程语言提供了允许更复杂的执行路径的各种控制结构。循环语句允许多次执行一个语句或一组语句，以下是大多编程语言中循环语句的一般流程图：

![1640936069742](Images/1640936069742.png)

 PL/SQL提供以下类型的循环来处理循环需求。可点击以下链接查看每个循环类型如何使用。 

| 编号 |   循环类型   |                             描述                             |
| :--: | :----------: | :----------------------------------------------------------: |
|  1   | 基本LOOP循环 | 在这个循环结构中，语句序列包含在`LOOP`和`END LOOP`语句之间。在每次迭代时，执行语句序列，然后在循环顶部继续控制。 |
|  2   |  while循环   | 当给定条件为真时，重复一个语句或一组语句。它在执行循环体之前测试状态。 |
|  3   |   for循环    |        多次执行一系列语句，并缩写管理循环变量的代码。        |
|  4   |   嵌套循环   | 可在任何其他基本循环中使用一个或多个循环，如：`while`或`for`循环。 |

##### LOOP

基本循环结构包含`LOOP`和`END LOOP`语句之间的语句序列。通过每次迭代，执行语句序列，然后在循环顶部继续控制。

语法：

```SQL
--PL/SQL编程语言的基本循环语法
LOOP
	Sequence of statements;
END LOOP;
```

语句序列(`Sequence of statements;`)可以是单个语句或一组语句。需要一个`EXIT`语句或一个`EXIT WHEN`语句来中断循环。

示例：

```SQL
--演示LOOP语句如何使用
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   x number := 10; 
BEGIN 
   LOOP 
      dbms_output.put_line(x); 
      x := x + 10; 
      IF x > 50 THEN 
         exit; 
      END IF; 
   END LOOP; 
   -- after exit, control resumes here  
   dbms_output.put_line('After Exit x is: ' || x); 
END; 
/


--使用EXIT WHEN语句来代替EXIT语句
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   x number := 10; 
BEGIN 
   LOOP 
      dbms_output.put_line(x); 
      x := x + 10; 
      exit WHEN x > 50; 
   END LOOP; 
   -- after exit, control resumes here 
   dbms_output.put_line('After Exit x is: ' || x); 
END; 
/
```

##### while

 只要给定条件为真，PL/SQL编程语言中的`WHILE LOOP`语句重复执行目标语句。 

语法：

```SQL
--WHILE LOOP语句的语法
WHILE condition LOOP 
   sequence_of_statements 
END LOOP;
```

示例：

```SQL
--有关WHILE LOOP语句的应用
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   a number(2) := 10; 
BEGIN 
   WHILE a < 20 LOOP 
      dbms_output.put_line('value of a: ' || a); 
      a := a + 1; 
   END LOOP; 
END; 
/
```

##### FOR

 `FOR LOOP`语句是一种重复控制结构，可以有效地编写一个需要执行特定次数的循环。 

语法：

```SQL
--如何使用FOR LOOP语句
FOR counter IN initial_value .. final_value LOOP 
   sequence_of_statements; 
END LOOP;
```

以下是`FOR`循环中的控制流程 - 

- 首先执行初始步骤，只执行一次。 此步骤允许声明和初始化任何循环控制变量。
- 接下来，评估条件，即`initial_value .. final_value`。如果结果为`TRUE`，则执行循环的主体。如果结果为`FALSE`，则循环主体不执行，并且控制流程跳转到`for`循环之后的下一个语句。
- 执行`for`循环的主体后，增加或减少计数器变量的值。
- 现在再次评估条件。 如果计算为`TRUE`，则执行循环并且该过程重复(循环体，然后增量步，然后再次调节)。 条件变为`FALSE`后，`FOR-LOOP`终止。

以下是PL/SQL `for`循环的一些特殊特性 -

- 循环变量或计数器的`initial_value`和`final_value`可以是文字，变量或表达式，但必须对数字求值。 否则，PL/SQL引发预定义的异常`VALUE_ERROR`。
- `initial_value`不必为`1`; 但是，循环计数器增量(或减量)必须为`1`。
- PL/SQL允许在运行时动态地确定循环范围。

示例：

```SQL
--演示如何使用for循环
SET SERVEROUTPUT ON SIZE 100000;
DECLARE 
   a number(2); 
BEGIN 
   FOR a in 10 .. 20 LOOP 
      dbms_output.put_line('value of a: ' || a); 
  END LOOP; 
END; 
/
```

##### 嵌套循环

 PL/SQL允许在另一个循环中使用一个循环。 以下部分显示了几个例子来说明这个概念。 

```SQL
--PL/SQL中嵌套的基本LOOP语句的语法
LOOP 
   Sequence of statements1 
   LOOP 
      Sequence of statements2 
   END LOOP; 
END LOOP;


--PL/SQL中嵌套FOR LOOP语句的语法
FOR counter1 IN initial_value1 .. final_value1 LOOP 
   sequence_of_statements1 
   FOR counter2 IN initial_value2 .. final_value2 LOOP 
      sequence_of_statements2 
   END LOOP; 
END LOOP;

--PL/SQL中嵌套的WHILE LOOP循环语句的语法
WHILE condition1 LOOP 
   sequence_of_statements1 
   WHILE condition2 LOOP 
      sequence_of_statements2 
   END LOOP; 
END LOOP;
```

示例：

```SQL
--使用嵌套的基本循环来求出2到100之间的素数
SET SERVEROUTPUT ON SIZE 999999;
DECLARE 
   i number(3); 
   j number(3); 
BEGIN 
   i := 2; 
   LOOP 
      j:= 2; 
      LOOP 
         exit WHEN ((mod(i, j) = 0) or (j = i)); 
         j := j +1; 
      END LOOP; 
   IF (j = i ) THEN 
      dbms_output.put_line(i || ' is prime'); 
   END IF; 
   i := i + 1; 
   exit WHEN i = 50; 
   END LOOP; 
END; 
/
```

##### 标记PL/SQL循环

在PL/SQL中，可以标记PL/SQL循环。标签使用双尖括号(`<<`和`>>`)括起来，并显示在LOOP语句的开头。标签名称也可以出现在`LOOP`语句的末尾。可以使用`EXIT`语句中的标签退出循环。

```SQL
--以下程序说明了这个概念
SET SERVEROUTPUT ON SIZE 1000000;
DECLARE 
   i number(1); 
   j number(1); 
BEGIN 
   << outer_loop >> 
   FOR i IN 1..3 LOOP 
      << inner_loop >> 
      FOR j IN 1..3 LOOP 
         dbms_output.put_line('i is: '|| i || ' and j is: ' || j); 
      END loop inner_loop; 
   END loop outer_loop; 
END; 
/
```

#### 循环控制语句

循环控制语句从其正常顺序更改执行。当执行离开范围时，在该范围内创建的所有自动对象都将被销毁。

PL/SQL支持以下控制语句。标签循环也有助于控制环外的控制。

| 编号 |   控制语句   |                             描述                             |
| :--: | :----------: | :----------------------------------------------------------: |
|  1   |   EXIT语句   |    Exit语句完成循环，控制在`END LOOP`之后立即传递给语句。    |
|  2   | CONTINUE语句 | 导致循环跳过其主体的剩余部分，并在重申之前立即重新测试其状态。 |
|  3   |   GOTO语句   |    转移控制到标记语句。虽然不建议在程序中使用`GOTO`语句。    |

##### EXIT

PL/SQL编程语言中的`EXIT`语句有以下两种用法 -

- 当循环中遇到EXIT语句时，循环将立即终止，程序控制在循环之后的下一个语句处恢复。
- 如果使用嵌套循环(即在另一个循环中有一个循环)，则`EXIT`语句将停止执行最内循环，并在块之后开始执行下一行代码。

语法：

```SQL
--PL/SQL中EXIT语句的语法
EXIT;
```

流程图：

![1640937092865](Images/1640937092865.png)

示例：

```SQL
--如何使用exit语句
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   a number(2) := 10; 
BEGIN 
   -- while loop execution  
   WHILE a < 20 LOOP 
      dbms_output.put_line ('value of a: ' || a); 
      a := a + 1; 
      IF a > 15 THEN 
         -- terminate the loop using the exit statement 
         EXIT; 
      END IF; 
   END LOOP; 
END; 
/
```

#####  EXIT WHEN

`EXIT-WHEN`语句允许评估`WHEN`子句中的条件。如果条件为:`TRUE`，则循环完成，并且在`END LOOP`之后立即将控制传递给语句。

以下是`EXIT WHEN`语句的两个重点 -

- 在条件为真之前，`EXIT-WHEN`语句的作用就像一个`NULL`语句，除了评估条件，并且不终止循环。
- 循环内的语句必须改变条件的值。

语法：

```SQL
--PL/SQL中的EXIT WHEN语句的语法
EXIT WHEN condition;
--EXIT WHEN语句替换if-then与EXIT语句一起使用的条件语句。
```

示例：

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   a number(2) := 10; 
BEGIN 
   -- while loop execution  
   WHILE a < 20 LOOP 
      dbms_output.put_line ('value of a: ' || a);  
      a := a + 1; 
      -- terminate the loop using the exit when statement 
   EXIT WHEN a > 15; 
   END LOOP; 
END;   
/
```

##### CONTINUE

`CONTINUE`语句导致循环跳过其主体的剩余部分，并在重新执行之前立即重新测试其状态。换句话说，它强制循环的下一次迭代发生，跳过其间(之后)的任何代码。

语法：

```SQL
--CONTINUE语句的语法
CONTINUE;
```

流程图：

![1640937275056](Images/1640937275056.png)

示例：

```SQL
--如何使用continue语句
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   a number(2) := 10; 
BEGIN 
   -- while loop execution  
   WHILE a < 20 LOOP 
      dbms_output.put_line ('value of a: ' || a); 
      a := a + 1; 
      IF a = 15 THEN 
         -- skip the loop using the CONTINUE statement 
         a := a + 1; 
         CONTINUE; -- 之后的代码跳过，回到条件开始重新迭代
      END IF; 
   END LOOP; 
END; 
/
```

##### GOTO

PL/SQL编程语言中的`GOTO`语句在同一子程序中提供从`GOTO`到标记语句的无条件跳转。

注意 - 在任何编程语言中不推荐使用GOTO语句，因为它难以追踪程序的控制流程，使程序难以理解和难以修改。 任何使用GOTO的程序都可以重写，以便将GOTO语句替换成其它语句。

语法：

```SQL
--PL/SQL中GOTO语句的语法
GOTO label;
..
..
<< label >>
statement;
```

流程图：

![1640937381108](Images/1640937381108.png)

示例：

```SQL
--goto语句的使用
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   a number(2) := 10; 
BEGIN 
   <<loopstart>> 
   -- while loop execution  
   WHILE a < 20 LOOP
   dbms_output.put_line ('value of a: ' || a); 
      a := a + 1; 
      IF a = 15 THEN 
         a := a + 1; 
         GOTO loopstart; 
      END IF; 
   END LOOP; 
END; 
/
```

**GOTO语句局限性**

PL/SQL中的GOTO语具有以下局限性 

- GOTO语句不能分支到`IF`语句，`CASE`语句，`LOOP`语句或子块中。
- GOTO语句不能从一个`IF`语句子句分支到另一个`IF`语句，或从一个`CASE`语句的`WHEN`子句分支到另一个。
- GOTO语句不能从外部块分支到子块(即，内部`BEGIN-END`块)。
- GOTO语句不能分支出子程序。要尽早结束子程序，请使用`RETURN`语句或将`GOTO`分支到子程序结束之前的某个地方。
- GOTO语句不能从异常处理程序分支回当前的`BEGIN-END`块。 但是，GOTO语句可以从异常处理程序分支到一个封闭的块中。

#### PL/SQL字符串

PL/SQL中字符串实际上是一个具有可选大小规格的字符序列。字符可以是数字、字母、空白、特殊字符或全部的组合、PL/SQL提供三种字符串：

- 固定长度字符串* - 在这样的字符串中，程序员在声明字符串时指定长度。该字符串的右边填充规定的长度。
- 可变长度字符串* - 在这样的字符串中，指定字符串的最大长度达`32,767`，并且不会填充。
- 字符大对象(CLOB)* - 这些可变长度字符串最多可达`128TB`。

PL/SQL字符串可以是变量或文字。字符串文字用引号括起来。例如：

```SQL
'This is a string literal.' 
--或者 
'hello world'
```

 在字符串文字中包含单引号，需要在彼此之间键入两个单引号。 例如:

```SQL
'this isn''t what it looks like'
```

##### 声明字符串变量

Oracle数据库提供了许多字符串数据类型，如：`CHAR`，`NCHAR`，`VARCHAR2`，`NVARCHAR2`，`CLOB`和`NCLOB`。 以`“N”`为前缀的数据类型为“国家字符集”数据类型，用于存储Unicode字符数据。

需要声明一个可变长度的字符串，则必须提供该字符串的最大长度。例如，`VARCHAR2`数据类型。 以下示例说明声明和使用一些字符串变量：

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   name varchar2(20); 
   company varchar2(30); 
   introduction clob; 
   choice char(1); 
BEGIN 
   name := 'Max Su'; 
   company := 'Hixiaoniu'; 
   introduction := ' Hello! I''m Max Su from Hixiaoniu.'; 
   choice := 'y'; 
   IF choice = 'y' THEN 
      dbms_output.put_line(name); 
      dbms_output.put_line(company); 
      dbms_output.put_line(introduction); 
   END IF; 
END; 
/
```

声明一个固定长度的字符串，请使用`CHAR`数据类型。 在这里，不必为固定长度变量指定最大长度。 如果不考虑长度约束，Oracle数据库将自动使用所需的最大长度。以下两个声明是相同的:

```SQL
red_flag CHAR(1) := 'Y'; 
red_flag CHAR   := 'Y';
```

##### 字符串函数和运算符

 PL/SQL提供用于连接两个字符串的级联运算符(`||`)。 下表提供了PL/SQL提供的字符串函数 

| 编号 |                      函数                       |                             描述                             |
| :--: | :---------------------------------------------: | :----------------------------------------------------------: |
|  1   |                    ASCII(x);                    |                    返回字符`x`的ASCII值。                    |
|  2   |                     CHR(x);                     |                   返回ASCII值为`x`的字符。                   |
|  3   |                  CONCAT(X, Y);                  |        连接两个字符串`x`和`y`，并返回连接后的字符串。        |
|  4   |                   INITCAP(X);                   |  将`x`中每个单词的初第一个字母转换为大写，并返回该字符串。   |
|  5   | INSTR(x, find_string [, start] [, occurrence]); |     在`x`字符串中搜索`find_string`子串并返回找到的位置。     |
|  6   |                   INSTRB(x);                    | 返回字符串`x`在另一个字符串中第一次再现的位置，但返回值(以字节为单位)。 |
|  7   |                   LENGTH(x);                    |          返回`x`中的字符数，也是计算字符串的长度。           |
|  8   |                   LENGTHB(x);                   |         返回单字节字符集的字符串长度(以字节为单位)。         |
|  9   |                    LOWER(x);                    |     将`x`字符串中的字母转换为小写，并返回此小写字符串。      |
|  10  |         LPAD(x, width [, pad_string]) ;         | 使用空格垫放在`x`字符串的左边，以使字符串的长度达到宽度字符。 |
|  11  |            LTRIM(x [, trim_string]);            |                  修剪`x`字符串左边的字符。                   |
|  12  |                NANVL(x, value);                 | 如果`x`匹配`NaN`特殊值(而不是数字)，则返回值，否则返回`x`字符串。 |
|  13  |                 NLS_INITCAP(x);                 | 与`INITCAP(x)`函数相同，只不过它可以使用`NLSSORT`指定的其他排序方法。 |
|  14  |                 NLS_LOWER(x) ;                  | 与`LOWER(x)`函数相同，除了可以使用`NLSSORT`指定的不同排序方法。 |
|  15  |                  NLS_UPPER(x);                  | 与`UPPER()`函数相同，除了可以使用`NLSSORT`指定的不同排序方法。 |
|  16  |                   NLSSORT(x);                   | 更改排序字符的方法。必须在任何`NLS()`函数之前指定; 否则，将使用默认排序。 |
|  17  |                 NVL(x, value);                  |        如果`x`为`null`则返回`value`值; 否则返回`x`。         |
|  18  |            NVL2(x, value1, value2);             | 如果`x`不为`null`则返回值`value1`; 如果`x`为`null`，则返回`value2`。 |
|  19  |   REPLACE(x, search_string, replace_string);    | 在`x`字符串中搜索`search_string`并将其替换为`replace_string`。 |
|  20  |         RPAD(x, width [, pad_string]);          | 使用空格垫放在`x`字符串的右边，以使字符串的长度达到宽度字符。 |
|  21  |            RTRIM(x [, trim_string]);            |                    从右边修剪`x`字符串。                     |
|  22  |                  SOUNDEX(x) ;                   |             返回一个包含`x`的语音表示的字符串。              |
|  23  |          SUBSTR(x, start [, length]);           | 返回`x`字符串从指定`start`位置开始到一个可选指定长度(`length`)范围内的子字符串。 |
|  24  |                   SUBSTRB(x);                   | 与`SUBSTR()`相同，除了参数以字节表示，还支持单字节字符系统的字符。 |
|  25  |            TRIM([trim_char FROM) x);            |              修剪`x`字符串的左边和右边的字符。               |
|  26  |                    UPPER(x);                    |      将`x`中的字母转换为大写，并返回此大写后的字符串。       |

示例：

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   greetings varchar2(11) := 'hello world'; 
BEGIN 
   dbms_output.put_line(UPPER(greetings)); 

   dbms_output.put_line(LOWER(greetings)); 

   dbms_output.put_line(INITCAP(greetings)); 

   /* retrieve the first character in the string */ 
   dbms_output.put_line ( SUBSTR (greetings, 1, 1)); 

   /* retrieve the last character in the string */ 
   dbms_output.put_line ( SUBSTR (greetings, -1, 1)); 

   /* retrieve five characters,  
      starting from the seventh position. */ 
   dbms_output.put_line ( SUBSTR (greetings, 7, 5)); 

   /* retrieve the remainder of the string, 
      starting from the second position. */ 
   dbms_output.put_line ( SUBSTR (greetings, 2)); 

   /* find the location of the first "e" */ 
   dbms_output.put_line ( INSTR (greetings, 'e')); 
END; 
/
```

示例：

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   greetings varchar2(30) := '......Hello World.....'; 
BEGIN 
   dbms_output.put_line(RTRIM(greetings,'.')); 
   dbms_output.put_line(LTRIM(greetings, '.')); 
   dbms_output.put_line(TRIM( '.' from greetings)); 
END; 
/
```

#### PL/SQL数组

PL/SQL编程语言提供了一种称为VARRAY的数据结构，它可以存储相同类型的元素的固定大小顺序集合。varray用于存储有序的数据集合，通常最好将数组视为相同类型变量的集合。

 所有`varray`是由连续的内存位置组成。最低的地址对应于第一个元素，而最后一个元素的地址最高。 

![1640939068740](Images/1640939068740.png)

数组是集合类型数据的一部分，表示可变大小的数组。 我们将在后面的“PL/SQL集合”这一章中学习其他集合类型。

`varray`中的每个元素都具有与之相关联的索引。它还具有可以动态更改的容量(大小)。

##### 创建Varray类型

使用CREATE TYPE语句创建varray类型。必须指定存储在varray中的元素的大小容量(大小)和类型。

在模式(schema)级创建VARRAY类型的基本语法：

```SQL
CREATE OR REPLACE TYPE varray_type_name IS VARRAY(n) of <element_type>
```

其中，

- `varray_type_name`是一个有效的属性名称；
- `n`是`varray`中元素的数量(最大值)；
- `element_type`是数组元素的数据类型。

 可以使用`ALTER TYPE`语句更改变量的最大大小。 

示例：

```SQL
CREATE Or REPLACE TYPE namearray AS VARRAY(3) OF VARCHAR2(10); 
/
```

 在PL/SQL块中创建`VARRAY`类型的基本语法 

```SQL
TYPE varray_type_name IS VARRAY(n) of <element_type>
```

示例：

```SQL
TYPE namearray IS VARRAY(5) OF VARCHAR2(10); 
Type grades IS VARRAY(5) OF INTEGER;
```

案例-1：

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   type namesarray IS VARRAY(5) OF VARCHAR2(10); 
   type grades IS VARRAY(5) OF INTEGER; 
   names namesarray; 
   marks grades; 
   total integer; 
BEGIN 
   names := namesarray('Kavita', 'Pritam', 'Ayan', 'Rishav', 'Aziz'); 
   marks:= grades(98, 97, 78, 87, 92); 
   total := names.count; 
   dbms_output.put_line('Total '|| total || ' Students'); 
   FOR i in 1 .. total LOOP 
      dbms_output.put_line('Student: ' || names(i) || ' 
      Marks: ' || marks(i)); 
   END LOOP; 
END; 
/
```

注意 

- 在Oracle环境中，`varrays`的起始索引始终为`1`。
- 可以使用`varray`类型的构造方法初始化`varray`元素，该方法与`varray`具有相同的名称。
- `varrays`是一维数组。
- `varray`在声明时自动为`NULL`，并且必须在引用元素之前初始化它。

案例-2：

变量的元素也可以是任何数据库表的`%ROWTYPE`或任何数据库表字段的`%TYPE`表来引用表示。 以下示例说明了这个概念。

```SQL
CREATE TABLE customers
( id number(10) NOT NULL,
  name varchar2(50) NOT NULL,
  age number(2) NOT NULL,
  address varchar2(50),
  salary float(2) NOT NULL,
  CONSTRAINT customers_pk PRIMARY KEY (id)
);

INSERT INTO customers (id,name,age,address,salary) VALUES(1, '罗大牛',32,'北京', 22999.00);
INSERT INTO customers (id,name,age,address,salary) VALUES(2, 'Maxsu',25,'海口', 5999.00);
INSERT INTO customers (id,name,age,address,salary) VALUES(3, 'Hinew',22,'广州', 9800.98);
INSERT INTO customers (id,name,age,address,salary) VALUES(4, '李小路',26,'北京', 18700.00);
INSERT INTO customers (id,name,age,address,salary) VALUES(5, '张友德',28,'上海', 18999.00);
INSERT INTO customers (id,name,age,address,salary) VALUES(6, '李连定',42,'深圳', 32999.00);
```

 使用游标引用 

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   CURSOR c_customers is 
   SELECT  name FROM customers; 
   type c_list is varray (6) of customers.name%type; 
   name_list c_list := c_list(); 
   counter integer :=0; 
BEGIN 
   FOR n IN c_customers LOOP 
      counter := counter + 1; 
      name_list.extend; 
      name_list(counter)  := n.name; 
      dbms_output.put_line('Customer('||counter ||'):'||name_list(counter)); 
   END LOOP; 
END; 
/
```

#### PL/SQL存储过程

子程序是执行特定任务的程序单元/模块，这些子程序组合起来形成更大的程序。这种做法被称为”模块化设计“。子程序可以被称为调用程序的另一个程序或程序调用。

创建子程序的位置：

- 在模式(schema)级别中
- 一个程序包中
- 在PL/SQL块中

在模式(schema)子程序是一个独立的子程序。它是使用CREATE PROCEDURE或CREATE FUNCTIN语句创建的。它存储在数据库中，可以使用DROP PROCEDURE或DROP FUNCTION语句进行删除。

在包中创建的子程序是打包的子程序。它存储在数据库中，只有当使用DROP PACHAGE语句删除程序包时，才能将其删除。

PL/SQL子程序被命名为可以使用一组参数调用的PL/SQL块、PL/SQL提供两种子程序：

- 函数：这些子程序返回单个值，主要用于计算和返回值
- 存储过程(程序)：这些子程序不直接返回值，主要用于执行动作

##### PL/SQL子程序的部分

每个PL/SQL子程序都有一个名称，也可能有一个参数列表，像匿名PL/SQL块医院，命名块也将具有以下三部分：

| 编号 | 部分       |                             描述                             |
| ---- | ---------- | :----------------------------------------------------------: |
| 1    | 声明部分   | 这是一个可选的部分。但是，子程序的声明不以DECLARE关键字开头。它包含类型、游标、常量、变量、异常和嵌套子程序的声明。这些项时本子程序，当子程序完成执行时，它们将不复存在。 |
| 2    | 可执行部分 |       这是一个强制性(必须有)，并包含指向指定操作的语句       |
| 3    | 异常处理   |       这是一个可选的部分，它包含处理运行时错误的代码。       |

##### 创建存储过程

使用CREATE OR REPLACE PROCEDURE语句创建一个存储过程。

CREATE OR REPLACE PROCEDURE简化语法：

```SQL
CREATE [OR REPLACE] PROCEDURE procedure_name 
[(parameter_name [IN | OUT | IN OUT] type [, ...])] 
{IS | AS} 
BEGIN 
  < procedure_body > 
END procedure_name;
```

其中，

- *procedure-name*是要创建的存储过程的名称。
- *[OR REPLACE]*选项允许修改现有的过程。
- 可选参数列表包含参数的名称，模式和类型。`IN`表示将从外部传递的值，`OUT`表示将用于返回过程外的值的参数。
- *procedure-body*包含可执行部分。
- 使用`AS`关键字而不是`IS`关键字来创建存储过程。

示例：

```SQL
--如何创建一个简单的存储过程，执行时它只显示字符串“Hello World！”在屏幕上
SET SERVEROUTPUT ON SIZE 99999;
CREATE OR REPLACE PROCEDURE greetings 
AS 
BEGIN 
   dbms_output.put_line('Hello World!'); 
END; 
/

-- 执行存储过程
exec greetings;
-- 或者
EXECUTE greetings;
```

##### 执行独立程序

独立的存储程序可以通过两种方式调用 

- 使用`EXECUTE`关键字
- 从PL/SQL块调用过程的名称

可以使用`EXECUTE`关键字调用名为`“greetings”`的存储过程如下 -

```sql
EXECUTE greetings;
```

 调用将显示结果 

```SQL
SQL> EXECUTE greetings;
Hello World!

PL/SQL 过程已成功完成。

SQL>
```

 该过程也可以从另一个PL/SQL块调用 

```SQL
BEGIN
	greetings;
END;
/
```

##### 删除独立存储过程

使用DROP PROCEDURE语句删除独立存储过程、删除程序的语法：

```SQL
DROP PROCEDURE procedure_name;
```

也可以使用以下语句删除greetings存储过程

```SQL
DROP PROCEDURE greetings;
```

##### 子程序中的参数模式

 下表列出了PL/SQL子程序中的参数模式 

| 编号 | 参数模式 |                             描述                             |
| :--: | :------: | :----------------------------------------------------------: |
|  1   |    IN    | `IN`参数允许将值传递给子程序。它是一个只读参数。在子程序中，`IN`参数的作用如常数，它不能被赋值。可以将常量，文字，初始化的变量或表达式作为`IN`参数传递。也可以将其初始化为默认值; 然而，在这种情况下，从子程序调用中省略它。 它是参数传递的默认模式。参数通过引用传递。 |
|  2   |   OUT    | `OUT`参数返回一个值给调用程序。在子程序中，`OUT`参数像变量一样。 可以更改其值并在分配该值后引用该值。实际参数必须是可变的，并且通过值传递。 |
|  3   |  IN OUT  | `IN OUT`参数将初始值传递给子程序，并将更新的值返回给调用者。 它可以分配一个值，该值可以被读取。对应于`IN OUT`形式参数的实际参数必须是变量，而不是常量或表达式。正式参数必须分配一个值。实际参数(实参)通过值传递。 |

##### IN和OUT模式

示例1：

假设以下存储过程需要求出两个值中的最小值。这里，存储过程两个输入的数字使用`IN`模式，并使用`OUT`模式参数返回最小值：

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   a number; 
   b number; 
   c number;
PROCEDURE findMin(x IN number, y IN number, z OUT number) IS 
BEGIN 
   IF x < y THEN 
      z:= x; 
   ELSE 
      z:= y; 
   END IF; 
END;   
BEGIN 
   a:= 12; 
   b:= 35; 
   findMin(a, b, c); 
   dbms_output.put_line('两个数：12, 35中的最小值是 : ' || c); 
END; 
/
```

示例2：

 此过程计算传递值的值的平方。此示例显示了如何使用相同的参数来接受值，然后返回另一个结果 :

```SQL
SET SERVEROUTPUT ON SIZE 99999;
DECLARE 
   a number; 
PROCEDURE squareNum(x IN OUT number) IS 
BEGIN 
  x := x * x; 
END;  
BEGIN 
   a:= 11; 
   squareNum(a); 
   dbms_output.put_line(' Square of (23): ' || a); 
END; 
/
```

##### 传递参数的方法

实际参数(实参)可以通过三种方式传递：

- 位置符号
- 命名符号
- 混合符号

**位置符号：**

在位置符号，可以调用存储过程

```SQL	
findMin(a, b, c, d);
```

















