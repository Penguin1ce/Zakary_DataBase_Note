## 2.1.1数据模型分类

**概念数据模型 CDM**：Conceptual Data Model

​	实体-联系模型**E-R**模型

**逻辑数据模型 LDM**：Logic Data Model

​	层次，网状，关系

## 2.1.3逻辑数据模型

### 数据模型的三要素

**数据结构**:描述数据库的组成对象以及对象之间的联系

**数据操纵**:是指对数据库中各种对象的实例允许执行的操作的集合,主要有查询和更新（包括插入、删除、修改）两大类操作。

**完整性约束**:是给定的数据模型中的数据及其联系所具有的制约和依存规则，用以限定符合数据模型的数据库状态以及状态的变化，以保证数据的正确、有效和相容。

## 2.1.4 层次模型

层次模型（hierarchical data model），数据模型是有根的定向有序树，表示各类实体以及实体间的联系。

1. 只有一个结点没有双亲结点，称为根结点。
2. 根以外的其他结点有且只有一个双亲结点。

<img src="./assets/image-20241205125846342.png" alt="image-20241205125846342" style="zoom:50%;" />

优点

​	层次模型的数据结构比较简单清晰。

​	记录之间的联系通过指针实现，查询效率较高。

缺点

​	现实世界中很多联系是非层次性的，如结点之间具有多对多联系，或者一个结点具有多个双亲结点，不适合层次模型表示。

## 2.1.5 网状模型 

网状模型（network data model），数据模型是有向图。

1. 允许一个以上的结点无双亲结点。

2. 一个结点可以有多于一个的双亲结点。

![image-20241205130717351](./assets/image-20241205130717351.png)

优点

​	能更为直接地描述现实世界，M:N联系容易实现

​	记录之间的联系通过指针实现，查询效率较高。

缺点

​	结构比较复杂，不利于最终用户掌握。

​	编写应用程序较复杂，程序员必须熟悉数据库的逻辑结构。

## 2.2 关系模型

关系模型优点：

​	1. 关系模型建立在严格的数学概念基础上。

​	2. 数据结构简单、清晰，用户易懂易用。

​	3. 关系模型的存取路径对用户隐蔽。有更强的数据独立性、更好的安全保密性，简化了程序员的工作。

## **2.2.3** **关系的键**KEY（码）

超键(SuperKey)：在一个关系中，可**唯一地标识元组的**一个属性或属性集合。

候选键 (Candidate Key)：能唯一标识一个关系的元组而又**不含有多余的属性的**一个属性或属性集合。

**候选键是不是超键？**

候选键是超键的子集，因此：

- **每一个候选键都是超键**。
- **但不是每一个超键都是候选键**，因为超键可以包含冗余属性。

**如果关系的全部属性构成关系的候选键**，则称为**全键(All-Key)**。

构成候选键的诸属性称为**主属性(Prime Attribute**)。

不包含在任意候选键中的属性称为**非主属性(Non-Prime Attribute)**。

**主键 (Primary Key/PK)：**关系中用户选择一个候选键作为插入，删除或检索元组的操作变量，被选用的候选键称为主键。

**外键(Foreign Key/FK)：**是指关系R中的属性A不是关系R的主键，但A是另一个关系S的主键，则属性A就是关系R的外键。其中R是参照关系，S是被参照关系。

外键在关系R中的取值有两种可能：或为**空值**，或必须是**被参照关系S中已有的属性值**。

外键值是否允许为空值，主要依赖于应用环境的语义。

## 2.2.4关系规则

第一范式(First Normal Form，1NF)

实体完整性规则

参照完整性规则

用户定义的完整性规则

**第一范式(First Normal Form，1NF)：**是指关系数据库中表的每一分量都是不可分割的基本数据项（原子性）。

|        | **家庭住址** |          |
| :----: | :----------: | :------: |
| **省** |   **城市**   | **街道** |

这种情况不允许。

**实体完整性规则：**定义关系中主键的取值不能为空值。

