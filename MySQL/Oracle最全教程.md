# Oracle最全基础教程

## 用户与权限

### 创建用户

```SQL
CREATE USER USER_NAME IDENTIFIED BY PASSWD; --创建用户
```

### 修改密码

```SQL
ALTER USER USER_NAME IDENTIFIED BY NEW_PASSWD; --修改新密码

--修改用户密码
PASSWD USER_NAME;
```

### 删除用户

```SQL
--可选参数 CASCADE
DROP USER USER_NAME [CASCADE];


--注意：
/*
在进行删除用户操作时，如果此用户已创建表，删除时需要加参数“CASCADE”，它具有级联的作用
*/
```

### 给用户赋权限

```SQL
GRANT 权限/角色 TO USER_NAME;
```

### 收回用户权限

```SQL
REVOKE 权限/角色 FROM USER_NAME;
```

### 系统权限

```SQL
-- “系统权限是数据库管理相关的权限”
CREATE SESSION							--登录权限
CREATE TABLE							--建表权限
CREATE INDEX							--创建索引权限
CREATE VIEW								--创建视图权限
CREATE SEQUENCE							--创建序列权限
CREATE TRRIGER							--创建触发器权限
```

### 连接角色

```SQL
--“是授予用户的最基本的权利，能够连接到Oracle数据中，能够访问其他用户的表权限时”
CREATE SESSION		--创建会话
CREATE VIEW			--创建视图
CREATE SEQUENCE		--创建序列
```

### 资源角色

```SQL
--“具有创建表、序列、视图的权限”
CREATE TABLE		--创建表
CREATE TRIGGER		--创建触发器
CREATE PROCEDURE	--创建过程
CREATE SEQUENCE		--创建序列
CREATE TYPE			--创建类型
```

### DBA角色

```SQL
--“是授予系统管理员的，拥有该角色的用户即系统管理员，拥有系统的所有权限”
```

## 表空间

```SQL
--创建表空间
CREATE TABLESPACE SPACE_NAME

--DATAFILE '/' 指向数据文件路径
--SIZE N(M) 表示初始化表空间为N(M)
--AUTOEXTEND ON NEXT 2M 自动扩展，每次扩展2M
--MAXSIZE UNLIMITED UNLIMITED最大扩展没有限制，N(M)最大扩展到N(M)
```

### 创建用户指定默认表空间

```SQL
CREATE USER USER_NAME IDENTIFIED BY PASSWD DEFAULT TABLESPACE SPACE_NAME
```

### 修改用户默认表空间

```SQL
ALTER USER USER_NAME IDENTIDIED BY PASSWD DEFAULT TABLESPACE SPACE_NAME
```

### 查看表表空间

```SQL
SELECT * FROM v$TABLESPACE
```

### 查看用户默认表空间

```SQL
SELECT USERNAME, DEFAULT_TABLESPACE FROM DBA_USERS WHERE USERNAME = 'SCOTT';
--用户名SCOTT必须为大写
```

## 表结构操作

```SQL
--创建表1
CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE
);

--创建表2
CREATE TABLE TABLE_NAME AS SELECT COLUMN_1, COLUMN_2 ...FROM TABLE_NAME;

--修改表
ALTER TABLE 语句添加、修改或删除列的语法

--添加列
ALTER TABLE TABLE_NAME ADD(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE
);

ALTER TABLE TABLE_NAME ADD COLUMN_1 DATA_TYPE;

--修改列
ALTER TABLE TABLE_NAME MODIFY(
	COLUMN_1 DATA_TYPE
);

--删除列
ALTER TABLE TABLE_NAME DROP(
	COLUMN_1,
    COLUMN_2
);

--修改表名称
RENAME TABLE TO NEW_TABLE_NAME

--修改列名
ALTER TABLE TABLE_NAME RENAME COLUMN OLD_COLUMN TO NEW COLUMN;

--查看表结构
DESC 表名;
```



## 约束

### 约束

- 非空约束(NOT NULL)
- 唯一约束(UNIQUE)
- 主键约束(PRIMARY KEY)
- 外键约束(FOREIGN KEY)
- 条件约束(CHECK)
- 约束存在表中(USER_CONSTRAINTS)

### 非空约束(NOT NULL)

