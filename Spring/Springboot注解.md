## 装配 bean

### @Component

用来装配bean，主要用于标注业务层组件，通过注解的方式将该类加入到spring 中进行管理。

如果是 Web 应用且采用了经典的三层分层结构的话，持久层、业务层、控制层分别采用 @Repository、@Service 和 @Controller。

@Configuration 用于定义配置类

四者是和 @Component 是等价的，是 @Component 的别名。

```java
@Component
public class UserService {
   User login(String username,String password){
   	
   }
}
```

### @Bean

@Bean注解告诉Spring这个方法将会返回一个对象，这个对象要注册为Spring应用上下文中的bean。通常方法体中包含了最终产生bean实例的逻辑。

@Bean 和 @Component 功能相同，区别在于一个注解类，一个注解方法。

### @Import

@Import 用来装配第三方包中的类。

@Import的用法：

> 1. 直接填class数组方式
>
>    用法：
>
>    ```java
>    @Import({ 类名.class , 类名.class... })
>    @Component
>    //@Component为了确保TestDemo被Spring扫描到，也可以使用其他做法
>    //TestDemo 中如果有用@Bean装备的bean，也会同样被扫描到（对于较低的SpringBoot,用@Configuration注解的类才会扫描类中装配的bean）
>    public class TestDemo {
>    
>    }
>    ```
>
> 2. ImportSelector方式
>
>    用法：
>
>    ```java
>    public class Myclass implements ImportSelector {
>        @Override
>        public String[] selectImports(AnnotationMetadata annotationMetadata) {
>            return new String[]{"com.hanxiao.MyService"};//返回需装配的类名数组，可以返回空数组但是不能返回null。
>        }
>    }
>    
>    @Import(Myclass.class)
>    @Component
>    //Myclass不会被装配，MyClass中定义的类会被装配
>    public class TestDemo {
>    
>    }
>    ```
>
> 3. ImportBeanDefinitionRegistrar方式
>
>    用法:
>
>    ```java
>    public class Myclass implements ImportBeanDefinitionRegistrar {
>    //该实现方法默认为空
>        @Override
>        public void registerBeanDefinitions(AnnotationMetadata annotationMetadata, BeanDefinitionRegistry registry) {
>          registry.registerBeanDefinition("MyService", new RootBeanDefinition(MyService.class));
>        }
>    }
>    
>    @Import(Myclass.class)
>    @Component
>    //Myclass不会被装配，MyClass中定义的类会被装配
>    public class TestDemo {
>    
>    }
>    ```
>
>    

### @ComponentScan

默认扫描注解的配置类所在的包。

参数：

> value： 用于指定包的路径，进行扫描
>
> basePackages： 用于指定包的路径，进行扫描。和 value 是一样的
>
> basePackageClasses：用于指定某个类的包的路径进行扫描
>
> nameGenerator：bean的名称的生成器
>
> scopeResolver：
>
> scopedProxy：
>
> resourcePattern：
>
> useDefaultFilters：是否开启对@Component，@Repository，@Service，@Controller的类进行检测
>
> includeFilters：包含的过滤条件，参数为 Filter注解 数组
>
> excludeFilters：排除的过滤条件，参数为 Filter注解 数组
>
> lazyInit：

#### @Filter

@ComponentScan 的参数 includeFilters 和 excludeFilters 的值类型

@Filter 中参数 FilterType 的取值：

> ANNOTATION：按照注解规则，过滤被指定注解标记的类；
>
> ASSIGNABLE_TYPE：按照给定的类型；
>
> ASPECTJ：按照ASPECTJ表达式；
>
> REGEX：按照正则表达式
>
> CUSTOM：自定义规则；

### @ComponentScans

ComponentScan 数组

### @Autowired

用来注入 bean，可以写在方法上，也可以写在字段上。默认情况下必须要求依赖对象必须存在，如果允许 null 值，可以设置 required 属性。@Autowired(required=false)

### @Qualifier

当你创建多个具有相同类型的 bean 时，并且想要用一个属性只为它们其中的一个进行注入，在这种情况下，你可以使用 @Qualifier 注释和 @Autowired 注释通过指定哪一个真正的 bean 将会被注入来消除混乱。也可以直接使用 @Resource 。

### @Inject 和 @Named

等同于 @Autowired 和 @Qualifier。区别在于这两个注解时 javax 提供的，JSR330 (Dependency Injection for Java)中的规范。

### @Resource