**参照完整性规则：**若属性或属性组F是关系R的外键，它与关系S的主键Ks相对应，则对于R中每个元组在F上的值或者取空值；或者等于S中某个元组的主键值。

**用户定义的完整性规则：**针对某一具体关系数据库的约束条件，反映某一具体应用所涉及的数据必须满足的语义要求。

## 2.4.2自然关系运算

<img src="./assets/image-20241205132625276.png" alt="image-20241205132625276" style="zoom:75%;" />

等值连接：

<img src="./assets/image-20241205132917491.png" alt="image-20241205132917491" style="zoom:50%;" />

自然连接：

<img src="./assets/image-20241205132934347.png" alt="image-20241205132934347" style="zoom:50%;" />

采用θ连接表示如下：

<img src="./assets/image-20241205140213829.png" alt="image-20241205140213829" style="zoom:80%;" />

n采用乘法表示如下:

<img src="./assets/image-20241205140310660.png" alt="image-20241205140310660" style="zoom:80%;" />

<img src="./assets/image-20241205140629500.png" alt="image-20241205140629500" style="zoom: 33%;" />

<img src="./assets/image-20241205140723783.png" alt="image-20241205140723783" style="zoom:70%;" />

<img src="./assets/image-20241205140743400.png" alt="image-20241205140743400" style="zoom:50%;" />

<img src="./assets/image-20241205140757372.png" alt="image-20241205140757372" style="zoom:33%;" />

### 题目

3.设有一个数据库Library，包括Book，Borrow，Reader四个关系模式：

Book(Bno，Btitle，Bauthor，Bprice)；

Borrow(Rno，Bno，BorrowDate，ReturnDate)；

Reader(Rno，Rname，Rsex，Rage，Reducation)；

图书表Book由图书编号(Bno)、图书名称(Btitle)、图书作者(Bauthor)、图书价格(Bprice)组成；

借阅表Borrow由读者编号(Rno)、图书编号(Bno)、借阅时间(BorrowDate)、归还时间(ReturnDate)组成；

读者表Reader由读者编号(Rno)、读者姓名(Rname)、读者性别(Rsex)、读者年龄(Rage)、读者学历(Reducation)组成。

针对数据库Library，用关系代数表达式表示下列查询语句。

①查询全体读者的姓名(Rname)、出生年份。

②查询所有年龄在18~20岁(包括18岁和20岁)之间的读者姓名(Rname)及年龄(Rage)。

③查询学历为研究生的读者的编号(Rno)、姓名(Rname)和性别(Rsex)。

④查询读者的借书情况，要求列出读者姓名，图书标题，借书日期。

⑤查询所有读者的基本情况和借书情况，没有借书的读者也输出基本信息。

⑥查询所有借了编号为B02的图书的读者编号(Rno)和读者姓名(Rname)。

⑦查询至少借阅了读者R01借阅的全部书籍的读者编号(Rno)和读者姓名(Rname)。

⑧查询图书名称包含“数据库” 和价格低于50元的图书的信息。

## 3.3 MySQL的组件结构

**连接器：**负责跟客户端建立连接、权限校验、获取权限、维持和管理连接。

**分析器：**对SQL的词法和语法进行分析。词法分析是分析出SQL中字符串代表的含义，识别对应的关键字。语法分析是根据语法的规则判断SQL是否满足MySQL的语法。

**优化器：**选择出最优的查询方案，或者重写查询（对一些执行耗费性能的语句，会依据一些规则，尽
 力转换成某种可高效执行的形式，比如决定表的读取顺序，选择需要的索引等）。

**执行器：**执行优化后的查询方案。执行前要判断当前用户是否有操作表的权限，如果有，则会根据表的存储引擎定义调用相应接口，对数据进行操作；如果无权限则报错。



**引擎层（存储引擎）：**是对于数据库文件的一种存取机制，如何实现存储数据，如何为存储的数据建立索引以及如何更新、查询数据等技术实现的方法。架构模式是插件式的，支持多个存储引擎。

**InnoDB引擎：**事务型存储引擎，提供对数据库事务的ACID支持，实现SQL标准的四种隔离级别，具有行级锁定，适用于高并发情形及外键支持。MySQL 5.5.5 版本后InnoDB成为了默认存储引擎。

