2022年1月4日

### Oracle

#### 创建表

```sql
CREATE TABLE <table_name>(
	column1 DATATYPE [NOT NULL] PRIMARY KEY,
    column2 DATATYPE [NOT NULL],
    ...
    [constraint <约束名> 约束类型（要约束的字段）...]
);
--说明
DATATYPE--是Oracle的数据类型
NOT NULL--可不可以允许治疗有空的（尚未有资料填入）
PRIMARY KEY--是本表的主键
constraint--是对表的字段添加约束（约束类型有Check, Unitque, Primary Key, Not Null, Foreign Key）
```

示例：

```SQL
CREATE TABLE stu(
	s_id number(8) PRIMARY KEY,
    S_NAME varchar2(20) NOT NULL,
    s_sex varchar2(8),
    clsid number(8),
    constraint u_1 Unique(s_name),
    constraint c_1 check (s_sex in ('MAEL', 'FEMALE'))
);
```

#### 复制表

```SQL
CREATE TABLE <table_name> as <SELECT 语句>；
--（主要的是复制表不能复制表的约束）
```

示例：

```SQL
CREATE TABLE test as SELECT * FROM emp;

--如果只复制表的结构不复制表的数据则：
SELECT TABLE test as SELECT * FROM emp WHERE 1 = 2;
```

### 数值型函数

#### ABS(s)

功能：返回x的绝对值

参数：x，数字型表达式

返回：数字

```SQL
SELECT ABS(100) abs0, ABS(-100) abs1 from dual;
```

![1641268269738](Images/1641268269738.png)

#### SIGN(x)

功能：返回x的正负值

参数：x，数字型表达式

返回：数字，若为正值返回1，负值返回-1，0返回0

```SQL
SELECT SIGN(100), SIGN(-100), SIGN(0) from dual;
```

![1641268297434](Images/1641268297434.png)

#### CEIL(X)

功能：返回大于等于x的最小整数值

参数：x，数字型表达式

返回：数字

```SQL
SELECT CEIL(3.1), CEIL(2.8 + 1.3), CEIL(0) from dual;
```

![1641262571664](Images/1641262571664.png)

#### FLOOR(x)

功能：返回小于等于x的最大整数值

参数：x，数字型表达式

返回：数字

```SQL
SELECT FLOOR(3.1), FLOOR(2.8 + 1.3), FLOOR(0) from dual;
```

![1641262681997](Images/1641262681997.png)

#### POWER(x, y)

功能：返回x的y次幂

参数：x, y 数字型表达式

返回：数字

```SQL
SELECT POWER(2.5, 2), POWER(1.5, 0), POWER(20, -1) from dual;

--关系（z=power(x,y),则y=1/log(z,x)   (条件z,x>0)）
```

![1641262792903](Images/1641262792903.png)

#### EXP(y)

功能：返回e的y次幂（e为数学常量）

参数：y，数字型表达式

返回：数字

```SQL
SELECT EXP(3), EXP(0), EXP(-3) from dual;
```

![1641262932079](Images/1641262932079.png)

#### LOG(X, Y)

功能：返回以x为底的y的对数

参数：x，y，数字型表达式

返回：数字

```SQL
SELECT POWER(4, 2), LOG(16, 2), 1/LOG(16, 4) from dual;
```

![1641263059334](Images/1641263059334.png)

```SQL
SELECT POWER(6.4, 3), LOG(274.625, 3), 1/LOG(POWER(6.5, 3), 6.5) from dual;
```

![1641263134896](Images/1641263134896.png)

#### LN(y)

功能：返回以e为底的y的对数（e为数学常量）

参数：y，数字型表达式

返回：数字

```SQL
SELECT EXP(3), EXP(-3), LN(20.0855369), LN(0.049787068) from dual;
```

![1641263548974](Images/1641263548974.png)

#### MOD(x, y)

功能：返回x除以y的余数

参数：x，y，数字型表达式

返回：数字

```SQL
SELECT MOD(23, 8), MOD(24, 8) from dual;
```

![1641263696259](Images/1641263696259.png)

#### ROUND(x[, y])

功能：返回四舍五入后的值

参数：x，y，数字型表达式，如果y部位整数则截取y的整数部分。如果y > 0则四舍五入为y位小数。如果y < 0则四舍五入到小数点向左第y位。

返回：数字

```SQL
SELECT ROUND(5555.6666, 2.1), ROUND(5555.6666, -2.6), ROUND(5555.6666) from dual;
```

![1641263954708](Images/1641263954708.png)

#### TRUNC(x[, y])

功能：返回x按精度y截取后的值

参数：x，y，数字型表达式，如果y不为整数则截取y整数部分，如果y > 0则截取y位小数，如果y < 0则截取小数点向左第y位，小数前其他数据用0表示。

返回：数字

```SQL
SELECT TRUNC(5555.6666, 2.1), TRUNC(5555.6666, -2.6), TRUNC(5555.03333) from dual;
```

![1641264178620](Images/1641264178620.png)

#### SQRT(x)

功能：返回x的平方根

参数：x数字表达式

返回：数字

```SQL
SELECT SQRT(64), SQRT(10) from dual;
```

![1641264291488](Images/1641264291488.png)

#### SIN(x)

功能：返回一个数字的正弦值

```SQL
SELECT SIN(1.57079) from dual;
```

![1641264469489](Images/1641264469489.png)

#### SINH(x)

功能：返回双曲正弦的值

```SQL
SELECT SIN(20), SINH(20) from dual;
```

![1641264533019](Images/1641264533019.png)

#### COS(x)

功能：返回一个给定数字的余弦

```SQL
SELECT COS(-3.1415927) from dual;
```

![1641264748358](Images/1641264748358.png)

#### COSH(x)

功能：返回一个数字反余弦值

```SQL
SELECT COSH(20) from dual;
```

![1641264761339](Images/1641264761339.png)

#### TAN(x)

功能：返回数字的正切值

```SQL
SELECT TAN(20), TAN(10) from dual;
```

![1641264978630](Images/1641264978630.png)

#### TANH(X)

功能：返回数字n的双曲正切值

```SQL
SELECT TANH(20), TAN(20) from dual;
```

![1641264993991](Images/1641264993991.png)

#### ACOS(x)

功能：给出反余弦的值

```SQL
SELECT ACOS(-1) from dual;
```

![1641265014556](Images/1641265014556.png)

#### ATAN(x)

功能：返回一个数字的反正切值

```SQL
SELECT ATAN(1) from dual;
```

![1641265096602](Images/1641265096602.png)


### 字符型函数

#### ASCII(X)

功能：返回字符表达式最左端的ASCII码值

参数：x1-字符表达式

返回：数值型

示例：

```SQL
SELECT ASCII('A') A, ASCII('a') a, ASCII(' ') space, ASCII('示') hz from dual;
```

![1641265128117](Images/1641265128117.png)

**说明：**在ASCII()函数中，村数字的字符串可不用''括起来，但含其他字符的字符串必须用''括起来使用，否则会出错。如果最左端是汉字，只取汉字最左边字符的ASCII码。

**互反函数：**char()

#### CONCAT(c1, c2)

功能：连接两个字符串

参数：c1, c2字符型表达式

返回：字符型

**同：**c1 || c2

示例：

```SQL
SELECT CONCAT('182', '00000007') || '接999' 码农电话 from dual;
```

![1641265149638](Images/1641265149638.png)

#### INITCAP(c1)

功能：返回字符串并将字符串的第一个字母变为大写，其他字母小写

参数：c1字符型表达式

返回：字符型

示例：

```SQL
SELECT INITCAP('smith abc aBC') upp from dual;
```

![1641265352197](Images/1641265352197.png)

#### LOWER(c1)

功能：将字符全部转为小写

参数：c1，字符表达式

返回：字符型

示例：

```SQL
SELECT LOWER('AaBbCcDd') asAaBbCcDd from dual;
```

![1641265398525](Images/1641265398525.png)

#### UPPER(c1)

功能：将字符串全部转为大写

参数：c1，字符表达式

返回：字符型

```SQL
SELECT UPPER('AaBbCcDd') upper from dual;
```

![1641268592983](Images/1641268592983.png)

#### NLS_INITCAP(x[, y])

功能：返回字符串并将字符串的第一个字母变为大写，其他字母小写

参数：x字符型表达式

参数：NLs_param可选

返回：字符型

```SQL
--查询数据级NLS设置
SELECT * FROM NLS_DATABASE_PARAMETERS;

/*
例如：
指定排序的方式(nls_sort = )
nls_sort = SCHINESE_RADICAL_M(部首， 笔画)
nls_sort = SCHINESE_STROKE_M(笔画、首部SCHINESE_PINYIN_M(拼音))

*/
```

![1641268749337](Images/1641268749337.png)

```SQL
SELECT nls_initcap('ab cde') "test", nls_initcap('a c b d e','nls_sort= SCHINESE_PINYIN_M') "test1" from dual;
```

![1641269098536](Images/1641269098536.png)

```SQL
select nls_initcap('ab cde') "test",nls_initcap('a c b d e','NLS_LANGUAGE=AMERICAN') "test1" from dual;
```

![1641269139513](Images/1641269139513.png)

#### NLS_LOWER(x[, y])

功能：返回字符串并将字符串变为小写

参数：x字符表达式

参数：NLS_PARMATER可以选，指定排序的方式（NLS_SORT = ）

SCHINESE_RADICAL_M(部首。笔画)

SCHINESE_STROKE_M(笔画、部首SCHINESE_PRINYIN_M(拼音))

返回：字符型

```SQL
SELECT NLS_LOWER('ab cde') "test", NLS_LOWER('a c b d e', 'nls_sort = SCHINESE_PINYIN_M') "test1" from dual;
```

![1641269492695](Images/1641269492695.png)

#### NLS_UPPER(x[, y])

功能：返回字符串并将字符串转换为大写

参数：x字符串表达式

参数：NLS_PAREMTER可选，指定排序的方式(nls_sort = )

SCHINESE_RADICAL_M(首部、笔画)

SCHINESE_STROKE_M(笔画、首部SCHINESE_PINYIN_M(拼音))

返回：字符型

```SQL
SELECT NLS_UPPER('ab cde') "test", NLS_UPPER('a c b d e', 'nls_sort = SCHINESE_PINYIN_M') "test1" from dual;
```

![1641269762234](Images/1641269762234.png)

#### INSTR(c1, c2[, I[, j]])

功能：在一个字符串中搜索指定的字符，返回发现指定的字符的位置

说明：多字节（汉字、全角符等），按1个字符计算

参数：

- c1：被搜索的字符串
- c2：希望被搜索的字符串
- I：搜索的开始位置，默认为1
- J：第J次出现的位置，默认为1

返回：数值

```SQL
SELECT INSTR('Oracle traning', 'ra', 1, 2) instring from dual;
```

![1641270047359](Images/1641270047359.png)

```SQL
SELECT INSTR('重庆某软件公司', '某', 1, 1), instrb('重庆某软件公司', '某', 1, 1) instring from dual;
```

![1641270455151](Images/1641270455151.png)

#### INSTRB(c1, c2[, I[, y]])

功能：在一个字符串中搜索指定的字符，返回发现指定的字符的位置

说明：多个字节（汉字、全角符等），按2个字符计算

参数：

- c1：被搜索的字符串
- c2：希望被搜索的字符串
- I：搜索的开始位置，默认为1
- J：第J次出现的位置，默认为1

```SQL
SELECT INSTR('重庆某软件公司', '某', 1, 1), INSTRB('重庆某软件公司', '某', 1, 1) instring from dual;
```

![1641270446969](Images/1641270446969.png)

#### LENGTH(c1)

功能：返回字符串的长度

说明：多个字节符（汉字、全角符等），按1个字符计算

参数：c1字符串

返回：数值型

```SQL
SELECT LENGTH('大力水手'), LENGTH('北京市海定区'), LENGTH('北京TO_CHAR') from dual;
```

![1641270659353](Images/1641270659353.png)

#### LENGTHB(c1)

功能：返回字符串的长度

说明：多个字节符（汉字、全角符等），按2个字符计算

参数：c1字符串

返回：数值

```SQL
SELECT LENGTH('大力水手'), LENGTHB('大力水手') from dual;
```

![1641270813228](Images/1641270813228.png)

#### LENGTH(c1).LENGTH2(c1).LENGTH4(C1)

功能：返回字符串的长度

说明：多字节发符（汉字、全角符等），按1个字符计算

参数：c1字符串

返回：数值型

```SQL
SELECT LENGTH('大力水手'), LENGTH('北京市海定区'), LENGTH('北京TO_CHAR') from dual;
```

![1641271008270](Images/1641271008270.png)

```SQL
Oracle中的字符函数中，有一类函数是求字符长度的函数，length、lengthB、lengthC、length2、length4几个函数中比较常用的是length、lengthB。

他们的含义分别是：
Length函数返回字符的个数，使用定义是给定的字符集来计算字符的个数
LENGTHB给出该字符串的byte
LENGTHC使用纯Unicode
LENGTH2使用UCS2
LENGTH4使用UCS4
```

```SQL
SELECT LENGTH('你好') from dual;
```

![1641271175327](Images/1641271175327.png)

```SQL
SELECT LENGTHB('你好'), LENGTH('你好'), LENGTH2('你好'), LENGTH4('你好') from dual;
```

![1641271208405](Images/1641271208405.png)

#### LPAD(c1, n[, c2])

功能：在字符串c1的左边用字符串c2填充， 直到长度为n时为止

参数：

- c1：字符串
- n：追加后的字符总长度
- c1：追加字符串，默认为空格

说明：如果c1长度大于n，则返回c1左边n个字符。如果c1长度小于n，c2和c1连接后大于n，则返回连接后的右边n个字符。

```SQL
SELECT LPAD('gao', 10, '*') from dual;
--不够字符则使用*来填满
```

![1641271444890](Images/1641271444890.png)

#### RPAD(c1, n[, c2])

功能：在字符串c1的右边用字符串c2填充，直到长度为n时为止

参数：

- c1：字符串
- n：追加后的字符总长度
- c1：追加字符串，默认为空格

返回：字符型

说明：如果c1长度大于n，则返回c1左边n个字符。如果c1长度小于n，c1和c2连接后大于n，则返回连接后的左边n个字符。如果c1长度小于n，c1和c2连接后小于n，则返回c1与多个重复c2连接（总长度 >= n）后的左边n个字符

```SQL
SELECT RPAD('gao', 10, '&*') from dual;
```

![1641271852224](Images/1641271852224.png)

#### LTRIM(c1, [, c2])

功能：删除左边出现的字符串

参数：

- c1 字符串
- c2 追加字符串，默认为空格

返回：字符串

```SQL
SELECT LTRIM('       gao qian', ' ') text from dual;
```

![1641271982067](Images/1641271982067.png)

#### RTRIM(c1, [, c2])

功能：删除右边出现的字符串

参数：

- c1 字符串
- c2 追加字符串，默认为空格

返回：字符串

```SQL
SELECT RTRIM('gao qianXXXXX', 'X') text from dual;
```

![1641272116226](Images/1641272116226.png)

#### REPLACE(c1, c2[, c3])

功能：将字符串表达式值中，部分相同字符串替换成新的字符串

参数：

- c1 希望被替换的字符串或变量
- c2 被替换的字符串
- c3 要替换的字符串，默认为空(即删除之意，不是空格)

