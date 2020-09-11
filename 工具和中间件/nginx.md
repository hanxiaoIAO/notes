[toc]

# linux系统下目录结构

- 所有的配置文件都在/etc/nginx下，并且每个虚拟主机已经安排在了/etc/nginx/sites-available下
- 程序文件在/usr/sbin/nginx
- 日志放在了/var/log/nginx中
- 并已经在/etc/init.d/下创建了启动脚本nginx
- 默认的虚拟主机的目录设置在了/var/www/nginx-default

# Nginx操作命令

- 安装：sudo apt-get install nginx
- 启动：sudo nginx start
- 重启：sudo nginx -s reload
- 停止：sudo nginx -s stop

# 负载均衡配置

修改配置 

```shell
sudo vi /etc/nginx/sites-available/default
```



```
upstream ERP{
	server 1.1.11.127:8091;
	server 1.1.11.127:8092;
	server 1.1.11.128:8091;
	server 1.1.11.128:8092;
}

server{
	listen 8081;
	location / {
        proxy_next_upstream off;
		proxy_pass http://ERP;
	}
}
```





upstream ERP{
​	server 1.1.11.127:8091;
​	server 1.1.11.127:8092;
​	server 1.1.11.128:8091;
​	server 1.1.11.128:8092;
}

server{
​	listen 8081;
​	location / {
​        proxy_next_upstream off;
​		proxy_pass http://ERP;
​	}
}

# ip_hash

​	nginx采用ip_hash的轮询方法,每个ip在一定时间内会被固定的后端服务器,这样我们不用解决session共享问题。

```
upstream ERP{
	ip_hash;
	server 1.1.11.127:8091;
	server 1.1.11.127:8092;
	server 1.1.11.128:8091;
	server 1.1.11.128:8092;
}
```



# 其他
[nginx proxy_set_header设置、自定义header](https://blog.csdn.net/bao19901210/article/details/52537279)



# 参数

## types_hash_max_size 1024;

types_hash_max_size影响散列表的冲突率。types_hash_max_size越大，就会消耗更多的内存，但散列key的冲突率会降低，检索速度就更快。types_hash_max_size越小，消耗的内存就越小，但散列key的冲突率可能上升。
 默认为1024

## client_max_body_size 1024M;

 上传文件大小限制,客户端上传的body的最大值。超过最大值就会发生413(Request Entity Too Large)错误。
 默认为1m，最好改大一点。