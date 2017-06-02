---
search:
    keywords: ['mybatis','分页']

---


# mybatis 中的分页

# 参考解答

mybatis中的分页有两种：一是mybatis自带的逻辑分页，二是自己编写分页sql实现物理分页

## 逻辑分页例子

Mapper接口：
```java
public interface EmpMapper {
	@Select("select * from emp")
	public List<Emp> findByPage(RowBounds rb);
}
```
使用：
```java
EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
RowBounds rb = new RowBounds(0, 5); // 查询第一页，每页5条
List<Emp> list = mapper.findByPage(rb);
```

逻辑分页的工作原理是：根据sql查询所有记录，然后通过jdbc中的的可滚动结果集实现分页，其中由RowBounds确定了本页第一条记录的下标(offset)和本页需要几条记录(limit)。

它的优点是实现简单，无需通晓分页sql的编写，缺点是在需要获取整个查询结果集来实现分页，效率低，尤其在数据量较大时。

## 物理分页例子
Page 分页信息类：

```java
public class Page {	
	private int page; // 页号	
	private int rows; // 每页记录数
	public Page(int page, int rows){
		this.page = page;
		this.rows = rows;
	}
	public int getPage() {
		return page;
	}
	public void setPage(int page) {
		this.page = page;
	}
	public int getRows() {
		return rows;
	}
	public void setRows(int rows) {
		this.rows = rows;
	}
	// 结束下标
	public int getEnd() {
		return rows * page;
	}	
	// 起始下标
	public int getBegin() {
		return rows * (page-1);
	}
}
```

Mapper接口：
```java
public interface EmpMapper {
	public List<Emp> findByPage(Page page);
}
```

Mapper XML：
```xml
<select id="findByPage" parameterType="Page" resultType="Emp">
	<![CDATA[
	select * from 
		(select a.*, rownum rn from 
		  (select * from emp) a
		where rownum <= #{end})
	where rn > #{begin}	
	]]>
</select>
```

使用：
```java
EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
Page page = new Page(1,5); // 查询第一页，每页5条
List<Emp> list = mapper.findByPage(page);
```

物理分页是直接使用sql语句实现分页，只会查询本页数据。

优点是效率高，缺点是不同数据库的分页sql语句有所不同，而mybatis并没有提供数据库方言，造成兼容性差。

> **注意** 有第三方的mybatis插件提供了更好的分页实现，主要是利用mybatis拦截器，在sql执行前，根据数据库方言，对原始硬编码植入分页代码

---

