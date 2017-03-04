# 关键字

\[hibernate\]

# 关于hibernate: 【基础】
  ## 1）在hibernate中，在配置文件呈标题一对多，多对多的标签是什么； 
  ## 2）Hibernate的二级缓存是什么； 
  ## 3）Hibernate是如何处理事务的；

# 参考解答：

 1）一对多的标签为<one-to-many> ；多对多的标签为<many-to-many>；
  
 2）sessionFactory的缓存为hibernate的二级缓存；
 
 3）Hibernate的事务实际上是底层的JDBC Transaction的封装或者是JTA Transaction     的封装；默认情况下使用JDBC Transaction。
 
 

详细解释：

![](/assets/12.png)

由上图可以看出，hibernate的二级缓存是多个session间共享的。
当执行查询操作时，默认第一次查到的记录会存放在session的一级缓存中。第二次查询时，会先在session的以及环中查找，如果没找到，会到session的二级缓存中查找。如果session的二级缓存中找不到，最后才会到数据库中查找。

---



