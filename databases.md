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

# MYSQL

## linux

1. 自启动(CentOS 7)

   ```shell
   cp support-files/mysql.server /etc/init.d/mysql
   chkconfig --add mysql
   chkconfig mysql on
   ```

   error

   /etc/init.d/mysql: 没有那个文件或目录

   文件是DOS格式，转成Unix格式即可


2. 安装libaio.so.1

   ```shell
   rpm -ivh libaio-0.3.107-10.el6.x86_64.rpm
   ```

3. 启动

   ```shell
   systemctl start mysqld
   ```

4. 用户

   检查mysql组和用户是否存在：

   ```shell
   cat /etc/group | grep mysql
   cat /etc/passwd| grep mysql
   ```

   如无，执行添加：

   ```shell
   groupadd mysql
   useradd -r -g mysql mysql
   ```

   // useradd -r参数表示mysql用户是系统用户，不可用于登录系统

   用户授权：

   ```shell
   chown -R mysql mysql/
   chgrp -R mysql mysql/
   ```

## 导入导出

```
mysqldump -u用户名 -p密码 数据库名 > 导出的文件名
```

error:

```
mysqldump: Got error: 2002: Can't connect to local MySQL server through socket '/tmp/mysqld.sock' (2) when trying to connect
```

原因是 mysql的存储目录更改了，需要加上-h127.0.0.1就好了

```
mysqldump -h127.0.0.1 -u用户名 -p密码 数据库名 > 导出的文件名
```

# ORACLE

 步骤一：  删除user

drop user ×× cascade(有删除权限)
select 'drop table '||table_name||';' from cat where table_type='TABLE'（没有删除权限）
说明： 删除了user，只是删除了该user下的schema objects，是不会删除相应的tablespace的。


步骤二： 删除tablespace

DROP TABLESPACE tablespace_name INCLUDING CONTENTS AND DATAFILES;

创建表空间语句：

create tablespace user_data    datafile 'D:\ a.dbf' size 50m   autoextend on  next 50m maxsize 20480m   extent management local;

创建表空间内的用户：

create user username identified by password   default tablespace user_data;

给用户授予权限  ：

grant connect,resource,dba to username;

SQL code
--删除空的表空间，但是不包含物理文件
drop tablespace tablespace_name;
--删除非空表空间，但是不包含物理文件
drop tablespace tablespace_name including contents;
--删除空表空间，包含物理文件
drop tablespace tablespace_name including datafiles;
--删除非空表空间，包含物理文件
drop tablespace tablespace_name including contents and datafiles;
--如果其他表空间中的表有外键等约束关联到了本表空间中的表的字段，就要加上CASCADE CONSTRAINTS
drop tablespace tablespace_name including contents and datafiles CASCADE CONSTRAINTS;


      1、设置表空间自动扩展与否

alter database datafile 文件路径 autoextend off；取消自动扩展

alter database datafile 文件路径 autoextend on；设置自动扩展

2、设置默认表空间

alter database default tablespace XXX;   整个数据库的，新建用户时不指定表空间则会默认这个。

alter user tanyixiu default tablespace smilespace; 只更改这个用户的.

3、查看用户默认表空间

select username,default_tablespace from dba_users where username='XXX'；

4、表空间更名

alter tablespace XXX rename to YYY;

5、更改表空间文件路径

    在線移
    
    1).alter tablespace tablespace_name offline; 
    
    2).os下copy d:\oradata\ datafilename to G:\oradata\datafilename 
    
    3).alter tablespace tablespace_name rename datafile 'd:\oradata\ datafilename' to 'G:\oradata\datafilename';
    
    4).alter tablespace tablespace_name online;
    
    不在線移
    
    1).startup mount
    
    2).os下copy d:\oradata\ datafilename to G:\oradata\datafilename 
    
    3).alter tablespace tablespace_name rename datafile 'd:\oradata\ datafilename' to 'G:\oradata\datafilename';
    
    4).alter database open





该命令在“开始菜单>>运行>>CMD”中执行（windows）
一、数据导出（exp.exe）
1、将数据库orcl完全导出，用户名system，密码accp，导出到d:\daochu.dmp文件中
​	exp system/accp@orcl file=d:\daochu.dmp full=y
​	
2、将数据库orcl中scott用户的对象导出
​	exp scott/accp@orcl file=d:\daochu.dmp  owner=(scott)
​	
3、将数据库orcl中的scott用户的表emp、dept导出
​	exp scott/accp@orcl file= d:\daochu.dmp tables=(emp,dept)

4、将数据库orcl中的表空间testSpace导出
​	exp system/accp@orcl file=d:\daochu.dmp tablespaces=(testSpace)

二、数据导入（imp.exe）
1、将d:\daochu.dmp 中的数据导入 orcl数据库中。
​	imp system/accp@orcl file=d:\daochu.dmp full=y

2、如果导入时，数据表已经存在，将报错，对该表不会进行导入；加上ignore=y即可，表示忽略现有表，在现有表上追加记录。
​	imp scott/accp@orcl file=d:\daochu.dmp  full=y  ignore=y

3、将d:\daochu.dmp中的表emp导入
imp scott/accp@orcl file=d:\daochu.dmp tables=(emp)