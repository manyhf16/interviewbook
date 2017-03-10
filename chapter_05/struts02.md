---
search:
    keywords: ['struts2','执行流程']

---



# Struts2的执行流程 


# 参考解答：
![](/assets/4.png)

一个请求在Struts2框架中的处理大概分为以下几个步骤：

1. 客户端发送请求

2. 这个请求经过一系列的其它过滤器（Filter），注意其它过滤器要放在struts2的过滤器之前，否则没有机会被执行

3. 接着StrutsPrepareAndExecuteFilter被调用，询问ActionMapper来决定是否有某个Action能处理这次请求（路径匹配上了）

4. 如果ActionMapper决定需要调用某个Action，StrutsPrepareAndExecuteFilter把请求的处理交给ActionProxy

5. ActionProxy通过访问配置文件，知道了这次请求要执行哪个Action的哪个方法

6. ActionProxy还会创建一个ActionInvocation的实例。

7. ActionInvocation真正创建Action，将Action对象压入值栈，调用调用各个拦截器以及Action

8. Action或拦截器执行结束会返回一个视图名，ActionProxy会根据视图名找到Result对象并执行

9. Result执行会导致进入jsp，jsp中利用struts标签从值栈获取模型数据，渲染显示，生成最后的html

10. 返回响应给客户端

> **注意**
早期版本的struts2 Filter类叫做FilterDispatcher，已经过时，被StrutsPrepareAndExecuteFilter所取代。

---