```SQL
--添加非空
CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE NOT NULL
);

ALTER TABLE TABLE_NAME MODIFY COLUMN_NAME NOT NULL;

--删除非空约束
ALTER TABLE TABLE_NAME MODIFY COLUMN_NAME NULL;
```

### 唯一约束(UNIQUE)

```SQL
--添加唯一
CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE UNIQUE
);

--修改唯一
ALTER TABLE TABLE_NAME ADDCONSTRAINT sUNIQUE_NAME UNIQUE (COLUMN_1, COLUMN_2);

--删除唯一
ALTER TABLE TABLE_NAME DROP CONSTRINT UNIQUE_NAME;
--备注：Oracle中，UNIQUE可以为单个NULL，也可多行为NULL
```

### 主键约束(PRIMARY KEY)

```SQL
--添加主键
CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE PRIMARY KEY
);

CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE,
    CONSTRAINT 约束名 PRIMARY KEY (COLUMN_1, COLUMN_2)
);

--修改主键
ALTER TABLE TABLE ADD CONSTRAINT 约束名 PRIMARY KEY (COLUMN_1, COLUMN_2);

--删除主键
ALTER TABLE TABLE_NAME DROP PRIMARY KEY CASCADE;
--备注：如果两表存在主从关系，删除主键约束时，需要加上CASCADE

/*
注意：每张表有且只有一个主键约束。
特别说明：
	PRIMARY KEY 与 UNIQUE 的区别：
	1、一张表可以对应多个UNIQUE（唯一约束）
	2、一张表只要存在一个主键
	3、设置为主键的列不能存在NULL值
*/
```

### 外键约束(FOREIGN KEY)

外键约束的作用：用来维护从表与主表之间的引用完整性，能够维护数据库的数据一致性，数据完整性，防止错误数据进库。

解释：用于定义主表和欧辰那个表之间的关系，外键约束要定义在从表上，主表则必须具有主键约束或UNIQUE约束，当i当以外键约束后，要求外键列数据必须在主表的主键列存在或为NULL。

```SQL
--添加主键
CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE REFERENCES MAIN_TABLEE_NAME(COLUMN)
);

CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE,
    CONSTRAINT 约束名 FOREIGN KEY(COLUMN) REFERENCES, MAIN_TABLE_NAME(COLUMN))
);

--修改主键
ALTER TABLE TABLE_NAME CONSTRAINT 约束名 FOREIGN KEY(COLUMN) REFERENCES MAIN_TABLE_NAME(COLUMN);

--删除主键
ALTER TABLE TABLE_NAME DROP CONSTRAINT 约束名称；
/*
特别说明：FOREIGN KEY外键细节
	1、外键指向主键列
	2、外键可指向UNIQUE列
	3、建表时先建主表，再建立从表，删除时，先删除从表，再删除主表
	4、外键列属性值要与主键或UNIQUE列属性值的类型保持一致
	5、外键列的值，必须再主键列中存在，但外键列的值运行为NULL
*/
```

### 条件约束(CHECK)

```SQL
--添加条件
CREATE TABLE TABLE_NAME(
	COLUMN_1 DATA_TYPE,
    COLUMN_2 DATA_TYPE CHECK (COLUMN_2 IN (VALUE1, VALUE2...))
);

--修改条件
ALTER TABLE TABLE_NAME ADD CONSTRAINT 约束名 CHECK(COLUMN IN (VALUE1, VALUE2...))

--删除条件
ALTER TABLE TABLE_NAME DROP CONSTRAINT 约束名称;
```

#### 约束命名规则

- 非空约束：NN_表名__列名
- 唯一约束：UK_表名__列名
- 主键约束：PK_表名
- 外键约束：FK_表名__列名
- 条件约束：CK_表名__列名

#### 查看约束信息

```SQL
SELECT * FROM USER_CONSTRAINT WHERE TABLE_NAME = "TABLE_NAMWE";
```

## 数据操作

### 插入数据

```SQL
INSERT INTO TABLE_NAME[(COLUMN [, COLUMN 2...])] VALUE(VALUE [, VALUE 2...]);
```

### 插入全部数据

```SQL
INSERT INTO TABLE_NAME VALUES(VALUE[, VALUE 2...]);
```

