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

