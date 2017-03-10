---
search:
    keywords: ['hibernate','使用步骤','执行流程']

---


# Hibernate的使用步骤？

# 参考解答：

1. 首先获得SessionFactory的对象 
```java
SessionFactory sessionFactory = new Configuration().configure(). buildSessionFactory(); 
```
2. 然后获得Session的对象 
```java
Session session = sessionFactory.openSession();
```
3. 开启事务 
```java
Transaction tx = session.beginTransaction(); 
```
4. 执行相关的数据库操作:增,删,改,查 
```java
session.save(user);  // 增加
session.delete(user); // 删除
session.update(user); // 修改
List<User> list = session.createQuery(“from User”).list(); // 查询
```
5. 提交事务 `tx.commit();` 如果有异常，要作事务的回滚 `tx.rollback();`
 
6. 最后还要关闭session
```java
session.close();
```



---