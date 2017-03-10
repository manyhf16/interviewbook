# hibernate中一对一关系有几种映射方式？


# 参考解答

一对一映射分为共享主键映射和唯一外键映射

## 共享主键：

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
即表B中的id取值来自于表A，它既是primary key 也是foreign key

## 唯一外键

表A
```sql
id name 
1  ''
2  ''
```

表B
```sql
id detail  pid
10  ''     1
20  ''     2
```
即表B中的id是独立的主键，但会有一个pid列取值来着于表A，它是foreign key 并且加了unique 来保证一对一关系

---

