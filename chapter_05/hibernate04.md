---
search:
    keywords: ['hibernate','二级缓存','onetomany','manytomany']

---

# 关于hibernate:
1. 在hibernate中，在配置文件中一对多，多对多的标签是什么； 
2. Hibernate的二级缓存是什么； 
3. Hibernate是如何处理事务的；

# 参考解答：

 1）一对多的标签为`<one-to-many>` ；多对多的标签为`<many-to-many>`；
  
 2）hibernate中的二级缓存是为了进一步提高查询效率，而增加的缓存。它会采用第三方的缓存实现。二级缓存中的对象可以在多个session中被共享，它的生命周期与sessionFactory相同。
 
 3）Hibernate的事务默认是封装了JDBC Transaction。
 

---



