​	Docker，开源的应用容器引擎，用于打包应用以及依赖包，可移植到流行的 Linux 机器上，可实现虚拟化。容器完全使用沙箱机制，相互之间不会有接口。

## 简介

​	Docker 是基于 LXC 的高级容器引擎，基于 go 语言并遵从 Apache2.0 协议开源。

​	早期 boot2docker 以及 Docker for Windows 工具都是以虚拟机的形式在异构操作系统(Windows、macOS )上运行 Docker 。但本身基于 linux 的 Docker 不支持 Windows 应用。

​	后来，微软与 Docker 在14年宣布合作，为传统的 Windows 应用程序的容器化改造提供了直接的支持。15 年推出为容器优化的 Windows Nano Server。16 年 Windows 10 的年度更新上，正式提供了 Windows 容器的开发环境。17 年推出 Windows Server 1709 版本包含了 Windows 容器，意味着这项技术可以用于生产环境。

### LXC(Linux Container)

​	Linux Container 容器是一种内核虚拟化技术，可以提供轻量级的虚拟化，以便隔离进程和资源。LXC 在资源管理方面依赖于 Linux 内核的 cgroups 子系统， cgroups 子系统是 Linux 内核提供的一个基于进程组的资源管理的框架，可以为特定的进程组限定可以使用的资源。 LXC 在隔离控制方面依赖于 Linux 内核的namespace 特性，具体而言就是在 clone 时加入相应的 flag(NEWNS NEWPID等等)。

## Docker

### Docker与传统虚拟化的不同

如图，容器是在操作系统层面上实现虚拟化，直接服用本地的操作系统，而传统的方式则是在硬件层面实现。

![virtualization](Docker/virtualization.png)

![docker](Docker/docker.png)

### Docker引擎

Docker 是一个c/s结构的应用，主要组件如图：

![docker engine components flow](Docker/engine-components-flow.png)

## 操作

操作以ubuntu为例

### 安装

ubuntu 在 14.04 版本之后，将提供了一份安装脚本，挂在网站上，用户可以用以下命令安装 Docker

```shell
curl -sSL https://get.docker.com/ | sh
```

### 添加用户组

避免每次都需要sudo运行

```shell
sudo groupadd docker
sudo gpasswd -a 当前登录用户名  docker
重启docker服务：service docker restart,再退出当前登录，重新登录
```

## Docker 构建 —— Dockerfile

​	Dockerfile 是一个用于包含用于组合镜像的命令的文本文档。Docker 通过读取 Dockerfile 中的指令自动生成镜像。

​	Docker Builder 命令用于从 Dockerfile 中构建镜像。

```shell
docker build -f /home/fendo/Dockerfile
```

