2021年12月28日

### MongoDB

MongoDb是一个基于分布式文件存储的数据库。由C++语言编写，旨在为WEB应用提供可扩展的高性能数据存储解决方案。

MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像数据库的。



### MongoDB概念解析

| SQL术语/概念 | MongoDB术语/概念 |              解释/说明              |
| :----------: | :--------------: | :---------------------------------: |
|   database   |     database     |               数据库                |
|    table     |    collection    |            数据库表/集合            |
|     row      |     document     |           数据记录行/文档           |
|    column    |      field       |             数据字段/域             |
|    index     |      index       |                索引                 |
| table joins  |                  |        表连接,MongoDB不支持         |
| primary key  |   primary key    | 主键,MongoDB自动将_id字段设置为主键 |

### MongoDB命令解析

#### 创建数据库

```sql
--语法格式
use DATABASE_NAME

--示例
use dsjprs_db
--解释：如果数据库不存在，则创建数据库，否则切换到指定的数据库
```

#### 删除数据库

```sql
--语法格式
db.dropDatabase()
--解释：删除当前数据库，默认为test,可以使用db命令查看当前的数据库名

--示例
--查看所有数据库
show dbs

--切换到创建的数据库
use dsjprs_db

--执行删除命令
db.dropDatabase()
{"droped" : "dsjprs_db", "ok" : 1}

--集合删除语法格式
db.collection.drop()

--创建数据库
use dsjprs.db

--先创建集合，类似数据库中的表
db.createCollection("dsjprs")

--查看表结构
show tables
```

#### 创建集合

```sql
--创建集合语法格式
db.createCollection(name, options)
--name：要创建的集合名称
--options：可选参数，指定内存大小和索引的选项

--示例：在test数据库中创建dsjprs集合
use test
--创建dsjprs集合
db.createCollection("dsjprs")
--查看已存在或创建的集合
show collections

--带有关键参数的createCollection()的用法
--创建固定集合mycol，整个集合空间大小为614200B，文档大小个数为10000个。
db.createCollection("mycol", {capped : true, autoIndexId : true, size : 6142800, max : 10000})
```

 options 可以是如下参数： 

|    字段     | 类型 |                             描述                             |
| :---------: | ---- | :----------------------------------------------------------: |
|   capped    | 布尔 | （可选）如果为 true，则创建固定集合。固定集合是指有着固定大小的集合，当达到最大值时，它会自动覆盖最早的文档。 **当该值为 true 时，必须指定 size 参数。** |
| autoIndexId | 布尔 | 3.2 之后不再支持该参数。（可选）如为 true，自动在 _id 字段创建索引。默认为 false。 |
|    size     | 数值 | （可选）为固定集合指定一个最大值，即字节数。 **如果 capped 为 true，也需要指定该字段。** |
|     max     | 数值 |          （可选）指定固定集合中包含文档的最大数量。          |

#### 删除集合

```sql
--语法格式
db.collection.drop()
--如果成功删除选定集合，则drop()方法返回true，否则返回false

--切换test数据库
use test

--查看集合
show collections

--删除集合
db.mycol.drop
```

#### 插入文档

```sql
--语法格式
db.collections_name.insert(document)
--或
db.collection_name.save(document)
--save()：如果 _id 主键存在则更新数据，如果不存在就插入数据。该方法新版本中已废弃，可以使用 db.collection.insertOne() 或 db.collection.replaceOne() 来代替。

--insert(): 若插入的数据主键已经存在，则会抛 org.springframework.dao.DuplicateKeyException 异常，提示主键重复，不保存当前数据。
```

3.2版本之后新增了db.collection.insertOne()和db.collection.insertMany()

```sql
--db.collection.insertOne() 用于向集合插入一个新文档，语法格式如下：
db.collection.insertOne(
	<document>,
    {
    	writeconcern: <document>
    }
)
```

```sql
--db.collection.insertMany() 用于向集合插入一个多个文档，语法格式如下：
db.collection.insertMany(
   [ <document 1> , <document 2>, ... ],
   {
      writeConcern: <document>,
      ordered: <boolean>
   }
)
```

