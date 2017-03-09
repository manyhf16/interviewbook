---
search:
    keywords: ['hibernate','opensession','getcurrentsession']

---



# hibernate中openSession()和getCurrentSession()两个方法的区别？


# 参考解答

* openSession() 方法每次都会创建新的session对象，使用完毕需要手动调用close()方法来关闭。

* getCurrentSession() 方法是将session对象与当前线程相绑定。如果是第一次调用，创建新的；如果之后多次调用，获取的是第一次创建的session。

* getCurrentSession() 方法必须工作在事务环境下（查询也不例外）当事务结束时会自动关闭session，不需要手动调用close()方法。

---