返回：字符串

```SQL
SELECT REPLACE('he do can for', 'he', 'i') test from dual;
```

![1641272311731](Images/1641272311731.png)

#### SOUNDEX(c1)

功能：返回字符串参数的语音表示形式

参数：c1，字符串

返回：字符串

说明：相对于比较以下读音相同，但是拼写不同的单词时非常有用的

```SQL
计算语音的算法：
　　1.保留字符串首字母，但删除a、e、h、i、o、w、y
　　2.将下表中的数字赋给相对应的字母
　　(1) 1：b、f、p、v
　　(2) 2：c、g、k、q、s、x、z
　　(3) 3：d、t
　　(4) 4：l
　　(5) 5：m、n
　　(6) 6：r
　　3. 如果字符串中存在拥有相同数字的2个以上（包含2个）的字母在一起（例如b和f），或者只有h或w，则删除其他的，只保留1个
　　4.只返回前4个字节，不够用0填充
```

```SQL
示例：
　　soundex('two'),soundex('too'),soundex('to')，他们的结果都是T000
　　soundex('cap'),soundex('cup')，他们的结果都是C100
　　soundex('house'),soundex('horse')，他们的结果都分别是H200，H620
```

#### SUBSTR(c1, n1[, n2])

功能：取字符串

说明：多字节符（汉字、全角符等），按1个字符计算

参数：在多个表达式，从n1开始取n2个字符，若不指定n2，则从第y个字符直到结束的子串。

返回：字符串

```SQL
SELECT SUBSTR('1308888888', 3, 8) test from dual;
```

![1641272705705](Images/1641272705705.png)

#### SUBSTR(c1, n1[, n2])

功能：取子字符串

说明：多字节符(汉字、全角符等)，按2个字符计算

参数：在字符表达式c1里，从n1开始取n2个字符;若不指定n2,则从第y个字符直到结束的字串.

返回：字符型,如果从多字符右边开始,则用空格表示。

```SQL
select substr('我手机13012345678',4,11),substrb('我手机13012345678',4,11),substrb('我手机13012345678',3,11) test from dual;
```

![1641272858490](Images/1641272858490.png)

#### TRANSLATE(c1, c2, c3)

功能：将字符表达式值中，指定字符替换为新字符

说明：多字节符（汉字、全角符等），按1个字符计算

参数：

- c1 希望被替换的字符或变量
- c2 查询原始的字符集
- c2 替换新的字符集，将c2对应的顺序字符，替换为c3对应顺序字符。如果c3长度大于c2，则c3长出后面的字符无效。如果c3长度小于c2，则c2长出后面的字符军替换为空（删除）。如果c3长度为0，则返回空字符串。如果c2里字符重复，按首次位置为替换依据。

返回：字符型

```SQL
select TRANSLATE('he love you','he','i'),
TRANSLATE('重庆的人','重庆的','上海男'),
TRANSLATE('重庆的人','重庆的重庆','北京男士们'),
TRANSLATE('重庆的人','重庆的重庆','1北京男士们'),
TRANSLATE('重庆的人','1重庆的重庆','北京男士们') from dual;
```

![1641273279190](Images/1641273279190.png)

#### TRIM (c1 from c2)

功能：删除左边和右边出现的字符串

参数：

- c2 删除前字符串
- c1 删除字符串，默认为空格

返回：字符型

```SQL
SELECT TRIM('X' from 'XXXgao qianXXX'), TRIM('X' from 'XXXgaoXXXqianXXX') text from dual;
```

![1641273438064](Images/1641273438064.png)

### 日期函数

#### SYSDATE

功能：返回当前日期

参数：没有参数，没有括号

返回：日期

```SQL
SELECT SYSDATE now_time from dual;
```

![1641273667255](Images/1641273667255.png)

#### ADD_MONTHS(d1, n1)

功能：返回在日期d1基础上再加n1个月后新的日期

参数：d1，日期型，n1数字型

返回：日期

```SQL
SELECT SYSDATE now_time, ADD_MONTHS(SYSDATE, 3) ADD_3_DAY from dual;
```

![1641273857053](Images/1641273857053.png)

#### LAST_DAY(d1)

功能：返回日期d1所在月份最后一天的日期

参数：d1，日期型

返回：日期

```SQL
SELECT SYSDATE, LAST_DAY(SYSDATE) NOW_LAST_DAY from dual;
```

![1641273973118](Images/1641273973118.png)

#### MONTHS_BETWEEN(d1, d2)

功能：返回日期d1到日期d2之间的月数

参数：d1、d2日期型

返回：数字

如果d1 大于 d2，则返回正数。如果d1 小于 d2，则返回负数

```SQL
SELECT SYSDATE, 
	MONTHS_BETWEEN(SYSDATE, TO_DATE('2006-01-01', 'YYYY-MM-DD')) start_time,
	MONTHS_BETWEEN(SYSDATE, TO_DATE('2016-01-01', 'YYYY-MM-DD')) end_time from dual;
```

![1641274247946](Images/1641274247946.png)

#### NEW_TIME(dt1, c1, c3)

功能：给出时间dt1在c1时区对应c2时区的日期和时间

参数：dt1, d2 日期型

返回：日期时间

参数：c1，c2对应的时区及其简写

大西洋标准时间：AST或ADT
  阿拉斯加_夏威夷时间：HST或HDT
  英国夏令时：BST或BDT
  美国山区时间：MST或MDT
  美国中央时区：CST或CDT
  新大陆标准时间：NST
  美国东部时间：EST或EDT
  太平洋标准时间：PST或PDT
  格林威治标准时间：GMT
  Yukou标准时间：YST或YDT

```SQL
 SELECT TO_CHAR(SYSDATE,'yyyy.mm.dd hh24:mi:ss') bj_time,
TO_CHAR(new_time(SYSDATE,'PDT','GMT'),'yyyy.mm.dd hh24:mi:ss') los_angles from dual;
```

![1641278599922](Images/1641278599922.png)

```SQL
SELECT SYSDATE bj_time,
NEW_TIME(sysdate,'PDT','GMT') los_angles from dual;
```

![1641278654586](Images/1641278654586.png)

#### ROUND(d1 [, c1])

功能：给出日期d1按期间参数（c1）四舍五入后的期间的第一天日期（与数值四舍五入，意思相近）

参数：d1日期类型，c1为字符型（参数），c1默认为j（即最近0点日期）

参数表：c1对应的参数表

最近0点日期：取消参数c1或j。最近的星期日：day或dy或d。最近月初星期日：mongth或mon或mm或rm。最近季日期：q，最近年初日期：syear或year或yyyy或yyy或yy或y(多个y表示精度)，最近世纪初日期：cc或scc

返回：日期

```SQL
SELECT SYSDATE 当时日期,
ROUND(SYSDATE) 最近0点日期,
ROUND(SYSDATE,'day') 最近星期日,
ROUND(SYSDATE,'month') 最近月初,
ROUND(SYSDATE,'q') 最近季初日期,
ROUND(SYSDATE,'year') 最近年初日期 from dual;
```

![1641281716239](Images/1641281716239.png)

#### TRUNC(d1 [, c1])

功能：返回日期d1所在期间（参数c1）的第一天日期

参数：d1日期型，c1为字符型(参数)，c1默认为j（即当前日期）

参数表：c1对应的参数表

最近0点日期: 取消参数c1或j
最近的星期日：day或dy或d (每周顺序：日，一，二，三，四，五，六）
最近月初日期：month或mon或mm或rm
最近季日期：q
最近年初日期：syear或year或yyyy或yyy或yy或y(多个y表示精度)
最近世纪初日期：cc或scc

返回：日期

```SQL
SELECT SYSDATE 当时日期,
TRUNC(SYSDATE) 今天日期,
TRUNC(SYSDATE,'day') 本周星期日,
TRUNC(SYSDATE,'month') 本月初,
TRUNC(SYSDATE,'q') 本季初日期,
TRUNC(SYSDATE,'year') 本年初日期 from dual;
```

![1641281657466](Images/1641281657466.png)

#### NEXT_DAY(d1[,c1])
功能：返回日期d1在下周，星期几(参数c1)的日期
参数：d1日期型,c1为字符型(参数)，c1默认为j（即当前日期)
参数表：c1对应:星期一，星期二，星期三……星期日
返回：日期

```SQL
SELECT SYSDATE 当时日期,
	NEXT_DAY(SYSDATE,'星期一') 下周星期一,
	NEXT_DAY(SYSDATE,'星期二') 下周星期二,
	NEXT_DAY(SYSDATE,'星期三') 下周星期三,
	NEXT_DAY(SYSDATE,'星期四') 下周星期四,
	NEXT_DAY(SYSDATE,'星期五') 下周星期五,
	NEXT_DAY(SYSDATE,'星期六') 下周星期六,
	NEXT_DAY(SYSDATE,'星期日') 下周星期日 from dual;
```

![1641281596472](Images/1641281596472.png)

#### EXTRACT(c1 from d1)

功能：日期/时间d1中，参数(c1)的值

参数：d1日期型(date)/日期时间型(timestamp)，c1为字符型(参数)

参数表：c1对应的参数表

返回：字符

```SQL
SELECT
	EXTRACT(hour from timestamp '2001-2-16 2:38:40') 小时，
	EXTRACT(minute from timestamp '2001-2-16 2:38:40') 分钟，
	EXTRACT(second from timestamp '2001-2-16 2:38:40') 秒，
	EXTRACT(DAY from timestamp '2001-2-16 2:38:40') 日，
	EXTRACT(MONTH from timestamp '2001-2-16 2:38:40') 月，
	EXTRACT(YEAR from timestamp '2001-2-16 2:38:40') 年 from dual;
```

![1641281513814](Images/1641281513814.png)

```SQL
SELECT
	EXTRACT (YEAR from date '2001-2-16') from dual;
```

![1641281789205](Images/1641281789205.png)

#### LOCALTIMESTAMP

功能：返回会话中的日期和时间

没有参数，没有括号

返回：日期

```SQL
SELECT LOCALTIMESTAMP from dual;
```

![1641282779185](Images/1641282779185.png)

#### CURRENT_TIMESTAMP

功能：以TIMESTAMP WITH TIME ZONE 数据类型返回当前会话时区中的当前日期

参数：没有参数，没有括号

返回：日期

```SQL
SELECT CURRENT_TIMESTAMP from dual;
```

![1641282896682](Images/1641282896682.png)

#### CURRENT_DATE

功能：返回当前会话时区中的当前日期

参数：没有参数，没有括号

返回：日期

```SQL
SELECT CURRENT_DATE from dual;
```

![1641282980595](Images/1641282980595.png)

#### DBTIMRZONE

功能：返回时区

参数：没有参数，没有括号

返回：字符型

```SQL
SELECT DBTIMEZONE from dual;
```

![1641283050266](Images/1641283050266.png)

#### SESSIONTIMEZONE

功能：返回会话时区

参数：没有参数，没有括号

返回：字符型

```SQL
SELECT DBTIMEZONE, SESSIONTIMEZONE from dual;
```

![1641283128575](Images/1641283128575.png)

#### INTERVAL c1 set1

功能：变动日期时间数值

参数：c1为数字字符串或日期时间字符串，set1为日期参数

参数表：set1具体参照

返回：日期时间格式的数值，前面多个+号，以天或天更小单位时可用数值表达式借用，如1表示1天，1/24表示1小时，1/24/60表示1分钟

```SQL
select
TRUNC(SYSDATE)+(INTERVAL '1' second), --加1秒(1/24/60/60)
TRUNC(SYSDATE)+(INTERVAL '1' minute), --加1分钟(1/24/60)
TRUNC(SYSDATE)+(INTERVAL '1' hour), --加1小时(1/24)
TRUNC(SYSDATE)+(INTERVAL '1' DAY),  --加1天(1)
TRUNC(SYSDATE)+(INTERVAL '1' MONTH), --加1月
TRUNC(SYSDATE)+(INTERVAL '1' YEAR), --加1年
TRUNC(SYSDATE)+(INTERVAL '01:02:03' hour to second), --加指定小时到秒
TRUNC(SYSDATE)+(INTERVAL '01:02' minute to second), --加指定分钟到秒
TRUNC(SYSDATE)+(INTERVAL '2 01:02' day to minute) --加指定天数到分钟
from dual;
```

![1641283381493](Images/1641283381493.png)

### 转换函数

#### CHARTOROWID(c1)

功能：转换varchar2类型的rowid值

参数：c1字符串，长度为18的字符串，字符串必须复合rowid格式

返回：rowid值

```SQL
SELECT CHARTOROWID('AAAADeAABAAAAZSAAA') FROM DUAL;
```

![1641283703737](Images/1641283703737.png)

说明：在Oracle中，每一条记录都有一个rowid，rowid在整个数据库中是唯一的，rowid确定了每条记录是在Oracle中的哪一个数据文件、块、行上。在重复的记录中，可能所有列的内容都相同，但rowid不会相同.

#### ROWIDTOCHAR(rowid)

功能：转换rowid值为varchar2类型

参数：rowid固定参数

返回：返回长度为18的字符串

```SQL
SELECT ROWIDTOCHAR(rowid) from dual;
```

![1641284133677](Images/1641284133677.png)

说明：在Oracle中，每一条记录都有一个rowid，rowid在整个数据库中是唯一的，rowid确定了每条记录是在Oracle中的哪一个数据文件、块、行上。在重复的记录中，可能所有列的内容都相同，但rowid不会相同.

#### CONVERT(c1, set1, set2)

功能：将原字符串c1，从一个语言字符集set2转换到另一个目的的set1字符集

参数：c1, 字符串，set1，set2为字符型参数

返回：字符串

```SQL
SELECT CONVERT('strutz', 'we8hp', 'f7dec') "conversion" from dual;
```

![1641284335829](Images/1641284335829.png)

#### HEXTORAW(c1)

功能：将一个十六进制构成的字符串转换为二进制

参数：c1，十六进制的字符串

返回：字符串

```SQL
SELECT HEXTORAW('A123') from dual;
```

![1641284430183](Images/1641284430183.png)

#### RAWTOHEX(c1)

功能：将一个二进制构成的字符串转换为十六进制

参数：c1，二进制的字符串

返回：字符串

```SQL
SELECT RAWTOHEX('A123') from dual;
```

![1641284541194](Images/1641284541194.png)

#### TO_CHAR(x[[, c2], c3])

功能：将日期或数据转换为char数据类型

参数：x是一个date或number数据类型，c2为格式参数，c3为NLS设置参数，如果x为日期nlsparm = NLS_DATE_LANGUAGE 控制返回的月份和日份使用的语言。如果x为数字nlsparm=NLS_NUMBERIC_CHARACTERS用来指定小数位和千分位的分隔符，以及货币符号。NLS_NUMERIC_CHARACTERS = 'dg', NLS_CURRENCY = "STRING"

返回：varchar2字符型

```SQL
 SELECT TO_CHAR(SYSDATE,' PM yyyy-mm-dd hh24:mi:sssss AD year mon day ddd iw') from dual;
```

![1641285174201](Images/1641285174201.png)

```SQL
SELECT TO_CHAR(SYSTIMESTAMP,'HH24:MI:SS.FF5') from dual;
```

![1641285224496](Images/1641285224496.png)

