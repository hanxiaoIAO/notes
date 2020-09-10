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