参数说明：

- document：要写入的文档。
- writeConcern：写入策略，默认为 1，即要求确认写操作，0 是不要求。
- ordered：指定是否按顺序写入，默认 true，按顺序写入。

```sql
--示例
db.col.insert({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: 'MongoDB_dsjprs教程',
    url: 'http://www.dsjprs.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})
```

#### 更新文档

MongoDB使用update()和save()方法来更新集合中的文档

```sql
--update()方法：用于更新已存在的文档。语法格式如下：
db.collection.update(
	<query>,
    <update>,
    {
    upsert:<boolean>,
    multi:<boolean>,
    writeConcern:<document>
    }
)
```

**参数说明：**

- **query** : update的查询条件，类似sql update查询内where后面的。
- **update** : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
- **upsert** : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
- **multi** : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
- **writeConcern** :可选，抛出异常的级别。

```sql
--示例
db.col.insert({
    title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: 'MongoDB_dsjprs',
    url: 'http://www.dsjprs.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})

db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})

db.col.find().pretty()
{
        "_id" : ObjectId("56064f89ade2f21f36b03136"),
        "title" : "MongoDB",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "MongoDB_dsjprs",
        "url" : "http://www.dsjprs.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
```

```sql
--save()方法：通过传入的文档来替换已有文档，_id主键存在就更新，不存在就插入。
db.collection.save(
	<document>,
    {
    	sriteConcern:<document>
    }
)
```

**参数说明：**

- **document** : 文档数据。
- **writeConcern** :可选，抛出异常的级别。

```sql
--示例
db.col.save({
    "_id" : ObjectId("56064f89ade2f21f36b03136"),
    "title" : "MongoDB",
    "description" : "MongoDB 是一个 Nosql 数据库",
    "by" : "Runoob",
    "url" : "http://www.dsjprs.com",
    "tags" : [
            "mongodb",
            "NoSQL"
    ],
    "likes" : 110
})
```

### 删除文档

```sql
--remove()函数用来移除集合中的数据，数据更新可以使用update()函数。在执行remove()函数前先执行find()命令来判断执行的条件是否正确。

--remove()方法的基本语法格式如下
db.collection.remove(
	<query>,
    <justOne>
)

--注意：如果MongoDB是2.6版本以后的，语法格式如下：
db.collection.remove(
	<query>,
    {
    	justone: <boolean>,
    	writeConcern:<document>
    }
)
```

**参数说明：**

- **query** :（可选）删除的文档的条件。
- **justOne** : （可选）如果设为 true 或 1，则只删除一个文档，如果不设置该参数，或使用默认值 false，则删除所有匹配条件的文档。
- **writeConcern** :（可选）抛出异常的级别

```sql
--示例
db.col.insert({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.dsjprs.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
})

--使用find()函数查询数据
db.col.find()
{ "_id" : ObjectId("56066169ade2f21f36b03137"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "教程", "url" : "http://www.dsjprs.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }
{ "_id" : ObjectId("5606616dade2f21f36b03138"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "教程", "url" : "http://www.dsjprs.com", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 

--移除title为MongoDB教程的文档
db.col.remove({'title':'MongoDB 教程'})
--删除了两条数据
writeResult({'nRemove' : 2}) 
```

### 查询文档

```sql
--查询文档使用find()方法
--查询数据的语法格式如下：
db.collection.find(query, projection)

--如果需要以易读的方式来读取数据，可以使用pretty()方法。语法格式如下：
db.col.find().pretty()
--pretty()方法以格式化的方式来显示所有文档
```

- **query** ：可选，使用查询操作符指定查询条件
- **projection** ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。

### MongoDB与RDBMS Where语句比较

常规的 SQL 数据，通过下表可以更好的理解 MongoDB 的条件语句查询：

