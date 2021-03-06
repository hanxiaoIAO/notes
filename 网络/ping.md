[toc]

# ping

## 概念

Ping(Packer Internet Groper)，因特网包探索器，用于测试网络连接量的程序。Ping 是工作在 TCP/IP 网络体系结构中间层的一个命令，主要向特定的目的主机发动 ICMP(Internet Control Message Protocol 因特网报文控制协议) Echo 请求报文，测试目的站是否可达及了解其有关状态。

Ping 用于确定本地主机是否能与另一台主机成功交换(发送与接收)数据包，再根据返回的信息，就可以推断 TCP/IP 参数是否设置正确，以及运行是否正常、网络是否通畅等。每个发送的数据包最多等待一秒，需要注意的是，Ping 成功并不一定代表 TCP/IP 配置正确，有可能还要执行大量的本地主机与远程主机的数据包交换，才能确定 TCP/IP 配置的正确性。如果执行 Ping 成功而网络仍无法使用，那么问题很可能出在网络系统的软件配置方面。Ping 成功只保证当前主机与目的主机之间存在一条连通的物理路径。

## 检查网络故障

典型的检测次序及对应的可能故障：

- Ping 127.0.0.1 -- 这个 Ping 命令被送到本地计算机的 IP 软件，该命令永不退出该计算机。如果没有做到这一点，就标识 TCP/IP 的安装或运行存在某些最基本的问题。

- Ping 本机 IP -- 这个命令被送到你计算机所配置的 IP 地址，你的计算机始终对该 Ping 命令做出应答，如果没有，则表示本地配置或安装存在问题。出现此问题时，局域网用户请断开网络电缆，然后重新发送该命令。如果重新发送该命令，本命令正确，则表示另一台计算机可能配置了相同的 IP 地址。

- Ping 局域网内的其他 IP -- 这个命令应该离开你的计算机，经过网卡及网络电缆到达其他计算机，再返回。收到会送应答表明本地网络中的网卡和载体运行正确。但如果收到0个回答迎送，那么表示子网掩码(进行子网分割时，将 IP 地址的网络部分与主机部分分开的代码)不正确或网卡配置错误或电缆系统有问题。

- Ping 网关 IP -- 这个命令如果应答正确，表示局域网中的网关路由器正在运行并能够做出应答。

- Ping 远程 IP -- 如果收到 4 个应答，表示成功的使用了缺省网关。对于拨号上网用户则表示能够成功的访问 Interner (但不派驻 ISP 的DNS 会有问题)

- Ping localhost -- localhost 是个操作系统的网络保留名，它是 127.0.0.1 的别名，每台计算机都应该能将改名字转换成该地址。如果没有做到这一条，则表示文件(/Windows/host)中存在问题。

- Ping www.baidu.com --  对这个域名执行 Ping 命令，你的计算机必须先将域名转换成 IP地址，通常通过 DSN 服务器。如果这里出现故障，则表示 DSN 服务器的 IP 地址配置不正确或 DSN 服务器有故障。、

  如果上面所列出的所有 Ping 命令都能正常运行，那么计算机可以本地和远程通信。但是，这些命令的成功并不代表所有的网络配置都没有问题，例如，某些子网掩码错误就可能无法用这些方法检测到。

## 影响因素

   	在物理链路连通和路由设置正确的情况下，使用 Ping 命令仍然 Ping 不通，可能有以下几个问题：

  1. 网线刚查到交换机上就 Ping 网关，忽略了生成树的收敛时间。当然，较新的交换机都支持快速生成树，或者有的管理员干脆把用户端口 (accessport) 的生成树协议关掉，问题就解决了。
  2. 不管中间经过了多少个节点，只要有节点(包括端节点)对 ICMP 信息包进行了过滤， Ping 不通是正常的。做常见的就是防火墙行为。
  3. 某些路由器端口是不允许用户 Ping 的。
  4. 网络因设备间的超时，造成 ICMP 报文无法在缺省时间(2s)内收到。超时的原因有：主机没有足够的时间和资源来响应；
  5. 引入 Nat 的场合会造成单向 Ping 通。NAT 可以起到隐蔽内部地址的作用，当由内 Ping 外时，可以 Ping 通是因为 Nat 表的映射关系存在，当由外发起 Ping 内网主机时，就无从查找路由器的 NAT 访问列表了。 

## 用途

1. 用来检测网络的连通情况和分析网络速度
2. 根据域名得到服务器IP
3. 根据 PIng 返回的 TTL 值来判断对方所使用的操作系统及数据包经过路由器数量

## 返回信息解释

直接ping IP地址或网关，ping通常会显示出bytes=32；time<1ms；TTL=128

bytes 值： 数据包大小，也就是字节。

time 值： 响应时间，时间越小，说明连接这个地址速度越快

TTL 值：Time To Live,表示DNS记录在DNS服务器上存在的时间，它是IP协议包的一个值，告诉路由器该数据包何时需要被丢弃。可以通过Ping返回的TTL值大小，粗略的判断目标系统的类型是Windows还是Unix、Linux。TTL虽然从字面上看是存活的时间，但实际上TTL是IP数据包在计算机网络中可以转发的最大跳转数。TTL字段由IP数据包的发送者设置，在IP数据包从源到目的地的这个转发路径上，没经过一个路由器，路由器都会修改这个TTL字段值，具体的做法是把该TTL的值减1，然后再将IP包转发出去。如果在IP包到达目的IP之前，TTL减少为0，路由器将会丢弃收到的TTL=0的IP包并向IP包的发送者发送 ICMP time exceeded消息。TTL的作用主要是避免IP包在网络中的无限循环和收发，节省网络资源，并能使IP 包的发送者收到告警消息。

默认情况下，Linux系统的TTL值为64或255，WindowsNT/2000/XP系统的TTL值为128，Windows98系统的TTL值为32，UNIX主机的TTL值为255。

因此一般TTL值：

100~130ms之间，Windows系统 ；

240~255ms之间，UNIX/Linux系统。

## 其他用途

ping -a IP:将地址解析为主机名

ping -n count IP:在默认情况下，一般都只发送4个数据包，通过这个命令可以自己定义发送的个数

ping -l size IP:在默认的情况下Windows的ping发送的数据包大小为32byt，最大能发送65500byt

ping -r count IP:在“记录路由”字段中记录传出和返回数据包的路由，探测经过的

路由个数，但最多只能跟踪到9个路由。