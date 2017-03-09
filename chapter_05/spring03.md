# 在Spring中,FactoryBean和BeanFactory的区别？


# 参考解答

* `FactoryBean<对象类型>`接口是在对象的创建过程比较复杂时，用来封装对象的创建过程，泛型指该工厂要生产的产品类型。当spring配置了FactoryBean类型的bean时，spring会在调用getBean("工厂id")间接调用工厂中的getObject()方法来获取产品对象。

* 而BeanFactory是spring容器的核心，主要提供了getBean()方法来获取由spring管理的bean。

* 如果要用通俗的方式解释：BeanFactory是一个大工厂负责管理各种产品，而FactoryBean是大工厂中的某一个车间，负责生产具体某一种产品。

---