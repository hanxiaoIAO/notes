[toc]

## 查看/修改最大连接数

查看最大连接数

```mysql
show variables like 'max_connections';
```

修改最大连接数

> - 通过命令行修改。只在mysql当前服务进程有效，一旦mysql重启，又会恢复到初始状态。
>
>   ```mysql
>   set global max_connections=1000;
>   ```
>
> - 修改配置文件
>
>   修改MySQL配置文件my.ini 或 my.cnf的参数max_connections，然后重启MySQL。

## 远程访问

设置权限

```mysql
grant all privileges on *.* to 'root'@'%' identified by 'root' with grant option;
flush privileges;
```

查看my.cnf 

```ini
[mysqld]
bind-address = 0.0.0.0  # 表示允许任何主机登陆MySQL
```

