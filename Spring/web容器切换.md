## 简介

springboot-web 中除了默认使用的 tomcat 服务器 `spring-boot-starter-tomcat`，还有两款比较常用的服务器，分别是 jetty  `spring-boot-starter-jetty` 和 undertow `spring-boot-starter-undertow`。jetty和undertow都是基于NIO实现的高并发轻量级的服务器，支持servlet3.1和websocket。

## 服务器的切换

切换其他 HTTP 服务器分两步，排除默认的 tomcat 依赖，包含所要使用的依赖。

```xml
排除：
<!-- Srping Boot Web 支持 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <!-- 排除掉 内置 Tomcat -->
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>

依赖jetty:
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>

依赖undertow:
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-undertow</artifactId>
</dependency>
```

