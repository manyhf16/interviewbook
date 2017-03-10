---
search:
    keywords: ['struts2','执行流程']

---



# Struts2的执行流程 


# 参考解答：
![](/assets/4.png)

一个请求在Struts2框架中的处理大概分为以下几个步骤：

1. 客户端发送请求。
2. 这个请求经过一系列的其它过滤器（Filter），注意其它过滤器要放在struts2的过滤器之前，否则没有机会被执行。
3. 接着StrutsPrepareAndExecuteFilter被调用，FilterDispatcher询问ActionMapper来决定这个请是否有某个Action能处理这次请求（路径匹配上了）。

4. 如果ActionMapper决定需要调用某个Action，FilterDispatcher把请求的处理交给ActionProxy（ActionProxy中包含了这次请求要执行哪个Action，执行的方法是哪个等信息）

5. ActionProxy通过Configuration Manager询问框架的配置文件，找到需要调用的Action类

6、 ActionProxy创建一个ActionInvocation的实例。

7、 ActionInvocation实例使用命名模式来调用，在调用Action的过程前后，涉及到相关拦截器（Intercepter）的调用。

8、 一旦Action执行完毕，ActionInvocation负责根据struts.xml中的配置找到对应的返回结果。返回结果通常是（但不总是，也可 能是另外的一个Action链）一个需要被表示的JSP。

> **注意**
早期版本的struts2 Filter类叫做FilterDispatcher，已经过时，被StrutsPrepareAndExecuteFilter所取代。

---

