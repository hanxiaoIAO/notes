[toc]

# 常用操作以及概念

## 查看版本

```shell
uname -a
```

linux查看版本当前操作系统内核信息

```shell
cat /etc/redhat-release
```

Linux查看版本当前操作系统发行版信息

## 快捷键

1. Tab：命令和文件名补全；
2. Ctrl+C：中断正在运行的程序；
3. Ctrl+D：结束键盘输入（End Of File，EOF）

## 进程
### 进程查看--ps 命令
ps 支持三种语法风格
+ 示例1<br>ps -e     显示所有进程
<br>![](linux_files/1.jpg)
+ 示例2<br>pe -ef    显示所有进程(f:更详细的进程信息,包含父进程的PID)
<br>![](linux_files/2.jpg)
+ 示例3<br>ps -aux   显示所有进程<br>(a:显示现行终端机下的所有程序，包括其他用户的程序<br>u:以用户为主的格式来显示程序状况<br>x:显示所有程序，不以终端机来区分)
<br>![](linux_files/3.jpg)

ps常利用一个管道符号将进程导向到grep去查找特定的进程
eg.  ps-ef|grep java

### 杀进程--kill 命令
kill <-信息编号> 进程号

kill可将指定的信息送至程序。预设的信息为SIGTERM(15),可将指定程序终止。若仍无法终止该程序,可使用SIGKILL(9)信息尝试强制删除程序。  
只有第9种信号(SIGKILL)才可以无条件终止进程,其他信号进程都有权利忽略。

kill -l 可列出所有信号名称  
常用信号：  
+ HUP     1    终端断线
+ INT     2    中断(同 Ctrl + C)
+ QUIT    3    退出(同 Ctrl + \)
+ TERM   15    终止
+ KILL    9    强制终止
+ CONT   18    继续(与STOP相反,fg/bg命令)
+ STOP   19    暂停(同 Ctrl + Z)

### 概念
一个进程，包括代码、数据和分配给进程的资源。fork（）函数通过系统调用创建一个与原来进程几乎完全相同的进程,也就是两个进程可以做完全相同的事，但如果初始参数或者传入的变量不同，两个进程也可以做不同的事。
正常情况下，子进程是通过父进程创建的，子进程在创建新的进程。子进程的结束和父进程的运行是一个异步过程,即父进程永远无法预测子进程 到底什么时候结束。 当一个 进程完成它的工作终止之后，它的父进程需要调用wait()或者waitpid()系统调用取得子进程的终止状态。

#### 孤儿进程
一个父进程退出，而它的一个或多个子进程还在运行，那么那些子进程将成为孤儿进程。孤儿进程将被init进程(进程号为1)所收养，并由init进程对它们完成状态收集工作。

#### 僵尸进程
一个进程使用fork创建子进程，如果子进程退出，而父进程并没有调用wait或waitpid获取子进程的状态信息，那么子进程的进程描述符仍然保存在系统中。这种进程称之为僵死进程。

#### 守护进程
守护进程（Daemon Process），也就是通常说的 Daemon 进程（精灵进程），是 Linux中的后台服务进程。它是一个生存期较长的进程，通常独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件。守护进程是个特殊的孤儿进程，这种进程脱离终端，为什么要脱离终端呢？之所以脱离于终端是为了避免进程被任何终端所产生的信息所打断，其在执行过程中的信息也不在任何终端上显示。由于在 linux 中，每一个系统与用户进行交流的界面称为终端，每一个从此终端开始运行的进程都会依附于这个终端，这个终端就称为这些进程的控制终端，当控制终端被关闭时，相应的进程都会自动关闭。

## 文件
### 移动、复制、删除
cp,mv,rm

### 解压缩
#### tar命令

主操作模式
+ -c: 建立压缩档案
+ -x：解压
+ -t：查看内容
+ -r：向压缩归档文件末尾追加文件
+ -u：更新原压缩包中的文件

必选的参数
-f: 这个参数是最后一个参数，后面只能接档案名。

压缩选项:  
-a, --auto-compress&emsp;使用归档后缀名来决定压缩程序  
-j, --bzip2&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;通过 bzip2 过滤归档  
-J, --xz&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;通过 xz 过滤归档  
&emsp;--lzip&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;通过 lzip 过滤归档  
&emsp;--lzma&emsp;&emsp;&emsp;&emsp;&emsp;通过 xz 过滤归档  
&emsp;--lzop
&emsp;--no-auto-compress     不使用归档后缀名来决定压缩程序  
-z, --gzip, --gunzip, --ungzip   通过 gzip 过滤归档  
-Z, --compress, --uncompress   通过 compress 过滤归档

