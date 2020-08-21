 ### 1. java.net.SocketException: Unrecognized Windows Sockets **error**: **10106**: create

​		解决方案：

​			1，以管理员身份打开命令提示符
​        	2，输入 netsh winsock reset  
​        	3，重启电脑就ok了

​	winsock是Windows网络编程接口，winsock工作在应用层，它提供与底层传输协议无关的高层数据传输编程接口 netsh winsock reset 是把它恢复到默认状态  

### 2. CMD执行命令报错：不是内部或外部命令，也不是可运行程序

在变量里面添加如下内容，（**解释：变量是以分号为一条的，如有重复的条目就不再添加）**

%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;C:\Windows\SysWOW64
