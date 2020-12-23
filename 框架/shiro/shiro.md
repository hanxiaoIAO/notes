## Shiro 基本功能

- Authentication：身份认证/登录。
- Authortization：授权，权限认证。
- Session Management：会话管理。
- Crytography：加密，保证数据的安全性。
- Web Support：Web 集成。
- Caching：缓存。
- Concurrency：多线程应用的并发验证。
- Run As：允许一个用户以另一个用户的身份登录。
- Remember Me：记住登录状态。

## Shiro 核心架构

- Subject：主体，代表了当前 “用户”。所有 Subject 都绑定到 SecurityManager，与 Subject 的所有交互都会委托给 SecurityManager。
- SecurityManager：安全管理器。
- Realm：域。存放安全数据，如用户、角色、权限。Realm 设计编写完成后注入到 SecurityManager 中。

## Shiro 身份验证

验证身份需要提供`principals` （身份）和 `credentials`（证明）。

**principals**：身份，即主体的标识属性，可以是任何东西，如用户名、邮箱等，唯一即可。一个主体可以有多个 `principals`，但只有一个 `Primary principals`，一般是用户名 / 密码 / 手机号。

**credentials**：证明 / 凭证，即只有主体知道的安全值，如密码 / 数字证书等。

最常见的 `principals` 和 `credentials` 组合就是用户名 / 密码

## 拦截器介绍

![img](resources/shiro拦截器.png)

### NameableFilter

设置 name 属性

```java
public abstract class NameableFilter extends AbstractFilter implements Nameable {
	private String name;
}
```

### OncePerRequestFilter

OncePerRequestFilter 用于防止多次执行 Filter 的；也就是说一次请求只会走一次拦截器链；另外提供 enabled  属性，表示是否开启该拦截器实例，默认 enabled=true 表示开启，如果不想让某个拦截器工作，可以设置为 false 即可。

### ShiroFilter 

ShiroFilter 是整个 Shiro 的入口点，用于拦截需要安全控制的请求进行处理

### AdviceFilter

AdviceFilter 提供了 AOP 风格的支持。

```java
boolean preHandle(ServletRequest request, ServletResponse response) throws Exception;
void postHandle(ServletRequest request, ServletResponse response) throws Exception;
void afterCompletion(ServletRequest request, ServletResponse response, Exception exception) throws Exception;
```

### PathMatchingFilter

PathMatchingFilter 提供了基于 Ant 风格的请求路径匹配功能及拦截器参数解析的功能。

### AccessControlFilter

提供了访问控制的基础功能；比如是否允许访问/当访问拒绝时如何处理等。

另外 AccessControlFilter 还提供了用于处理如登录成功后/重定向到上一个请求的功能。

```java
abstract boolean isAccessAllowed(ServletRequest request, ServletResponse response, Object mappedValue) throws Exception;
boolean onAccessDenied(ServletRequest request, ServletResponse response, Object mappedValue) throws Exception;
abstract boolean onAccessDenied(ServletRequest request, ServletResponse response) throws Exception;
```

isAccessAllowed：表示是否允许访问；mappedValue 就是[urls]配置中拦截器参数部分，如果允许访问返回 true，否则 false；  

onAccessDenied：表示当访问拒绝时是否已经处理了；如果返回 true 表示需要继续处理；如果返回 false 表示该拦截器实例已经处理了，将直接返回即可。  

## 默认拦截器 org.apache.shiro.web.filter.mgt.DefaultFilter