-v：显示所有过程
-O：将文件解开到标准输出

## nohup &
nohup :不挂断地运行命令,标准输出和标准错误默认重定向到当前目录下的nohup.out文件中  
&     :在后台运行

command &      :将任务放到后台,关闭xshell,对应的任务也跟着停止.
nohup command  :将sh test.sh任务放到后台,关闭标准输入,终端不再能够接收任何输入(标准输入),重定向标准输出和标准错误,即使关闭xshell退出当前session依然继续运行.  
nohup command &: test.sh任务放到后台,但是依然可以使用标准输入,终端能够接收任何输入,重定向标准输出和标准错误,即使关闭xshell退出当前session依然继续运行。

## grub
启动的时候按ESC进入grub启动界面，按E可临时编辑启动设置信息
  /ect/default/grub 启动信息

  GRUB_CMDLINE_LINUX_DEFAULT属性
​	quiet 内核启动的时候简化提示信息
​	splash 启动的时候图形化进度
​	nomodeset
​		最新的内核已经把视频模式设置嵌入内核中，所以所有显卡硬件程序的指定时钟和寄存器当图形服务器启动时在内核进行而不是图形设备运行，这使得我们在启动时可以看到不闪的和高分辨率的好看的启动界面，但是，在某些视频卡它不能正常工作而现实黑屏，增加nomodeset参数则告诉内核不要加载显卡而用BIOS模式直到图形界面运行
## 变量
  设置变量   
​	export 变量名=变量值  
  取变量  
​	$变量名
## 时间
date 查看当前时间
sudo ntpdate cn.pool.ntp.org  时间和网络的服务器上的时间同步

## 求助

### 1. --help

指令的基本用法与选项介绍。

### 2. man

man 是 manual 的缩写，将指令的具体信息显示出来。

当执行`man date`时，有 DATE(1) 出现，其中的数字代表指令的类型，常用的数字及其类型如下：

| 代号 | 类型 |
| :--: | -- |
| 1 | 用户在 shell 环境中可以操作的指令或者可执行文件 |
| 5 | 配置文件 |
| 8 | 系统管理员可以使用的管理指令 |

### 3. info

info 与 man 类似，但是 info 将文档分成一个个页面，每个页面可以进行跳转。

### 4. doc

/usr/share/doc 存放着软件的一整套说明文件。

## VIM 三个模式

- 一般指令模式（Command mode）：VIM 的默认模式，可以用于移动游标查看内容；
- 编辑模式（Insert mode）：按下 "i" 等按键之后进入，可以对文本进行编辑；
- 指令列模式（Bottom-line mode）：按下 ":" 按键之后进入，用于保存退出等操作。

![](linux_files/4.jpg)

在指令列模式下，有以下命令用于离开或者保存文件。

| 命令 | 作用 |
| :--: | :--: |
| :w | 写入磁盘|
| :w! | 当文件为只读时，强制写入磁盘。到底能不能写入，与用户对该文件的权限有关 |
| :q | 离开 |
| :q! | 强制离开不保存 |
| :wq | 写入磁盘后离开 |
| :wq!| 强制写入磁盘后离开 |

## 获取文件内容

### 1. cat

取得文件内容。

```html
# cat [-AbEnTv] filename
-n ：打印出行号，连同空白行也会有行号，-b 不会
```

### 2. tac

是 cat 的反向操作，从最后一行开始打印。

### 3. more

和 cat 不同的是它可以一页一页查看文件内容，比较适合大文件的查看。

### 4. less

和 more 类似，但是多了一个向前翻页的功能。

### 5. head

取得文件前几行。

```html
# head [-n number] filename
-n ：后面接数字，代表显示几行的意思
```

### 6. tail

是 head 的反向操作，只是取得是后几行。

### 7. od

以字符或者十六进制的形式显示二进制文件。

## 文件权限
### 修改权限

可以将一组权限用数字来表示，此时一组权限的 3 个位当做二进制数字的位，从左到右每个位的权值为 4、2、1，即每个权限对应的数字权值为 r : 4、w : 2、x : 1。

```html
# chmod [-R] xyz dirname/filename
```

示例：将 .bashrc 文件的权限修改为 -rwxr-xr--。

```html
# chmod 754 .bashrc
```

也可以使用符号来设定权限。