### 从另一张表中导入数据

```SQL
INSERT INTO TABLE_NAME1 (SELECT VALUE1, VALUE2, VALUE3,....FROM TABLE_NAME2);
```

### 修改数据

```SQL
UPDATE TABLE_NAME SET COLUMN_NAME = EXP(表达式) [, COLUMN 2 = EXP 2,....][WHERE 条件];
```

### 删除数据

```SQL
DELETE FROM TABLE_NAME [WHERE 条件表达式];

--删除的几种方式
DELETE FROM TABLE_NAME;

--删除所有记录，表结构还在，写日志，可以恢复，但速度较慢
DROP TABLE TABLE_NAME

--删除表的结构和数据
TRUNCATE TABLE TABLE_NAME;
--删除表中的所有记录，表接哦古还在，不屑日志，无法找回删除记录，速度块
```

## 查询数据

### 基本语法

```SQL
SELECT
	[DISTINCT] *|{COLUMN1(), COLUMN2()}
FROM TABLE_NAME AS AS_NAME
	[WHERE {条件}];
	
/*
“解释”
	1、SELECT 指向列进行查询
	2、COLUMN 指定列名
	3、* 代表查询所有数据
	4、FROM 指定查询表源
	5、DISTINCT 是否进行数据去重
	6、WHERE 条件
	7、AS 别名	
*/

--使用列别名
SELECT
	ENAME AS "姓名",
	SAL * 12 + NVL(COMM, 0) * 13 AS "年收入"
FROM 
	EMP;
/*
解释：
	Oracle在使用别名时，可以使用双引号或不使用， 或使用 AS 来表明别名，但是不能使用单引号。
*/
```

### 处理NULL值

NVL函数：用于处理NULL值使用

```SQL
SELECT ENAME, SAL * 13(COMM, 0) * 13 FROM EMP;
--NVL(VALUE1, VALUE2)
--解释：NVL值VALUE1为NULL时则取值VALUE2，VALUE1部位NULL时则取值VALUE1原值
```

### 拼接字符串

在进行查询时，希望将多列内容结果作为一列内容结果进行返回时。可使用 ” || “进行连接。

```SQL
SELECT ENAME || "年收入" || SAL * 13 + NVL(COMM, 0) * 13 "雇员的年收入" FROM EMP;
```

### 取范围内的值

在进行查询时，想获取一个范围内的数据时，可使用BETWEEN

```SQL
SELECT * FROM EMP WHERE SAL BETWEEN 2000 AND 2500;
--BETWEEN  AND 指定区间内取值
```

### LIKE操作符

%：表示任意0到多个字符

_：表示任意单个字符

```SQL
--如何显示首字符为S的员工姓名和工资
SELECT ENAME, SAL FROM EMP WHERE ENAME LIKE 'S%'；

--如何显示第三个字符为大写O的所有员工的姓名和工资
SELECT ENAME, SAL FROM EMP WHERE ENAME LIKE 'O%';
```

### 区间判断

在WHERE语句中使用IN

```SQL
SELECT * FROM EMP WHERE EMPNO IN (123, 345, 800);
--注意：IN只能放1000个值
```

### 操作符(IS NULL)

在查询语句中不能使用=或者!= NULL来进行判空

```SQL
SELECT * FROM EMP WHERE MAGE IS NULL;

SELECT * FROM EMP WHERE MAGE IS NOT NULL;
```

### 逻辑操作符

```SQL
--查询薪资高于100或职位为CODE的人员，同时还要满足姓名首字母大写J的
SELECT * FROM EMP WHERE (SAL > 100 OR JOB = 'CODE') AND (ENAME LIKE 'J%');
```

### 排序

使用ORDER BY进行排序（ASC写或不屑都是升序排序即从小到大，DESC则是降序排序从大到小排序）

````SQL
SELECT * FROM EMP ORDER BY SAL SAC;

--使用别名排序
SELECT ENAME, SAL * 12 "年薪" FROM EMP ORDER BY "年薪" ASC;
--备注：别名使用需要用 "" 
````

## 分组查询

在进行复杂的数据统计时，往往需要使用分组函数，如：MAX(), MIN(), AVG(), SUM(), COUNT()等

### MAX(), MIN()

取最大值和取最小值

