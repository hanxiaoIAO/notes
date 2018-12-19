​	Docker，开源的应用容器引擎，用于打包应用以及依赖包，可移植到流行的 Linux 机器上，可实现虚拟化。容器完全使用沙箱机制，相互之间不会有接口。

## 简介

​	Docker 是基于 LXC 的高级容器引擎，基于 go 语言并遵从 Apache2.0 协议开源。

​	早期 boot2docker 以及 Docker for Windows 工具都是以虚拟机的形式在异构操作系统(Windows、macOS )上运行 Docker 。但本身基于 linux 的 Docker 不支持 Windows 应用。

​	后来，微软与 Docker 在14年宣布合作，

### LXC(Linux Container)

​	Linux Container 容器是一种内核虚拟化技术，可以提供轻量级的虚拟化，以便隔离进程和资源。LXC 在资源管理方面依赖于 Linux 内核的 cgroups 子系统， cgroups 子系统是 Linux 内核提供的一个基于进程组的资源管理的框架，可以为特定的进程组限定可以使用的资源。 LXC 在隔离控制方面依赖于 Linux 内核的namespace 特性，具体而言就是在 clone 时加入相应的 flag(NEWNS NEWPID等等)。。

