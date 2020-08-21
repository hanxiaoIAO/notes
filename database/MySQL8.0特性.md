[toc]

## 驱动包更换

驱动包用的是mysql-connector-java-8.0.11.jar 

新版的驱动类改成了com.mysql.cj.jdbc.Driver 

```
Driver=com.mysql.cj.jdbc.Driver
URL=jdbc:mysql://localhost:3306/wshh?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC
```

## 必须指定时区(ServerTimeZone)

新版必须指定时区，否则会报错。

常用时区

```
serverTimezone=UTC //全球标准时间 和国内有8个小时的时差，北京时区也就是东八区，领先UTC八个小时。
serverTimezone=GMT%2B8 //北京时间东八区 有的地方识别不了GMT%2B8。
serverTimezone=Asia/Shanghai //上海时间
```



## 客户端连接报错ERROR:authentication plugin caching_sha2

客户端不支持新的加密方式。

mysql 8.0 默认使用 caching_sha2_password 身份验证机制 —— 从原来的 mysql_native_password 更改为 caching_sha2_password。

从 5.7 升级 8.0 版本的不会改变现有用户的身份验证方法，但新用户会默认使用新的 caching_sha2_password 。

解决方案：

方法一，修改新用户的密码和加密方式

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
```

方法二，使用以前的密码加密方式，就修改文件 /etc/my.cnf

```
[mysqld]
default_authentication_plugin=mysql_native_password
```

## 关闭连接对象时SSL异常

之后还有一个在关闭连接对象时会产生的一个无关紧要的报错，不解决也可以正常使用，但是占据控制台的大量篇幅，导致使用体验极差：

```
javax.net.ssl.SSLException
MESSAGE: closing inbound before receiving peer's close_notify
```

MySQL 8.0开始，数据库URL需要设置是否使用SSL安全连接，在URL后面加上参数useSSL=false即可，多个参数键值对中间用&隔开：

```
url=jdbc:mysql://localhost:3306/test?serverTimezone=GMT%2B8&useSSL=false
```

## 重启应用后，应用连接数据库时报错：Public Key Retrieval

重启应用后，应用连接数据库时报错：

```
java.sql.SQLNonTransientConnectionException: Public Key Retrieval is not allowed
```

在URL后加上allowPublicKeyRetrieval=true即可

```
url=jdbc:mysql://localhost:3306/test?serverTimezone=GMT%2B8&useSSL=false&allowPublicKeyRetrieval=true
```

## getTables()方法默认返回所有库的表

8.0及以上版本的驱动默认将nullCatalogMeansCurrent的默认值由true改为了false，如果使用DatabaseMetaData类的对象调用getTables方法，就会返回所有库的表，而非在url参数中指定的数据库（本例中数据库名为test）。此时就需要手动在参数中指定nullCatalogMeansCurrent值为true：

```
url=jdbc:mysql://localhost:3306/test?serverTimezone=GMT%2B8&useSSL=false&useSSL=false&allowPublicKeyRetrieval=true&nullCatalogMeansCurrent=true
```