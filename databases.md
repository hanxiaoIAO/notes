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


