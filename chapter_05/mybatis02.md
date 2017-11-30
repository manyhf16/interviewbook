---
search:
    keywords: ['mybatis']

---


# mybatis 中 #{} 和 ${} 的区别？

# 参考解答

## 1. #{} 和 ${}工作原理
假设有如下java实体对象：

```java
package entity;
public class City {
    private int id;
    private String name;
    // get, set 方法 
}
```

### 1)`#{}` 
用于生成PreparedStatement方式的占位参数，mapper文件编写如下：
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

### 2)`${}` 
是采用拼接字符串方式生成sql语句，不会利用占位参数的方式，mapper文件编写如下：
```xml
<insert id="insert" parameterType="entity.City">
    insert into city(id,name) values(${id},${name})
</insert>
```
最后执行时会生成如下的等价jdbc代码：

```java
PreparedStatement psmt = conn.prepareStatement("insert into city(id,name) values(id值,'name值')");
pstm.executeUpdate();
```

## 2. 它们的区别
由以上工作原理可知：
* `${}` 安全性较差，可能会导致SQL注入攻击；而`#{}`相对安全
* `#{}` 只能替换sql语句中的`值部分`，不能替换表名、列名；而`${}` 
可以替换sql语句的任意部分
* `#{}` 内不能含有表达式，不能进行运算；而`${}` 内可以使用ognl语法进行简单运算
 

---







