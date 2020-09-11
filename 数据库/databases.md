[TOC]



# SQL

## 事务ACID特性

### I(isolation)隔离 

隔离性是指，多个用户的并发事务访问同一个数据库时，一个用户的事务不应该被其他用户的事务干扰，多个并发事务之间要相互隔离。 
并发的事务可能造成其他事务：读脏，不可重复读，幻读 
按SQL92标准，InnoDB实现四种不同事务的隔离级别：读未提交，读提交，可重复读，序列化/串行化 
不同事务的隔离级别，实际上是一致性与并发性的一个平衡和折衷 

[innodb并发](https://blog.csdn.net/z50L2O08e2u4afToR9A/article/details/82186189)

[innodb Select阻塞insert](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651961471&idx=1&sn=da257b4f77ac464d5119b915b409ba9c&chksm=bd2d0da38a5a84b5fc1417667fe123f2fbd2d7610b89ace8e97e3b9f28b794ad147c1290ceea&scene=21#wechat_redirect)

[innode 意向锁](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651961461&idx=1&sn=b73293c71d8718256e162be6240797ef&chksm=bd2d0da98a5a84bfe23f0327694dbda2f96677aa91fcfc1c8a5b96c8a6701bccf2995725899a&scene=21#wechat_redirect)

## hint语句

​	用于优化一个sql的执行计划

# SQL 语法和报错

## merge语句

​	在SQL Server、Oracle数据库中可用，MySQL、PostgreSQL中不可用。
​	MERGE是Oracle9i新增的语法，用来合并UPDATE和INSERT语句。在Oracle 10g之前，merge语句支持匹配更新和不匹配插入两种简单的用法，在10g中Oracle对merge语句做了增强，增加了条件选项和DELETE操作。
​	通过MERGE语句，根据一张表（原数据表，source table）或子查询的连接条件对另外一张（目标表，target table）表进行查询，连接条件匹配上的进行UPDATE，无法匹配的执行INSERT。这个语法仅需要一次全表扫描就完成了全部工作，执行效率要高于INSERT+UPDATE。

​	merge语法

```sql
MERGE [hint] INTO [schema ] table [t_alias]
USING [schema ]{ table | view | subquery } [t_alias]
ON ( condition )
WHEN MATCHED THEN merge_update_clause
WHEN NOT MATCHED THEN merge_insert_clause;
```

## MySQL报错：Data truncated for column

原因:

更新字段长度超过列的长度

在修改主键时，如果表中有数据或者设置主键的那一列数据为NULL

## mysql遇见Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggre的问题

MySQL 5.7.5及以上功能依赖检测功能。如果启用了ONLY_FULL_GROUP_BY  SQL模式（默认情况下），MySQL将拒绝选择列表，HAVING条件或ORDER BY列表的查询引用在GROUP  BY子句中既未命名的非集合列，也不在功能上依赖于它们。（5.7.5之前，MySQL没有检测到功能依赖关系，默认情况下不启用ONLY_FULL_GROUP_BY。有关5.7.5之前的行为的说明，请参见“MySQL 5.6参考手册”。）

解决方法一：

打开navcat，

用sql查询：

select @@global.sql_mode

查询出来的值为：

ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

去掉ONLY_FULL_GROUP_BY，重新设置值。

set @@global.sql_mode 
 =’STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION’;


解决方法二：

成功的步骤：

iterm打开

sudo vim /etc/mysql/conf.d/mysql.cnf

滚动到文件底部复制并粘贴

[mysqld] 
 sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

到文件的底部

保存并退出输入模式

sudo service mysql restart

重启MySQL。 
 完成！

## 修改字段长度

alter table <表名> alter column <字段名> 新类型名(长度)

informax数据库修改字段语法为

alter table 表名 modify 字段名 varchar(200)

## mysql的表复制及其表之间的数据转移

1.复制表结构及数据到新表 
CREATE TABLE 新表 SELECT * FROM 旧表 


2.只复制表结构到新表 
CREATE TABLE 新表 SELECT * FROM 旧表 WHERE 1=2 
即:让WHERE条件不成立. 


3.复制旧表的数据到新表(假设两个表结构一样) 
INSERT INTO 新表 SELECT * FROM 旧表 


4.复制旧表的数据到新表(假设两个表结构不一样) 
INSERT INTO 新表(字段1,字段2,.......) SELECT 字段1,字段2,...... FROM 旧表 