|    操作    |     格式     |                    范例                     |  RDBMS中的类似语句  |
| :--------: | :----------: | :-----------------------------------------: | :-----------------: |
|    等于    |    `{:`}     |    `db.col.find({"by":"教程"}).pretty()`    | `where by = '教程'` |
|    小于    | `{:{$lt:}}`  | `db.col.find({"likes":{$lt:50}}).pretty()`  | `where likes < 50`  |
| 小于或等于 | `{:{$lte:}}` | `db.col.find({"likes":{$lte:50}}).pretty()` | `where likes <= 50` |
|    大于    | `{:{$gt:}}`  | `db.col.find({"likes":{$gt:50}}).pretty()`  | `where likes > 50`  |
| 大于或等于 | `{:{$gte:}}` | `db.col.find({"likes":{$gte:50}}).pretty()` | `where likes >= 50` |
|   不等于   | `{:{$ne:}}`  | `db.col.find({"likes":{$ne:50}}).pretty()`  | `where likes != 50` |

### AND条件

MongoDB的find()方法可以传入多个键(key)，每个键(key)以逗号隔开，即常规SQL的AND条件

```sql
db.col.find({key1:value1, key2:value2}).pretty()

--示例
db.col.find({"by":"教程", "title":"MongoDB 教程"}).pretty()
{
        "_id" : ObjectId("56063f17ade2f21f36b03133"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "教程",
        "url" : "http://www.dsjprs.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}
--类似WHERE语句：WHERE by = 教程 AND title = 'MongoDB教程'
```

### OR条件

MongoDB OR条件语句使用了关键字$or，语法格式如下

```sql
db.col.find(
	{
    	$or: [
            {key1:value1}, {key2:value2}
        ]
    }
).pretty()
```

AND和OR联合使用

```sql
db.col.find({"likes":{$gt:50}, $or:[{"by":"教程"}, "title": "MongoDB教程"]})。pretty()
```

### 条件操作符

条件操作符用于比较两个表达式并从mongoDB集合中获取数据。

MongoDB中条件操作符有：

- (>) 大于 - $gt
- (<) 小于 - $lt
- (>=) 大于等于 - $gte
- (<= ) 小于等于 - $lte

#### MongoDB( > ) 大于操作符 -$gt

```sql
--获取col集合中likes大于100的数据
db.col.find({likes: {$gt:100}})

--类似SQL语句
select * from col where likes > 100;
```

#### MongoDB( < ) 小于操作符 -$lt

```sql
--获取col集合中likes小于150的数据
db.col.find({likes: {$lt: 150}})

--类似SQL语句
select * from col where likes < 150;
```

#### MongoDB( <= ) 小于操作符 -$lte

```sql
--获取col集合中likes小于等于150的数据
db.col.find({likes: {$lte: 150}})

--类似SQL语句
select * from col where likes <= 150;
```

####  MongoDB使用(<)和(>)查询 -$lt和$gt

```sql
--获取col集合中likes大于100，小于200的数据
db.col.find({likes: {$lt: 200, $gt: 100}})

--类似SQL语句
select * from col where likes > 100 AND likes < 200;
```

### $type操作符

$type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果。

MongoDB 中可以使用的类型如下表所示：

|        **类型**         | **数字** |     **备注**     |
| :---------------------: | :------: | :--------------: |
|         Double          |    1     |                  |
|         String          |    2     |                  |
|         Object          |    3     |                  |
|          Array          |    4     |                  |
|       Binary data       |    5     |                  |
|        Undefined        |    6     |     已废弃。     |
|        Object id        |    7     |                  |
|         Boolean         |    8     |                  |
|          Date           |    9     |                  |
|          Null           |    10    |                  |
|   Regular Expression    |    11    |                  |
|       JavaScript        |    13    |                  |
|         Symbol          |    14    |                  |
| JavaScript (with scope) |    15    |                  |
|     32-bit integer      |    16    |                  |
|        Timestamp        |    17    |                  |
|     64-bit integer      |    18    |                  |
|         Min key         |   255    | Query with `-1`. |
|         Max key         |   127    |                  |

#### MongoDB操作符 - $type示例

```sql
--获取col集合中titile为String的数据
db.col.find({"title": {$tyoe: 2}})
--或
db.col.find({"title": {$type: "String"}})
```

