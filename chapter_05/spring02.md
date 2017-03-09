# spring 应用

# 题目问法

1. 你都用过spring的哪些功能？
2. 请描述Spring和SpringMVC的区别？
3. spring框架中需要引用哪些jar包，以及这些jar包的用途？



# 参考解答:

|jar包|用途简介|
|-----|:-----:|
|spring-core |spring核心包，包括各项基础功能：反射，IO，注解处理，XML处理等工具类，并集成了cglib和objenesis(反射创建实例用) 
|spring-beans |对spring中bean定义的抽象，用来管理bean的各个方面：创建、bean工厂、类型转换、各种依赖注入
|spring-context <br>spring-context-support |spring容器的核心实现，另外包括缓存管理、远程访问、任务调度、spring脚本、数据校验等功能
|spring-expression |springel的实现，包括语法分析器等
|spring-aop |Aop的核心实现
|spring-jdbc |spring对jdbc和数据源的封装，提供了统一的Dao异常处理
|spring-tx |提供事务管理器的抽象，事务通知的实现
|spring-orm |spring对orm：hibernate和jpa的封装
|spring-web |spring容器在web方向的扩展，提供了处理文件上传,<br>json转换，参数绑定，http远程访问等功能
|spring-webmvc |mvc的实现，提供了路径映射，控制适配，拦截器，视图解析，视图
|spring-test |配合junit进行单元测试，一些mock对象的实现


spring官方提供的模块图：
![](/assets/3.png)

spring是一个开源框架，使用容器的思想管理bean，利用ioc和aop思想来解耦应用程序的耦合，提高整个应用的健壮与扩展性。

springmvc 是spring中的一个子项目，依托于spring其它核心模块，专注于解决web开发时的问题。它是一个mvc框架，主要通过控制器解耦模型和视图。