**MYISAM引擎：**不支持事务，不支持细粒度的锁（行锁）及外键，当表Insert与update时需要锁定整个表，效率低，高并发时可能会遇到瓶颈。

MYISAM独立于操作系统，可以在Windows及Linux上使用。MYISAM具有高效的查询速度，插入数据的速度很快，在web、数据仓库等应用环境中常用。

**Memory引擎：**表数据是存储在内存中的，由于会受到硬件问题或断电问题的影响，只能将这些表作为临时表或缓存使用。

​	特点：

​	①内存存放，读写速度快

​	②hash索引（默认）

**存储引擎选择：**

​	如果要提供提交、回滚和崩溃恢复能力的事务安全（ACID兼容）能力，并要求实现并发控制，选择InnoDB。

​	如果数据表主要用来插入和查询记录，则MyISAM引擎能提供较高的处理效率。

​	如果只是临时存放数据，数据量不大，并且不需要较高的数据安全性，可以选择将数据保存在内存中的Memory引擎。

## 3.6 MySQL的数据库

### 系统数据库

**mysql：**存储MySQL服务器运行时所需信息的表。包含存储数据库对象元数据的数据字典表、用于其他操作目的的系统表。

**information_schema：** 提供对数据库元数据、有关MySQL服务器的信息（例如数据库或表的名称、列的数据类型或访问权限）的访问。该数据库包含几个只读表（实际上是视图，而不是基表）。

**performance_schema：**该数据库的表是不使用持久磁盘存储的内存表，内容在服务器启动时重新填充，并在服务器关闭时丢弃。提供对有关服务器执行的有用信息的访问，同时对服务器性能的影响最小。

**sys：**通过视图的形式把information_schema和performance_schema 结合起来，帮助系统管理员监控MySQL的技术性能。可用于典型的调优和诊断用例。

### 示例数据库

示例数据库既可以用于日常学习和测试，也可以作为设计数据库的一个参考。

**Sakila ：**是一个在线 DVD 出租数据库。提供了actor、film、film_actor等16个表、7个视图、3个存储过程、3个函数。

**world** 是一个小型的简单数据库，主要用于基础查询测试。

## 4.1 SQL概述

### SQL的特点

 **（1）综合统一**

​	DQL(Data Query Language，数据查询语言 )

​	DML(Data Manipulation Language，数据操纵语言)

​	DDL(Data Definition Language，数据定义语言)

​	DCL(Data Control Language，数据控制语言 ) 

**（2）非过程化**

**（3）面向集合的操作方式**

**（4）提供交互式和嵌入式**

**（5）语言简洁**

| SQL功能  | **关键动词**            |
| :------- | :---------------------- |
| 数据查询 | SELECT                  |
| 数据定义 | CREATE,  DROP, ALTER    |
| 数据操纵 | INSERT,  UPDATE, DELETE |
| 数据控制 | GRANT,  REVOKE          |

安全等于`<=>`运算符是MySQL特有的，表示如果两个操作数相等（即使为NULL），值为真。

### SQL的数据定义语句

| 操作对象 | 创建            | 修改           | 删除          |
| :------- | :-------------- | :------------- | ------------- |
| 数据库   | CREATE DATABASE | ALTER DATABASE | DROP DATABASE |
|          | CREATE SCHEMA   | ALTER SCHEMA   | DROP SCHEMA   |
| 表       | CREATE TABLE    | ALTER TABLE    | DROP TABLE    |
| 视图     | CREATE VIEW     | ALTER VIEW     | DROP VIEW     |
| 索引     | CREATE INDEX    |                | DROP INDEX    |

## 4.2.1 数据库的相关操作

`COLLATE` 选项指定数据库排序规则。规定字符之间如何排序和比较。排序规则和字符集相关，每种排序规则有多种所支持的字符集，每种字符集都指定一种排序规则为默认值。MySQL支持的字符集排序规则有272个。省略表示采用默认值`utf8mb4_0900_ai_ci`。