#### TO_DATE(x, c2[, c3])

功能：将字符串X转化为日期型

参数：c2, c3字符型，参照TO_CHAR()

返回：字符串

如果x格式日期型(date)格式时，则相同表达式：date x。如果x格式为日期时间型（timestamp）格式时，则相同表达：timestamp x

```SQL
SELECT TO_DATE('199912','yyyymm'),
TO_DATE('2000.05.20','yyyy.mm.dd'),
(date '2008-12-31') XXdate,
TO_DATE('2008-12-31 12:31:30','yyyy-mm-dd hh24:mi:ss'),
(TIMESTAMP '2008-12-31 12:31:30') XXtimestamp
from dual;
```

![1641285607818](Images/1641285607818.png)

#### TO_NUMBER(x[[, c2], c3])

功能：将字符串x转化为数字型

参数：c2, c3字符型，参照TO_CHAR()

返回数字串：

```SQL
SELECT TO_NUMBER('199912'), TO_NUMBER('450.05') from dual;
```

![1641285758468](Images/1641285758468.png)

#### TO_MULTI_BYTE(c1)

功能：将字符串中的半角转换为全角

参数：c1，字符型

返回：字符串

```SQL
SELECT TO_MULTI_BYTE('高A') text from dual;
```

![1641285871161](Images/1641285871161.png)

#### TO_SINGLE_BYTE(c1)

功能：将字符串中的全角转换为半角

参数：c1，字符型

返回：字符串

```SQL
SELECT TO_SINGLE_BYTE('高A') from dual;
```

![1641286017560](Images/1641286017560.png)

#### NLS_CHARSET_ID(c1)

功能：返回字符集名称参与id值

参数：c1，字符型

返回：数值型

```SQL
SELECT NLS_CHARSET_ID('zhs16gbk') from dual;
```

![1641286131000](Images/1641286131000.png)

#### NLS_CHARSET_NAME(n1)

功能：返回字符集名称参应ID值

参数：n1，数值型

返回：字符型

```SQL
SELECT NLS_CHARSET_NAME(852) from dual;
```

![1641286252167](Images/1641286252167.png)

### 聚组函数

#### AVG([DISTINCT | ALL]X)

功能：统计数据表选中行x列的平均值

参数：all表示对所有的值求平均值，DISTINCT只对不同的值平均值，默认为ALL，如果有参数DISTINT或ALL，需有空格与x(列)隔开。

参数：x，只能为数值型字段

返回：数值

```SQL
CREATE TABLE table3(xm varchar(8),sal number(7,2));
INSERT INTO table3 VALUES('gao',1111.11);
INSERT INTO table3 VALUES('gao',1111.11);
INSERT INTO table3 VALUES('zhu',5555.55);
commit;
```

```SQL
SELECT AVG(DISTINT sal),AVG(all sal),AVG(sal) from table3;
```

![1641286838589](Images/1641286838589.png)

#### SUM([DISTINTCT | ALL] X)

功能：统计数据表选中行x列合计值。

参数：all表示对所有的值求合计值,distinct只对不同的值求合计值，默认为all
如果有参数distinct或all，需有空格与x(列)隔开。

参数：x，只能为数值型字段

返回：数字值

```SQL
SELECT SUM(DISTINCT sal), SUM(ALL sal), SUM(sal) from table3;
```

![1641287068434](Images/1641287068434.png)

#### STDDEV([DISTINCT | ALL] x)

功能：统计数据表中选中行x列的标准误差

参数：all表示对所有的值求标准差，distinct只对不同的值求标准误差，默认为all，如果参数distinct或all，需要空格与x(列)隔开

参数：x，只能为数值型字段

返回：数字值

```SQL
SELECT STDDEV(DISTINCT SAL), STDDEV(ALL SAL), STDDEV(SAL) from table3;
```

![1641287373712](Images/1641287373712.png)

#### VARIANCE([DISTINCT | ALL] x)

功能：统计数据表选中行x列的方差

参数：all表示对所有的值求方差,distinct只对不同的值求方差，默认为all
如果有参数distinct或all，需有空格与x(列)隔开。

参数：x，只能为数值型字段

返回：数字值

```SQL
SELECT VARIANCE(DISTINCT SAL), VARIANCE(ALL SAL), VARIANCE(SAL) from table3;
```

![1641287519613](Images/1641287519613.png)

#### COUNT(*| [DISTINCT | ALL] X)

功能：统计数据表选中行x列的合计值

参数：
*表示对满足条件的所有行统计，不管其是否重复或有空值(NULL)

all表示对所有的值统计,默认为all
distinct只对不同的值统计，
如果有参数distinct或all，需有空格与x(列)隔开，均忽略空值(NULL)。

参数：x，可为数字、字符、日期型及其它类型的字段

返回：数字值

conut(*) = sum(1)

```SQL
SELECT COUNT(*), COUNT(XM), COUNT(ALL XM), COUNT(DISTINCT SAL), COUNT(ALL SAL), COUNT(SAL), SUM(1) from table3;
```

![1641287737352](Images/1641287737352.png)

#### MAX([distinct|all]x)
功能：统计数据表选中行x列的最大值。

参数：all表示对所有的值求最大值,distinct只对不同的值求最大值，默认为all
如果有参数distinct或all，需有空格与x(列)隔开。

参数：x，可为数字、字符或日期型字段

返回：对应x字段类型

```SQL
SELECT MAX(DISTINCT SAL), MAX(XM) from table3;
```

![1641287869433](Images/1641287869433.png)

#### MIN([distinct|all]x)
功能：统计数据表选中行x列的最大值。

参数：all表示对所有的值求最大值,distinct只对不同的值求最大值，默认为all
如果有参数distinct或all，需有空格与x(列)隔开。

参数：x，可为数字、字符或日期型字段

返回：对应x字段类型
注：字符型字段，将忽略空值(NULL)

```SQL
SELECT MIN(DISTINCT SAL), MIN(XM), MIN(DISTINCT XM), MIN(ALL XM) from table3;
```

![1641287995143](Images/1641287995143.png)

### 分析函数

#### Oracle分析函数

一、总体介绍

分析函数如何工作？

语法：

```SQL
FUNCTION(<参数>,...) OVER( >) PARTITION子句 ORDER BY子句 WINDOWING子句 
--缺省时相当于RANGE UNBOUNDED PRECEDIND
```

1.值域窗（RANGE WINDOW）

RANGE(range)  N PRECEDING 仅对数值或日期类型有效，选定窗位排序后当前行之前，某列（即排序列）值大于/小于（当前行该列值 -/+ N）的所有行，因此ORDER BY 子句有关系。

2.行窗(ROW WINDOW)

ROWS N PRECEDING 选定窗为当前行及前N行。还可以加上BETWEEN AND形式。例如：RANGE M PRECEDING AND N FOLLOWING

函数 AVG(expr)

一组或选定窗中表达式的平均值 CORR(expr, expr) 即COVAR_POP(exp1,exp2) / (STDDEV_POP(expr1) * STDDEV_POP(expr2)),两个表达式的互相关,-1(反相关) ~ 1(正相关),0表示不相关
COUNT( <*> ) 计数
COVAR_POP(expr, expr) 总体协方差
COVAR_SAMP(expr, expr) 样本协方差
CUME_DIST 累积分布,即行在组中的相对位置,返回0 ~ 1
DENSE_RANK 行的相对排序(与ORDER BY搭配),相同的值具有一样的序数(NULL计为相同),并不留空序数
FIRST_VALUE 一个组的第一个值
LAG(expr, , ) 访问之前的行,OFFSET是缺省为1 的正数,表示相对行数,DEFAULT是当超出选定窗范围时的返回值(如第一行不存在之前行)
LAST_VALUE 一个组的最后一个值
LEAD(expr, , ) 访问之后的行,OFFSET是缺省为1 的正数,表示相对行数,DEFAULT是当超出选定窗范围时的返回值(如最后行不存在之前行)
MAX(expr) 最大值
MIN(expr) 最小值
NTILE(expr) 按表达式的值和行在组中的位置编号,如表达式为4,则组分4份,分别为1 ~ 4的值,而不能等分则多出的部分在值最小的那组
PERCENT_RANK 类似CUME_DIST,1/(行的序数 - 1)
RANK 相对序数,答应并列,并空出随后序号
RATIO_TO_REPORT(expr) 表达式值 / SUM(表达式值)
ROW_NUMBER 排序的组中行的偏移
STDDEV(expr) 标准差
STDDEV_POP(expr) 总体标准差
STDDEV_SAMP(expr) 样本标准差
SUM(expr) 合计
VAR_POP(expr) 总体方差
VAR_SAMP(expr) 样本方差
VARIANCE(expr) 方差
REGR_ xxxx(expr, expr) 线性回归函数
REGR_SLOPE：返回斜率，等于COVAR_POP(expr1, expr2) / VAR_POP(expr2)
REGR_INTERCEPT：返回回归线的y截距，等于
AVG(expr1) - REGR_SLOPE(expr1, expr2) * AVG(expr2)
REGR_COUNT：返回用于填充回归线的非空数字对的数目
REGR_R2：返回回归线的决定系数，计算式为：
If VAR_POP(expr2) = 0 then return NULL
If VAR_POP(expr1) = 0 and VAR_POP(expr2) != 0 then return 1
If VAR_POP(expr1) > 0 and VAR_POP(expr2 != 0 then
return POWER(CORR(expr1,expr),2)
REGR_AVGX：计算回归线的自变量(expr2)的平均值，去掉了空对(expr1, expr2)后，等于AVG(expr2)
REGR_AVGY：计算回归线的应变量(expr1)的平均值，去掉了空对(expr1, expr2)后，等于AVG(expr1)
REGR_SXX： 返回值等于REGR_COUNT(expr1, expr2) * VAR_POP(expr2)
REGR_SYY： 返回值等于REGR_COUNT(expr1, expr2) * VAR_POP(expr1)
REGR_SXY: 返回值等于REGR_COUNT(expr1, expr2) * COVAR_POP(expr1, expr2)

首先：创建表及接入测试数据

```SQL
CREATE TABLE students
(id number(15,0),
area varchar2(10),
stu_type varchar2(2),
score number(20,2));
insert into students values(1, '111', 'g', 80 );
insert into students values(1, '111', 'j', 80 );
insert into students values(1, '222', 'g', 89 );
insert into students values(1, '222', 'g', 68 );
insert into students values(2, '111', 'g', 80 );
insert into students values(2, '111', 'j', 70 );
insert into students values(2, '222', 'g', 60 );
insert into students values(2, '222', 'j', 65 );
insert into students values(3, '111', 'g', 75 );
insert into students values(3, '111', 'j', 58 );
insert into students values(3, '222', 'g', 58 );
insert into students values(3, '222', 'j', 90 );
insert into students values(4, '111', 'g', 89 );
insert into students values(4, '111', 'j', 90 );
insert into students values(4, '222', 'g', 90 );
insert into students values(4, '222', 'j', 89 );
commit;
```



二、具体应用：
1、分组求和：
1）GROUP BY子句
--A、GROUPING SETS

```SQL
SELECT id,area,stu_type,sum(score) score
from students
GROUP BY grouping sets((id,area,stu_type),(id,area),id)
ORDER BY id,area,stu_type;
```

![1641344833490](Images/1641344833490.png)

/*--------理解grouping sets
select a, b, c, sum( d ) from t
group by grouping sets ( a, b, c )

等效于

select * from (
select a, null, null, sum( d ) from t group by a
union all
select null, b, null, sum( d ) from t group by b
union all
select null, null, c, sum( d ) from t group by c
)
*/

--B、ROLLUP

select id,area,stu_type,sum(score) score
from students
group by rollup(id,area,stu_type)
order by id,area,stu_type;

/*--------理解rollup
select a, b, c, sum( d )
from t
group by rollup(a, b, c);

等效于

select * from (
select a, b, c, sum( d ) from t group by a, b, c
union all
select a, b, null, sum( d ) from t group by a, b
union all
select a, null, null, sum( d ) from t group by a
union all
select null, null, null, sum( d ) from t
)
*/

--C、CUBE

```SQL
SELECT id,area,stu_type,sum(score) score
from students
GROUP BY cube(id,area,stu_type)
ORDER BY id,area,stu_type;
```

![1641344876251](Images/1641344876251.png)

/*--------理解cube
select a, b, c, sum( d ) from t
group by cube( a, b, c)

等效于

select a, b, c, sum( d ) from t
group by grouping sets(
( a, b, c ),
( a, b ), ( a ), ( b, c ),
( b ), ( a, c ), ( c ),
() )
*/

--D、GROUPING
/*从上面的结果中我们很容易发现,每个统计数据所对应的行都会出现null,
如何来区分到底是根据那个字段做的汇总呢,grouping函数判断是否合计列!*/

```SQL
SELECT decode(grouping(id),1,'all id',id) id,
decode(grouping(area),1,'all area',to_char(area)) area,
decode(grouping(stu_type),1,'all_stu_type',stu_type) stu_type,
sum(score) score
from students
GROUP BY cube(id,area,stu_type)
ORDER BY id,area,stu_type;
```

![1641344913454](Images/1641344913454.png)

二、OVER()函数的使用
1、统计名次——DENSE_RANK(),ROW_NUMBER()
1)允许并列名次、名次不间断，DENSE_RANK()，结果如122344456……
将score按ID分组排名：dense_rank() over(partition by id order by score desc)
将score不分组排名：dense_rank() over(order by score desc)

```SQL
SELECT id,area,score,
dense_rank() over(partition by id order by score desc) 分组id排序,
dense_rank() over(order by score desc) 不分组排序
from students order by id,area;
```

![1641344940995](Images/1641344940995.png)

2)不允许并列名次、相同值名次不重复，ROW_NUMBER()，结果如123456……
将score按ID分组排名：row_number() over(partition by id order by score desc)
将score不分组排名：row_number() over(order by score desc)

```SQL
SELECT id,area,score,
row_number() over(partition by id order by score desc) 分组id排序,
row_number() over(order by score desc) 不分组排序
from students order by id,area;
```

![1641344960976](Images/1641344960976.png)

3)允许并列名次、复制名次自动空缺，rank()，结果如12245558……
将score按ID分组排名：rank() over(partition by id order by score desc)
将score不分组排名：rank() over(order by score desc)

```SQL
SELECT id,area,score,
rank() over(partition by id order by score desc) 分组id排序,
rank() over(order by score desc) 不分组排序
from students order by id,area;
```

![1641344984859](Images/1641344984859.png)

4)名次分析，cume_dist()——-最大排名/总个数
函数：cume_dist() over(order by id)

```SQL
SELECT id,area,score,
cume_dist() over(order by id) a, --按ID最大排名/总个数
cume_dist() over(partition by id order by score desc) b, --ID分组中，scroe最大排名值/本组总个数
row_number() over (order by id) 记录号
from students order by id,area;
```

![1641345001196](Images/1641345001196.png)

5)利用cume_dist()，允许并列名次、复制名次自动空缺，取并列后较大名次，结果如22355778……
将score按ID分组排名：cume_dist() over(partition by id order by score desc)*sum(1) over(partition by id)
将score不分组排名：cume_dist() over(order by score desc)*sum(1) over()