```SQL
--如何显示所有员工最高工资和最低工资
SELECT MAX(SAL) "最高工资", MIN(SAL) "最低工资" FORM EMP;

--查询最高年工资
SELECT MAX(SAL * 13 + NVL(COMM, 0) * 13) "最高年工资", MIN(SAL * 13 + NVL(COMM, 0) * 13) "最低年工资" FROM EMP;
```

### AVG()

求平均值

```SQL
--显示平均工资和工资总和
SELECT AVG(SAL) "平均工资", SUM(SAL) "工资总和" FROM EMP;
--备注：AVG(SAL)不会把SAL为NULL的行进行统计，如果为空值也需要考虑，则可以
SELECT SUM(SAL) COUNT(*) FROM EMP;
```

### COUNT(*)

计算总数

```SQL
SELECT COUNT(*) "共有员工" FROM EMP;
```

### GROUP BY

对查询结果进行分组统计

HAVING：限制(过滤)分组显示结果

```SQL
--显示每个部门的平均工资和最高工资
SELECT AVG(SAL) "平均工资", MAX(SAL) "最高工资", DEMPNO "部门编号" FROM EMP GROUP BY DEPTNO;

/*
分组函数总结：
	1、分组函数(AVG)只能出现在选中列表、HAVING、ORDER BY子句中
	2、如果在SELECT 语句中同时包含GROUP BY/ HAVING/ ORDER BY，其顺序为GROUP BY/ HAVING/ ORDER BY
	3、在选择列中如果有列、表达式和分组函数，那么这些列和表达式必须有一个出现在GROUP BY子句中，否则会报错
*/
```

## 函数

### ASCII()

返回与指定的字符对应的十进制

```SQL
SELECT ASCII('A') A, ASCII('a') a, ASCII('0') ZERO, ASCII(' ') SPACE FROM DUAL;
```

### CHR()

给出整数，返回对应的字符

```SQL
SELECT CHR(54740) ZHAO, CHR(65) CHR65 FROM DUAL;
```

### CONCAT()

连接连个字符串，与 || 作用相同

```SQL
SELECT CONCAT('HELLO', 'WORLD') FROM DUAL;
```

### INITCAP()

返回字符串并将字符串的第一个字母变成大写

```SQL
SELECT INITCAP('SMITH') UPP FROM DUAL;
```

### INSTR(C1, C2, J)

在一个字符中搜索指定的字符，返回发现指定的字符位置

```SQL
/*
C1		被搜索的字符串
C2		希望被搜索的字符串
L		搜索的开始位置，默认为1
J		第J次出现的位置，默认为1
*/
SELECT INSTR('ORACLE TRAING', 'RA', 1, 2) INSTRING FROM DUAL;
```

### LENGTH()

返回字符串的长度

```SQL
SELECT ENAME, LENGTH(ENAME) FROM EMP;
```

### LOWER()

返回字符串，并将所有的字符小写

```SQL
SELECT LOWER('AaBbCc') "LOWER" FROM DUAL;
```

### UPPER()

返回字符串，并将所有的字符大写

```SQL
SELECT UPPER('AaBbCc') "UPPER" FROM DUAL;
```

### 粘贴字符

RAPD在列的右边粘贴字符， RAPD(“显示内容”或字段， 显示长度， “填充占位符”)

LAPD在列的右边粘贴字符， LAPD(“显示内容”或字段， 显示长度， “填充占位符”)

```SQL
SELECT LAPD(RAPD('MNB', 10, "*"), 17, "=") FROM DUAL;
```

### 删除字符

ltrim 删除左边出现的字符串 ltrim('原内容'或字段,'要删除的字符串')

rtrim 删除右边出现的字符串 rtrim('原内容'或字段,'要删除的字符串')

```SQL
SELECT RTRIM('**NBA CODE**', '*') FROM DUAL;
```

### 截取字符串

SUBSTR截取子字符串，从STRAT开始，取COUNT个

```SQL
SELECT SUBSTR('1110000000', 3, 8) FROM DUAL;
```

### 替换字符串

REPLACE('STRING', 'S1', 'S2')

```SQL
/*
STRING		希望被替换的字符或常量
S1			被替换的字符串
S2			要替换的字符串
*/
SELECT REPLACE('i L C', 'i', 'I') FROM DUAL;
```

