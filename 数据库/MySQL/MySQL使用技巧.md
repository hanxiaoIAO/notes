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

```mysql
show status like  'Threads%';
+-------------------+-------+
| Variable_name     | Value |
+-------------------+-------+
| Threads_cached    | 32    |
| Threads_connected | 10    |
| Threads_created   | 50    |
| Threads_rejected  | 0     |
| Threads_running   | 1     |
+-------------------+-------+

Threads_connected ：这个数值指的是打开的连接数.

Threads_running ：这个数值指的是激活的连接数，这个数值一般远低于connected数值.

Threads_connected 跟show processlist结果相同，表示当前连接数。准确的来说,Threads_running是代表当前并发数
```



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