```SQL
SELECT id,area,score,
sum(1) over() as 总数,
sum(1) over(partition by id) as 分组个数,
(cume_dist() over(partition by id order by score desc))*(sum(1) over(partition by id)) 分组id排序,
(cume_dist() over(order by score desc))*(sum(1) over()) 不分组排序
from students order by id,area
```

![1641345032721](Images/1641345032721.png)

2、分组统计－－sum(),max(),avg(),RATIO_TO_REPORT()

```SQL
SELECT id,area,
sum(1) over() as 总记录数,
sum(1) over(partition by id) as 分组记录数,
sum(score) over() as 总计 ,
sum(score) over(partition by id) as 分组求和,
sum(score) over(order by id) as  分组连续求和,
sum(score) over(partition by id,area) as 分组ID和area求和,
sum(score) over(partition by id order by area) as 分组ID并连续按area求和,
max(score) over() as 最大值,
max(score) over(partition by id) as 分组最大值,
max(score) over(order by id) as 分组连续最大值,
max(score) over(partition by id,area) as 分组ID和area求最大值,
max(score) over(partition by id order by area) as 分组ID并连续按area求最大值,
avg(score) over() as 所有平均,
avg(score) over(partition by id) as 分组平均,
avg(score) over(order by id) as 分组连续平均,
avg(score) over(partition by id,area) as 分组ID和area平均,
avg(score) over(partition by id order by area) as 分组ID并连续按area平均,
RATIO_TO_REPORT(score) over() as "占所有%",
RATIO_TO_REPORT(score) over(partition by id) as "占分组%",
score from students;
```

![1641345073805](Images/1641345073805.png)

![1641345109274](Images/1641345109274.png)

3、LAG(COL,n,default)、LEAD(OL,n,default) --取前后边N条数据
取前面记录的值：lag(score,n,x) over(order by id)
取后面记录的值：lead(score,n,x) over(order by id)
参数：n表示移动N条记录，X表示不存在时填充值，iD表示排序列

```SQL
SELECT id,lag(score,1,0) over(order by id) lg,score from students;
SELECT id,lead(score,1,0) over(order by id) lg,score from students;
```

![1641345127964](Images/1641345127964.png)

![1641345153146](Images/1641345153146.png)

4、FIRST_VALUE()、LAST_VALUE()
取第起始1行值：first_value(score,n) over(order by id)
取第最后1行值：LAST_value(score,n) over(order by id)

```SQL
SELECT id,first_value(score) over(order by id) fv,score from students;
SELECT id,last_value(score) over(order by id) fv,score from students;
```

![1641345172918](Images/1641345172918.png)

![1641345186678](Images/1641345186678.png)

#### 连续求和分析函数

SUM(....) OVER.....

功能：连续求和分析函数

参数：具体参数

说明：Oracle分析函数

```SQL
SELECT bdcode, SUM(1) OVER(ORDER BY bdcode) aa from bd_bdinfo;
```

示例：

```SQL
1.原表信息： SQL> break on deptno skip 1  -- 为效果更明显，把不同部门的数据隔段显示。
SQL> select deptno,ename,sal
   2   from emp
   3   order by deptno;

DEPTNO ENAME          SAL
---------- ---------- ----------
       10 CLARK          2450
          KING          5000
          MILLER           1300

       20 SMITH          800
          ADAMS          1100
          FORD          3000
          SCOTT          3000
          JONES          2975

       30 ALLEN          1600
          BLAKE          2850
          MARTIN           1250
          JAMES          950
          TURNER           1500
          WARD          1250

2.先来一个简单的，注意over(...)条件的不同，
使用 sum(sal) over (order by ename)... 查询员工的薪水“连续”求和,
注意over (order   by ename)如果没有order by 子句，求和就不是“连续”的，
放在一起，体会一下不同之处：

SQL> select deptno,ename,sal,
   2   sum(sal) over (order by ename) 连续求和,
   3   sum(sal) over () 总和,                -- 此处sum(sal) over () 等同于sum(sal)
   4   100*round(sal/sum(sal) over (),4) "份额(%)"
   5   from emp
   6   /

DEPTNO ENAME          SAL 连续求和    总和 份额(%)
---------- ---------- ---------- ---------- ---------- ----------
       20 ADAMS          1100    1100    29025    3.79
       30 ALLEN          1600    2700    29025    5.51
       30 BLAKE          2850    5550    29025    9.82
       10 CLARK          2450    8000    29025    8.44
       20 FORD          3000    11000    29025    10.34
       30 JAMES          950    11950    29025    3.27
       20 JONES          2975    14925    29025    10.25
       10 KING          5000    19925    29025    17.23
       30 MARTIN           1250    21175    29025    4.31
       10 MILLER           1300    22475    29025    4.48
       20 SCOTT          3000    25475    29025    10.34
       20 SMITH          800    26275    29025    2.76
       30 TURNER           1500    27775    29025    5.17
       30 WARD          1250    29025    29025    4.31

3.使用子分区查出各部门薪水连续的总和。注意按部门分区。注意over(...)条件的不同，
sum(sal) over (partition by deptno order by ename) 按部门“连续”求总和
sum(sal) over (partition by deptno) 按部门求总和
sum(sal) over (order by deptno，ename) 不按部门“连续”求总和
sum(sal) over () 不按部门，求所有员工总和，效果等同于sum(sal)。

SQL> select deptno,ename,sal,
   2   sum(sal) over (partition by deptno order by ename) 部门连续求和,--各部门的薪水"连续"求和
   3   sum(sal) over (partition by deptno) 部门总和,   -- 部门统计的总和，同一部门总和不变
   4   100*round(sal/sum(sal) over (partition by deptno),4) "部门份额(%)",
   5   sum(sal) over (order by deptno,ename) 连续求和, --所有部门的薪水"连续"求和
   6   sum(sal) over () 总和,   -- 此处sum(sal) over () 等同于sum(sal)，所有员工的薪水总和
   7   100*round(sal/sum(sal) over (),4) "总份额(%)"
   8   from emp
   9   /

DEPTNO ENAME SAL 部门连续求和 部门总和 部门份额(%) 连续求和 总和   总份额(%)
------ ------ ----- ------------ ---------- ----------- ---------- ------ ----------
10 CLARK 2450       2450    8750       28    2450   29025    8.44
   KING 5000       7450    8750    57.14    7450   29025    17.23
   MILLER   1300       8750    8750    14.86    8750   29025    4.48

20 ADAMS 1100       1100    10875    10.11    9850   29025    3.79
   FORD 3000       4100    10875    27.59    12850   29025    10.34
   JONES 2975       7075    10875    27.36    15825   29025    10.25
   SCOTT 3000        10075    10875    27.59    18825   29025    10.34
   SMITH 800        10875    10875        7.36    19625   29025    2.76

30 ALLEN 1600       1600    9400    17.02    21225   29025    5.51
   BLAKE 2850       4450    9400    30.32    24075   29025    9.82
   JAMES 950       5400    9400    10.11    25025   29025    3.27
   MARTIN   1250       6650    9400        13.3    26275   29025    4.31
   TURNER   1500       8150    9400    15.96    27775   29025    5.17
   WARD 1250       9400    9400        13.3    29025   29025    4.31


4.来一个综合的例子，求和规则有按部门分区的，有不分区的例子
SQL> select deptno,ename,sal,sum(sal) over (partition by deptno order by sal) dept_sum,
   2   sum(sal) over (order by deptno,sal) sum
   3   from emp;

DEPTNO ENAME          SAL DEPT_SUM        SUM
---------- ---------- ---------- ---------- ----------
       10 MILLER           1300    1300    1300
          CLARK          2450    3750    3750
          KING          5000    8750    8750

       20 SMITH          800        800    9550
          ADAMS          1100    1900    10650
          JONES          2975    4875    13625
          SCOTT          3000    10875    19625
          FORD          3000    10875    19625

       30 JAMES          950        950    20575
          WARD          1250    3450    23075
          MARTIN           1250    3450    23075
          TURNER           1500    4950    24575
          ALLEN          1600    6550    26175
          BLAKE          2850    9400    29025

5.来一个逆序的，即部门从大到小排列，部门里各员工的薪水从高到低排列，累计和的规则不变。

SQL> select deptno,ename,sal,
   2   sum(sal) over (partition by deptno order by deptno desc,sal desc) dept_sum,
   3   sum(sal) over (order by deptno desc,sal desc) sum
   4   from emp;

DEPTNO ENAME          SAL DEPT_SUM        SUM
---------- ---------- ---------- ---------- ----------
       30 BLAKE          2850    2850    2850
          ALLEN          1600    4450    4450
          TURNER           1500    5950    5950
          WARD          1250    8450    8450
          MARTIN           1250    8450    8450
          JAMES          950    9400    9400

       20 SCOTT          3000    6000    15400
          FORD          3000    6000    15400
          JONES          2975    8975    18375
          ADAMS          1100    10075    19475
          SMITH          800    10875    20275

       10 KING          5000    5000    25275
          CLARK          2450    7450    27725
          MILLER           1300    8750    29025


6.体会：在"... from emp;"后面不要加order   by 子句，使用的分析函数的(partition by deptno order by sal)
里已经有排序的语句了，如果再在句尾添加排序子句，一致倒罢了，不一致，结果就令人费劲了。如：

SQL> select deptno,ename,sal,sum(sal) over (partition by deptno order by sal) dept_sum,
   2   sum(sal) over (order by deptno,sal) sum
   3   from emp
   4   order by deptno desc;

DEPTNO ENAME          SAL DEPT_SUM        SUM
---------- ---------- ---------- ---------- ----------
       30 JAMES          950        950    20575
          WARD          1250    3450    23075
          MARTIN           1250    3450    23075
          TURNER           1500    4950    24575
          ALLEN          1600    6550    26175
          BLAKE          2850    9400    29025

       20 SMITH          800        800    9550
          ADAMS          1100    1900    10650
          JONES          2975    4875    13625
          SCOTT          3000    10875    19625
          FORD          3000    10875    19625

       10 MILLER           1300    1300    1300
          CLARK          2450    3750    3750
          KING          5000    8750    8750
```

#### 排序值分析函数

RANK() DESE_RANK()

```SQL
--语法
RANK ( ) OVER ( [query_partition_clause] order_by_clause )
	dense_RANK ( ) OVER ( [query_partition_clause] order_by_clause )
```

功能：聚合函数RANK和DENSE_RANK主要的功能时计算一组数值的排序值

参数

DENSE_RAN与RANK()用法相当

区别：DENSE_RANK在并列关系，相关等级不会跳过。RANK则跳过，RANK()时跳跃排序，有两个第二名时接下来就是第四名（同样时在各个分组内）DENSE_RANK()是连续排序，有两个第二名时仍然跟着第三名。

说明：Oracle分析函数

```SQL
--示例
聚合函数RANK 和 dense_rank 主要的功能是计算一组数值中的排序值。
　　
　　在9i版本之前，只有分析功能（analytic ），即从一个查询结果中计算每一行的排序值，是基于order_by_clause子句中的value_exprs指定字段的。
　　
　　其语法为：
　　
　　RANK ( ) OVER ( [query_partition_clause] order_by_clause )
　　
　　在9i版本新增加了合计功能（aggregate），即对给定的参数值在设定的排序查询中计算出其排序值。这些参数必须是常数或常值表达式，且必须和ORDER BY子句中的字段个数、位置、类型完全一致。
　　
　　其语法为：
　　
　　RANK ( expr [, expr]... ) WITHIN GROUP
　　( ORDER BY
　　expr [ DESC | ASC ] [NULLS { FIRST | LAST }]
　　[, expr [ DESC | ASC ] [NULLS { FIRST | LAST }]]...
　　)
　　
　　例子1：
　　
　　有表Table内容如下
　　
　　COL1　COL2
　　　 1　1
　　　 2　1
　　　 3　2
　　　 3　1
　　　 4　1
　　　 4　2
　　　 5　2
　　　 5　2
　　　 6　2
　　
　　分析功能：列出Col2分组后根据Col1排序,并生成数字列。比较实用于在成绩表中查出各科前几名的信息。
　　
　　SELECT a.*,RANK() OVER(PARTITION BY col2 ORDER BY col1) "Rank" FROM table a;
　　
　　结果如下：
　　
　　COL1　COL2　Rank
　　　 1　1　　 1
　　　 2　1　　 2
　　　 3　1　　 3
　　　 4　1　　 4
　　　 3　2　　 1
　　　 4　2　　 2
　　　 5　2　　 3
　　　 5　2　　 3
　　　 6　2　　 5
　　
　　例子2：
　　
　　TABLE：A （科目，分数）
　　
　　数学，80
　　语文，70
　　数学，90
　　数学，60
　　数学，100
　　语文，88
　　语文，65
　　语文，77
　　
　　现在我想要的结果是：（即想要每门科目的前3名的分数）
    数学，100
　　数学，90
　　数学，80
　　语文，88
　　语文，77
　　语文，70
　　
　　那么语句就这么写：
　　
　　select * from (select rank() over(partition by 科目 order by 分数 desc) rk,a.* from a) t
　　where t.rk<=3;
　　
　　例子3：
　　
　　合计功能：计算出数值(4,1)在Orade By Col1,Col2排序下的排序值，也就是col1=4,col2=1在排序以后的位置
　　
　　SELECT RANK(4,3) WITHIN GROUP (ORDER BY col1,col2) "Rank" FROM table;
　　
　　结果如下：
　　Rank
　　4
　　
　　dense_rank与rank()用法相当，但是有一个区别：dence_rank在并列关系是，相关等级不会跳过。rank则跳过
　　
　　例如：表
　　
　　A　　　　　　B　　　　　　C
　　a　　　　　liu　　　　　wang
　　a　　　　　jin　　　　　shu
　　a　　　　　cai　　　　　kai
　　b　　　　　yang　　　　 du
　　b　　　　　lin　　　　　ying
　　b　　　　　yao　　　　　cai
　　b　　　　　yang　　　　 99
　　
　　例如：当rank时为：
　　
　　select m.a,m.b,m.c,rank() over(partition by a order by b) liu from test3 m
　　
　　 A　　　　　B　　　　　　 C　　　　　LIU
　　 a　　　　　cai　　　　　 kai　　　　　1
　　 a　　　　　jin　　　　　 shu　　　　　2
　　 a　　　　　liu　　　　　 wang　　　　 3
　　 b　　　　　lin　　　　　 ying　　　　 1
　　 b　　　　　yang　　　　　du　　　　　 2
　　 b　　　　　yang　　　　　99　　　　　 2
　　 b　　　　　yao　　　　　 cai　　　　　4
　　
　　而如果用dense_rank时为：
　　
　　select m.a,m.b,m.c,dense_rank() over(partition by a order by b) liu from test3 m
　　
　　 A　　　　　B　　　　　　 C　　　　　LIU
　　 a　　　　　cai　　　　　kai　　　　　1
　　 a　　　　　jin　　　　　shu　　　　　2
　　 a　　　　　liu　　　　　wang　　　　 3
　　 b　　　　　lin　　　　　ying　　　　 1
　　 b　　　　　yang　　　　 du　　　　　 2
　　 b　　　　　yang　　　　 99　　　　　 2
　　 b　　　　　yao　　　　　cai　　　　　3
```

#### 排序后顺序号分析函数

ROW_NUMBER

语法：

```SQL
ROW_NUMBER() OVER(PARTITION BY COL1 ORDER BY COL2)
```