### TRIM

TRIM('S' FROM 'STRING')

如果不指定参数，默认为空格符

```SQL
SELECT TRIM(0 FROM 0009) "TRIM EXAMPLE" FROM DUAL;
```

## 数学函数

### CEIL()

向上取整：返回大于或等于给出数字的最小整数

```SQL
SELECT CEIL(3.14159) FROM DUAL
```

### FLOOR()

向下取整：对给定的数字取整数

```SQL
SELECT FLOOR(2345.67) FROM DUAL;
```

### TRUNC()

精度截取：按照指定的精度截取一个数

```SQL
SELECT TRUNC(124,1666, -2), TRUNC(124,16666, 2) FROM DUAL;
```

### ROUND()

按照指定的精度进行舍入

ROUND函数为四舍五入

TRUNC函数直接截取

```SQL
SELECT ROUND(55.5), ROUND(-55.4), TRUNC(-55.5), TRUNC(55.5) FROM DUAL;
```

### ABS()

返回指定值的绝对值

```SQL
SELECT ABS(-100) FROM DUAL;
```

### ACOS()

返回反余弦的值

```SQL
SELECT ACOS(-1) FROM DUAL;
```

### ASIN()

返回正余弦的值

```SQL
SELECT ASIN(0.5) FROM DUAL;
```

### ATAN()

返回反正切的值

```SQL
SELECT ATAN(1) FROM DUAL;
```

### COS()

返回余弦值

```SQL
SELECT COS(-3.14159265) FROM DUAL;
```

### MOD()

返回一个N1除以N2的余数（取模）

```SQL
SELECT MOD(10, 3), MOD(3,3) FROM DUAL;
```

## 日期函数

日期函数用于处理DATE类型的数据

### ADD_MONTHS(日期值， 增加(减少))

减去或减去月份

```SQL
SELECT  TO_CHAR(LAST_DAY(SYSDATE), 'YYYY-MM-DD') FROM DUAL;
```

### MONTHS_BETWEEN(DATE2, DATE1)

给出DATE2-DATE1的月份，计算总的月份数

```SQL
SELECT MONTHS_BETWEEN('1999-12-01', '2000-02-19') MON_BET FROM DUAL;
```

### SYSDATE

系统的当前时间

```SQL
SELECT TO_CHAR(SYSDATE, 'DAY') FROM DUAL;
```

## 日期转换函数

### TO_CHAR(DATE, 'FORMAT')

日期类型转换成字符串格(主要用于将日期以习惯的格式输出显示)

```SQL
SELECT TO_CHAR(SYSDATE, 'YYYY/MM/DD HH24:MI:SS') FROM DUAL;
/*
TO_CHAR()
解释说明：
	1、YY：两位数字的年份 2004 --04
	2、YYYY：四位数字的年份 2004年
	3、MM：两位数字的月份 8月 --08
	4、DD：两位数字的天数 30日 --30
	5、HH24：二十四小时制 8点 --20
	6、HH12：十二小时制 8点 --08 MI:SS --显示分钟/秒
	7、DAY：显示星期几
	8、MONTH：显示月份
	9、YEAR：显示年
数字格式：
	1、9：显示数字，并忽略前面的0
	2、0：显示数字，如位数不足，则用0补齐
	3、.:在指定的位置显示小数点
	4、,:在指定的位置显示逗号
	5、$:在数字前面加美元符号
	6、L:在数字前面加本地货币符号
	7、C:在数字前面加国际货币符号
	8、G:在指定位置显示组分隔符
	9、D:在指定位置显示小数点符号(.)
	
说明:
,逗号.和小数点可以合在一起使用，G 分隔符和 D 小数点符可以合在一起使用，但,.不能和 GD, 综合使用，否则报错。
*/
```

### TO_DATE(STRING, 'FORMAT')

将字符串转换成日期(主要用于将日期按习惯的格式输入到数据库中)

### TO_NUMBER

将给出的数字类型的字符串转换为数字

## 系统函数

### DECODE()

类似与JAVA中的SWITCH CASE分支语句