查看MYSQL支持的字符集

`SHOW CHARACTER SET;`

MySQL共支持41种字符集

**ASCII编码：**采用一个字节存储编码，只有127个字符被编码到计算机里，包括大小写英文字母、数字和一些符号

**Unicode编码：**中文至少需要两个字节，中国制定了GB2312编码，但全世界有上百种语言，在多语言混合的文本中，显示出来会有乱码。Unicode把所有语言都统一到一套编码里，这样就不会再有乱码问题。现在操作系统和大多数编程语言都直接支持Unicode。

**UTF-8编码：**可变长编码，把一个Unicode字符编码成1-6个字节，英文字母编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。一般选择UTF-8编码，满足系统运行时可能需要的各类语言编码需求。

**utf8mb3和utf8mb4**，区别在于：most bytes 3和most bytes 4，即最多使用3 / 4个字节来表示1个字符。



### 表的分类

**基本表(Base Table)：**是实际独立存放在数据库中的表，是实表，在SQL中一个关系就对应一个基本表。

**派生表：**派生表是从SELECT语句返回的虚拟表。

**视图**：视图是从一个或几个基本表导出的表。视图是一个虚表。==即数据库中只存放视图的定义而不存放视图对应的数据==

## 4.2.2基本表的相关操作

`create table newtable(id int unsigned,name varchar(64));`

### MySQL的数据类型

数值类型，日期和时间类型，字符串类型，空间类型和JSON数据类型。

1. 定点类型（精确值）包括 `DECIMAL` 和 `NUMERIC`，这两个是同一个意思，使用numeric定义的列会被转换成decimal。

​	例 `salary DECIMAL(5,2)`，5是精度，表示值存储的有效位数，2是小数位数。存储值的范围为-999.99到	999.99。

​	`DECIMAL`在不指定精度时，默认整数为10，小数为0,即(10, 0)。

​	浮点类型（近似值）包括`FLOAT`和 `DOUBLE`，单精度值`FLOAT`使用四个字节，双精度值`DOUBLE`使用八个字	节。

​	当表需要存储小数，并且有精度要求，比如存储金额时，建议使用`DECIMAL`类型。

2. 日期和时间类型：包括`DATE、TIME、DATETIME、TIMESTAMP`和`YEAR`。

   **DATE  :** 用于具有日期部分但没有时间部分的值，以`‘YYYY-MM-DD’`格式检索和显示值。

   **TIME : **以'hh：mm：ss'格式检索和显示值（或'hhh：mm：ss'格式表示大小时值）。 值的范围可以从`'-838:59:59'` 到 `'838:59:59'`。小时部分不仅可用于表示一天中的时间（必须小于 24 小时），还可以表示两个事件之间的经过时间或时间间隔（可能远大于 24 小时，甚至为负数）。

​	**YEAR ：**用于表示年份值的 1 字节类型。MySQL 以 YYYY 格式显示值，范围为 '1901'到'2155'

​	**DATETIME（常用）：**用于同时包含日期和时间部分的值,以`‘YYYY-MM-DD hh:mm:ss[.fraction]’`格式检	索和显示值。占用8个字节，从MySQL5.6版本开始， DATETIME支持毫秒， `DATETIME（N）`中的N表示毫秒	的精度。常用的日期函数也能精确到毫秒。

<img src="./assets/image-20241205151206746.png" alt="image-20241205151206746" style="zoom:33%;" />

​	**时间戳TIMESTAMP**存储的是自`‘1970-01-01 00:00:00’ UTC`（格林尼治标准时间）(北京时间1970年01月	01日08时00分00秒)到现在的秒数。存储范围`‘1970-01-01 00:00:01’ to ‘2038-01-19 03:14:07’`，占	用4个字节

​	**timestamp**类型适合用来记录数据的最后修改时间，可以设置为只要更改了记录中其他字段值，timestamp	字段的值都会被自动更新。

