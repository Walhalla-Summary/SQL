### Oracle面试题

1. 数据库的几种物理文件？
   1）数据文件 

   2）控制文件 

   3）日志文件  

2. 控制文件都含有哪些信息？
   包含维护和验证有选举权据库完整性的必要信息、例如，控制文件用于识别数据文件和重做日志文件，一个有选举权据库至少需要一个控制文件

3. decode函数的用法？
   decode的语法：decode(value,if1,then1,if2,then2,if3,then3,...,else)，表示如果value等于if1时，decode函数的结果返回then1,...,如果不等于任何一个if值，则返回else。初看一下，decode 只能做等于测试，但刚才也看到了，我们通过一些函数或计算替代value，是可以使decode函数具备大于、小于或等于功能。

4. 如何用decode进行大于小于的比较？
   利用sign()函数和decode和在一起用

5. case语句的用法？
   oracle用法很简单：
   select last_name, job_id, salary
   case job_id
        when 'it_prog'then 1.10*salary
        when 'st_clerk'then 1.15*salary
        when 'sa_rep' then1.20*salary
   else salary end "revised_salary"
   from employees

6. truncate和delete的区别？

   1、truncate在各种表上无论是大的还是小的都非常快。如果有rollback命令delete将被撤销，而truncate则不会被撤销。

   2、truncate是一个ddl语言，向其他所有的ddl语言一样，他将被隐式提交，不能对truncate使用rollback命令。

   3、truncate将重新设置高水平线和所有的索引。在对整个表和索引进行完全浏览时，经过truncate操作后的表比delete操作后的表要快得多。

   4、truncate不能触发任何delete触发器。

   5、不能授予任何人清空他人的表的权限。

   6、当表被清空后表和表的索引讲重新设置成初始大小，而delete则不能。

   7、不能清空父表。

7. 表空间如何扩展？并用语句写出？
   两种扩展方式：
   1）        增加数据文件
   2）        扩展数据文件大小

8. 表空间区管理方式？哪种方式现在是推荐使用的？
   1）        数据字典管理方式
   2）        本地文件管理方式

9. 用什么函数获得日期？和日期中的月，日，年
   to_char(sysdate,'day') 返回星期几
   trunc('25-may-95 ','month')            

   trunc('25-may-95 ','year')

10. 分区表的应用？
    1）        一个分区表有一个或多个分区，每个分区通过使用范围分区、散列分区、或组合分区分区的行
    2）        分区表中的每一个分区为一个段，可各自位于不同的表空间中
    3）        对于同时能够使用几个进程进行查询或操作的大型表分区非常有用

11. 谈谈索引的用法及原理？
       索引是若干数据行的关键字的列表，查询数据时，通过索引中的关键字可以快速定位到要访问的记录所在的数据块，从而大大减少读取数据块的i/o次数，因此可以显著提高性能。

12. 存储过程的应用，如何既有输入又有输出？
    利用in out参数

13. 常发生的异常有哪些？
    no data found     too many rows

14. 如何使用异常？
    在oracle中有三种类型的异常。预定义的异常非预定义的异常 用户定义的异常 第二种非预定义的异常是与特定的oracle错误关联。并且用pragmexception_init(exception_name,error_number)关联一起的。但是到底有什么用啊？例如：declare dup_primary_key exception; pragmaexception_init(dup_primary_key,-1); begin insert into itemfilevalues('i201','washer','spares',100,50,250,12,30); exception whendup_primary_key then dbms_output.put_line('重复项编号-主键冲突');

 

   ORACLE 面试问题-技术篇 (2)

21.如何判断数据库的时区？

解答：SELECT DBTIMEZONE FROM DUAL;

22.解释GLOBAL_NAMES 设为TRUE的用途

解答：GLOBAL_NAMES指明联接数据库的方式。如果这个参数设置为TRUE,
   在建立数据库链接时就必须用相同的名字连接远程数据库。

23.如何加密PL/SQL程序？

解答：WRAp

24.解释FUNCTION,PROCEDURE和PACKAGE区别