| 默认拦截器名      | 拦截器类                                                     | 说明（括号里的表示默认值）                                   |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| anon              | org.apache.shiro.web.filter.authc .AnonymousFilter           | 匿名拦截器，即不需要登录即可访问；一般用于静态资源过滤；示例 “/static/**=anon” |
| authc             | org.apache.shiro.web.filter.authc .FormAuthenticationFilter  | 基于表单的拦截器；如  “`/**=authc`”，如果没有登录会跳到相应的登录页面登录；主要属性：usernameParam：表单提交的用户名参数名（  username）；  passwordParam：表单提交的密码参数名（password）；  rememberMeParam：表单提交的密码参数名（rememberMe）；  loginUrl：登录页面地址（/login.jsp）；successUrl：登录成功后的默认重定向地址；  failureKeyAttribute：登录失败后错误信息存储 key（shiroLoginFailure）； |
| authcBasic        | org.apache.shiro.web.filter.authc .BasicHttpAuthenticationFilter | Basic HTTP 身份验证拦截器，主要属性： applicationName：弹出登录框显示的信息（application）； |
| logout            | org.apache.shiro.web.filter.authc .LogoutFilter              | 退出拦截器，主要属性：redirectUrl：退出成功后重定向的地址（/）; 示例 “/logout=logout” |
| user              | org.apache.shiro.web.filter.authc .UserFilter                | 用户拦截器，用户已经身份验证 / 记住我登录的都可；示例 “/**=user” |
|                   |                                                              |                                                              |
| perms             | org.apache.shiro.web.filter.authz .PermissionsAuthorizationFilter | 权限授权拦截器，验证用户是否拥有所有权限；属性和 roles 一样；示例 “/user/**=perms["user:create"]” |
| port              | org.apache.shiro.web.filter.authz .PortFilter                | 端口拦截器，主要属性：port（80）：可以通过的端口；示例 “/test= port[80]”，如果用户访问该页面是非 80，将自动将请求端口改为 80 并重定向到该 80 端口，其他路径 / 参数等都一样 |
| rest              | org.apache.shiro.web.filter.authz .HttpMethodPermissionFilter | rest 风格拦截器，自动根据请求方法构建权限字符串（GET=read,  POST=create,PUT=update,DELETE=delete,HEAD=read,TRACE=read,OPTIONS=read,  MKCOL=create）构建权限字符串；示例  “/users=rest[user]”，会自动拼出“user:read,user:create,user:update,user:delete” 权限字符串进行权限匹配（所有都得匹配，isPermittedAll）； |
| roles             | org.apache.shiro.web.filter.authz .RolesAuthorizationFilter  | 角色授权拦截器，验证用户是否拥有所有角色；主要属性： loginUrl：登录页面地址（/login.jsp）；unauthorizedUrl：未授权后重定向的地址；示例 “/admin/**=roles[admin]” |
| ssl               | org.apache.shiro.web.filter.authz .SslFilter                 | SSL 拦截器，只有请求协议是 https 才能通过；否则自动跳转会 https 端口（443）；其他和 port 拦截器一样； |
|                   |                                                              |                                                              |
| noSessionCreation | org.apache.shiro.web.filter.session .NoSessionCreationFilter | 不创建会话拦截器，调用 subject.getSession(false) 不会有什么问题，但是如果 subject.getSession(true) 将抛出 DisabledSessionException 异常； |

## Shiro 权限注解

配置

```java
@Configuration
public class ShiroConfig {   
   /**
     * 开启注解
     * @param securityManager
     * @return
     */
    @Bean
    public AuthorizationAttributeSourceAdvisor authorizationAttributeSourceAdvisor(SecurityManager securityManager){
        AuthorizationAttributeSourceAdvisor authorizationAttributeSourceAdvisor = new AuthorizationAttributeSourceAdvisor();
        authorizationAttributeSourceAdvisor.setSecurityManager(securityManager);

        return authorizationAttributeSourceAdvisor;
    }
}
```

注解用来注释方法

> ```
> @RequiresAuthentication
> ```
>
> 表示当前 Subject 已经通过 login 进行了身份验证；即 Subject.isAuthenticated() 返回 true。  
>
> ```
> @RequiresUser
> ```
>
> 表示当前 Subject 已经身份验证或者通过记住我登录的。  
>
> ```
> @RequiresGuest
> ```
>
> 表示当前 Subject 没有身份验证或通过记住我登录过，即是游客身份。  
>
> ```
> @RequiresRoles(value={“admin”, “user”}, logical= Logical.AND)
> ```
>
> 表示当前 Subject 需要角色 admin 和 user。  
>
> ```
> @RequiresPermissions (value={“user:a”, “user:b”}, logical= Logical.OR)
> ```
>
> 表示当前 Subject 需要权限 user：a 或 user：b。  