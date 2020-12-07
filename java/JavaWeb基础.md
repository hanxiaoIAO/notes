## JavaWeb三大组件

Servlet、Filter、Listener是JavaEE Web服务规定的服务器动态组件。加载顺序为Linstener -> Fliter -> Servlet，与它们在web.xml中配置的顺序没有关系。

### Servlet

Servlet是用来处理客户端请求的动态资源，在web容器的管理下实现对web请求的处理与分发，并且可以动态的生成web页面。

#### Servlet的生命周期方法

- void init(ServletConfig)

　　servlet的初始化方法，只在创建servlet实例时候调用一次，Servlet是单例的，整个服务器就只创建一个同类型Servlet

- void service(ServletRequest,ServletResponse)

  servlet的处理请求方法，在servle被请求时，会被马上调用，每处理一次请求，就会被调用一次。

  ServletRequest类为请求类，ServletResponse类为响应类。

  客户端请求会被封装成HttpServletRequest对象，里面包含了请求头、参数等各种信息。处理完请求后，我们一般会转发（forward）或者重定向（redirect）到某个页面，转发是HttpServletRequest中的方法，重定向是HttpServletResponse中的方法

- void destory()

　　servlet销毁之前执行的方法，只执行一次，用于释放servlet占有的资源，通常Servlet是没什么可要释放的，所以该方法一般都是空的。

#### Fliter

Filter主要负责拦截请求，和放行,可以用来转换HTTP请求、响应和头信息。它不能产生一个请求或者响应，它只是修改对某一资源的请求，或者修改从某一的响应。

#### Listener

通过listener可以监听web服务器中某一个执行动作，并根据其要求作出相应的响应。通俗的语言说就是在application，session，request三个对象创建消亡或者往其中添加修改删除属性时自动执行代码的功能组件。

servlet2.4规范中提供了8个listener接口，可以将其分为三类，分别如下：

> 第一类：与servletContext有关的listner接口。包括：ServletContextListener、ServletContextAttributeListener
>
> 第二类：与HttpSession有关的Listner接口。包括：HttpSessionListner、HttpSessionAttributeListener、 HttpSessionBindingListener、HttpSessionActivationListener；
>
> 第三类：与ServletRequest有关的Listener接口，包括：ServletRequestListner、ServletRequestAttributeListener