解答：function和procedure是PL/SQL代码的集合，通常为了完成一个任务。

procedure不需要返回任何值而function将返回一个值在另一方面，Package

是为了完成一个商业功能的一组function和procedure得集合

25.解释TABLE Function的用途

解答：TABLE Function 是通过PL/SQL逻辑返回一组记录，用于普通的表/视

图。他们也用于pipeline 和ETL过程。

26.举出三中可以收集three advisorystatistics

解答：Buffer Cache Advice,Segment Level Statistics,TimedStatistics

27.Audit trace存放在哪个oracle目录结构中？

解答：unix $ORACLE_HOME/rdbms/audit
       Windows the event viewer

28.解释materialized view 的作用

解答：Materialized view 用于减少那些汇总，集合和分组的信息的几何

数量。它们统称适合于数据仓库和DSS系统。

29.当用户进程出错，哪个后台进程负责清理它

解答：PMON

30.哪个后台进程刷新materialized view?
解答：The Job Queue Processes

31.如何判断哪个session正在连接以及他们等待的资源？
解答: V$SESSION /V$SESSION_WAIT

32.描述什么是redo logs
解答：Redo Logs是用于存放数据库数据改动状况的物理和逻辑结构。可以用

来修复数据库。

33.如何进行强制LOG SWITCH?
解答：ALTER SYSTEM SWITCH LOGFILE;

34.举出两个判断DDL改动的方法？

解答：你可以使用Logminer或Streams

35.Coalescing做了什么？
解答：Coalescing针对于字典管理的tablespace进行碎片整理，将临近的小

extents合并成单个的大extent。

36.TEMPORARY tablespace和PERMANENTtablespace的区别是？
解答：A temporary tablespace 用于临时对象列如排序结构而

permanenttablespaces用来存储那些真实的对象（例如表，回滚段等）

37.创建数据库时自动建立的tablespace名称？
解答：SYSTEM tablespace.

38创建用户时，需要赋予新用户什么权限才能使它联上数据库。
解答：CONNECT

39.如何在tablespace里增加数据文件？
解答：ALTER TABLESPACE<tablespace_name>ADD

DATAFILE<datafile_name>SIZE<size>

40.如何变动数据文件的大小？
解答：ALTER DATABASEDATAFILE<datafile_name>RESIZE<new_size>;

41.哪个VIEW用来检查数据文件的大小？
解答：DBA_DATA_FILES

42.哪个VIEW用来判断tablespace的剩余空间？
解答：DBA_FREE_SPACE

43.如何判断谁往表里增加了一条记录？
解答：auditing

44.如何重构索引？
解答：ALTER INDEX<index_name>REBULID;

45.解释什么是Partitioning(分区)以及它的优点。
解答：Partition将大表和索引分割成更小，易于管理的分区。

46，你刚刚编译了一个PL/SQL Package 但是有错误报道，如何显示出错信息

？
解答：SHOW ERRORS

47.如何搜集表的各种状态数据？
解答：ANALYZE
    The ANALYZE command

48.如何启动SESSION 级别的TRACE
解答：DBMS_SESSION.SET_SQL_TRACE
      ALTER SESSION SET SQL_TRACE=TRUE;

50.用于网络连接的2个文件？
解答：TNSNAMES.ORA and SQLNET.ORA


51.数据库切换日志的时候，为什么一定要发生检查点？这个检查点有什么意

义？
解答：(checkpoint queue是dirtybuffer按时间顺序排列的列表,用来表识

DBWR写过的block.)

当发生log switch时候,CKPT 会写redo log中checkpoint position到

datafile header,
这个checkpoint postion对应着checkpointqueue中的checkpoint

position,对应相应的RBA.
DBWn会根据checkpoint queue中的checkpointposition来识别已经写到

datafile的blocks.
识别以后,DBWn会从checkpoint queue移除这些checkpoint position.

如果在log switch发生的时候,没有checkpoint发生,那么等这些日志被覆盖,

那么这些checkpoint position也就相应丢失了,DBWn又知道从哪写起呢

