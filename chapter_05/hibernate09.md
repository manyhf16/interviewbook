# hibernate中一对一关系有几种映射方式？


# 参考解答

一对一映射分为共享主键映射和唯一外键映射

共享主键：
表A
```sql
id name 
1  ''
2  ''
```

表B
```sql
id detail
1  ''
2  ''
```