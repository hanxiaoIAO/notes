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

### @Autowired

用来装配 bean，可以写在方法上，也可以写在字段上。默认情况下必须要求依赖对象必须存在，如果允许 null 值，可以设置 required 属性。@Autowired(required=false)

### @Qualifier

当你创建多个具有相同类型的 bean 时，并且想要用一个属性只为它们其中的一个进行装配，在这种情况下，你可以使用 @Qualifier 注释和 @Autowired 注释通过指定哪一个真正的 bean 将会被装配来消除混乱。也可以直接使用 @Resource 。

### @Resource

@Resource的作用相当于@Autowired 只不过@Autowired按byType自动注入， 而@Resource默认按 byName自动注入。

@Resource有两个属性是比较重要的，分是name和type，Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。

@Resource装配顺序:

> 如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常 
>
> 如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常。
>
> 如果指定了type，则从上下文中找到类型匹配的唯一bean进行装配，找不到或者找到多个，都会抛出异常。
>
> 如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则按照类型进行匹配，如果匹配则自动装配。

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

## 参考

[spring的注解及其解释]:(https://juejin.cn/post/6862571318877880333)