52。表空间的管理方式有哪几种，各有什么优劣？
解答： DBA 面试题之---表空间管理方式有哪几种，各有什么优劣。收藏
表空间管理方式有以下两种：

第一、字典管理表空间

    将Oracle的区管理信息存放在表空间的字典中进行管理，所有区的分配

与释放，都会使字典的记录的增减变动。也就是在字典的记录中会执行更新

、插入、删除操作，在执行上述操作时，都会生成重做日志，对字典的管理

，将影响正常操作的效率，并且在区分配、回收的过程中，产生磁盘碎片，

如果磁盘碎片增加到一定的程度，会浪费空间，严重影响效率,同时，Oracle

在管理表空间的管理中，会产生递归SQL。

    如果要用字典的方式管理表空间，可以在创建表空间时，使用： EXTENT

MANAGEMENT DICTIONARY 选项。

第二、本地管理表空间

    本地管理是以位图的方式，将区的分配信息保存在数据文件本身，所有

区的分配等操作都只是位图的运算，位图中的每一位对应数据文件中的一个

区或几个连续的区，这样在进行区管理时，生成的重做日志将非常少，并且

运行的效率很高。并且产生磁盘碎片很少。

如果要用本地管理表空间，可以在创建表空间时，使用： EXTENT

MANAGEMENT LOCAL 选项。

    在表空间的管理中，Oracle8I中可以采用字典管理，也可以采用本地管

理，如果不指定，将采用字典管理方式。

      在Oracle9I中，推荐采用本地管理的方式，如果不指定，将采用本地

管理的方式。

      从Oracle10g开如，要求采用本地管理的方式。

53.本地索引与全局索引的差别与适用情况。
解答：本地索引适用于sql语句种限定一个范围的查询比如时间之类的， 全

局索引适用于在全部记录中查询，比如要查询一个手机号之类的。
全局索引总可能出现unused的情况，需要重建

本地索引适合条件中包含partition key的，当然不是绝对
全局索引总可能出现unused的情况，通常我会问那该怎么办？
9i里面有update global index 的子句

54.一个表a varchar2(1),b number(1),cchar(2)，有100000条记录，创建

B-Tree索引在字段a上，那么表与索引谁大？为什么？
解答：这个要考虑到rowid所占的字节数，假设char总是占用2字节的情况，

比较rowid和3
另外，table 和 index在segment free block的管理也有差别

55.9i的data guard有几种模式，各有什么差别？
解答：三种模式
maxmize performance 采用异步传送
maxmize availablity 允许采用异步传送，在两者之间摇摆
==> 不叫摇摆，正常情况maxmize availablity 传输方式等同于maxmize

protection ，只是在从库Crash时允许primary继续工作
maxmize protection 采用同步传送
==>保证Standby 与 primary 绝对数据一致
个人以为采用maxmize performance好一点，对主数据库影响比较小

56.执行计划是什么，查看执行计划一般有哪几种方式？
解答：执行计划是数据库内部的执行步骤
set autotrace on
select * from table
alter session set event ‘10046 trace name contextforever,level 12

‘
一般采用pl/sql developer，其它的比较少用，记不住
==>差不多，再加个Explain plan , v$sql_plan

57.简单描述一下nest loop与hash join的差别。
解答：nest loop适用于返回结果比较小的情况。
for in 1…n loop
对小表进行遍历
根据小表的结果遍历大表（大表需要索引）
end loop
这个在数据库高效设计里面有很好的解释，一时还写不出来
==>小表称为驱动的结果集更为贴切
hash join适用在返回大结果集的情况
==>也未必一定大结果集
58.db file sequential read与db file scattered read等待的差别，如果

以上等待比较多，证明了什么问题？
解答：db file sequential read指的是需要一个但当前不在sga中的块，等

待从磁盘中读取。db file scattered read需要多个连续的数据库引起等待

。
db file sequential read出现大量的等待，或许不是个问题。如果这两个事

件等待比较多，根据p1,p2,p3以及sid检查sql语句，是否有调优的可能
==>db file scattered read基本可以定性为FTS/IFS