功能：表示根据COL1分组，在分组内部根据COL2排序，而这个值就表示魅族内部排序后的顺序编号（组内联系的唯一的），ROW_NUMBER()返回的主要是“行”的信息，并没有排名

主要功能：用于取前几名或者最后几名

示例：

```SQL
表内容如下：
name | seqno | description
A | 1 | test
A | 2 | test
A | 3 | test
A | 4 | test
B | 1 | test
B | 2 | test
B | 3 | test
B | 4 | test
C | 1 | test
C | 2 | test
C | 3 | test
C | 4 | test

有一个sql语句，搜索的结果是
A | 1 | test
A | 2 | test
B | 1 | test
B | 2 | test
C | 1 | test
C | 2 | test
实现:
select name,seqno,description
from(select name,seqno,description,row_number() over (partition by name order by seqno) id
from table_name) where id<=3;
```

#### 取上下行数据分析函数

LAG()和LEAD()

语法：

```SQL
LAG(EXPR,,)
LEAD(EXPR,,)
```

功能：表示根据COL1分组，在分组内部根据COL2排序，而这个值就表示魅族内部排序后的顺序编号（组内连续的唯一的）LEAD()下一个值LAG()上一个值

参数：EXPR是从其他行返回的表达式。OFFEST是缺省为1的正数，表示相对行数，希望检索的当前行分区的偏移量。DEFAULT是在OFFEST表示的数目超出了分组的范围时返回的值。

示例：

```SQL
-- Create table
create table LEAD_TABLE
(
 CASEID VARCHAR2(10),
 STEPID VARCHAR2(10),
 ACTIONDATE DATE
)
tablespace COLM_DATA
 pctfree 10
 initrans 1
 maxtrans 255
 storage
 (
 initial 64K
 minextents 1
 maxextents unlimited
 );

insert into LEAD_TABLE values('Case1','Step1',to_date('20070101','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step2',to_date('20070102','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step3',to_date('20070103','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step4',to_date('20070104','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step5',to_date('20070105','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step4',to_date('20070106','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step6',to_date('20070101','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case1','Step1',to_date('20070201','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case2','Step2',to_date('20070202','yyyy-mm-dd'));
insert into LEAD_TABLE values('Case2','Step3',to_date('20070203','yyyy-mm-dd'));
commit;




结果如下：

Case1 Step1 2007-1-1 Step2 2007-1-2
Case1 Step2 2007-1-2 Step3 2007-1-3 Step1 2007-1-1
Case1 Step3 2007-1-3 Step4 2007-1-4 Step2 2007-1-2
Case1 Step4 2007-1-4 Step5 2007-1-5 Step3 2007-1-3
Case1 Step5 2007-1-5 Step4 2007-1-6 Step4 2007-1-4
Case1 Step4 2007-1-6 Step6 2007-1-7 Step5 2007-1-5
Case1 Step6 2007-1-7 Step4 2007-1-6
Case2 Step1 2007-2-1 Step2 2007-2-2
Case2 Step2 2007-2-2 Step3 2007-2-3 Step1 2007-2-1
Case2 Step3 2007-2-3 Step2 2007-2-2

还可以进一步统计一下两者的相差天数

select caseid,stepid,actiondate,nextactiondate,nextactiondate-actiondate datebetween from (
select caseid,stepid,actiondate,lead(stepid) over (partition by caseid order by actiondate) nextstepid,
lead(actiondate) over (partition by caseid order by actiondate) nextactiondate,
lag(stepid) over (partition by caseid order by actiondate) prestepid,
lag(actiondate) over (partition by caseid order by actiondate) preactiondate
from lead_table)
结果如下：

Case1 Step1 2007-1-1 2007-1-2 1
Case1 Step2 2007-1-2 2007-1-3 1
Case1 Step3 2007-1-3 2007-1-4 1
Case1 Step4 2007-1-4 2007-1-5 1
Case1 Step5 2007-1-5 2007-1-6 1
Case1 Step4 2007-1-6 2007-1-7 1
Case1 Step6 2007-1-7
Case2 Step1 2007-2-1 2007-2-2 1
Case2 Step2 2007-2-2 2007-2-3 1
Case2 Step3 2007-2-3


每一条记录都能连接到上/下一行的内容

lead （） 下一个值 lag（） 上一个值

select caseid,stepid,actiondate,lead(stepid) over (partition by caseid order by actiondate) nextstepid,
lead(actiondate) over (partition by caseid order by actiondate) nextactiondate,
lag(stepid) over (partition by caseid order by actiondate) prestepid,
lag(actiondate) over (partition by caseid order by actiondate) preactiondate
from lead_table
```

### 其他函数

#### DUMP(w[, x[, y[, z]]])

功能：饭hi数据类型、字节长度和再内部的存储位置

参数：w为各种类型的字符串（如字符型、数值型、日期型。。。）

x为返回位置用上面方式表达，可为：8，10， 16或17，分别表示：8、10、16进制和字符串，默认为10；y和z决定了内部参数位置

返回：类型<[长度]>，符号/指数为[数字1，数字2，数字3，，，，，数字20]

```SQL
如：Typ=2 Len=7: 60,89,67,45,23,11,102

SELECT DUMP('ABC',1016) FROM dual;　
返回结果为：Typ=96 Len=3 CharacterSet=ZHS16GBK: 41,42,43

　　代码 数据类型
　　0 对应 VARCHAR2
　　1 对应 NUMBER
　　8 对应 LONG
　　12 对应 DATE
　　23 对应 RAW
　　24 对应 LONG RAW
　　69 对应 ROWID
　　96 对应 CHAR
　　106 对应 MSSLABEL



各位的含义如下:

1.类型: Number型,Type=2 (类型代码可以从Oracle的文档上查到)
2.长度:指存储的字节数
3.符号/指数位
在存储上,Oracle对正数和负数分别进行存储转换:
正数：加1存储(为了避免Null)
负数：被101减,如果总长度小于21个字节，最后加一个102(是为了排序的需要)

指数位换算:
正数：指数=符号/指数位 - 193 (最高位为1是代表正数)
负数：指数=62 - 第一字节

4.从<数字1>开始是有效的数据位

从<数字1>开始是最高有效位,所存储的数值计算方法为：

将下面计算的结果加起来：

每个<数字位>乘以100^(指数-N) (N是有效位数的顺序位，第一个有效位的N=0)

5、举例说明

SQL> select dump(123456.789) from dual;
返回：Typ=2 Len=6: 195,13,35,57,79,91

<指数>:    195 - 193 = 2
<数字1>     13 - 1     = 12 *100^(2-0) 120000
<数字2>     35 - 1     = 34 *100^(2-1) 3400
<数字3>     57 - 1     = 56 *100^(2-2) 56
<数字4>     79 - 1     = 78 *100^(2-3) .78
<数字5>     91 - 1     = 90 *100^(2-4) .009
　                            123456.789

SQL> select dump(-123456.789) from dual;
返回：Typ=2 Len=7: 60,89,67,45,23,11,102
算法：
<指数>  62 - 60 = 2(最高位是0，代表为负数)
<数字1> 101 - 89 = 12 *100^(2-0) 120000
<数字2> 101 - 67 = 34 *100^(2-1) 3400
<数字3> 101 - 45 = 56 *100^(2-2) 56
<数字4> 101 - 23 = 78 *100^(2-3) .78
<数字5> 101 - 11 = 90 *100^(2-4) .009
　                              123456.789(-)

现在再考虑一下为什么在最后加102是为了排序的需要，-123456.789在数据库中实际存储为

60,89,67,45,23,11

而-123456.78901在数据库中实际存储为

60,89,67,45,23,11,91

可见，如果不在最后加上102，在排序时会出现-123456.789<-123456.78901的情况。
```

#### GREATEST(exp1, exp2, exp3, ..., expn)

功能：返回表达式列表中值最大的一个。如果表达式类型不同，会隐含转换为第一个表达式类型。

参数：exp1.....n，各类型表达式

返回：exp1类型

SELECT GREATEST(10.32, '123', '2006') FROM dual;

SELECT GREATE('kdnf', 'dfd', 'a', '206') FROM dual;

![1641447033634](Images/1641447033634.png)

#### least(exp1,exp2,exp3,……,expn)

```sql
【功能】返回表达式列表中值最小的一个。如果表达式类型不同，会隐含转换为第一个表达式类型。
【参数】exp1……n，各类型表达式
【返回】exp1类型

【示例】
SELECT least(10,32,'123','2006') FROM dual;

SELECT least('kdnf','dfd','a','206') FROM dual;
```

#### NVL

```SQL
语法】NVL (expr1, expr2)
【功能】若expr1为NULL，返回expr2；expr1不为NULL，返回expr1。
注意两者的类型要一致


【语法】NVL2 (expr1, expr2, expr3)
【功能】expr1不为NULL，返回expr2；expr2为NULL，返回expr3。
	expr2和expr3类型不同的话，expr3会转换为expr2的类型
```

#### USER

```SQL
【功能】返回当前会话对应的数据库用户名。
【参数】无

【返回】字符型
```

#### UID

```SQL
【功能】返回当前会话所对应的用户id号。
【参数】无

【返回】字符型
```

#### USERENV

```SQL
【功能】返回当前会话上下文属性。
【参数】Parameter是参数，可以用以下参数代替：
Isdba:若用户具有dba权限，则返回true,否则返回false.
Language:返回当前会话对应的语言、地区和字符集。
LANG:返回当前环境的语言的缩写
Terminal:返回当前会话所在终端的操作系统标识符。
Sessionid:返回正在使用的审计会话号.
Client_info:返回用户会话信息，若没有则返回null.
【返回】根据参数不同则类型不同

【示例】
Select userenv('isdba'),userenv('Language'),userenv('Terminal'),userenv('Client_info') from dual;
```

#### DECODE

```SQL
(条件,值1,翻译值1,值2,翻译值2,...值n,翻译值n,缺省值)
【功能】根据条件返回相应值
【参数】c1, c2, ...,cn,字符型/数值型/日期型，必须类型相同或null
注：值1……n 不能为条件表达式,这种情况只能用case when then end解决

·含义解释：　　
　　decode(条件,值1,翻译值1,值2,翻译值2,...值n,翻译值n,缺省值)　　
　　该函数的含义如下：　　
　　IF 条件=值1 THEN
　　RETURN(翻译值1)
　　ELSIF 条件=值2 THEN
　　RETURN(翻译值2)
　　......
　　ELSIF 条件=值n THEN
　　RETURN(翻译值n)　　
　　ELSE
　　RETURN(缺省值)
　　END IF
　　
或：
　　when case 条件=值1 THEN
　　RETURN(翻译值1)
　　ElseCase 条件=值2 THEN
　　RETURN(翻译值2)
　　......
　　ElseCase 条件=值n THEN
　　RETURN(翻译值n)　　
　　ELSE
　　RETURN(缺省值)
　　END


【示例】
　　·使用方法：　　
　　1、比较大小　　
　　select decode(sign(变量1-变量2),-1,变量1,变量2) from dual; --取较小值
　　sign()函数根据某个值是0、正数还是负数，分别返回0、1、-1　　
　　例如：
　　变量1=10，变量2=20
　　则sign(变量1-变量2)返回-1，decode解码结果为“变量1”，达到了取较小值的目的。
　　
　　2、表、视图结构转化　　
　　现有一个商品销售表sale，表结构为：　　
　　month　　　 char(6)　　　　　 --月份
　　sell　　　　number(10,2)　　　--月销售金额　　
　　现有数据为：　　
　　200001　　1000
　　200002　　1100
　　200003　　1200
　　200004　　1300
　　200005　　1400
　　200006　　1500
　　200007　　1600
　　200101　　1100
　　200202　　1200
　　200301　　1300
　　
　　想要转化为以下结构的数据：　　
　　year　　　char(4)　　　　　 --年份
　　month1　　number(10,2)　　　--1月销售金额
　　month2　　number(10,2)　　　--2月销售金额
　　month3　　number(10,2)　　　--3月销售金额
　　month4　　number(10,2)　　　--4月销售金额
　　month5　　number(10,2)　　　--5月销售金额
　　month6　　number(10,2)　　　--6月销售金额
　　month7　　number(10,2)　　　--7月销售金额
　　month8　　number(10,2)　　　--8月销售金额
　　month9　　number(10,2)　　　--9月销售金额
　　month10　　number(10,2)　　　--10月销售金额
　　month11　　number(10,2)　　　--11月销售金额
　　month12　　number(10,2)　　　--12月销售金额
　　
　　结构转化的SQL语句为：
　　
　　create or replace view
　　v_sale(year,month1,month2,month3,month4,month5,month6,　　
　　month7,month8,month9,month10,month11,month12)
　　as
　　select
　　substrb(month,1,4),
　　sum(decode(substrb(month,5,2),'01',sell,0)),
　　sum(decode(substrb(month,5,2),'02',sell,0)),
　　sum(decode(substrb(month,5,2),'03',sell,0)),
　　sum(decode(substrb(month,5,2),'04',sell,0)),
　　sum(decode(substrb(month,5,2),'05',sell,0)),
　　sum(decode(substrb(month,5,2),'06',sell,0)),
　　sum(decode(substrb(month,5,2),'07',sell,0)),
　　sum(decode(substrb(month,5,2),'08',sell,0)),
　　sum(decode(substrb(month,5,2),'09',sell,0)),
　　sum(decode(substrb(month,5,2),'10',sell,0)),
　　sum(decode(substrb(month,5,2),'11',sell,0)),
　　sum(decode(substrb(month,5,2),'12',sell,0))
　　from sale
　　group by substrb(month,1,4);
```

#### NULLIF

```SQL
【语法】NULLIF (expr1, expr2)
【功能】expr1和expr2相等返回NULL，不相等返回expr1
```

#### COALESCE

```SQL
COALESCE(c1, c2, ...,cn)
【功能】返回列表中第一个非空的表达式，如果所有表达式都为空值则返回1个空值
【参数】c1, c2, ...,cn,字符型/数值型/日期型，必须类型相同或null
【返回】同参数类型
【说明】从Oracle 9i版开始，COALESCE函数在很多情况下就成为替代CASE语句的一条捷径
【示例】
select COALESCE(null,3*5,44) hz from dual; 返回15
select COALESCE(0,3*5,44) hz from dual; 返回0
select COALESCE(null,'','AAA') hz from dual; 返回AAA
select COALESCE('','AAA') hz from dual; 返回AAA
```

#### ROWNUM

```SQL
rownum
【功能】返回当前行号
【参数】无

【返回】数值型
```

#### BFILENAME

```SQL
BFILENAME(dir,file)
【功能】函数返回一个空的BFILE位置值指示符，函数用于初始化BFILE变量或者是BFILE列。
【参数】dir是一个directory类型的对象，file为一文件名。

insert into lobdemo(key,bfile_col) values (-1,biflename('utils','file1'));
```

#### VSIZE

```SQL
VSIZE(X)
【功能】返回X的大小(字节)数
【参数】x

select vsize(user),user from dual;
返回：6 asdied


　　select length('adfad合理') "bytesLengthIs" from dual --7

　　select lengthb('adfad') "bytesLengthIs" from dual --5

　　select lengthb('adfad合理') "bytesLengthIs" from dual --9

　　select vsize('adfad合理') "bytesLengthIs" from dual --9

　　select lengthc('adfad合理')"bytesLengthIs" from dual --7


　　lengthb=vsize

　　lengthc=length
```

