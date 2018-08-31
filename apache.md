linux环境下

apachectl -v 查看版本

三种启动方式
sudo service spache2 start 启动
sudo apache2ctl -k start 启动
sudo /etc/init.d/apache2 start

/var/log/apache2 日志位置

# 负载均衡
一般来说，负载均衡就是将客户端的请求分流给后端的各个真实服务器，达到负载均衡的目的。还有一种方式是用两台服务器，一台作为主服务器(Master)，另一台作为热备份(Hot Standby)，请求全部分给主服务器，
在主服务器当机时，立即切换到备份服务器，以提高系统的整体可靠性。

负载均衡需要启动几个模块 启动的命令为a2enmod 禁用命令为a2dismod
sudo a2enmod proxy proxy_ajp proxy_balancer proxy_connect proxy_ftp proxy_http lbmethod_byrequests
sudo a2enmod mod_lbmethod_bytraffic

mod_proxy提供代理服务器功能，mod_proxy_balancer提供负载均衡功能， mod_proxy_http让代理服务器能支持HTTP协议

a2enmod是属于apache2.2-common包下的一个工具，如没有这个命令
apt-get install apache2.2-common

修改配置 
sudo vi /etc/apache2/mods-enabled/proxy.conf
``` ProxyRequests Off  
<Proxy *>  
    Order deny,allow  
    Deny from all  
    #Allow from .your_domain.com  
</Proxy> 
```
修改配置 
sudo vi /etc/apache2/sites-available/000-default.conf
```ProxyRequests Off  
         Proxypass / balancer://proxy/  
         ProxyPassReverse / balancer://proxy/   
    <Proxy balancer://proxy>  
            Order Deny,Allow  
            Allow from all  
            BalancerMember http://1.1.11.127:8091  
            BalancerMember http://1.1.11.127:8092  
    </Proxy> 
```
# 调试
    SetHandler balancer-manager
    Order Deny,Allow
    Deny from all
    Allow from localhost
	用来监视负载均衡的工作情况的，调试时可以加上（生产环境中禁止使用！），然后访问 http://localhost/balancer-manager/ 即可看到负载均衡的工作状况。
	
# 热备份(Hot Standby)
热备份的实现很简单，只需添加 status=+H 属性，就可以把某台服务器指定为备份服务器：
``BalancerMember http://node-b.myserver.com:8080 status=+H``

# 负载均衡的三种形式
ProxySet lbmethod=byrequests 为实现负载均衡的方式，共有三种类型
#lbmethod=byrequests 按照请求次数均衡(默认) 
#lbmethod=bytraffic 按照流量均衡 
#lbmethod=bybusyness 按照繁忙程度均衡(总是分配给活跃请求数最少的服务器)

apache服务器和tomcat的连接方法其实有三种:JK、http_proxy和ajp_proxy