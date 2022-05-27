- # Oracle：建立远程链接数据库（跨库连接）

  

  一、授权（本地客户器端授权当前用户）

  ```
  grant create database link to testdb
  ```

  二、配置本地数据库服务器的tnsnames.ora文件 

  ```
  user =
    (DESCRIPTION =
      (ADDRESS_LIST =
        (ADDRESS = (PROTOCOL = TCP)(HOST = 0.0.0.0)(PORT = 80))
      )
      (CONNECT_DATA =
        (SERVICE_NAME = users)
      )
    )
  ```

  三、创建dblink

  方法一：通过编写SQL语句

  ```
  -- Drop existing database link 
  drop database link 如来神掌;
  -- Create database link 
  create database link 如来神掌
    connect to testdb
    using '(DESCRIPTION =
      (ADDRESS_LIST =
        (ADDRESS = (PROTOCOL = TCP)(HOST = 0.0.0.0)(PORT = 80))
      )
      (CONNECT_DATA =
        (SERVICE_NAME = test)
      )
    )';
  ```

  方法二：手动添加

  1、Oracle对象集中找到Database Link

  ![img](https://images2015.cnblogs.com/blog/653280/201704/653280-20170415104820783-845480338.png)

  2、新建

  ![img](https://images2015.cnblogs.com/blog/653280/201704/653280-20170415104900720-451970518.png)

  3、填写配置信息

  ![img](https://images2015.cnblogs.com/blog/653280/201704/653280-20170415105002611-833195427.png)

  注：

  所有者：选择当前数据库

  名称：按需求命名

  连接到（目标数据库）：输入用户名、口令和连接字符串

  鉴定者一栏可不填

  4、删除dblink

  ```
  Drop database link test;
  ```

  5、跨库连接实例

  ```
  select * from usr_mstr@test
  /*
  注：blog、clob无法直接通过远程连接获取，当表中存在这两个类型的字段时，应避开这两个大数据类型的字段
  */
  ```

# 为 Oracle 数据库创建数据库链接

导入应用程序之前，必须在源数据库和目标数据之间创建数据库链接。

在目标数据库中执行这些步骤。

要在源 Oracle DB 和 HFM Schema 中创建数据库链接：

1. 以 sysdba 用户身份登录，并授予创建 HFM Schema 的数据库链接的权限。

   ```
   GRANT CREATE DATABASE LINK TO hfm;
   ```

2. 登录到目标系统的 HFM Schema 并执行以下命令：

   ```
   CREATE DATABASE LINK <link name> CONNECT TO<hfm schema name>IDENTIFIED BY HFM1 USING '//<host name>:<port>/<service name>';
   ```

   例如，要连接主机 **SLCK58001** 上的 HFM Schema 以及端口 **1521** 上运行的 Oracle：

   ```
   CREATE DATABASE LINK ToTestSystem CONNECT TO HFM IDENTIFIED BY HFM1 USING '//slck58001.xxxx:1521/service name';
                  
   ```

3. 验证步骤：以下命令应列出源系统中的应用程序：

   ```
   Select * from HSX_DATASOURCES@ToTestSystem
   ```

4. 可删除数据库链接的命令：

   ```
   drop database link ToTestSystem;
   ```

5. 可列出所有数据库链接的命令：

   ```
   select * from all_db_links
   ```