```html
# chmod [ugoa]  [+-=] [rwx] dirname/filename
- u：拥有者
- g：所属群组
- o：其他人
- a：所有人
- +：添加权限
- -：移除权限
- =：设定权限
```

示例：为 .bashrc 文件的所有用户添加写权限。

```html
# chmod a+w .bashrc
```

### 文件默认权限

- 文件默认权限：文件默认没有可执行权限，因此为 666，也就是 -rw-rw-rw- 。
- 目录默认权限：目录必须要能够进入，也就是必须拥有可执行权限，因此为 777 ，也就是 drwxrwxrwx。

可以通过 umask 设置或者查看文件的默认权限，通常以掩码的形式来表示，例如 002 表示其它用户的权限去除了一个 2 的权限，也就是写权限，因此建立新文件时默认的权限为 -rw-rw-r--。

### 目录的权限

文件名不是存储在一个文件的内容中，而是存储在一个文件所在的目录中。因此，拥有文件的 w 权限并不能对文件名进行修改。

目录存储文件列表，一个目录的权限也就是对其文件列表的权限。因此，目录的 r 权限表示可以读取文件列表；w 权限表示可以修改文件列表，具体来说，就是添加删除文件，对文件名进行修改；x 权限可以让该目录成为工作目录，x 权限是 r 和 w 权限的基础，如果不能使一个目录成为工作目录，也就没办法读取文件列表以及对文件列表进行修改了。


## 关机、重启
重启命令：
1、reboot
2、shutdown -r now 立刻重启(root用户使用)
3、shutdown -r 10 过10分钟自动重启(root用户使用) 
4、shutdown -r 20:35 在时间为20:35时候重启(root用户使用)
如果是通过shutdown命令设置重启的话，可以用shutdown -c命令取消重启

关机命令：
1、halt   立即停止系统，需要人工关闭电源
2、poweroff  立即停止系统，并且关闭电源
3、shutdown -h now 立刻关机(root用户使用)
4、shutdown -h 10 10分钟后自动关机
如果是通过shutdown命令设置关机的话，可以用shutdown -c命令取消重启

## netstat
netstat命令各个参数说明如下：

　　-t : 指明显示TCP端口

　　-u : 指明显示UDP端口

　　-l : 仅显示监听套接字(所谓套接字就是使应用程序能够读写与收发通讯协议(protocol)与资料的程序)

　　-p : 显示进程标识符和程序名称，每一个套接字/端口都属于一个程序。

　　-n : 不进行DNS轮询，显示IP(可以加速操作)
netstat -ntlp   //查看当前所有tcp端口·

netstat -ntulp |grep 80   //查看所有80端口使用情况·

netstat -an | grep 3306   //查看所有3306端口使用情况·

## top



# Ubuntu

## 设置自启动
在/etc/init.d/ 下以管理员权限新建文件
使用以下模板修改启动脚本的内容

```shell
#!/bin/bash
### BEGIN INIT INFO
#
# Provides:  location_server
# Required-Start:   $local_fs  $remote_fs
# Required-Stop:    $local_fs  $remote_fs
# Default-Start:    2 3 4 5
# Default-Stop:     0 1 6
# Short-Description:    initscript
# Description:  This file should be used to construct scripts to be placed in /etc/init.d.
#
### END INIT INFO

## Fill in name of program here.
PROG="location_server"
PROG_PATH="/opt/location_server" ## Not need, but sometimes helpful (if $PROG resides in /opt for example).
PROG_ARGS="" 
PID_PATH="/var/run/"

start() {
    if [ -e "$PID_PATH/$PROG.pid" ]; then
        ## Program is running, exit with error.
        echo "Error! $PROG is currently running!" 1>&2
        exit 1
    else
        ## Change from /dev/null to something like /var/log/$PROG if you want to save output.
        $PROG_PATH/$PROG $PROG_ARGS 2>&1 >/var/log/$PROG &
    $pid=`ps ax | grep -i 'location_server' | sed 's/^\([0-9]\{1,\}\).*/\1/g' | head -n 1`

        echo "$PROG started"
        echo $pid > "$PID_PATH/$PROG.pid"
    fi
}

stop() {
    echo "begin stop"
    if [ -e "$PID_PATH/$PROG.pid" ]; then
        ## Program is running, so stop it
    pid=`ps ax | grep -i 'location_server' | sed 's/^\([0-9]\{1,\}\).*/\1/g' | head -n 1`
    kill $pid

        rm -f  "$PID_PATH/$PROG.pid"
        echo "$PROG stopped"
    else
        ## Program is not running, exit with error.
        echo "Error! $PROG not started!" 1>&2
        exit 1
    fi
}

## Check to see if we are running as root first.
## Found at http://www.cyberciti.biz/tips/shell-root-user-check-script.html
if [ "$(id -u)" != "0" ]; then
    echo "This script must be run as root" 1>&2
    exit 1
fi

case "$1" in
    start)
        start
        exit 0
    ;;
    stop)
        stop
        exit 0
    ;;
    reload|restart|force-reload)
        stop
        start
        exit 0
    ;;
    **)
        echo "Usage: $0 {start|stop|reload}" 1>&2
        exit 1
    ;;
esac
```