| **完整性约束条件**                                       | **含义**                                         |
| -------------------------------------------------------- | ------------------------------------------------ |
| PRIMARY  KEY/KEY                                         | 定义主键                                         |
| NOT  NULL/NULL                                           | 定义的属性不能取空值/可以空值                    |
| DEFAULT                                                  | 设置默认值                                       |
| UNIQUE/UNIQUE  KEY                                       | 定义的属性值必须唯一                             |
| FOREIGN  KEY(属性名1)REFERENCES   表名[(属性名2)]        | 定义外键                                         |
| CHECK  (条件表达式)                                      | 定义的属性值须满足CHECK中的条件                  |
| AUTO_INCREMENT                                           | 设置列为自增属性。                               |
| {INDEX  \| KEY} [index_name] [index_type] (key_part,...) | 创建索引                                         |
| CONSTRAINT                                               | 设置约束，主键、唯一键、外键、CHECK 可定义为约束 |

```sql
CREATE TABLE customers (  
cid char(4) NOT NULL PRIMARY KEY, -- 列级完整性约束
cname varchar(30),  
city varchar(50) ,  
discnt float  CHECK(discnt>0)
) ;
```

```sql
-- 创建示例数据库中的订购表ORDERS。
-- 一个数据库中的约束不允许重名，即同一数据库中表与表之间的约束不能同名
CREATE TABLE orders
(ordno char(4) NOT NULL,  
month varchar(12) DEFAULT (LEFT(MONTHNAME(NOW()), 3)),  
cid  char(4) NOT NULL,  
aid char(3) NOT NULL,  
pid char(3) NOT NULL,  
qty float DEFAULT 0,  
dollars float DEFAULT 0,-- 默认值  
PRIMARY KEY (ordno), -- 表级完整性约束
CONSTRAINT aid1 FOREIGN KEY (aid) REFERENCES agents (aid), 
CONSTRAINT cid1 FOREIGN KEY (cid) REFERENCES customers(cid),
CONSTRAINT pid1 FOREIGN KEY (pid) REFERENCES products (pid), 
CONSTRAINT dollars_check1 CHECK (dollars >= 0),  
CONSTRAINT qty_check1 CHECK (qty >= 0) -- 约束
) ;

```

**复制表**

（1）只复制表结构，包括主键、索引，但不会复制表数据

CREATE TABLE *new_tbl* LIKE *orig_tbl*;

**例** `CREATE TABLE customers1 LIKE customers;`

（2）复制表结构及全部数据，但不会复制主键、索引等

CREATE TABLE *new_tbl* [AS] SELECT * FROM *orig_tbl*;

例：`CREATE TABLE customer2 AS SELECT * FROM customers;` 

## 4.3 SQL的数据查询功能

| **查询条件** | **谓词**                                                    |
| ------------ | ----------------------------------------------------------- |
| 比较         | =、<=>、>、<、>=、<=、<>、!=                                |
| 确定范围     | BETWEEN  AND(介于两者之间),NOT  BETWEEN AND(不介于两者之间) |
| 确定集合     | IN(在其中),NOT  IN(不在其中)                                |
| 存在         | EXISTS,NOT  EXISTS                                          |
| 量化比较     | ANY,ALL                                                     |
| 字符匹配     | LIKE(匹配),NOT  LIKE(不匹配)                                |
| 空值         | IS  NULL(是空值),IS  NOT NULL(不是空值)                     |
| 多重条件     | AND(与),OR(或),NOT(非)                                      |

### 查询结果排序

使用`ORDER BY`对查询结果排序。升序排列用`ASC`，降序排列用`DESC`，默认为升序排列。

查询所有的顾客信息，按照顾客姓名(Cname)升序排列。

`select * from customers`

`order by cname asc;`

对于字符排序，按照排序规则，一般升序指从A到Z的顺序，降序指从Z到A的顺序。

### 查询结果分组

`GROUP BY`子句将表中的元组按某一列或多列值分组，值相等的为一组，针对不同的组归纳信息，汇总相关数据。

查询每种产品的订购总量。

`select pid, sum(qty) total` 

`from orders group by pid;`

