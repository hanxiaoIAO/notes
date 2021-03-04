### 云服务

> - **IaaS**：基础设施服务，Infrastructure-as-a-service
> - **PaaS**：平台服务，Platform-as-a-service
> - **SaaS**：软件服务，Software-as-a-service

### SSH

SSH(Secure Shell)，由IETF网络小组制定，为建立在应用层基础上的安全协议。SSH是目前较可靠的，专为远程登录会话和其他网络服务器提供安全性的协议。

### 正向代理与反向代理

[简介](正向代理与反向代理简介.md)

### 分布式与集群

[简介](分布式与集群简介.md)

### epoll and kqueue

- [ ] TODO

[参考文档](https://www.cnblogs.com/FG123/p/5256553.html)

[参考文档](https://www.cnblogs.com/linganxiong/p/5583415.html)

### 磁盘阵列 RAID

> 磁盘阵列(Redundant Arrays of Independent Drives，RAID)，有“独立磁盘构成的具有冗余能力的阵列”之意。
>
> ​	磁盘阵列是由很多价格较便宜的，组合成一个容量巨大的磁盘组，利用个别磁盘提供数据所产生加成效果提升整个磁盘系统效能。利用这项技术，将数据切割成许多区段，分别存放在各个硬盘上。
>
> ​	磁盘阵列还能利用同位检查（Parity Check）的观念，在数组中任意一个硬盘故障时，仍可读出数据，在数据重构时，将数据经计算后重新置入新硬盘中。

### typescript

>TypeScript是一种由微软开发的自由和开源的编程语言。它是JavaScript的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。
>
>TypeScript扩展了JavaScript的语法，所以任何现有的JavaScript程序可以不加改变的在TypeScript下工作。TypeScript是为大型应用的开发而设计，而编译它时产生 JavaScript 以确保兼容性。
>
>TypeScript 支持为已存在的 JavaScript 库添加类型信息的头文件，扩展了它对于流行的库如 jQuery，MongoDB，Node.js 和 D3.js 的好处。

### 绿色设计

> 在产品整个生命周期内，着重考虑产品环境属性(可拆卸性，可回收性，可维护性，可重复利用性等)，并将其作为设计目标，在满足环境目标要求的同时，保证产品应有的功能、使用寿命、质量等要求。
>
> 软件工程中，对象之间的耦合度就是对象之间的依赖性，对象之间的耦合度越改，维护成本越高。
>
> 解耦即可以理解为降低耦合度。
>
> 架构的目的就是为了实现软件的模块化，高内聚、低耦合。

### 架构

[B/S与C/S架构	三层架构	MVC架构](BS、CS、三层、MVC.md)

### Java

#### java 不可变类

>不变类的意思是创建该类的实例后，该实例的实例变量是不可改变的。满足以下条件则可以成为不可变类：
>
>1. 使用private和final修饰符来修饰该类的成员变量
>2. 提供带参的构造器用于初始化类的成员变量；
>3. 仅为该类的成员变量提供getter方法，不提供setter方法，因为普通方法无法修改fina修饰的成员变量；
>4. 如果有必要就重写Object类 的hashCode()和equals()方法，应该保证用equals()判断相同的两个对象其Hashcode值也是相等的。

#### FatJar

FatJar 又称作 uber-Jar，是包含所有依赖的 Jar 包。Jar 包中嵌入了除 java 虚拟机以外的所有依赖。FatJar 是一个 all-in-one Jar 包。FatJar 技术可以让那些用于最终发布的 Jar 便于部署和运行。

[三种打包方式](https://www.jianshu.com/p/a7bd1f89f29f)

### CI/CD

CI: 持续集成 Continuous Integration

CD: 持续交付 Continuous Delivery

[详细](https://zhuanlan.zhihu.com/p/42286143)

### AD(Active Directory)

活动目录，微软Windows Server中，负责架构中大型网路环境的集中式目录管理服务（Directory Services）。它处理了在组织中的网路物件，物件可以是**计算机，用户，群组，组织单元（OU）**等等，只要是在Active Directory结构定义档（schema）中定义的物件，就可以储存在Active Directory资料档中，并利用Active Directory Service Interface来存取。

[详细](https://www.cnblogs.com/IFire47/p/6672176.html)

## 键盘 KeyCode

[键盘 KeyCode](https://www.cnblogs.com/shyy/archive/2012/04/09/2453029.html)

## Jenkins

java语言开发，用于监控持续重复的工作，包括：持续的软件版本发布/测试项目，监控外部调用执行的工作。

[中文官网](http://www.jenkins.org.cn/)

## RPC

RPC是远程过程调用（Remote Procedure Call）的缩写形式。