#### CASE WHEN THEN END

```SQL
case [<表达式>]
when <表达式条件值1> then <满足条件时返回值1>
[when <表达式条件值2> then <满足条件时返回值2>
……
[else  <不满足上述条件时返回值>]]
end

【功能】当：<表达式>＝<表达式条件值1……n> 时，返回对应 <满足条件时返回值1……n>
当<表达式条件值1……n>不为条件表达式时，与函数decode()相同，
decode(<表达式>,<表达式条件值1>,<满足条件时返回值1>,<表达式条件值2>,<满足条件时返回值2> ……,<不满足上述条件时返回值>)

【参数】
<表达式> 默认为true (逻辑型)
<表达式条件值1……n> 类型要与<表达式>类型一致，
若<表达式>为字符型，则<表达式条件值1……n>也要为字符型

【注意点】
1、以CASE开头，以END结尾
2、分支中WHEN 后跟条件，THEN为显示结果
3、ELSE 为除此之外的默认情况，类似于高级语言程序中switch case的default，可以不加
4、END 后跟别名
5、只返回第一个符合条件的值,剩下的when部分将会被自动忽略，得注意条件先后顺序

【示例】
建立环境：
create table xqb
(xqn number(1,0));
insert into xqb xqn values(1);
insert into xqb xqn values(2);
insert into xqb xqn values(3);
insert into xqb xqn values(4);
insert into xqb xqn values(5);
insert into xqb xqn values(6);
insert into xqb xqn values(7);
commit;

查询结果：
SELECT xqn,
       CASE
          WHEN xqn = 1  THEN '星期一'
          WHEN xqn = 2  THEN '星期二'
          WHEN xqn = 3  THEN '星期三'
	  else '星期三以后'
       END 星期
FROM xqb

另类写法
SELECT xqn,
       CASE xqn
          WHEN 1  THEN '星期一'
          WHEN 2  THEN '星期二'
          WHEN 3  THEN '星期三'
	  else '星期三以后'
       END 星期
FROM xqb


decode正确表达：
SELECT xqn,
decode(xqn,1,'星期一',2,'星期二',3,'星期三','星期三以后') 星期
FROM xqb

decode错误表达：
SELECT xqn,
decode(TRUE,xqn=1,'星期一',xqn=2,'星期二',xqn=3,'星期三','星期三以后') 星期
FROM xqb

组合条件表达：
SELECT xqn,
       CASE
          WHEN xqn <= 1  THEN '星期一'
          WHEN xqn <= 2  THEN '星期二'   --条件同：not(xqn<=1) and xqn<=2
          WHEN xqn <= 3  THEN '星期三'   --条件同：not(xqn<=1 and xqn<=2) and xqn<=3
	  else '星期三以后'
       END 星期
FROM xqb
```

#### SYS_GUID

```SQL
【语法】sys_guid()
【功能】生产32位的随机数，不过中间包括一些大写的英文字母。

【返回】长度为32位的字符串，包括0－9和大写A－F

【示例】
select sys_guid() from  dual
```

#### SYS_CONTEXT(c1, c2)

```SQL
【语法】SYS_CONTEXT(c1,c2)
【功能】返回系统c1对应的c2的值。可以使用在SQL/PLSQL中，但不可以用在并行查询或者RAC环境中

【参数】
c1，'USERENV'
c2,参数表，详见示例

【返回】字符串


【示例】
select
SYS_CONTEXT('USERENV','TERMINAL') terminal,
SYS_CONTEXT('USERENV','LANGUAGE') language,
SYS_CONTEXT('USERENV','SESSIONID') sessionid,
SYS_CONTEXT('USERENV','INSTANCE') instance,
SYS_CONTEXT('USERENV','ENTRYID') entryid,
SYS_CONTEXT('USERENV','ISDBA') isdba,
SYS_CONTEXT('USERENV','NLS_TERRITORY') nls_territory,
SYS_CONTEXT('USERENV','NLS_CURRENCY') nls_currency,
SYS_CONTEXT('USERENV','NLS_CALENDAR') nls_calendar,
SYS_CONTEXT('USERENV','NLS_DATE_FORMAT') nls_date_format,
SYS_CONTEXT('USERENV','NLS_DATE_LANGUAGE') nls_date_language,
SYS_CONTEXT('USERENV','NLS_SORT') nls_sort,
SYS_CONTEXT('USERENV','CURRENT_USER') current_user,
SYS_CONTEXT('USERENV','CURRENT_USERID') current_userid,
SYS_CONTEXT('USERENV','SESSION_USER') session_user,
SYS_CONTEXT('USERENV','SESSION_USERID') session_userid,
SYS_CONTEXT('USERENV','PROXY_USER') proxy_user,
SYS_CONTEXT('USERENV','PROXY_USERID') proxy_userid,
SYS_CONTEXT('USERENV','DB_DOMAIN') db_domain,
SYS_CONTEXT('USERENV','DB_NAME') db_name,
SYS_CONTEXT('USERENV','HOST') host,
SYS_CONTEXT('USERENV','OS_USER') os_user,
SYS_CONTEXT('USERENV','EXTERNAL_NAME') external_name,
SYS_CONTEXT('USERENV','IP_ADDRESS') ip_address,
SYS_CONTEXT('USERENV','NETWORK_PROTOCOL') network_protocol,
SYS_CONTEXT('USERENV','BG_JOB_ID') bg_job_id,
SYS_CONTEXT('USERENV','FG_JOB_ID') fg_job_id,
SYS_CONTEXT('USERENV','AUTHENTICATION_TYPE') authentication_type,
SYS_CONTEXT('USERENV','AUTHENTICATION_DATA') authentication_data
from dual;
```

####  Oracle dbms_random

```sql
from:http://space.myfarmer.cn/?action-viewthread-tid-17039

1.dbms_random.value方法

dbms_random是一个可以生成随机数值或者字符串的程序包。这个包有initialize()、seed()、terminate()、value()、normal()、random()、string()等几个函数，但value()是最常用的，value()的用法一般有两个种，第一
function value return number;
这种用法没有参数，会返回一个具有38位精度的数值，范围从0.0到1.0，但不包括1.0，如下示例：
SQL> set serverout on
SQL> begin
   2    for i in 1..10 loop
   3      dbms_output.put_line(round(dbms_random.value*100));
   4    end loop;
   5  end;
   6  /
46
19
45
37
33
57
61
20
82
8

PL/SQL 过程已成功完成。
SQL>

第二种value带有两个参数，第一个指下限，第二个指上限，将会生成下限到上限之间的数字，但不包含上限，“学无止境”兄说的就是第二种，如下：
SQL> begin
   2    for i in 1..10 loop
   3      dbms_output.put_line(trunc(dbms_random.value(1,101)));
   4    end loop;
   5  end;
   6  /
97
77
13
86
68
16
55
36
54
46

PL/SQL 过程已成功完成。



2. dbms_random.string 方法

某些用户管理程序可能需要为用户创建随机的密码。使用10G下的dbms_random.string 可以实现这样的功能。

例如：
SQL> select dbms_random.string('P',8 ) from dual ;

DBMS_RANDOM.STRING('P',8)
----
3q
```

#### UTL_INADDR

```SQL
作用:用于取得局域网或Internet环境中的主机名和IP地址.


1、utl_inaddr.get_host_address 环境中IP地址
如果查询失败，则提示系统错误
查询www.qq.com的IP地址
select UTL_INADDR.get_host_address('www.qq.com') from dual;
查询本机IP地址
select UTL_INADDR.get_host_address() from dual;
查询局域网内yuechu的IP地址
select UTL_INADDR.get_host_address('yuechu') from dual;


2、UTL_INADDR.get_host_name返回环境中主机名
返回本机主机名
select UTL_INADDR.get_host_name() from dual;
返回局域网内指定IP地址的主机名
select UTL_INADDR.get_host_name('192.168.0.156') from dual;
返回intrenet中指定IP地址的网址
select UTL_INADDR.get_host_name('219.153.50.84') from dual;
```

### 基本SQL语言

#### DDL（数据定义语言）

##### CREATE(创建)

```SQL
CREATE TABLE <table_name>(
column1 DATATYPE [NOT NULL] [PRIMARY KEY],
column2 DATATYPE [NOT NULL],
...
[constraint <约束名> 约束类型 (要约束的字段)
... ] ）
说明：　
DATATYPE --是Oracle的数据类型,可以查看附录。
NUT NULL --可不可以允许资料有空的（尚未有资料填入）。
PRIMARY KEY --是本表的主键。
constraint --是对表里的字段添加约束.(约束类型有
            Check,Unique,Primary key,not null,Foreign key)。

示例:
create table stu(
s_id number(8) PRIMARY KEY,
s_name varchar2(20) not null,
s_sex varchar2(8),
clsid number(8),
constraint u_1 unique(s_name),
constraint c_1 check (s_sex in ('MALE','FEMALE'))
);

复制表

CREATE TABLE <table_name> as <SELECT 语句>

(需注意的是复制表不能复制表的约束);

示例:
create table test as select * from emp;

如果只复制表的结构不复制表的数据则:
create table test as select * from emp where 1=2;

CREATE [UNIQUE] INDEX <index_name> ON <table_name>(字段 [ASC|DESC]);

UNIQUE --确保所有的索引列中的值都是可以区分的。
[ASC|DESC] --在列上按指定排序创建索引。

(创建索引的准则：
1.如果表里有几百行记录则可以对其创建索引(表里的记录行数越多索引的效果就越明显)。
2.不要试图对表创建两个或三个以上的索引。
3.为频繁使用的行创建索引。
)


示例
create index i_1 on emp(empno asc);

CREATE SYNONYM <synonym_name> for <tablename/viewname>

同义词即是给表或视图取一个别名。

示例:
create synonym mm for emp;
```

##### ALTER(修改)

```SQL
1.向表中添加新字段
ALTER TABLE <table_name> ADD (字段1 类型 [NOT NULL],
字段2 类型 [NOT NULL]
.... );

2.修改表中字段
ALTER TABLE <table_name> modify(字段1 类型,
字段2 类型
.... );

3 .删除表中字段
ALTER TABLE <table_name> drop(字段1,
字段2
.... );

4 .修改表的名称
RENAME <table_name> to <new table_name>;

5 .对已经存在的表添加约束
ALTER TABLE <table_name> ADD CONSTRAINT <constraint_name> 约束类型 (针对的字段名);
示例：
Alter table emp add constraint S_F Foreign key (deptno) references dept(deptno);

6 .对表里的约束禁用;
ALTER TABLE <table_name> DISABLE CONSTRAINT <constraint_name>;

7 .对表里的约束重新启用;
ALTER TABLE <table_name> ENABLE CONSTRAINT <constraint_name>;

8 .删除表中约束
ALTER TABLE <table_name> DROP CONSTRAINT <constraint_name>;
示例:
ALTER TABLE emp drop CONSTRAINT <Primary key>;
```

##### DROP(删除)

```SQL
DROP TABLE <table_name>;

示例
drop table emp;

DROP INDEX <index_name>;

示例
drop index i_1;

DROP SYNONYM <synonym_name>;

示例
drop synonym mm;
```

#### DML（数据操作语言）

```SQL
插入记录
INSERT INTO table_name (column1,column2,...)
values ( value1,value2, ...);

示例
insert into emp (empno,ename) values(9500,'AA');


把 一个表中的数据插入另一个表中

INSERT INTO <table_name> <SELECT 语句>
示例
create table a as select * from emp where 1=2;
insert into a select * from emp where sal>2000;

查询记录
一般查询
SELECT [DISTINCT] <column1 [as new name] ,columns2,...>
FROM <table1>
[WHERE <条件>]
[GROUP BY <column_list>]
[HAVING <条件>]
[ORDER BY <column_list> [ASC|DESC]]


DISTINCT --表示隐藏重复的行
WHERE --按照一定的条件查找记录
GROUP BY --分组查找(需要汇总时使用)
HAVING --分组的条件
ORDER BY --对查询结果排序


要显示全部的列可以用*表示
示例：
select * from emp;

WHERE 语句的运算符
where <条件１>AND<条件２> --两个条件都满足
示例：
select * from emp where deptno=10 and sal>1000;

where <条件１>OR<条件２> --两个条件中有一个满足即可
示例：
select * from emp where deptno=10 OR sal>2000;

where NOT <条件> --不满足条件的
示例：
select * from emp where not deptno=10;

where IN(条件列表) --所有满足在条件列表中的记录
示例：
select * from emp where empno in(7788,7369,7499);

where BETWEEN .. AND　..　 --按范围查找
示例：
select * from emp where sal between 1000 and 3000;

where 字段 LIKE --主要用与字符类型的字段
示例1：
select * from emp where ename like '_C%'; --查询姓名中第二个字母是'C'的人
'-' 表示任意字符;
'%' 表示多字符的序列；

where 字段 IS [NOT] NULL --查找该字段是[不是]空的记录

汇总数据是用的函数
SUM --求和
示例：
select deptno,sum(sal) as sumsal from emp GROUP BY deptno;

AVG --求平均值
MAX --求最大值
MIN --求最小值
COUNT --求个数


子查询
SELECT <字段列表> from <table_name> where 字段 运算符(<SELECT 语句>);

示例：
select * from emp where sal=(select max(sal) from emp);

运算符
Any
示例：
select * from emp where sal>ANY(select sal from emp where deptno=30) and deptno<>30;
--找出比deptno=30的员工最低工资高的其他部门的员工

ALL
select * from emp where sal>ALL(select sal from emp where deptno=30) and deptno<>30;
--找出比deptno=30的员工最高工资高的其他部门的员工


连接查询
SELECT <字段列表> from <table1,table2> WHERE table1.字段[(+)]=table2.字段[(+)]

示例
select empno,ename,dname from emp,dept where emp.deptno=dept.deptno;


查询指定行数的数据
SELECT <字段列表> from <table_name> WHERE ROWNUM<行数;
示例:
select * from emp where rownum<=10;--查询前10行记录
注意ROWNUM只能为1 因此不能写 select * from emp where rownum between 20 and 30;

要查第几行的数据可以使用以下方法:
select * from emp where rownum<=3 and empno not in (select empno from emp where rownum<=3);
结果可以返回整个数据的3-6行;

更新数据
UPDATE table_name set column1=new value,column2=new value,...
WHERE <条件>

示例
update emp set sal=1000,empno=8888 where ename='SCOTT'

更新数据
DELETE FROM <table_name>
WHERE <条件>

示例
delete from emp where empno='7788'
```

#### DCL（数据控制语言）

```SQL
数据控制语言
1.授权
GRANT <权限列表> to <user_name>;

2.收回权限
REVOKE <权限列表> from <user_name>


Oracle 的权限列表
connect 连接
resource 资源
unlimited tablespace 无限表空间
dba 管理员
session 会话
```

#### TCL（事务控制语言）

```SQL
数据控制语言
1.COMMIT 提交；

2.ROLLBACK [TO savepoint]　回滚;

3.SAVEPOINT <savepoint> 保存位置。
```

### Oracle其他对象

#### 视图

```SQL
创建视图
CREATE [OR REPLACE] VIEW <view_name>
AS
<SELECT 语句>;

OR REPLACE --表示替换以有的视图

删除视图
DROP VIEW <view_name>
```