查询满足条件为某个代理商所订购的某种产品的总量超过1000的代理商ID、产品ID和总量。

`select aid,pid, sum(qty) as total from orders` 

`group by aid,pid having sum(qty) > 1000;`

## 4.3.3 嵌套查询

### IN

```sql
select distinct cid from orders 
where aid in 
(select aid from agents 
where city = 'duluth'or city = 'dallas');
```

```sql
select distinct cid from orders 
where aid in 
(select aid from agents 
where city = 'duluth'or city = 'dallas');
```

```sql
select distinct cid from orders 
where aid in 
(select aid from agents 
where city in ('duluth','dallas'));
```

### NOT IN

查询没有人订购过的产品名称，订购过的产品。

```sql
Select pname from products
where pid not in (select pid from orders); 
```

查询佣金百分率最小的代理商的aid值。

第一种写法：

`select aid from agents where percent<=all`

`(select percent from agents);` 

第二种写法：

`Select aid from agents where` 

`percent = (select min(percent) from agents);`

| 量化比较谓词                         | 含义                           | 量化比较谓词     | 含义                           |
| ------------------------------------ | ------------------------------ | ---------------- | ------------------------------ |
| ＞ANY  ＞SOME                        | 大于子查询结果中的某一个值     | ＞ALL            | 大于子查询结果中的所有值       |
| ＜ANY  ＜SOME                        | 小于子查询结果中的某一个值     | ＜ALL            | 小于子查询结果中的所有值       |
| ＞＝ANY  ＞＝SOME                    | 大于等于子查询结果中的某一个值 | ＞＝ALL          | 大于等于子查询结果中的所有值   |
| ＜＝ANY  ＜＝SOME                    | 小于等于子查询结果中的某一个值 | ＜＝ALL          | 小于等于子查询结果中的所有值   |
| ＝ANY  ＝SOME                        | 等于子查询结果中的某一个值     | ＝ALL            | 等于子查询结果中的所有值       |
| ！＝ANY或＜＞ANY  ！＝SOME或＜＞SOME | 不等于子查询结果中的某一个值   | ！＝ALL或＜＞ALL | 不等于子查询结果中的任何一个值 |

### 带有EXISTS谓词的子查询

语法格式为：

EXISTS (子查询)

当且仅当子查询返回的集合存在元素，即非空，其值为真。

带有exists谓词的子查询不返回任何数据，只产生逻辑真值true或逻辑假值false，子查询给出列名无实际意义。

由于带exists谓词的相关子查询只关心内层查询是否有返回值，并不需要具体查询值，有时候是高效的方法。

e.g. 查询既订购了产品p01又订购了产品p07的顾客的cid。

```sql
select distinct cid from orders x 
where pid='p01' and exists
(select * from orders 
where cid=x.cid and pid='p07');
```

语法格式为：

NOT EXISTS (子查询)

e.g. 当且仅当子查询返回的集合不存在元素，即为空，其值为真。查询没有通过代理商a05订货的所有顾客的名字。

```sql
select distinct c.cname from customers c 
where not exists 
(select * from orders x
where c.cid=x.cid and x.aid='a05');
```

### 关于EXISTS子查询的说明：

1) 一些带EXISTS或NOT EXISTS谓词的子查询不能被其它形式的子查询等价替换。

2) 所有带IN谓词、比较运算符、SOME(ANY)和ALL谓词的子查询都能用带EXISTS谓词的子查询等价替换。

3) [NOT] EXISTS子查询的效率要优于连接查询和集合查询（IN谓词查询）。

## 4.3.5 复杂查询 

查询订购了所有产品的顾客的cid值。

<img src="./assets/image-20241205210007525.png" alt="image-20241205210007525" style="zoom:70%;" />

对于“订购了所有产品的顾客”，可以等价于“没有一个产品该顾客没有订购”，所以：

<img src="./assets/image-20241205210733089.png" alt="image-20241205210733089" style="zoom:70%;" />

第一步：用SQL语句描述反例：有一个产品我们的候选顾客没有订购；

`select pid from products x` 

