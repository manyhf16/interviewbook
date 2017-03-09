---
search:
    keywords: ['spring','事务','tx','transaction']

---



# spring 事务

# 题目问法


## 1. 在Spring容器中,容器如何知道事务已经完成并且可以提交了? 用户如何控制事务回滚?


## 参考解答
* spring由代理对象调用TransactionInterceptor在正常业务方法执行前后进行拦截

* 业务方法正常执行结束，事务提交。

* 如果业务方法执行出现异常，会根据异常类型进行判断，默认情况是RuntimeException和Error异常会导致回滚，其它异常仍然会让事务提交。
> 如果要希望其它异常也导致回滚，可以通过配置事务属性中的rollbackOn来达到目的

---