#### 序列

```SQL
创建序列
CREATE SEQUENCE <sequencen_name>
INCREMENT BY n
START WITH n
[MAXVALUE n][MINVALUE n]
[CYCLE|NOCYCLE]
[CACHE n|NOCACHE];

INCREMENT BY n --表示序列每次增长的幅度;默认值为1.
START WITH n --表示序列开始时的序列号。默认值为1.
MAXVALUE n --表示序列可以生成的最大值(升序).
MINVALUE n --表示序列可以生成的最小值(降序).
CYCLE --表示序列到达最大值后，在重新开始生成序列.默认值为 NOCYCLE。
CACHE --允许更快的生成序列.


示例:
create sequence se_1
increment by 1
start with 100
maxvalue 999999
cycle;
```

#### 用户

```SQL
创建用户
CREATE USER <user_name> [profile "DEFAULT"]
identified by "<password>" [default tablespace "USERS"]


删除用户

DROP USER <user_name> CASCADE
```

#### 角色

```SQL
创建角色
CREATE ROLE <role_name>
identified by "<password>"


删除角色

DROP ROLE <role_name>
```

### PL/SQL

#### 基本结构

```SQL
PL/SQL 结构
DECLARE        --声明部分
        声明语句
BEGIN         --执行部分
        执行语句

EXCEPTION         --异常处理部分
        执行语句

END;

变量声明
<变量名> 类型[:=初始值];
特殊类型 字段%type
示例: name emp.ename%type --表示name的类型和emp.ename的类型相同
表 %rowtype
示例: test emp%rowtype --表示test的类型为emp表的行类型;也有 .empno; .ename; .sal ;等属性

常量声明
<变量名> CONSTANT 类型:=初始值;
示例: pi constant number(5,3):=3.14;

全局变量声明
VARIABLE <变量名> 类型;
示例: VARIABLE num number;

使用全局变量
:<变量名>
示例:
:num:=100;
i=:num;

查看全局变量的值
print <变量名>
示例: print num;

赋值运算符: :=
示例: num := 100;

使用SELECT <列名> INTO <变量名> FROM <表名> WHERE <条件>
注意select into 语句的返回结果只能为一行;
示例：test emp%rowtype;
select * into test from emp where empno=7788;

用户交互输入
<变量>:='&变量'
示例：
num:=&num;

注意oracle的用户交互输入是先接受用户输入的所有值后在执行语句；
所以不能使用循环进行用户交互输入;


条件控制语句
IF <条件1> THEN
    语句
[ELSIF <条件2> THEN
   语句
          .
          .
          .
ELSIF <条件n> THEN
   语句]
[ELSE
    语句]
END IF;



循环控制语句
1.LOOP
LOOP
   语句;
   EXIT WHEN <条件>
END LOOP;

2.WHILE LOOP
WHILE <条件>
LOOP
   语句;
END LOOP;

3.FOR
FOR <循环变量> IN 下限..上限
LOOP
   语句;
END LOOP;


NULL 语句
null;
表示没有操作;


注释使用
单行注释： --
多行注释：/* .......
      ...............*/


异常处理

EXCEPTION
   WHEN <异常类型> THEN
            语句;
   WHEN OTHERS THEN
            语句;
END;
```

#### 游标

```SQL
显示游标

定义:CURSOR <游标名> IS <SELECT 语句> [FOR UPDATE | FOR UPDATE OF 字段];

[FOR UPDATE | FOR UPDATE OF 字段] --给游标加锁,既是在程序中有"UPDATE","INSERT","DELETE"语句对数据库操作时。
游标自动给指定的表或者字段加锁，防止同时有别的程序对指定的表或字段进行"UPDATE","INSERT","DELETE"操作.
在使用"DELETE","UPDATE"后还可以在程序中使用CURRENT OF <游标名> 子句引用当前行.

操作:OPEN <游标名> --打开游标
    FETCH <游标名> INTO 变量1,变量2,变量3,....变量n,;
                或者
    FETCH <游标名> INTO 行对象;         --取出游标当前位置的值
    CLOSE <游标名> --关闭游标
属性: %NOTFOUND --如果FETCH语句失败，则该属性为"TRUE"，否则为"FALSE";
    %FOUND --如果FETCH语句成果，则该属性为"TRUE"，否则为"FALSE";
    %ROWCOUNT --返回游标当前行的行数;
    %ISOPEN --如果游标是开的则返回"TRUE"，否则为"FALSE";

使用:
LOOP循环
   示例:
DECLARE
     cursor c_1 is select * from emp;     --定义游标
     r c_1%rowtype;      --定义一个行对象，用于获得游标的值
BEGIN
     if c_1%isopen then
          CLOSE c_1;
     end if;              
     OPEN c_1;          --判断游标是否打开.如果开了将其关闭，然后在打开
     dbms_output.put_line('行号 姓名 薪水');
     LOOP
     FETCH c_1 INTO r;     --取值
     EXIT WHEN c_1%NOTFOUND;     --如果游标没有取到值，退出循环.
     dbms_output.put_line(c_1%rowcount||' '||r.ename||' '||r.sal);    --输出结果,需要 set serverout on 才能显示.
     END LOOP;
END;


FOR循环
   示例:
DECLARE
     cursor c_1 is select ename,sal from emp;     --定义游标     
BEGIN
     dbms_output.put_line('行号 姓名 薪水');
     FOR i IN c_1         --for循环中的循环变量i为c_1%rowtype类型;
     LOOP
     dbms_output.put_line(c_1%rowcount||' '||i.ename||' '||i.sal);    --输出结果,需要 set serverout on 才能显示.
     END LOOP;
END;

for循环使用游标是在循环开始前自动打开游标，并且自动取值到循环结束后，自动关闭游标.

游标加锁示例:
DECLARE
     cursor c_1 is select ename,sal from emp for update of sal;     --定义游标对emp表的sal字段加锁.     
BEGIN
     dbms_output.put_line('行号 姓名 薪水');
     FOR i IN c_1         --for循环中的循环变量i为c_1%rowtype类型;
     LOOP
     UPDATE EMP set sal=sal+100 WHERE CURRENT OF c_1; --表示对当前行的sal进行跟新.
     END LOOP;
     FOR i IN c_1        
     LOOP
     dbms_output.put_line(c_1%rowcount||' '||i.ename||' '||i.sal);    --输出结果,需要 set serverout on 才能显示.
     END LOOP;
END;



代参数的游标
定义:CURSOR <游标名>(参数列表) IS <SELECT 语句> [FOR UPDATE | FOR UPDATE OF 字段];
示例:
DECLARE
     cursor c_1(name emp.ename%type) is select ename,sal from emp where ename=name;     --定义游标     
BEGIN
     dbms_output.put_line('行号 姓名 薪水');
     FOR i IN c_1('&name')         --for循环中的循环变量i为c_1%rowtype类型;
     LOOP
     dbms_output.put_line(c_1%rowcount||' '||i.ename||' '||i.sal);    --输出结果,需要 set serverout on 才能显示.
     END LOOP;
END;


隐试游标
隐试游标游标是系统自动生成的。每执行一个DML语句就会产生一个隐试游标，起名字为SQL;

隐试游标不能进行"OPEN" ,"CLOSE","FETCH"这些操作;

属性:
    %NOTFOUND --如果DML语句没有影响到任何一行时，则该属性为"TRUE"，否则为"FALSE";
    %FOUND --如果DML语句影响到一行或一行以上时，则该属性为"TRUE"，否则为"FALSE";
    %ROWCOUNT --返回游标当最后一行的行数;

个人认为隐试游标的作用是判断一个DML语句；
示例：
BEGIN
    DELETE FROM EMP WHERE empno=&a;
    IF SQL%NOTFOUND THEN
        dbms_output.put_line('empno不存在');
    END IF;
   IF SQL%ROWCOUNT>0 THEN
        dbms_output.put_line('删除成功');
    END IF;
END;
```

#### PL/SQL表

```SQL
PL/SQL表
pl/sql表只有两列,其中第一列为序号列为INTEGER类型,第二列为用户自定义列.

定义:TYPE <类型名> IS TABLE OF <列的类型> [NOT NULL] INDEX BY BINARY_INTEGER;
<列的类型>可以为Oracle的数据类行以及用户自定义类型;

属性方法:
.count --返回pl/sql表的总行数
.delect --删除pl/sql表的所有内容
.delect(行数) --删除pl/sql表的指定的行
.delct(开始行，结束行) --删除pl/sql表的多行
.first --返回表的第一个INDEX;
.next(行数) --这个行数的下一条的INDEX;
.last --返回表的最后一个INDEX;

使用
示例:
DECLARE
     TYPE mytable IS TABLE OF VARCHAR2(20) index by binary_integer; --定义一个名为mytable的PL/sql表类型;
     cursor c_1 is select ename from emp;
     n number:=1;
     tab_1 mytable; --为mytable类型实例化一个tab_1对象;
BEGIN
     for i in c_1
     loop
          tab_1(n):=i.ename; --将得到的值输入pl/sql表
          n:=n+1;
    end loop;
     n:=1;
     tab_1.delete(&要删除的行数); --删除pl/sql表的指定行
     for i in tab_1.first..tab_1.count
     loop
          dbms_output.put_line(n||' '||tab_1(n)); --打印pl/sql表的内容
          n:=tab_1.next(n);
     end loop;
EXCEPTION
     WHEN NO_DATA_FOUND THEN                    --由于删除了一行，会发生异常，下面语句可以接着删除的行后显示
          for i in n..tab_1.count+1
     loop
          dbms_output.put_line(n||' '||tab_1(n));
          n:=tab_1.next(n);
     end loop;
END;
```

#### PL/SQL记录类型

```SQL
PL/SQL记录
pl/sql表只有一行,但是有多列。

定义:TYPE <类型名> IS RECORD <列名1 类型1,列名2 类型2,...列名n 类型n,> [NOT NULL]
<列的类型>可以为Oracle的数据类行以及用户自定义类型;可以是记录类型的嵌套

使用
示例:
DECLARE
     TYPE myrecord IS RECORD(id emp.empno%type,
     name emp.ename%type,sal emp.sal%type);     --定义一个名为myrecoed的PL/sql记录类型;
     rec_1 myrecord; --为myrecord类型实例化一个rec_1对象;
BEGIN
          select empno,ename,sal into rec_1.id,rec_1.name,rec_1.sal
          from emp where empno=7788;        --将得到的值输入pl/sql记录
          dbms_output.put_line(rec_1.id||' '||rec_1.name||' '||rec_1.sal); --打印pl/sql记录的内容
END;



结合使用PL/SQL表和PL/SQL记录
示例:
DECLARE
     CURSOR c_1 is select empno,ename,job,sal from emp;
     TYPE myrecord IS RECORD(empno emp.empno%type,ename emp.ename%type,
job emp.job%type,sal emp.sal%type);     --定义一个名为myrecoed的PL/sql记录类型;
     TYPE mytable IS TABLE OF myrecord index by binary_integer;
                                                                   --定义一个名为mytable的PL/sql表类型;字段类型为PL/sql记录类型；

     n number:=1;
     tab_1 mytable; --为mytable类型实例化一个tab_1对象;
BEGIN
          --赋值
          for i in c_1
          loop
               tab_1(n).empno:=i.empno;
               tab_1(n).ename:=i.ename;                    
               tab_1(n).job:=i.job;
               tab_1(n).sal:=i.sal;
               n:=n+1;
          end loop;
          n:=1;
          --输出
          for i in n..tab_1.count
          loop
                dbms_output.put_line(i||' '||tab_1(i).empno
                ||' '||tab_1(i).ename||' '||tab_1(i).job||' '||tab_1(i).sal);
          end loop;
END;
```

#### REF游标

```SQL
强型REF游标

定义:TYPE <游标名> IS REF CURSOR RETURN<返回类型>;


操作:OPEN <游标名> For <select 语句> --打开游标
    FETCH <游标名> INTO 变量1,变量2,变量3,....变量n,;
                或者
    FETCH <游标名> INTO 行对象;         --取出游标当前位置的值
    CLOSE <游标名> --关闭游标
属性: %NOTFOUND --如果FETCH语句失败，则该属性为"TRUE"，否则为"FALSE";
    %FOUND --如果FETCH语句成果，则该属性为"TRUE"，否则为"FALSE";
    %ROWCOUNT --返回游标当前行的行数;
    %ISOPEN --如果游标是开的则返回"TRUE"，否则为"FALSE";

使用:
   示例:
DECLARE
     type c_type is ref cursor return emp%rowtype;     --定义游标
     c_1 c_type;      --实例化这个游标类型
     r emp%rowtype;
BEGIN
     dbms_output.put_line('行号 姓名 薪水');
     open c_1 for select * from emp;
     loop
     fetch c_1 into r;
     exit when c_1%notfound;
     dbms_output.put_line(c_1%rowcount||' '||r.ename||' '||r.sal);    --输出结果,需要 set serverout on 才能显示.
     END LOOP;
close c_1;
END;


弱型REF游标
定义:TYPE <游标名> IS REF CURSOR;


操作:OPEN <游标名> For <select 语句> --打开游标
    FETCH <游标名> INTO 变量1,变量2,变量3,....变量n,;
                或者
    FETCH <游标名> INTO 行对象;         --取出游标当前位置的值
    CLOSE <游标名> --关闭游标
属性: %NOTFOUND --如果FETCH语句失败，则该属性为"TRUE"，否则为"FALSE";
    %FOUND --如果FETCH语句成果，则该属性为"TRUE"，否则为"FALSE";
    %ROWCOUNT --返回游标当前行的行数;
    %ISOPEN --如果游标是开的则返回"TRUE"，否则为"FALSE";
示例：
set autoprint on;
var c_1 refcursor;
DECLARE
   n number;
BEGIN
   n:=&请输入;
   if n=1 then
         open :c_1 for select * from emp;
   else
         open :c_1 for select * from dept;
   end if;
END;
```

#### 过程

```SQL
过程

定义:CREATE [OR REPLACE] PROCEDURE <过程名>[(参数列表)] IS
         [局部变量声明]
         BEGIN
            可执行语句
          EXCEPTION
            异常处理语句
          END [<过程名>];

变量的类型:in 为默认类型,表示输入; out 表示只输出;in out 表示即输入又输出;


操作以有的过程:在PL/SQL块中直接使用过程名;在程序外使用execute <过程名>[(参数列表)]

使用:
   示例:
创建过程:
create or replace procedure p_1(n in out number) is
    r emp%rowtype;
BEGIN
     dbms_output.put_line('姓名 薪水');
     select * into r from emp where empno=n;
     dbms_output.put_line(r.ename||' '||r.sal);    --输出结果,需要 set serverout on 才能显示.
    n:=r.sal;
END;
使用过程:
declare
    n number;
begin
    n:=&请输入员工号;
    p_1(n);
    dbms_output.put_line('n的值为 '||n);
end;


删除过程:
    DROP PROCEDURE <过程名>;
```

#### 函数

