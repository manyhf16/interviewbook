---
search:
    keywords: ['hibernate','分页']

---

# Hibernate分页怎样实现？【中等难度】  

# 参考解答：

Hibernate的分页方法为：

查询第一页：
```java
Query query = session.createQuery("from Student"); 
query.setFirstResult(0);  //设置每页开始的记录编号，编号从0开始
query.setMaxResults(10);  //设置每页显示的记录数 
Collection students = query.list(); 
```
查询第二页：
```java
Query query = session.createQuery("from Student"); 
query.setFirstResult(10); //设置每页开始的记录编号，编号从10开始
query.setMaxResults(10);  //设置每页显示的记录数 
Collection students = query.list(); 
```
查询第三页：
```java
Query query = session.createQuery("from Student"); 
query.setFirstResult(20); //设置每页开始的记录编号，编号从10开始
query.setMaxResults(10);  //设置每页显示的记录数 
Collection students = query.list(); 
```

底层会根据数据库方言，应用不同的分页SQL：

```java
if (useLimit); sql = dialect.getLimitString(sql);      
PreparedStatement st = session.getBatcher().prepareQueryStatement(sql, scrollable);
```
其中MySQLDialect的实现为：

```java 
public String getLimitString(String sql); {  
  StringBuffer pagingSelect = new StringBuffer(100);  
  pagingSelect.append(sql);  
  pagingSelect.append(" limit ?, ?");  
  return pagingSelect.toString(); 
}
```
Oracle9Dialect的实现为：
```java      
public String getLimitString(String sql); {  
  StringBuffer pagingSelect = new StringBuffer(100); 
  pagingSelect.append("select * from ( select row_.*, rownum rownum_ from ( ");  
  pagingSelect.append(sql);  
  pagingSelect.append(" ); row_ where rownum <= ?); where rownum_ > ?");  
  return pagingSelect.toString();  
}
```
除此之外，PostgreSQL，HSQL也支持分页的sql语句，在相应的Dialect里面，大家自行参考。
可见使用Hibernate一大好处是，既兼顾了查询分页的性能，同时又保证了代码在不同的数据库之间的可移植性。

---