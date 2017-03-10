---
search:
    keywords: ['springmvc','struts2']

---

# Struts2 vs SpringMVC？  

# 参考解答

主要区别如下：
1)Struts2中的Action用实例变量接收请求参数，为了保证请求参数的处理互不影响，就需要每个请求创建一个新的Action对象；而SpringMVC的Controller使用方法参数对应请求参数，方法参数都是线程安全的，因此所有请求可以共用同一个Controller对象。
从这点上来讲，SpringMVC可以更自然地实现Restful.

2)Struts2中使用Filter来作为前控制器来作为请求的入口，SpringMVC中使用Servlet作为前控制器。Struts2的Filter过滤的是/*所有请求，优先级最高，比较“霸道”；SpringMVC的Servlet映射的路径是/，和其它Servlet是平级关系，其它Servlet的路径匹配不到才会进入SpringMVC的处理，相对“谦和”。

3)如果返回jsp视图，Struts2中的拦截器是包围在action+jsp前后，SpringMVC中的拦截器是包围在controller前后。

4)Struts2中视图渲染使用值栈作为传值容器，值栈分为Root和Context部分，其中Root是栈结构，Context是Map结构；而SpringMVC使用Model作为传值容器，Model就是一个Map结构。

5)Struts2对一些标准的支持较为落后，而SpringMVC支持Servlet3.0及更新的规范，如WebSocket，AsyncServlet，CORS等。
Struts2曾一度暴露安全漏洞，对其口碑影响较大。

详细解释：