@Resource的作用相当于@Autowired 只不过@Autowired按byType自动注入， 而@Resource默认按 byName自动注入。

@Resource有两个属性是比较重要的，分是name和type，Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。

@Resource注入顺序:

> 如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常 
>
> 如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常。
>
> 如果指定了type，则从上下文中找到类型匹配的唯一bean进行装配，找不到或者找到多个，都会抛出异常。
>
> 如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则按照类型进行匹配，如果匹配则自动注入。

### @Scope

用来配置 spring bean 的作用域，它标识 bean 的作用域。 默认值是单例。

>singleton:单例模式,全局有且仅有一个实例 
>
>prototype:原型模式,每次获取Bean的时候会有一个新的实例
>
>request:request表示该针对每一次HTTP请求都会产生一个新的bean，同时该bean仅在当前HTTP request内有效
>
>session:session作用域表示该针对每一次HTTP请求都会产生一个新的bean，同时该bean仅在当前HTTP session内有效
>
>global session:只在portal应用中有用，给每一个 global http session 新建一个Bean实例

### @Required

适用于bean属性setter方法。受影响的bean属性必须在配置时进行填充。

### @DependsOn

控制bean加载顺序

### @Lazy

延迟加载bean。容器启动不创建对象，第一次获取Bean的时候创建对象。

### @Configuration

Spring3.0+，@Configuration用于定义配置类，可替换xml配置文件。被注解的类内部包含有一个或多个被@Bean注解的方法，这些方法将会被AnnotationConfigApplicationContext或AnnotationConfigWebApplicationContext类进行扫描，并用于构建bean定义，初始化Spring容器。

**注意**：@Configuration注解的配置类有如下要求：

1. @Configuration不可以是final类型；
2. @Configuration不可以是匿名类；
3. 嵌套的configuration必须是静态类。

## web 相关

### @Controller

标识该类是 Spring MVC Controller 处理器，用来处理创建处理 http 请求的对象。

```java
@Controller
public class TestController {
        @RequestMapping("/hello")
        public String hello(Map<String,Object> map){
            return "hello";
        }
}
```

### @RestController

定义的控制器所有方法默认返回的都是 @ResponseBody 的方法, 都会将返回值转换为JSON。**注意：**@RestController=@Controller+@ResponseBody

### @ResponseBody

设置了 @ResponseBody 以后，如果控制器方法返回了Java Bean 对象，则这个JavaBean会被转换为 JSON 对象， 放到响应的正文中发送浏览器，而且响应的 ContentType是 application/json, 表示JSON类型数据。

### @RequestMapping

定义在类上：提供初步的请求映射信息，相当于 WEB 应用的根目录。

定义在方法上：提供进一步的戏份映射信息，相当于类定义处的 URL。

### @GetMapping

和 @RequestMapping(method = RequestMethod.GET)等价的，为了简化 RequestMapper。专门用于处理Get 请求。

### @PostMapping

和 @RequestMapping(method = RequestMethod.Post)等价的，为了简化 RequestMapping。专门用于处理 Post 请求。

### @RequestParam

用于将请求参数区数据映射到功能处理的参数上。

如果接口传递过来的参数名和接收的不一致，也可以定义要接收的传递参数名。

```java
public Resp test(@RequestParam Integer id){
        return Resp.success(customerInfoService.fetch(id));
}
public Resp test(@RequestParam(value="userId") Integer id){
    return Resp.success(customerInfoService.fetch(id));
}
```

### @ModelAttribute