其中，PROG变量为所要运行的可执行程序的名称， PROG_PATH为可执行文件所在的目录，PROG_ARGS为执行程序的各个参数。 
需要注意的是，在stop()函数中利用kill命令结束进程，有两种方法可以处理，一种是利用进程名称，如“location_server”查找相应的进程号，然后调用kill <进程号>结束进程，另一种方法是直接使用killall <进程名称>，但是在这种方法下，本启动脚本的名称不能和可执行文件的名称相同，不然的话，stop后会出现”Terminated“说明脚本也被kill掉。也可以在start()中将进程号存储在.pid文件中，然后在stop()中从文件中取得要结束的进程号，但是这样的话，还想获得的进程号会比实际进程号小2，现在还不知道是什么原因。

添加删除服务

```shell
添加： sudo update-rc.d 服务名 defaults
删除：sudo update-rc.d -f 服务名 remove
```

启动、关闭、重启服务

```shell
/etc/init.d/服务名 start
/etc/init.d/服务名 stop
/etc/init.d/服务名 start
```

### 其他相关内容

[在Ubuntu 16.04 中将应用添加到系统服务中](https://blog.csdn.net/u013685902/article/details/78452482)

## 重装VIM

```shell
# 卸载
sudo apt-get remove vim-common 
# 安装
sudo apt-get install vim 
sudo apt-get install vim-gtk 
```
# shell脚本备忘

1.把文件重命名为以日期结尾

```shell
export time=`date +%H:%M:%S`
mv -b -S $time webapps/yigo/WEB-INF/classes/logs/* webapps/yigo/WEB-INF/classes/log.bak 
```

2.读取文本内容，然后把内容赋值给变量，然后进行字符串处理

```shell
export dataline=$(cat /root/data/data.txt)
echo $dataline
```



# centOS 7

1、firewalld的基本使用

启动： systemctl start firewalld

关闭： systemctl stop firewalld

查看状态： systemctl status firewalld 

开机禁用  ： systemctl disable firewalld

开机启用  ： systemctl enable firewalld

2.配置firewalld-cmd

查看版本： firewall-cmd --version

查看帮助： firewall-cmd --help

显示状态： firewall-cmd --state

查看所有打开的端口： firewall-cmd --zone=public --list-ports

更新防火墙规则： firewall-cmd --reload

查看区域信息:  firewall-cmd --get-active-zones

查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0

拒绝所有包：firewall-cmd --panic-on

取消拒绝状态： firewall-cmd --panic-off

查看是否拒绝： firewall-cmd --query-panic

 

那怎么开启一个端口呢

添加

firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）

重新载入

firewall-cmd --reload

查看

firewall-cmd --zone= public --query-port=80/tcp

删除

firewall-cmd --zone= public --remove-port=80/tcp --permanent

## systemctl
systemctl是CentOS7的服务管理工具中主要的工具，它融合之前service和chkconfig的功能于一体。

启动一个服务：systemctl start firewalld.service  
关闭一个服务：systemctl stop firewalld.service  
重启一个服务：systemctl restart firewalld.service  
显示一个服务的状态：systemctl status firewalld.service  
在开机时启用一个服务：systemctl enable firewalld.service  
在开机时禁用一个服务：systemctl disable firewalld.service  
查看服务是否开机启动：systemctl is-enabled firewalld.service  
查看已启动的服务列表：systemctl list-unit-files|grep enabled  
查看启动失败的服务列表：systemctl --failed  

## 设置自启动
service 脚本在/etc/systemd/system下
***.service 服务脚本
范本：

```shell
[Unit]
Description=
 
[Service]
ExecStart=
ExecReload=
ExecStop=
 
[Install]
WantedBy=multi-user.target
```
ExecStart 制定的脚本需要开头加上#!/bin/sh


