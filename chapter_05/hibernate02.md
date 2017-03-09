---
search:
    keywords: ['hibernate','工作原理']

---

# 简述hibernate的工作原理，为什么要使用该框架？

hibernate 是一个数据持久层框架，它封装了jdbc，简化了对数据库增删改查的操作，根据实体类和表结构的映射，在运行时生成sql语句。

使用hibernate可以提高开发效率，减少数据访问代码。

hibernate的工作原理从下面几个点来理解：

## 它是一个ORM框架
ORM 即 Object/Relational Mapping，意思是在java对象与数据库记录之间建立映射关系，依据映射关系生成增删改查SQL语句，从而减少程序员的工作量。

例如：
```java
<class name="entity.User" table="h_user">
  <id name="id" column="id">
    <generator class="assigned"/>
  </id>
  <property name="username" column="username"/>
  <property name="password" column="password"/>
</class>
```
hibernate 会根据此映射文件预先生成如下SQL语句：
```sql
insert into h_user (id,username,password) values(?,?,?)
update h_user set username=?, password=? where id = ?
delete from h_user where id = ?
select id, username, password from h_user where id = ?
```
当执行 session.save(user)时，会执行如下的等价jdbc代码：
```java
PreparedStatement ps = conn.preparedStatement("insert into h_user (id,username,password) values(?,?,?)");
ps.setInt(1, user.getId());
ps.setString(2, user.getUsername());
ps.setString(3, user.getPassword());
ps.executeUpdate();
```

## 实体类的三种状态

## 延迟加载实现

## 脏数据检查实现

## 缓存管理




