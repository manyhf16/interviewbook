---
search:
    keywords: ['spring','核心','ioc','aop','di','控制反转','依赖注入','面向切面编程 ']

---


# spring核心思想

# 题目问法

1. 你知道IOC(Inversion of Control)吗? IOC有哪几种类型? 使用IOC有哪些好处? 现在有哪些比较流行的IoC容器?

2. 简述面向切面编程AOP的好处？spring中常见的基础切面有哪些？切面的实现原理是什么？

3. spring中BeanFactory和ApplicationContext的联系和区别


# 参考解答
spring 有两大核心思想：控制反转（IOC）和面向切面编程（AOP）

## IOC
IOC即控制反转，是指将java bean的创建、生命周期、依赖关系管理交给**容器**来控制。

在没有使用IOC思想之前，需要程序员主动去创建bean，维护其是否单例，生命周期等等，这样做的缺点是，对象的创建与对象的使用相耦合，对象与对象之间的关系紧耦合，不利于程序的扩展，经常会牵一发而动全身：某个对象发生了修改，使用这个对象的所有代码都需要跟着修改。

IOC的思想是将刚才提到的创建bean，bean实例个数和声明周期的控制，都交给容器来管理。相当于将bean的控制权移交给了容器，因此被称为控制反转。控制反转的好处是，bean的创建和声明周期均可通过容器配合配置文件的方式来管理，降低了耦合。

## DI
DI即Dependency Injection，是对IOC概念的一个补充。

传统的web开发中也存在容器的概念，例如tomcat 容器控制servlet和jsp的创建以及生命周期。虽然web容器也存在控制反转的思想，但与之前提到的IOC容器不同的是，web容器没有管理对象之间的依赖关系。

为了强调IOC容器的特点，又提出了依赖注入的概念。IOC容器不仅管理bean，还管理bean与bean之间的依赖关系。例如 service使用了 dao，那么称service依赖于 dao，它们之间的依赖关系并不是由代码来建立，而是IOC容器通过配置文件或注解的方式，在程序运行期间关联起来，进一步降低了耦合。

## 小结
正是因为控制反转和依赖注入，使得spring可以和绝大多数开源框架整合。

## Spring IOC 容器的类型
spring中的容器类型有两种：BeanFactory和ApplicationContext

* BeanFactory接口定义了Spring最基本的功能：实例化和依赖注入，可以按照bean id或bean type从容器获取bean实例。

* ApplicationContext扩展了BeanFactory：
 * 容器之间可以继承，子容器能够访问父容器定义的bean，但反之不行
 * 不像是BeanFactory只能一个个地得到容器中的bean，ApplicationContext可以获取所有bean的名称，或者按照条件查询容器中的bean
 * ApplicationContext继承了MessageSource来承诺实现资源文件管理和国际化
 * ApplicationContext继承了ApplicationEventPublisher来承诺实现事件推送编程
 * ApplicatonContext继承了ResourcePatternResolver来处理Spring中的Resource资源

> 值得一提的是：BeanFactory的另一个重要子接口
ConfigurableListableBeanFactory承诺实现容器外的bean的属性织入，并具备添加BeanPostProcessor等功能


---









