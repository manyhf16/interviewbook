---
search:
    keywords: ['struts2','执行流程']

---



# Struts2的执行流程 


# 参考解答：
![](/assets/4.png)

一个请求在Struts2框架中的处理大概分为以下几个步骤：

1、 客户端发送请求；
2、 这个请求经过一系列的过滤器（Filter）
3、 接着StrutsPrepareAndExecuteFilter被调用，FilterDispatcher询问ActionMapper来决定这个请是否需要调用某个Action。FilterDispatcher的功能如下：

   (1)执行Actions
   (2)清除ActionContext
   (3)维护静态内容
   (4)清除reques生命周期的XWork的interceptors


4、 如果ActionMapper决定需要调用某个Action，FilterDispatcher把请求的处理交给ActionProxy

5、 ActionProxy通过Configuration Manager询问框架的配置文件，找到需要调用的Action类

6、 ActionProxy创建一个ActionInvocation的实例。

7、 ActionInvocation实例使用命名模式来调用，在调用Action的过程前后，涉及到相关拦截器（Intercepter）的调用。

8、 一旦Action执行完毕，ActionInvocation负责根据struts.xml中的配置找到对应的返回结果。返回结果通常是（但不总是，也可 能是另外的一个Action链）一个需要被表示的JSP。

> **注意**
早期版本的struts2 Filter类叫做FilterDispatcher，已经过时，被StrutsPrepareAndExecuteFilter所取代。

---

