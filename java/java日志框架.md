[toc]

## 常见的日志框架和关系

目前主流的日志框架主要包括：JUL, Log4j,  Log4j2, Conmmons-logging, Slf4j, Logback。

其中 Conmmons-logging 和 Slf4j 属于日志的接口，遵循面向接口编程的原则。

JUL, Log4j,  Log4j2, Logback 则属于日志实现。

Log4j2 与 Log4j1 发生了很大的变化，基本所有核心全都重构了一遍，因此Log4j2 不兼容 Log4j1。

比较常用的组合使用方式是 Slf4j 与 Logback 组合使用，Commons Logging 与 Log4j 组合使用。

    ## 框架简介

### JUL

JUL 全称 java.util.logging.Logger，JDK 自带的日志系统，从 JDK1.4 就有了。JUL 是自带具体实现的。

JUL 不需要导入任何依赖，JDK 中已包含 JUL 的接口和具体实现。

#### 用法

```
import java.util.logging.Logger;
...
Logger logger = Logger.getLogger("test");

```

相同名字的 Logger 全局唯一

配置文件默认使用 jre/lib/logging.properties，日志级别默认为 INFO

### Log4j 和  Log4j2

Log4j 是 Apache 的一个开放源代码项目，通过使用 Log4j ，我们可以控制日志信息输送的目的地是控制台、文件、数据库等。我们也可以控制每一条日志的输出格式；通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。它是一个里程碑式的框架，它定义的 Logger、Appender、Level 等概念如今已经被广泛使用。**已经停用，使用Log4j2**

Log4j2 是 Log4j 和 Logback 的改进版。日志的吞吐量、性能比 Log4j 提高10倍，并解决了一些死锁的bug，而且配置更加简单灵活。

Log4j 有 7 种不同的log 级别，按照等级从低到高依次为：TRACE、DEBUG、INFO、WARN、ERROR、FATAL、OFF。如果配置为 OFF 级别，表示关闭 log。

包含三个主要的组件：Logger、appender、Layout。

#### 依赖

```xml
<dependency>
   <groupId>org.apache.logging.log4j</groupId>
   <artifactId>log4j-core</artifactId>
   <version>2.13.3</version>
</dependency>
<dependency>
   <groupId>org.apache.logging.log4j</groupId>
   <artifactId>log4j-api</artifactId>
   <version>2.13.3</version>
</dependency>
```

如果使用 SpringBoot 开发的话，会看到在 SpringBoot 的 jar 包中已经包含了 Log4j2 的  log4j-api.jar 包，但是，这里的 log4j-api 是为了将 Log4j2 的接口适配到 Slf4j 上而存在的，如果想单独使用  Log4j2，则需要单独引入 log4j-api.jar 并且将 log4j-to-slf4j 下的 log4j-api 排除掉。

 log4j-api 包含的是 .class 一堆接口，实际使用需要 log4j-core，log4j-core 包含 .class 与 .java 也就是源码。

#### 用法

单独使用

```
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
...
private static Logger logger = LogManager.getLogger("log4jFile");
```

配置文件: 在 src/main/resources 下构建 log4j2.xml 配置文件

Log4j2 配置文件后缀名只能为".xml",".json"或者".jsn"。

系统选择配置文件的优先级(从先到后)如下：

> a. classpath下的名为log4j2-test.json 或者log4j2-test.jsn的文件.
>
> b. classpath下的名为log4j2-test.xml的文件.
>
> c. classpath下名为log4j2.json 或者log4j2.jsn的文件.
>
> d. classpath下名为log4j2.xml的文件.

### Conmmons-logging

Jakarta Commons Logging，简称 JCL，是 Apache 提供的一个通用日志门面接口 API，可以让应用程序不再依赖于具体的日志实现工具。

 Commons-logging 包中对其它一些日志工具，包括 Log4J、Avalon LogKit、JUL 等，进行了简单的包装，可以让应用程序在运行时，直接将 JCL API 打点的日志适配到对应的日志实现工具中。

 Commons-logging 通过动态查找的机制，在程序运行时自动找出真正使用的日志库。这一点与 Slf4j 不同，Slf4j 是在编译时静态绑定真正的 Log 实现库。

#### 依赖

```xml
<dependency>
   <groupId>commons-logging</groupId>
   <artifactId>commons-logging</artifactId>
   <version>1.2</version>
</dependency>
```

这个框架已经停止更新了。

### Logback

Logback 是一个“ 可靠、通用、快速而又灵活的 Java 日志框架 ”。

Logback 的核心对象：Logger、Appender、Layout。

> Logger：日志的记录器，把它关联到应用的对应的 context 上后，主要用于存放日志对象，也可以定义日志类型、级别。Logger 对象一般多定义为静态常量.
>
>  Appender：用于指定日志输出的目的地，目的地可以是控制台、文件、远程套接字服务器、 MySQL、 PostreSQL、Oracle 和其他数据库、 JMS 和远程 UNIX Syslog 守护进程等。
>
>  Layout：负责把事件转换成字符串，格式化的日志信息的输出。

#### 依赖

```xml
<dependency>
   <groupId>ch.qos.logback</groupId>
   <artifactId>logback-classic</artifactId>
   <version>1.2.3</version>
</dependency>
<dependency>
   <groupId>ch.qos.logback</groupId>
   <artifactId>logback-core</artifactId>
   <version>1.2.3</version>
</dependency>
<dependency>
   <groupId>ch.qos.logback</groupId>
   <artifactId>logback-access</artifactId>
   <version>1.2.3</version>
</dependency>
```

在 SpringBoot 下是不需要引入 Logback 的，因为在 spring-boot-starter-logging 中已经内置了该依赖。

 Logback当前分成三个模块：logback-core，logback- classic和logback-access。

>  logback-core 模块为其他两个模块奠定了基础。
>
>  logback-classic 模块可以被同化为 Log4j 的显着改进版本。logback-classic 本身实现了  slf4j-api，因此我们可以在 logback 和其他日志框架（如 Log4j  或java.util.logging（JUL））之间来回切换。
>
>  logback-access 模块与 Servlet 容器（如 Tomcat 和 Jetty）集成，以提供 HTTP 访问日志功能。

#### 用法

在 src/main/resources 下添加 logback.xml。

代码中一般默认搭配 SLF4J 使用。

### SLF4J

SLF4J 全称 The Simple Logging Facade for Java，简单日志门面，这个不是具体的日志解决方案，而是通过门面模式提供一些 Java Logging API，类似于 JCL。

#### Slf4j 的一些桥接包

- slf4j-log4j12：可以使用log4j进行底层日志输出。
- slf4j-jdk14：可以使用JUL进行日志输出。

#### 依赖

```xml
<dependency>
   <groupId>org.slf4j</groupId>
   <artifactId>slf4j-api</artifactId>
   <version>1.7.25</version>
</dependency>
```

一般不会导入 slf4j-api jar 包，而是导入针对另一个具体实现的 jar 包。

#### 用法

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.slf4j.MDC;

private static Logger logger = LoggerFactory.getLogger("test");

MDC.put("logFileName","Slf4j2Logback");
logger.info("{}", i + " thread-1" + System.lineSeparator());
MDC.remove("logFileName");
```

MDC ( Mapped Diagnostic Contexts )，它是一个线程安全的存放诊断日志的容器。用于在分布式系统中区分区分日志到底是那个请求输出。

Logback配置：

```xml
<appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender"> 
  <layout>
    <Pattern>%X{first} %X{last} - %m%n</Pattern>
  </layout> 
</appender>
```

##  参考

[Java中各种日志框架整理](https://blog.csdn.net/weixin_43999395/article/details/109504092)