```SQL
DECODE(
	VALUE, IF1, THEN1, IF2, THEN2, IF3, THEN3, ... ELSE
)

--若VALUE为0，则为1，否则为2
DECODE(VALUE, '0', '1', '2')
```

## 表连接

### 自连接

指在同一种表的来凝结查询(把一张表看两张表)

```SQL
--显示职员上级领导的姓名
SELECT E2.ENAME FROM EMP E1, EMP E2 WHERE E1.MAGE = E2.EMPNO;
```

### 内连接(INNER JOIN ON)

基本语法：

```SQL
SELECT COLUMN_NAME1, ... FROM TABLE_NAME INNER JOIN TABLE_NAME ON CONDITION;
--说明：内连接只要两张表同时满足条件曹辉被查询到

--显示职员的信息和部门名称
SELECT E.*, D.DNAME FROM EMP E INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO
```

### 左外连接(LEFT JOIN ON)

如果查询出左表完全显示，称为左外连接

基本语法：

```SQL
SELECT COLUMN_NAME_1, COLUMN_NAME_2,...FROM TABLE_NAME_1 LEFT JOIN TABLR_NAME_2 ON CONDITION;

SELECT COLUMN_NAME_1, COLUMN_NAME_2,...FROM TABLE_NAME_1, TABLE_NAME_2 WHERE CONDITON_1 = CONDITION_2(+);
```

### 右外连接

如果查询的表右侧完全显示，称为右外连接

基本语法：

```SQL
SELECT COLUMN_NAME_1, COLUMN_NAME_2, ...FROM TABLE_NAME_1 RIGHT JOIN TABLE_NAME_2 ON CONDITION;

SELECT COLUMN_NAME_1, COLUMN_NAME_2 TABLR_NAME_1, TABLE_NAME_2 WHERE CONDITION_1(+) = CONDITION_2;
```

### 完全外连(FULL OUTER JOIN ON)

完全显示两张表，没有匹配的记录记录为空

基本语法：

```SQL
SELECT COLUMN_NAME_1, COLUMN_NAME_2, ... FROM TABLE_NAME_1 FULL OUTER JOIN TABLE_NAME_2 ON CONDITION;
```

## 分页查询

```SQL
SELECT T2.*  FROM (SELECT T1.*, ROWNUM RN FROM (SELECT *  FROM TABLE_NAME) t1

WHERE RN<=大范围(取到多少条数据)) T2 WHERE RN>=小范围(从第几条数据开始取);

/*
说明：Oracle分页查询时通过三层筛选进行查询的。每一次都可以带WHERE条件来对目标数据进行筛选。
1、第一层：构建所需查询字段信息并排序
2、第二层：构建ROWNUM， 别名为RN
3、第三层：加WHERE条件， RN >= M AND M <= N
*/
```

## 视图

创建视图基本语法：

```SQL
CREATE VIEW VIEW_NAME AS SELECT 语句 [WITH READ ONLY]
--说明：WITH READ ONLY表示只进行查询操作
```

创建或修改视图的基本语法：

```SQL
CREATE OR REPLACE VIEW VIEW_NAME AS SELECT 语句 [WITH READ ONLY]
--说明：WITH READ ONLY表示只进行查询操作
```

删除视图的基本语法：

```SQL
DROP VIEW VIEW_NAME
```

## 创建序列

基本语法：

```SQL
-----------------------------------------
------创建序列
-----------------------------------------
CREATE SEQUENCE CREATE_SEQUENCE_NAME_ROW_NUM_AUTOINC --序列名称
INCREMENT BY 1 --每次增长多少
START WITH 1 --从几开始
MINVALUE 1 --最小值
NOMAXVALUE --无最大值
NO CYCLE --序列到达最大值之后怎么办，CYCLE
CACHE 10 --需要不需要使用缓
```

### 创建触发器

基本语法：

```SQL
-----------------------------------------
------创建触发器
-----------------------------------------
CREATE OR REPLACE TRIGGER insert_CREATE_TRIGGER_NAME_ROW_NUM_AUTOINC
BEFORE INSERT ON CREATE_TRIGGER_NAME
FOR EACH ROW
BEGIN
SELECT CREATE_TRIGGER_NAME_ROW_NUM_autoinc.NEXTVAL INTO :NEW.ROW_NUM FROM DUAL;
END;
```

