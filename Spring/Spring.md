spring boot默认开启了静态文件的配置，任何放在static文件夹下的资源都是静态文件。引用静态文件时以/或者前缀不加任何定位符，都会去static文件夹下查找。
Thymeleaf模版默认会使用templatess作为视图文件下

application.yml配置文件：

用法一、文件放在resources下

```
server:
  port: 8080
spring:
  mvc:
    view:
      suffix: .html
    static-path-pattern: /**
  resources:
    static-locations: classpath:/templates/,classpath:/static/
```

用法二、文件放在任意路径下

```
server:
  port: 8080
spring:
  mvc:
    view:
      suffix: .html
    static-path-pattern: /**
  resources:
    static-locations: file:D:\gzzg\springboot-example08\templates\,file:D:\gzzg\springboot-example08\static
```

