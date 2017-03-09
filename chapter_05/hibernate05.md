# Hibernate的应用（Hibernate的结构）？

# 参考解答：

1)首先获得SessionFactory的对象 
SessionFactory sessionFactory = new Configuration().configure(). buildSessionFactory(); 

2)然后获得session的对象 Session session = sessionFactory.openSession();

3)其次获得Transaction的对象 Transaction tx = session.beginTransaction(); 

4)执行相关的数据库操作:增,删,改,查 session.save(user); 

5)增加, user是User类的对象 session.delete(user); 

6)删除 session.update(user); 

7)更新 Query query = session.createQuery(“from User”); 

8)查询 List list = query.list(); 

9)提交事务 tx.commit();

10)如果有异常,我们还要作事务的回滚,恢复到操作之前 tx.rollback();
 
11)最后还要关闭session,释放资源 session.close();

---