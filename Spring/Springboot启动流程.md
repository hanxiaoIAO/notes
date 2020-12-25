## 参考

[监听Spring Boot的启动、停止、重启、关闭](http://blog.sina.com.cn/s/blog_70ae1d7b0102wfq2.html)

[ContextRefreshedEvent](https://blog.csdn.net/bwh0520/article/details/79935435)

[springboot项目启动成功后执行一段代码的两种方式](https://www.cnblogs.com/zuidongfeng/p/9926471.html)

## 监听Spring Boot的事件

继承 SmartApplicationListener 以监听 Springboot 事件

```java
@Component
public class SmartApplicationListenerImp implements SmartApplicationListener {
	public SmartApplicationListenerImp() {
		LoggerFactory.getLogger(getClass()).info("初始化 ApplicationRunner");
	}

	@Override
	public void onApplicationEvent(ApplicationEvent arg0) {
//		LoggerFactory.getLogger(getClass()).info("SmartApplicationListener dealWith:"+arg0.getClass().getName());
		System.out.println(arg0.getClass().getName());
	}

	@Override
	public boolean supportsEventType(Class<? extends ApplicationEvent> arg0) {
//		LoggerFactory.getLogger(getClass()).info("SmartApplicationListener supportsEventType:"+arg0.getName());
		return true;
	}

}
```

Web应用，打印监听到的事件


```
org.springframework.boot.web.servlet.context.ServletWebServerInitializedEvent

org.springframework.context.event.ContextRefreshedEvent

//study.demo.StartApplication              : Started StartApplication in 1.776 seconds (JVM running for 2.277)

org.springframework.boot.context.event.ApplicationStartedEvent

org.springframework.boot.availability.AvailabilityChangeEvent

//study.demo.config.ApplicationRunnerImpl  : ApplicationRunner  run args:org.springframework.boot.DefaultApplicationArguments@5d96bdf8

org.springframework.boot.context.event.ApplicationReadyEvent

org.springframework.boot.availability.AvailabilityChangeEvent
```

非 Web 应用，打印监听到的事件

```
org.springframework.context.event.ContextRefreshedEvent

//study.demo.StartApplication              : Started StartApplication in 0.841 seconds (JVM running for 1.227)

org.springframework.boot.context.event.ApplicationStartedEvent

org.springframework.boot.availability.AvailabilityChangeEvent

//study.demo.config.ApplicationRunnerImpl  : ApplicationRunner  run args:org.springframework.boot.DefaultApplicationArguments@718607eb

org.springframework.boot.context.event.ApplicationReadyEvent

org.springframework.boot.availability.AvailabilityChangeEvent

org.springframework.context.event.ContextClosedEvent
```

### 备注，存疑，实际使用 MVC 并未发现该现象

applicationontext和使用MVC之后的webApplicationontext会两次调用上面的方法，即系统会存在两个容器，一个是root application  context ,另一个就是我们自己的 projectName-servlet context（作为root application  context的子容器）。这种情况下，就会造成onApplicationEvent方法被执行两次。为了避免上面提到的问题，我们可以只在root application context初始化完成后调用逻辑代码，其他的容器的初始化完成，则不做任何处理，修改后代码  

```java
 @Override  
 public void onApplicationEvent(ContextRefreshedEvent event) {  
 	if(event.getApplicationContext().getParent() == null){// root application context 没有parent，他就是老大.  
 		//需要执行的逻辑代码，当spring容器初始化完成后就会执行该方法。  
 	}  
 }  
```

## 初始化 bean 之前

实现 BeanDefinitionRegistryPostProcessor 接口

## 为bean提供了初始化方法的方式

实现 InitializingBean 接口，会在初始化 bean 之后执行该 bean 中的 afterPropertiesSet 方法

## 启动成功后执行一段代码的两种方式

- 实现ApplicationRunner接口
- 实现CommandLineRunner接口

两种实现方式的不同之处在于run方法中接收的参数类型不一样

## SpringbootApplication 源码分析

```java
public class SpringApplication {
    public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
        this.resourceLoader = resourceLoader;
		Assert.notNull(primarySources, "PrimarySources must not be null");
		this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
		//3. 设置 webApplicationType(web 应用类型) 
        // 判断逻辑：WebApplicationType.deduceFromClasspath() 
        // 值:1.NONE 非 web 应用	2.SERVLET SERVLET 类型 web 应用 3.REACTIVE REACTIVE 类型 web 应用
		//4. 加载所有classpath下面的META-INF/spring.factories ApplicationContextinitializer
		//5. 加载所有classpath下面的META-INF/spring.factories ApplicationListener
		//6. 设置 mainApplicationClass 应用 main 方法所在的类
        // 判断逻辑 deduceMainApplicationClass()
    }
    
    public ConfigurableApplicationContext run(String... args) {
        //1. StopWatch 计时工具 开始计时
        //2. 设置系统属性,即使没有检测到显示器,也允许启动.[](https://www.cnblogs.com/wangxuejian/p/10603034.html)
        //3. 获取SpringApplicationRunListeners。SpringApplicationRunListener的集合
        //   SpringApplicationRunListener 会在调用 ApplicationListener
        //   默认实现类 org.springframework.boot.context.event.EventPublishingRunListener，封装了不同的事件
        //4. listeners.starting()
        //5. 参数封装，也就是在命令行下启动应用带的参数，如--server.port=9000
        //6. 准备环境 ConfigurableEnvironment
        //7. 打印Banner
        //8. 创建ApplicationContext
        //9. 用户自定义异常处理回调接口。解析ＭETA-INF/spring.factories文件下接口的实现类，基于ＳＰＩ可插拔
        //10. 准备 ApplicationContext
        //11.刷新 ApplicationContext
		//12.停止计时，打印启动完成信息
        //13.listeners.started
        //14.callRunners
        //15.listeners.running
    }
}
```