`where not exists` 

 `(select * from orders y` 

 `where x.pid = y.pid and y.cid = ？.cid)`

第二步：用SQL语句描述不存在反例。

`not exists`

`(select pid from products x where not exists` 

`(select * from orders y` 

`where x.pid = y.pid and y.cid = ？.cid))`

第三步：完成该查询。

```sql
select c.cid from customers c
where not exists
(select pid from products x where not exists 
(select * from orders y
	where x.pid = y.pid and y.cid = c.cid))
```

对于需要用关系代数除法解决的查询问题，转换成SQL语句的一般形式为：

`Select …… where NOT EXISTS(select …… where NOT EXISTS(select …… ))；`

 查询被所有居住在New York的顾客订购的产品的pid。

`select pid from products p` 

`where not exists` 

`(select cid from customers c` 

`where c.city = 'new york' and not exists` 

`(select * from orders x` 

`where x.pid = p.pid and x.cid = c.cid));`

## 4.4 SQL的数据操纵功能

### 更新数据

将所有订货总金额超过2000的顾客的折扣率增加10%。

```sql
update customers 
set discnt=discnt*1.1 
where cid in 
	(select cid from orders 
	group by cid having sum(dollars)>2000);
```

### 删除数据

单表删除命令格式为：
DELETE FROM <表名> [WHERE<条件>]
【例45】 删除数据表agents中的居住在“New York”的所有代理商的记录。
`delete from agents  
where city = 'new york'`
【例46】 删除所有没有人订购的产品。
`delete from products
where pid not in (select pid from orders)`

删除表中所有数据
`delete from agents;` 
`delete`是逐行删除，速度极慢，不适合大量数据删除。
`TRUNCATE TABLE table_name;`
`TRUNCATE`删除所有数据，保留表结构，适合删除拥有大量数据的表
如使用InnoDB，在删除数据之前检查表中是否有可用的外键约束。如果外键约束指定DELETE CASCADE，则子表中的相应行也将被删除。否则将逐个删除行，遇到由子表中的行引用的行时，将停止并发出错误。
如果表没有任何外键约束，则TRUNCATE TABLE语句将删除该表并重新创建一个具有相同结构的新表

## 4.5视图

**视图(VIEW):**是从一个或几个基本表(或视图)导出的一个虚拟表。数据库中只存放了视图的定义。

视图中的数据依赖于原来表中的数据，一旦表中数据发生改变，视图中的数据也会发生改变。

**优点：**

提高安全性。  

重复利用SQL语句，简化操作。

逻辑数据独立性。

CREATE VIEW *view_name* [<*column_name*>[,< *column_name* >][ ,...n )] 

AS *select_statement* [WITH CHECK OPTION]

==WITH CHECK OPTION==：对视图进行更新操作时要保证更新的行满足视图查询语句中的条件表达式。

表和视图共享数据库中相同的名称空间，因此，数据库不能包含具有相同名称的表和视图。

创建一个视图custp01，列出订购了产品p01的顾客编号、姓名、产品编号、产品数量和总金额。

```sql
create view custp01 
As select c.cid,cname,pid,qty,dollars
from customers c, orders o
where c.cid = o.cid and o.pid ='p01';
```

建立一个视图，查询折扣率小于15的顾客信息。

```sql
create view cust1 as
select * from customers 
where discnt<15; 

create view cust2 as 
select * from customers 
where discnt<15 with check option; 
```

视图分为只读视图、可更新视图和可插入视图
如果视图包含以下任何内容，则该视图为**只读视图（不可更新）：**
`集合函数`
`DISTINCT`
`GROUP BY`
`HAVING`
`并集`
`非相关子查询对于 INSERT 失败，但可以UPDATE和DELETE。对于相关子查询，不允许使用任何数据更改语句。`
`某些连接`
`在子句中引用不可更新视图`
`使用临时表`

**可插入视图**
如果可更新视图还满足视图列的以下附加要求，则该视图是可插入的：
不能有重复的视图列名称。
该视图必须包含基表中没有缺省值的所有列。
视图列必须是简单的列引用。它们不能是表达式，例如：
3.14159 
col1 + 3 
UPPER(col2)