```SQL
函数

定义:CREATE [OR REPLACE] FUNCTION <过程名>[(参数列表)] RETURN 数据类型 IS
         [局部变量声明]
         BEGIN
            可执行语句
          EXCEPTION
            异常处理语句
          END [<过程名>];

变量的类型:in 为默认类型,表示输入; out 表示只输出;in out 表示即输入又输出;


使用:
   示例:
创建函数:
create or replace function f_1(n number) return number is
    r emp%rowtype;
BEGIN
     dbms_output.put_line('姓名 薪水');
     select * into r from emp where empno=n;
     dbms_output.put_line(r.ename||' '||r.sal);    --输出结果,需要 set serverout on 才能显示.
     return r.sal;
END;
使用函数:
declare
    n number;
     m number;
begin
    n:=&请输入员工号;
    m:=f_1(n);
    dbms_output.put_line('m的值为 '||m);
end;


删除函数:
    DROP FUNCTION <函数名>;
```

#### 数据包

```SQL
数据包

定义:
   定义包的规范
      CREATE [OR REPLACE] PACKAGE <数据包名> AS
               --公共类型和对象声明
               --子程序说明
      END;
    定义包的主体
      CREATE [OR REPLACE] PACKAGE BODY <数据包名> AS
               --公共类型和对象声明
               --子程序主体
      BEGIN
            -初始化语句
      END;


使用:
   示例:
创建数据包规范:
create or replace package pack_1 as
      n number;
      procedure p_1;
      FUNCTION f_1 RETURN number;
end;

创建数据包主体:
create or replace package body pack_1 as
  procedure p_1 is
       r emp%rowtype;
  begin
       select * into r from emp where empno=7788;
       dbms_output.put_line(r.empno||' '||r.ename||' '||r.sal);
   end;

   FUNCTION f_1 RETURN number is
       r emp%rowtype;
   begin
        select * into r from emp where empno=7788;
       return r.sal;
   end;
end;

使用包:
declare
      n number;
begin
      n:=&请输入员工号;
      pack_1.n:=n;
      pack_1.p_1;
      n:=pack_1.f_1;
      dbms_output.put_line('薪水为 '||n);
end;

在包中使用REF游标
示例:
创建数据包规范:
create or replace package pack_2 as
     TYPE c_type is REF CURSOR; --建立一个ref游标类型
     PROCEDURE p_1(c1 in out c_type); --过程的参数为ref游标类型;
end;

创建数据包主体:
create or replace package body pack_2 as
  PROCEDURE p_1(c1 in out c_type) is
  begin
       open c1 for select * from emp;
   end;
end;

使用包:
var c_1 refcursor;
set autoprint on;
execute pack_2.p_1(:c_1);



删除包:
    DROP PACKAGE <包名>;
```

#### 触发器

```SQL
触发器
创建触发器:
    CREATE [OR REPLACE] TRIGGER <触发器名>
    BEFORE|AFTER
    INSERT|DELETE|UPDATE [OF <列名>] ON <表名>
    [FOR EACH ROW]
     WHEN (<条件>)
     <pl/sql块>

     关键字"BEFORE"在操作完成前触发;"AFTER"则是在操作完成后触发;
     关键字"FOR EACH ROW"指定触发器每行触发一次.
      关键字"OF <列名>" 不写表示对整个表的所有列.
     WHEN (<条件>)表达式的值必须为"TRUE".

特殊变量:
     :new --为一个引用最新的列值;
     :old --为一个引用以前的列值;
这些变量只有在使用了关键字 "FOR EACH ROW"时才存在.且update语句两个都有,而insert只有:new ,delect 只有:old;

使用RAISE_APPLICATION_ERROR
     语法:RAISE_APPLICATION_ERROR(错误号(-20000到-20999),消息[,{true|false}]);
     抛出用户自定义错误.
     如果参数为'TRUE',则错误放在先前的堆栈上.

INSTEAD OF 触发器
     INSTEAD OF 触发器主要针对视图（VIEW)将触发的dml语句替换成为触发器中的执行语句，而不执行dml语句.


禁用某个触发器
     ALTER TRIGGER <触发器名> DISABLE
重新启用触发器
     ALTER TRIGGER <触发器名> ENABLE
禁用所有触发器
     ALTER TRIGGER <触发器名> DISABLE ALL TRIGGERS
启用所有触发器
     ALTER TRIGGER <触发器名> ENABLE ALL TRIGGERS
删除触发器
     DROP TRIGGER <触发器名>
```

#### 自定义对象

```SQL
自定义对象
创建对象:
    CREATE [OR REPLACE] TYPE <对象名> AS OBJECT(
    属性1 类型
    属性2 类型
          .
           .
    方法1的规范(MEMBER PROCEDURE <过程名>
    方法2的规范 (MEMBER FUNCTION <函数名> RETURN 类型)
          .
           .
    PRAGMA RESTRIC_REFERENCES(<方法名>,WNDS/RNDS/WNPS/RNPS);
      关键字"PRAGMA RESTRIC_REFERENCES"通知ORACLE函数按以下模式之一操作;
      WNDS-不能写入数据库状态;
      RNDS-不能读出数据库状态;
      WNPS-不能写入包状态;
      RNDS-不能读出包状态;


    创建对象主体:
      CREATE [OR REPLACE] TYPE body <对象名> AS
     方法1的规范(MEMBER PROCEDURE <过程名> is   <PL/SQL块>
    方法2的规范 (MEMBER FUNCTION <函数名> RETURN 类型 is <PL/SQL块>  
     END;

使用MAP方法和ORDER方法
     用于对自定义类型排序。每个类型只有一个MAP或ORDER方法。
     格式:MAP MEMBER FUNCTION <函数名> RETURN 类型
            ORDER MEMBER FUNCTION <函数名> RETURN NUMBER

创建对象表
      CREATE TABLE <表名> OF <对象类型>

示例:
     1. 创建name 类型
     create or replace type name_type as object(
          f_name varchar2(20),
          l_name varchar2(20),
          map member function name_map return varchar2);
    
     create or replace type body name_type as
          map member function name_map return varchar2 is --对f_name和l_name排序
          begin
               return f_name||l_name;
          end;
          end;
      2 创建address 类型
     create or replace type address_type as object
       ( city varchar2(20),
           street varchar2(20),
           zip number,
      order member function address_order(other address_type) return number);

      create or replace type body address_type as
      order member function address_order(other address_type) return number is --对zip排序
      begin
           return self.zip-other.zip;
      end;
      end;

3 创建stu对象
       create or replace type stu_type as object (
       stu_id number(5),
       stu_name name_type,
       stu_addr address_type,
       age number(3),
       birth date,
       map member function stu_map return number,
      member procedure update_age);

      create or replace type body stu_type as
       map member function stu_map return number is --对stu_id排序
       begin
             return stu_id;
       end;
      member procedure update_age is --求年龄用现在时间-birth
       begin
             update student set age=to_char(sysdate,'yyyy')-to_char(birth,'yyyy') where stu_id=self.stu_id;
       end;
       end;
4. 创建对象表
      create table student of stu_type(primary key(stu_id));
5.向对象表插值
      insert into student values(1,name_type('关','羽'),address_type('武汉','成都路',43000), null,sysdate-365*20);
6.使用对象的方法
     delcare
          aa stu_type;
     begin
          select value(s) into aa from student s where stu_id=1; --value()将对象表的每一行转成行对象括号中必须为表的别名
          aa.update_age();
     end;
7.select stu_id,s.stu_name.f_name,s.stu_name.l_name from student s; --查看类型的值
8.select ref(s) from student s ; --ref()求出行对象的OID,括号中必须为表的别名;deref()将oid变成行队像；
```

#### 其他

```SQL
其他
1.在PL/SQL中使用DDL
     将sql语句赋给一个varchar2变量,在用execute immediate 这个varchar2变量即可;
     示例：
     declare
          str varchar2(200);
     begin
          str:='create table test(id number,name varchar2(20))'; --创建表
          execute immediate str;   
          str:='insert into test values(3,''c'')'; --向表里插数据
          execute immediate str;
     end;    
     但是要队这个表插入数据也必须使用execute immediate 字符变量

2.判断表是否存在;
     示例：
     declare
          n tab.tname%type;
     begin
          select tname into n from tab where tname='&请输入表名';
          dbms_output.put_line('此表以存在');
     exception
          when no_data_found then
          dbms_output.put_line('还没有此表');
     end;


2.查看以有的过程;
     示例：
     select object_name,object_type,status from user_objects where object_type='PROCEDURE';
```

#### Oracle的数据类型

![1641448505640](Images/1641448505640.png)

#### 函数

```SQL
字符函数
名称
    描述
CONCAT(字符串1,字符串2)
将字符串1和字符串2连接成一个新的字符串
示例: select CONCAT(job,ename) from emp
LPAD(字段,总的大小,添充字符)
左填充即向右对齐
示例: select empno,lpad(sal,10,'*') from emp
RPAD(字段,总的大小,添充字符)
右填充即向左对齐
示例: select empno,rpad(sal,10) from emp
LOWER(字符串)
将字符串全部变成小写;
UPPER(字符串)
将字符串全部变成大写;
INITCAP(字符串)
将字符串变成第一个字母大写,其余都变成小写;
LENGTH(字符串)
求出字符串的长度;
SUBSTR(字符串,开始位置,长度)
从字符串中取子串;
示例: select substr(ename,2,3) from emp;--从ename的第2位开始取3位
INSTR(字符串,字符)
查看字符是否在字符串中存在;不存在返回0;存在则返回字符所在的的位置；如果有两个以上的字符则返回第一个的位置.
示例:select instr(ename,'S') from emp;
TRIM(字符 FROM 字符串)
去掉字符串首尾的字符;
示例: select trim('S' from ename) from emp;
TO_CHAR()
将不是其他类型转成字符类型；
对于日期型可以控制其格式:TO_CHAR(日期,'格式');
其中格式有: 'YYYY' --以4为显示年;
'YEAR' --以标准格式显示年； 'MM' ; 'MON' ; 'DD' ; 'DAY'; 'HH' ; 'MI' ;'SS'
REPLACE(字符串,字符串1,字符串2)
将字符串中的字符1替换成字符2;
示例: select replace(ename,'SC','SS') from emp;
TRANSLATE(字符串,字符串1,字符串2)
替换多的字符;
示例: select translate(ename,'SH','AB') from emp;
--表示将ename中的'S'换成'A','H'换成'B';
ASCII(char)
求字符的ascii码
NLSSORT(字符串)
对字符串排序.

数学函数

名称
    描述
ABS(数字)
一个数的绝对值
CEIL(数字)
向上取整;不论小数后的书为多少都要向前进位;
CEIL(123.01)=124;
CEIL(-123.99)=-123;
FLOOR(数字)
向下取整;不论小数后的书为多少都删除;|
floor(123.99)=123;
floor(-123.01)=-124;
MOD(被除数,除数)
取余数;
MOD(20,3)=2
ROUND(数字,从第几为开始取)
四舍五入;
ROUND(123.5,0)=124;
ROUND(-123.5,0)=-124;
ROUND(123.5,-2)=100;
ROUND(-123.5,-2)=-100;
SIGN(数字)
判断是正数还是负数;正数返回1，负数返回-1，0返回0;
SQRT(数字)
对数字开方；
POWER(m,n)
求m的n次方；
TRUNC(数字,从第几位开始)
切数字;
TRUNC(123.99,1)=123.9
TRUNC(-123.99,1)=-123.9
TRUNC(123.99,-1)=120
TRUNC(-123.99,-1)=-120
TRUNC(123.99)=123
GREATEST(数字列表)
找出数字列表中最大的数;
示例:
select greatest(100,200,-100) from dual; --结果为200
LEAST(数字列表)
找出数字列表中最小的数;
SIN(n)
求n的正旋
COS(n)
求n的余旋
TAN(n)
求n的正切
ACos(n)
求n的反正切
ATAN(n)
求n的反正切
exp(n)
求n的指数
LN(n) 
求n的自然对数,n必须大于0
LOG(m,n)
求n以m为底的对数,m和n为正数,且m不能为0

日期函数

名称
    描述
ADD_MONTHS(日期,数字)
在以有的日期上加一定的月份;
示例:
select add_months(hiredate,20),hiredate from emp;
LAST_DAY(日期)
求出该日期的最后一天.
MONTHS_BETWEEN(日期1，日期2)
求出两个月之间的天树（注意返回的天数为小数);
示例:
select months_between(sysdate,hiredate) from emp;
NEW_TIME(时间,时区,'gmt')
按照时区设定时间.
NEXT_DAY(d,char)
返回d指定的日期之后并满足char指定条件的第一个日期

其他函数

名称
    描述
VSIZE(类型)
求出数据类型的大小;
NVL(字符串,替换字符)
如果字符串为空则替换，否则不替换
```

#### 常用命令

```SQL

命令
    描述
DESC 表名
查看表的信息.
SET SERVEROUT [ON|OFF]
设置系统输出的状态.
SET PAGESIZE <大小>
设置浏览中没页的大小
SET LINESIZE <大小>
设置浏览中每行的长度
SET AUTOPRINT [ON|OFF]
设置是否自动打印全局变量的值
SELECT SYSDATE FROM DUAL
查看当前系统时间
ALTER SESSION SET nls_date_format='格式'
设置当前会话的日期格式
示例:ALTER SESSION SET nls_date_format='dd-mon-yy hh24:mi:ss'
SELECT * FROM TAB
查看当前用户下的所有表
SHOW USER
显示当前用户
HELP TOPIC
显示有那些命令
SAVE <file_name>
将buf中的内容保存成一个文件
RUN <file_name>
执行已经保存的文件;也可以写成@<file_name>
GET <file_name>
显示文件中的内容
LIST
显示buf中的内容
ED
用记事本打开buf,可以进行修改
DEL 行数
删除buf中的单行
DEL 开始行 结束行
删除buf中的多行
INPUT 字符串
向buf中插入一行
APPEND 字符串
将字符串追加到当前行
C/以前的字符串/替换的字符串
修改buf中当前行的内容
CONNECT
连接
DISCONNECT
断开连接
QUIT
退出sql*plus
EXP
导出数据库（可以在DOS键入exp help=y 可以看到详细说明)
示例: exp scott/tiger full=y file=e:\a.dmp; --导出scott下的所有东西
        exp scott/tiger tables=(emp,dept) file=e:\emp.dmp --导出scott下的                                                                                             emp,dept表
IMP
导入数据库（可以在DOS键入imp help=y 可以看到详细说明)
imp scott/tiger tables=(emp,dept) file=e:\emp.dmp

可以通过help <命令>获得命令的帮助
```

#### 异常类型

```SQL
异常
    描述
CURSOR_ALREADY_OPEN
试图"OPEN"一个已经打开的游标
DUP_VAL_ON_INDEX
试图向有"UNIQUE"中插入重复的值
INVALID_CURSOR
试图对以关闭的游标进行操作
INVALID_NUMBER
在SQL语句中将字符转换成数字失败
LOGIN_DENIED
使用无效用户登陆
NO_DATA_FOUND
没有找到数据时
NOT_LOGIN_ON
没有登陆Oracle就发出命令时
PROGRAM_ERROR
PL/SQL存在诸如某个函数没有"RETURN"语句等内部问题
STORAGE_ERROR
PL/SQL耗尽内存或内存严重不足
TIMEOUT_ON_RESOURCE
Oracle等待资源期间发生超时
TOO_MANY_ROWS
"SELECT INTO"返回多行时
VALUE_ERROR当出现赋值错误
ZERO_DIVIDE
除数为零
```