[toc]

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

