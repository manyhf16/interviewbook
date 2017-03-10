---
search:
    keywords: ['springmvc','原理','执行流程']

---

# srpingMVC的原理

# 参考解答

SpringMVC的执行流程（ModelAndView）可以参考下图：![](/assets/2.png)


1. 客户端请求提交到DispatcherServlet，DispatcherServlet会在服务器启动时初始化spring容器，生成控制器(Controller)实例。

2. 由DispatcherServlet根据请求匹配到一个合适的处理映射器(HandlerMapping)，由处理映射器(HandlerMapping)生成一个执行链(HandlerExecutionChain)，`执行链=多个拦截器+HandlerAdapter`。

3. 处理适配器(HandlerAdapter)类的职责是调用控制器(Controller)中的方法来真正处理请求。

4. 由处理适配器(HandlerAdapter)调用控制器(Controller)中的方法，在控制器方法执行前后会调用多个拦截器中的前处理和后处理方法

5. Controller方法执行后，结果会封装为ModelAndView对象。由 DispatcherServlet利用视图解析器(ViewResoler)生成视图(View)对象

6. 在请求到达视图之前，spring会将模型数据存入request作用域

7. 视图取出模型数据，渲染为html页面后作为响应返回给客户端

> **注意**
如果使用@ResponseBody返回响应，还会走AbstractHttpMessageConverter的流程，这时，返回的ModelAndView为null，不会再走之后的View流程了

---