### Limit与Skip

#### Limit()方法

```sql
--如果需要读取指定数量的数据记录，可以使用Limit方法，Limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数
--limit()方法基本语法如下所示
db.COLLECTION_NAME.find().limit(NUMBER)
```

#### Skip()方法

```sql
--使用skip()方法来跳过指定数量的数据，skip方法同意接受一个数字参数作为跳过的记录条数
--skip()方法基本语法格式如下：
db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
--注：skip()方法默认参数为0

--示例
db.col.find({}, {"title": 1, _id: 0}).limit(1).skip(1)
```

### 排序

使用sort()方法对数据进行排序，sort()方法可以通过参数指定排序的字段，并使用1和-1来指定排序的方式，其中1为升序排序，-1为降序排序

```sql
--sort()方法基本语法格式如下
db.COLLECTION_NAME.find().sort({key: 1})

--示例:col集合中的数据按字段likes的降序排列
db.col.find({}, {"title" : 1, _id: 0}).sort("likes" : -1)
```

### 索引

索引通常能够极大的提高查询的效率，如果没有索引，MongoDB在读取数据时必须扫描集合中的每个文件并选取那些符合查询条件的记录。

这种扫描全集合的查询效率是非常低的，特别在处理大量的数据时，查询可以要花费几十秒甚至几分钟，这对网站的性能是非常致命的。

索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构

```sql
--MongoDB使用createIndex()方法来创建索引(注意：在3.0.0版本前创建索引方法为db.collection.ensureIndex()，之后的版本使用了db.collection.createIndex()方法，ensureIndex()还能使用，但只是createIndex()的别名)

--createIndex()方法基语法格式
db.collection.createIndex(keys, options)
--(语法中key值为需要创建的索引字段，1为指定升序创建索引，-1为降序创建索引)

--示例
db.col.createIndex({"title": 1})
--createIndex()方法也可以设置多个字段创建索引（关系型数据库中称为复合索引）
db.col.createIndex({"title": 1, "description": -1})
```

createIndex() 接收可选参数，可选参数列表如下：

|     Parameter      |     Type      |                         Description                          |
| :----------------: | :-----------: | :----------------------------------------------------------: |
|     background     |    Boolean    | 建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为**false**。 |
|       unique       |    Boolean    | 建立的索引是否唯一。指定为true创建唯一索引。默认值为**false**. |
|        name        |    string     | 索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。 |
|      dropDups      |    Boolean    | **3.0+版本已废弃。**在建立唯一索引时是否删除重复记录,指定 true 创建唯一索引。默认值为 **false**. |
|       sparse       |    Boolean    | 对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 **false**. |
| expireAfterSeconds |    integer    | 指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。 |
|         v          | index version | 索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。 |
|      weights       |   document    | 索引权重值，数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。 |
|  default_language  |    string     | 对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语 |
| language_override  |    string     | 对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language. |

```sql
--1、查看集合索引
db.col.getIndexes()

--2、查看集合索引的大小
db.col.totalIndesxSize()

--3、删除集合所有索引
db.col.dropIndexes()

--4、删除集合指定索引
db.col.dropIndex("索引名称")
```

### 聚合

MongoDB中聚合(aggregate)主要用于处理数据(诸如：统计平均值，求和等)，并返回计算后的数据结果。有点类似SQL语句中的count(*)。

MongoDB中聚合的方法使用aggregate()

```sql
--aggregate()方法的基本语法格式
db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)

--示例
db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
{
   "result" : [
      {
         "_id" : "dsjprs.com",
         "num_tutorial" : 2
      },
      {
         "_id" : "Neo4j",
         "num_tutorial" : 1
      }
   ],
   "ok" : 1
}
--类似SQL语句
select by_user, count(*) from mycol group by by_user;
```



下表展示了一些聚合的表达式:

