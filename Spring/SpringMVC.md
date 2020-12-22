![Spring MVC工作原理图](resources/SpringMVC原理图.jpg)

```java
DispatcherServlet extends FrameworkServlet
					extends HttpServletBean
					extends HttpServlet
{
    protected void initStrategies(ApplicationContext context) {
        //默认来自配置文件/org/springframework/web/servlet/DispatcherServlet.properties
        
        initMultipartResolver(context);
		initLocaleResolver(context);
		initThemeResolver(context);
		initHandlerMappings(context);
		initHandlerAdapters(context);
		initHandlerExceptionResolvers(context);
		initRequestToViewNameTranslator(context);
		initViewResolvers(context);
		initFlashMapManager(context);
    }
    
    
    @Override
	protected void doService(HttpServletRequest request, HttpServletResponse response) throws Exception {
        //处理request,往里面塞一些东西
        ...
        doDispatch(request, response);
    }
    
    protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
        HttpServletRequest processedRequest = request;
        ...
        HandlerExecutionChain mappedHandler = getHandler(processedRequest);
        HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
        ...
        // Actually invoke the handler.
        ModelAndView mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
        
        processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
    }
}
```



