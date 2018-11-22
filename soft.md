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

# redis
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

1.项目是通过外部.sh文件或.bat文件启动
　　tomcat的startup.bat/startuo.sh和shutdown.bat/shutdown.sh实质上还是调用catalina.bat/catalina.sh（主要是进行环境配置和调用catalina.bat/catalina.sh）
2.*/tomcat/conf/server.xml文件
​	 <Connector port="18089" protocol="HTTP/1.1" 
​               connectionTimeout="20000" 
​               redirectPort="18443" />
http 连接端口
3.*/tomcat/conf/tomcat-users.xml文件
​	需提前修改登陆名信息
​	<tomcat-users>
​		<user username="tomcat" password="tomcat" roles="manager-gui"/>
​	</tomcat-users>
4.java.lang.OutOfMemoryError: PermGen space

java.lang.OutOfMemoryError: PermGen space PermGen space的全称是Permanent Generation space,是指内存的永久保存区域, 这块内存主要是被JVM存放Class和Meta信息的,Class在被Loader时就会被放到PermGen space中, 它和存放类实例(Instance)的Heap区域不同,GC(Garbage Collection)不会在主程序运行期对 PermGen space进行清理，所以如果你的应用中有很多CLASS的话,就很可能出现PermGen space错误, 这种错误常见在web服务器对JSP进行pre compile的时候。如果你的WEB APP下都用了大量的第三方jar, 其大小超过了jvm默认的大小(4M)那么就会产生此错误信息了。
 解决方法： 手动设置MaxPermSize大小。修改TOMCAT_HOME/bin/catalina.sh 在“echo "Using CATALINA_BASE: $CATALINA_BASE"上面加入以下行： -Xms1024m  -Xmx2048m -XX:PermSize=512m -XX:MaxPermSize=376m
5.ps -ef |grep tomcat	查看tomcat进程
　　kill+进程编号结束掉
　　kill -s 9 进程编号强制结束进程
　　netstat -ntulp |grep 80   查看所有80端口使用情况。
7.bin目录下一般放二进制文件如：.exe，.dll等可执行文件
　　conf目录下一般放配置文件
　　lib目录下为库文件
　　logs目录下为错误日志
　　webapps目录下放要部署的程序，目录名可变，但需另行配置
　　work存放jsp文件编译后生成的文件　　问题：修改后的页面在tomcat运行的时候显示不了修改后的痕迹。做法：删除work目录下对应的项目文件夹，重新启动tomcat
8.linux ifconfig -a　查看端口号