|  表达式   |                             描述                             |                             实例                             |
| :-------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   $sum    |                          计算总和。                          | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}]) |
|   $avg    |                          计算平均值                          | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}]) |
|   $min    |              获取集合中所有文档对应值得最小值。              | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}]) |
|   $max    |              获取集合中所有文档对应值得最大值。              | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}]) |
|   $push   |         将值加入一个数组中，不会判断是否有重复的值。         | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}]) |
| $addToSet | 将值加入一个数组中，会判断是否有重复的值，若相同的值在数组中已经存在了，则不加入。 | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}]) |
|  $first   |            根据资源文档的排序获取第一个文档数据。            | db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}]) |
|   $last   |            根据资源文档的排序获取最后一个文档数据            | db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}]) |

#### 管道的概念

管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。

MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。

表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。

介绍一下聚合框架中常用的几个操作：

- $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
- $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
- $limit：用来限制MongoDB聚合管道返回的文档数。
- $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
- $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
- $group：将集合中的文档分组，可用于统计结果。
- $sort：将输入文档排序后输出。
- $geoNear：输出接近某一地理位置的有序文档。

#### 管道操作符示例

```sql
--$project示例
db.article.aggregate(
	{$project: {
    	title: 1,
    	author: 1,
    }}
);

--$match实例
db.articles.aggregate( [
                        { $match : { score : { $gt : 70, $lte : 90 } } },
                        { $group: { _id: null, count: { $sum: 1 } } }
                       ] );
--$match用于获取分数大于70小于或等于90记录，然后将符合条件的记录送到下一阶段$group管道操作符进行处理

--$skip实例
db.article.aggregate(
    { $skip : 5 });
--经过$skip管道操作符处理后，前五个文档被"过滤"掉。
```

### 复制（副本集）

MongoDB复制是将数据同步在多个服务器的过程。

复制提供了数据的冗余备份，并在多个服务器上存储数据副本，提高了数据的可用性， 并可以保证数据的安全性。

复制还允许您从硬件故障和服务中断中恢复数据。

#### 什么是复制?

- 保障数据的安全性
- 数据高可用性 (24*7)
- 灾难恢复
- 无需停机维护（如备份，重建索引，压缩）
- 分布式读取数据

#### MongoDB复制原理

mongodb的复制至少需要两个节点。其中一个是主节点，负责处理客户端请求，其余的都是从节点，负责复制主节点上的数据。

mongodb各个节点常见的搭配方式为：一主一从、一主多从。

主节点记录在其上的所有操作oplog，从节点定期轮询主节点获取这些操作，然后对自己的数据副本执行这些操作，从而保证从节点的数据与主节点一致。

#### 副本集特征：

- N 个节点的集群
- 任何节点可作为主节点
- 所有写入操作都在主节点上
- 自动故障转移
- 自动恢复



#### MongoDB副本集设置

```sql
--1、关闭正在运行的MongoDB服务器
--replSet选项来启动MongoDB.--replSer基本语法格式如下
mogod --port "port" --dbpath "your_db_data_path" --replSet "replice_set_instance_name"
--示例
mongod --port 27017 --dbpath "D:\set up\mongodb\data" --replSet rs0
```

#### 副本集添加成员

```sql
--添加副本集的成员，使用rs.add()方法来添加副本集的成员
--rs.add()命令基本语法格式
rs.add(HOST_NAME.PORT)

--示例
rs.add("mongod1.net": 27017)
```

### 分片

在Mongodb里面存在另一种集群，就是分片技术,可以满足MongoDB数据量大量增长的需求。

当MongoDB存储海量的数据时，一台机器可能不足以存储数据，也可能不足以提供可接受的读写吞吐量。这时，我们就可以通过在多台机器上分割数据，使得数据库系统能存储和处理更多的数据。

#### 为什么使用分片

- 复制所有的写入操作到主节点
- 延迟的敏感数据会在主节点查询
- 单个副本集限制在12个节点
- 当请求量巨大时会出现内存不足。
- 本地磁盘不足
- 垂直扩展价格昂贵

#### 主要有如下所述三个主要组件：

- Shard:

  用于存储实际的数据块，实际生产环境中一个shard server角色可由几台机器组个一个replica set承担，防止主机单点故障

- Config Server:

  mongod实例，存储了整个 ClusterMetadata，其中包括 chunk信息。

