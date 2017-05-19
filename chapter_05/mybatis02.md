---
search:
    keywords: ['mybatis']

---


# mybatis 中 #{} 和 ${} 的区别？

# 参考解答

`#{}` 用于生成PreparedStatement方式的占位参数，例如：

```java
package entity;
public class City {
    private int id;
    private String name;
    // get, set 方法 
}
```

```xml
<insert id="insert" parameterType="entity.City">
    insert into city(id,name) values(#{id},#{name})
</insert>
```

最后执行时会生成如下的等价jdbc代码：

```java
PreparedStatement psmt = conn.prepareStatement("insert into city(id,name) values(?,?)");
psmt.setInt(1, id值);
psmt.setStirng(s, name值);
pstm.executeUpdate();
```




