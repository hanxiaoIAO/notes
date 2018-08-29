# 常用操作以及概念
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
	quiet 内核启动的时候简化提示信息
	splash 启动的时候图形化进度
	nomodeset
		最新的内核已经把视频模式设置嵌入内核中，所以所有显卡硬件程序的指定时钟和寄存器当图形服务器启动时在内核进行而不是图形设备运行，这使得我们在启动时可以看到不闪的和高分辨率的好看的启动界面，但是，在某些视频卡它不能正常工作而现实黑屏，增加nomodeset参数则告诉内核不要加载显卡而用BIOS模式直到图形界面运行
## 变量
  设置变量   
	export 变量名=变量值  
  取变量  
	$变量名
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

