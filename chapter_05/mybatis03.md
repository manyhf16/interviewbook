---
search:
    keywords: ['mybatis','分页']

---


# mybatis 中的分页

# 参考解答

mybatis中的分页有两种：一是mybatis自带的逻辑分页，二是自己编写分页sql实现物理分页

## 逻辑分页例子

```java
public interface EmpMapper {
	@Select("select * from emp")
	public List<Emp> selectByPage(RowBounds rb);

}
```

逻辑分页的工作原理是：根据sql查询所有记录，然后通过jdbc中的的可滚动结果集实现分页，其中由RowBounds确定了本页第一条记录的下标(offset)和本页需要几条记录(limit)

