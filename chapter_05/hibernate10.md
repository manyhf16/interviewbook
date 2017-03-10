# 关键字

\[hibernate\]

# Hibernate分页怎样实现？【中等难度】  

# 参考解答：

方法为： 
Hibernate的分页：
Query query = session.createQuery("from Student"); 
query.setFirstResult(firstResult);//设置每页开始的记录号 
query.setMaxResults(resultNumber);//设置每页显示的记录数 
Collection students = query.list(); 


详细解释：

Hibernate底层如何实现分页的呢？实际上Hibernate的查询定义在net.sf.hibernate.loader.Loader这个类里面

Hibernate2.0.3的Loader源代码第480行以下： 

```
if (useLimit); sql = dialect.getLimitString(sql);;        
PreparedStatement st = session.getBatcher().prepareQueryStatement(sql, scrollable);
```


MySql的分页,net.sf.hibernate.dialect.MySQLDialect:

Java代码  
   
```
 public boolean supportsLimit(); {  
      return true;  
    }  
    public String getLimitString(String sql); {  
      StringBuffer pagingSelect = new StringBuffer(100);  
      pagingSelect.append(sql);  
      pagingSelect.append(" limit ?, ?");  
      return pagingSelect.toString(); 
    }  

```
Oracle的分页，net.sf.hibernate.dialect.Oracle9Dialect:

Java代码  


```
public boolean supportsLimit(); {  
      return true;  
    }  
      
    public String getLimitString(String sql); {  
      StringBuffer pagingSelect = new StringBuffer(100); 
      pagingSelect.append("select * from ( select row_.*, rownum rownum_ from ( ");  
      pagingSelect.append(sql);  
      pagingSelect.append(" ); row_ where rownum <= ?); where rownum_ > ?");  
      return pagingSelect.toString();  
    }  

```
Oracle采用嵌套3层的查询语句结合rownum来实现分页，这在Oracle上是最快的方式，如果只是一层或者两层的查询语句的rownum不能支持order by。

除此之外，Interbase，PostgreSQL，HSQL也支持分页的sql语句，在相应的Dialect里面，大家自行参考。

如果数据库不支持分页的SQL语句，那么根据在配置文件里面
hibernate.jdbc.use_scrollable_resultset true
默认是true，如果你不指定为false，那么Hibernate会使用JDBC2.0的scrollable result来实现分页，看Loader第430行以下：


Java代码  

   

```
 if ( session.getFactory();.useScrollableResultSets(); ); {  
      // we can go straight to the first required row  
      rs.absolute(firstRow);  
    }  
    else {  
      // we need to step through the rows one row at a time (slow);  
      for ( int m=0; m<firstRow; m++ ); rs.next();  
    }  
```


如果支持scrollable result，使用ResultSet的absolute方法直接移到查询起点，如果不支持的话，使用循环语句，rs.next一点点的移过去。

可见使用Hibernate，在进行查询分页的操作上，是具有非常大的灵活性，Hibernate会首先尝试用特定数据库的分页sql，如果没用，再尝试Scrollable，如果不行，最后采用rset.next()移动的办法。

在查询分页代码中使用Hibernate的一大好处是，既兼顾了查询分页的性能，同时又保证了代码在不同的数据库之间的可移植性。

---