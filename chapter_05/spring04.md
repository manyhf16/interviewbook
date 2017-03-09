---
search:
    keywords: ['spring','事务','tx','transaction']

---



# spring 事务

# 题目问法

1. 在Spring容器中,容器如何知道事务已经完成并且可以提交了，用户如何控制事务回滚？
2. spring如何实现事务管理的？
3. Spring支持的事务管理类型有哪些？事务管理有哪些优点？你更倾向于那种事务类型管理？

## 如何控制事务提交和回滚
* spring由代理对象调用TransactionInterceptor在正常业务方法执行前后进行拦截

* 业务方法正常执行结束，事务提交。

* 如果业务方法执行出现异常，会根据异常类型进行判断，默认情况是RuntimeException和Error异常会导致回滚，其它异常仍然会让事务提交。
> 如果要希望其它异常也导致回滚，可以通过配置事务属性中的rollbackOn来达到目的

## spring如何实现事务管理
spring中的事务管理分为声明式和编程式两种。以声明式事务管理为例：

1. 首先spring解决的一个问题是，同一个事务内多次方法调用所用到的数据库资源应当是同一个对象，例如如果用Hibernate，那么同一事务应该对应同一个Session资源；如果是使用jdbc或mybatis，那么同一事务应该对应同一个Connection资源，Spring中使用了ThreadLocal技术将事务所依赖资源与当前线程绑定，如下图所示（简化了部分逻辑）：
![](/assets/5.png)

2. 第二针对不同的事务依赖资源，spring抽象为PlatformTransactionManager，根据资源的不同选择不同的实现：hibernate有HibernateTransactionManager，而jdbc和mybatis有DataSourceTransactionManager，这些事务管理器负责执行具体的开启事务、提交事务、回滚事务等操作

3. 为了让事务逻辑重用，不要影响正常业务代码，spring采用了aop思想，应用代理模式，为业务逻辑对象（目标）产生相应的代理对象，由代理对象协调调用事务通知和业务逻辑对象，将它俩结合起来。产生代理的技术spring用到了jdk动态代理或cglib

4. spring提供了TransactionInterceptor类充当事务通知，它负责管理事务属性（具体到哪些方法需要事务，事务传播行为，隔离级别等），并由它再去调用PlatformTransactionManager 真正执行事务操作。

## spring支持的事务管理类型
分为声明式事务和编程式事务。声明式事务指利用`<tx:advice>`或@Transactional注解来标注需要事务控制的方法，而编程式事务是指利用TransactionTemplate 将多次方法调用纳入一个事务中。

显然声明式事务更

---