[详细用法和范例](https://www.jianshu.com/p/741490df48fa)

### @SessionAttributes

默认情况下Spring MVC将模型中的数据存储到request域中。当一个请求结束后，数据就失效了。如果要跨页面使用，就需要使用到session。而@SessionAttributes注解就可以使得模型中的数据存储一份到session域中。

当需要清除session当中的值得时候，我们只需要在controller的方法中传入一个SessionStatus的类型对象 通过调用setComplete方法就可以清除了。

参数： names：这是一个字符串数组。里面应写需要存储到session中数据的名称。 types：根据指定参数的类型，将模型中对应类型的参数存储到session中 value：和names是一样的。

```java
 @Controller
 @SessionAttributes(value={"names"},types={Integer.class})
 public class ScopeService {
         @RequestMapping("/testSession")
         public String test(Map<String,Object> map){
             map.put("names", Arrays.asList("a","b","c"));
             map.put("age", 12);
             return "hello";
         }
     
     	 @RequestMapping("/success")
　　		public ModelAndView index4(SessionStatus status) {
　　			ModelAndView mav = new ModelAndView("success.jsp");
　　			status.setComplete();
　　			return mav;
		}
}
```

### @SessionAttribute

获取存储在session中的属性。

```java
@Controller
@RequestMapping("/user")
public class UserController {

   /*
    * Get user from session attribute
    */
   @GetMapping("/info")
   public String userInfo(@SessionAttribute("user") User user) {

      System.out.println("Email: " + user.getEmail());
      System.out.println("First Name: " + user.getFname());

      return "user";
   }
}
```

### @PathVariable

@PathVariable可以用来映射URL中的占位符到目标方法的参数中。

```java
@RequestMapping("/testPathVariable/{id}")
public String testPathVariable(@PathVariable("id") Integer id){
    System.out.println("testPathVariable:"+id);
    return SUCCESS;
}
```

## 定时任务

### @EnableScheduling

注解类，一般注解启动类或者配置类，用于开启计划任务。

任一个地方有则认为开启，也就是说无法通过该注解控制某个特定类里的任务启动。

### @Scheduled

注解方法,该注解包含八个参数：

> cron 表达式；
>
> zone 时区；
>
> fixedDelay 固定延迟时间-从上此次任务结束开始延迟；
>
> fixedDelayString 固定延迟时间-字符串形式；
>
> fixedRate 固定频率-间隔时间根据开始时间计算。同步状态下任务时间超过定义频率的在上一次任务结束后立即执行，异步状态下按照频率执行；
>
> fixedRateString 固定频率-字符串形式；
>
> initialDelay 第一次延迟多长时间执行；
>
> initialDelayString 第一次按时多长时间执行-字符串形式；

同一个注解下 'cron', 'fixedDelay(String)' 或 'fixedRate(String)' 属性只能有一个。

基于注解@Scheduled默认为单线程。

### @EnableAsync

使用@EnableAsync 开启多线程，注解启动类或者配置类，一般和 @EnableScheduling 放在一块。

### @Async

任务使用多线程。

## 缓存

### @Cacheable

用来标记缓存查询。可用用于方法或者类中， 当标记在一个方法上时表示该方法是支持缓存的， 当标记在一个类上时则表示该类所有的方法都是支持缓存的。

```java
@Cacheable(value="UserCache")// 使用了一个缓存名叫 accountCache   
public Account getUserAge(int id) {  
     //这里不用写缓存的逻辑，直接按正常业务逻辑走即可，
     //缓存通过切面自动切入  
    int age=getUser(id);   
     return age;   
} 
```

### @CacheEvict

用来标记要清空缓存的方法，当这个方法被调用后，即会清空缓存。 

@CacheEvict(value=”UserCache”)

## 加载过程

### @PostConstruct

用来标记是在项目启动的时候执行这个方法。多用于一些全局配置、数据字典之类的加载。

被 @PostConstruct 修饰的方法会在服务器加载 Servlet 的时候运行，并且只会被服务器执行一次。PostConstruct 在构造函数之后执行,init() 方法之前执行。

### @PreDestroy

被@PreDestroy 修饰的方法会在服务器卸载 Servlet 的时候运行，并且只会被服务器调用一次。

PreDestroy 修饰的方法在destroy()方法执行之后执行

## 数据库

### @Repository

用于标注数据访问组件，即DAO组件。

## 事务

### @EnableTransactionManagement

开启事务。可不加，因为SpringBoot在TransactionAutoConfiguration类里为我们自动配置启用了@EnableTransactionManagement注解。

### @Transactional

事务。

默认spring事务只在发生未被捕获的 RuntimeExcetpion/Error时才回滚，即被拦截的方法需显式抛出异常，并不能经任何处理，这样aop代理才能捕获到方法的异常，才能进行回滚，默认情况下aop只捕获runtimeexception/Errors的异常。可以通过参数指定回滚，例如@Transactional(rollbackFor=Exception.class) 。

在 Spring 的 AOP 代理下，只有目标方法由外部调用，目标方法才由 Spring 生成的代理对象来管理，这会造成自调用问题。若同一类中的其他没有@Transactional 注解的方法内部调用有@Transactional 注解的方法，有@Transactional 注解的方法的事务被忽略，不会发生回滚。

注：可以通过方法 TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();手动回滚事务，则不需要像上层抛出异常。

## 参考

[spring的注解及其解释]:(https://juejin.cn/post/6862571318877880333)