## 4.6 索引

索引是存储引擎用于快速找到记录的一种数据结构。

### 建立索引的优点

1. 大大加快数据的检索速度;
2. 创建唯一性索引，保证数据库表中每一行数据的唯一性;
3. 加速表和表之间的连接;
4. 在使用分组和排序子句进行数据检索时，可以显著减少查询中分组和排序的时间。

### 索引的缺点

1. 索引需要占物理空间。

2. 当对表中的数据进行增加、删除和修改的时候，索引也要动态的维护，降低了数据的维护速度。

### MySQL索引类型

根据索引的具体用途，在逻辑上分为 5 类：

1. 普通索引： MySQL 中最基本的索引类型，目的就是加快系统对数据的访问速度。允许在定义索引的列中插入重复值和空值。
   `create index indexname on tablename (字段名称);`
   `alert table tablename add index [索引的名字] (字段名);`
2. 唯一索引：索引列值必须唯一，允许有空值。
   `create UNIQUE index indexname on tablename (字段名称);`
   `alert table tablename add UNIQUE index [索引的名字] (字段名);`

3. 主键索引：一种特殊的唯一索引，不允许值重复或者为空。创建主键索引在创建表时使用 PRIMARY KEY ，不能使用 CREATE INDEX 语句创建。
   `CREATE TABLE tablename ([...], PRIMARY KEY (字段名) );`
   `ALTER TABLE tablename ADD PRIMARY KEY (字段名);`
4. 空间索引：是对空间数据类型GEOMETRY的字段建立的索引，使用 SPATIAL 关键字进行扩展。
   `create SPATIAL index indexname on tablename (字段名称);`
   `alert table tablename add SPATIAL index [索引的名字] (字段名);`

5. 全文索引：用来查找文本中的关键字，只能在 CHAR、VARCHAR 或 TEXT 类型的列上创建。对于大容量的数据表，生成全文索引非常消耗时间和硬盘空间。
   `CREATE FULLTEXT INDEX <索引的名字> ON tablename (字段名);`
   `ALTER TABLE tablename ADD FULLTEXT [索引的名字] (字段名);`

**从数据存储和索引键值逻辑关系划分：聚集（聚簇）索引、非聚集（聚簇）索引**
InnoDB的聚簇索引按照主键顺序构建 B+Tree结构。在叶子节点行记录和主键值紧凑地存储在一起。

InnoDB的表要求必须要有**聚簇索引：**

如果表定义了主键，则主键索引就是**聚簇索引**

如果表没有定义主键，则第一个非空unique列作为聚簇索引

否则InnoDB会建一个隐藏的row-id作为聚簇索引

**非聚集索引：**根据索引列构建 B+Tree结构。但在 B+Tree 的叶子节点中只存了索引列和主键的信息。

一个表可以创建多个非聚集索引。

**回表查询：**通过非聚集索引（InnoDB辅助索引）无法直接定位行记录，通常情况下，需要扫描两遍索引树。先通

过辅助索引定位主键值，然后再通过聚簇索引定位行记录，叫做回表查询，它的性能比扫一遍索引树低。

**索引覆盖：**只需要在一棵索引树上就能获取SQL所需的所有列数据，无需回表，速度更快，叫做索引覆盖。 实现

索引覆盖最常见的方法就是：将被查询的字段，建立成组合索引。



**一般来说，应该在这些列上创建索引：**

经常需要搜索的列上，可以加快搜索的速度；

在作为主键的列上；

经常用在连接的列上，这些列主要是一些外键，可以加快连接的速度；

经常需要根据范围进行搜索的列上创建索引；

如date>”20050101” and date< “20050131”；

经常需要排序的列上创建索引；

经常使用在WHERE子句中的列创建索引。

**一般来说，不应该创建索引的列：**

在查询中很少使用的列。

那些只有很少数据值的列也不应该创建索引。

定义为text, bit数据类型的列不应该创建索引。

当修改性能远远大于检索性能时，不应该创建索引。