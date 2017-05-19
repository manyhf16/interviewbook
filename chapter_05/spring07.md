---
search:
    keywords: ['spring', 'beanfactory', 'applicationcontext']

---


# spring中BeanFactory和ApplicationContext的联系和区别？

# 参考解答
spring中的容器类型有两种：BeanFactory和ApplicationContext

* BeanFactory接口定义了Spring最基本的bean实例化和依赖注入功能，它根据bean定义(bean definition)来创建bean实例。

* ApplicationContext对BeanFactory的功能做了扩展：
 * ApplicationContext继承了MessageSource来承诺实现资源文件管理和国际化
 * ApplicationContext继承了ApplicationEventPublisher来承诺实现事件推送编程
 * ApplicatonContext继承了ResourcePatternResolver来处理Spring中的Resource资源
 * ApplicationContext提供了bean的`后处理`扩展
 
* ApplicationContext和BeanFactory的关系是组合而非继承。

---

