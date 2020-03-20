[toc]



## 远程访问

设置权限

```mysql
grant all privileges on *.* to 'root'@'%' identified by 'root' with grant option;
flush privileges;
```

查看my.cnf 

```
[mysqld]
bind-address = 0.0.0.0  # 表示允许任何主机登陆MySQL
```

## 导入导出

### 导入



### 导出

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

## mysql8.0+

```
Driver=com.mysql.cj.jdbc.Driver
URL=jdbc:mysql://localhost:3306/wshh?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC
```

### ERROR:authentication plugin caching_sha2

mysql 8.0 默认使用 caching_sha2_password 身份验证机制 —— 从原来的 mysql_native_password 更改为 caching_sha2_password。客户端不支持新的加密方式。

从 5.7 升级 8.0 版本的不会改变现有用户的身份验证方法，但新用户会默认使用新的 caching_sha2_password 。

方法一，修改新用户的密码和加密方式

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
```

方法二，使用以前的密码加密方式，就修改文件 /etc/my.cnf

```
[mysqld]
default_authentication_plugin=mysql_native_password
```



## linux下安装

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

## linux 环境中 /tmp/mysql.sock 不存在的解决方法

my.cnf中修改了socket的默认路径，处理方法：

```shell
ln -s /usr/local/mysql/mysql.sock /tmp/mysql.sock 
```

