# SecureCRT
SecureCRT是一款支持SSH（SSH1和SSH2）的终端仿真程序，简单地说是Windows下登录UNIX或Linux服务器主机的软件。

SFTP
sftp -P端口号   grid@IP 
cd 路径                        更改远程目录到“路径” 
lcd 路径                       更改本地目录到“路径” 
ls [选项] [路径]               显示远程目录列表 
lls [选项] [路径]              显示本地目录列表 
put 本地路径                   上传文件 
get 远程路径                   下载文件 

put -r

#redis
1.访问redis根目录    cd  /usr/local/redis-2.8.19
2.登录redis：redis-cli -h 127.0.0.1 -p 6379
3.查看所有key值：keys *
4.删除指定索引的值：del key
5.清空整个 Redis 服务器的数据：flushall 
6.清空当前库中的所有 key：flushdb 

Redis 启动,采用指定配置文件的启动方式：
redis-server /home/erp10/redis-2.8.24/redis.conf &

# tomcat 
配置apr模式
sudo apt-get install libapr1-dev

./configure --with-apr=/usr/bin --with-java-home=/home/erp1/jdk1.8.0_linux
make
sudo make install

    <Connector port="8092" protocol="org.apache.coyote.http11.Http11AprProtocol"
               connectionTimeout="20000"
                maxThreads="300"
               redirectPort="8443"/>
	
	-Xdebug -agentlib:jdwp=transport=dt_socket,address=6000,server=y,suspend=n \
	-Djava.library.path=/usr/local/apr/lib/ "