- Query Routers:

  前端路由，客户端由此接入，且让整个集群看上去像单一数据库，前端应用可以透明使用。

```sql
--1、第一步启动Shared Server
--2、第二步启动Config Server
--3、第三步启动Route Process
--4、配置Sharding
```

### 备份(mongodump)与恢复(mongorestore)

#### 数据备份

在Mongodb中我们使用mongodump命令来备份MongoDB数据。该命令可以导出所有数据到指定目录中。

mongodump命令可以通过参数指定导出的数据量级转存的服务器。

```sql
--mongodump命令基本语法格式如下
mongodump -h dbhost -d dbname -o dbdirectory
```

- -h：

  MongoDB 所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017

- -d：

  需要备份的数据库实例，例如：test

- -o：

  备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。

 mongodump 命令可选参数列表如下所示： 

|                       语法                        |              描述              |                       实例                       |
| :-----------------------------------------------: | :----------------------------: | :----------------------------------------------: |
|   mongodump --host HOST_NAME --port PORT_NUMBER   |  该命令将备份所有MongoDB数据   |     mongodump --host runoob.com --port 27017     |
| mongodump --dbpath DB_PATH --out BACKUP_DIRECTORY |                                | mongodump --dbpath /data/db/ --out /data/backup/ |
|  mongodump --collection COLLECTION --db DB_NAME   | 该命令将备份指定数据库的集合。 |      mongodump --collection mycol --db test      |

#### 数据恢复

 mongodb使用 mongorestore 命令来恢复备份的数据。 

```sql
--mongorestore命令基本语法格式
mongorestore -h <hostname><:port> -d dbname <path>

--执行如下命令
mongorestore
```



- --host <:port>, -h <:port>：

  MongoDB所在服务器地址，默认为： localhost:27017

- --db , -d ：

  需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2

- --drop：

  恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！

- <path>：

  mongorestore 最后的一个参数，设置备份数据所在位置，例如：c:\data\dump\test。

  你不能同时指定 <path> 和 --dir 选项，--dir也可以设置备份目录。

- --dir：

  指定备份的目录

  你不能同时指定 <path> 和 --dir 选项。

### 监控

 MongoDB中提供了mongostat 和 mongotop 两个命令来监控MongoDB的运行情况 

#### mongostat 命令

mongostat是mongodb自带的状态检测工具，在命令行下使用。它会间隔固定时间获取mongodb的当前运行状态，并输出。如果发现数据库突然变慢或者有其他问题的话，第一手的操作就考虑采用mongostat来查看mongo的状态。

启动Mongod服务，进入到安装的MongoDB目录下的bin目录， 然后输入mongostat命令，如下所示：

```cmd
D: \set up\mongod\bin>mongostat
```

#### mongotop 命令

mongotop也是mongodb下的一个内置工具，mongotop提供了一个方法，用来跟踪一个MongoDB的实例，查看哪些大量的时间花费在读取和写入数据。 mongotop提供每个集合的水平的统计数据。默认情况下，mongotop返回值的每一秒。

启动Mongod服务，进入到安装的MongoDB目录下的bin目录， 然后输入mongotop命令，如下所示：

```cmd
D:\set up\mongodb\bin>mongotop

--带参数示例
E:\mongodb-win32-x86_64-2.2.1\bin>mongotop 10

--后面的10是<sleeptime>参数 ，可以不使用，等待的时间长度，以秒为单位，mongotop等待调用之间。通过的默认mongotop返回数据的每一秒。

E:\mongodb-win32-x86_64-2.2.1\bin>mongotop --locks
```

输出结果字段说明：

- ns：

  包含数据库命名空间，后者结合了数据库名称和集合。

- **db：**

  包含数据库的名称。名为 . 的数据库针对全局锁定，而非特定数据库。

- **total：**

  mongod花费的时间工作在这个命名空间提供总额。

- **read：**

  提供了大量的时间，这mongod花费在执行读操作，在此命名空间。

- **write：**

  提供这个命名空间进行写操作，这mongod花了大量的时间。