59.ibrary cache pin与library cache lock是什么地方的等待事件，一般说

明什么问题？
解答：一般出现在对package,procedure进行编译，addcontraint的时候。
==>差不多，说明DDL过多

60.在一个24*7的应用上，需要把一个访问量很大的1000万以上数据级别的表

的普通索引(a,b)修改成唯一约束(a,b,c)，你一般会选择怎么做，请说出具

体的操作步骤与语句
解答：不能确定，是否可以采用先建索引后建立约束
create index idx_w1 on w_1 (a,b,c) online ;
alter table w_1 add constraint uni_w1 unique (a,b,c) novalidate;
==>
差不多，另外，一定要考虑非繁忙时间

61.如果一个linux上的oracle数据库系统突然变慢，你一般从哪里去查找原

因。

解答：先top看看是哪些进程，看看这些进程在做什么
看看v$session_wait
==>
差不多，能加上vmstat , iostat就更好了

62.说明一下对raid5与raid01/10的认识。
解答：raid5采用校验信息，硬盘的利用率n-1/n,raid10先采用先镜像在进

行条带化，是最高效的硬盘利用方式，硬盘的利用率50%
==> 通常会提一下redo log 不能 inraid5. 还有 01/10的区别及优劣

62.EXISTS与IN的执行效率问题
在许多基于基础表的查询中,为了满足一个条件,往往需要对另一个表进行联

接.在这种情况下，如果另一个表是小表用in 效率高，是大表用exists 效率

高。

63.BETWEEN AND 是否包含边界？ ›

解答;Between and 包括边界值

64.列出常用的DML，DDL有哪些语句
解答：DDL 数据定义语言:

CREATE,DROP,ALTER,GRANT,REVOKE,TRUNCATE,ANALYZE
DML 数据操纵语言: SELECT,INSERT,UPDATE,DELETE,SET TRANCTION等


65.存储过程和函数的区别
解答：存储过程是用户定义的一系列sql语句的集合，涉及特定表或其它对象

的任务，用户可以调用存储过程，而函数通常是数据库已定义的方法，它接

收参数并返回某种类型的值并且不涉及特定用户表

66.事务是什么？ACID是什么意思？

解答：事务是作为一个逻辑单元执行的一系列操作，一个逻辑工作单元必须

有四个属性，称为ACID（原子性、一致性、隔离性和持久性）属性，只有这

样才能成为一个事务：
原子性
事务必须是原子工作单元；对于其数据修改，要么全都执行，要么全都不执

行。
一致性
事务在完成时，必须使所有的数据都保持一致状态。在相关数据库中，所有

规则都必须应用于事务的修改，以保持所有数据的完整性。事务结束时，所

有的内部数据结构（如B树索引或双向链表）都必须是正确的。
隔离性
由并发事务所作的修改必须与任何其它并发事务所作的修改隔离。事务查看

数据时数据所处的状态，要么是另一并发事务修改它之前的状态，要么是另

一事务修改它之后的状态，事务不会查看中间状态的数据。这称为可串行性

，因为它能够重新装载起始数据，并且重播一系列事务，以使数据结束时的

状态与原始事务执行的状态相同。
持久性
事务完成之后，它对于系统的影响是永久性的。该修改即使出现系统故障也

将一直保持。

67.下面叙述正确的是______。
　　A、算法的执行效率与数据的存储结构无关
　　B、算法的空间复杂度是指算法程序中指令(或语句)的条数
　　C、算法的有穷性是指算法必须能在执行有限个步骤之后终止
　　D、以上三种描述都不对

解答：C

68.以下数据结构中不属于线性数据结构的是______。A、队列B、线性表C、

二叉树D、栈
答案为： C

69.在一棵二叉树上第5层的结点数最多是______。A、8 B、16 C、32 D、15

答案为： B

70.下面描述中，符合结构化程序设计风格的是______。
　　A、使用顺序、选择和重复(循环)三种基本控制结构表示程序的控制逻辑
　　B、模块只有一个入口，可以有多个出口
　　C、注重提高程序的执行效率 D、不使用goto语句
答案为： A