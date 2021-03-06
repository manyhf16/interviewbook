---
search:
    keywords: ['mybatis']

---

# mybatis中的缓存

# 参考解答

* 缓存主要的目的是提高查询效率，减轻数据库的访问压力。mybatis 中的缓存分为一级缓存与二级缓存

* 一级缓存是每个SqlSession自带的，无需额外配置，在SqlSession打开一级缓存就会创建，第一次查询的结果会存入一级缓存，后续只要执行了相同的sql，那么会从缓存中获取上次的结果，而不必查询数据库，从而提高了效率。当SqlSession关闭时，一级缓存也会清空。不同的SqlSession之间不能共享一级缓存的结果。

* 二级缓存从功能上与一级缓存类似，不同在于二级缓存的数据可以在多个SqlSession中共享，SqlSession1查询的结果会存入二级缓存，只要执行的sql相同，SqlSession2也可以从二级缓存中获取该结果。二级缓存需要在映射文件中添加 `<cache>` 标签来进行配置。

* mybatis中二级缓存是一个Mapper对应一个二级缓存，此Mapper中的查询，会将结果存入二级缓存，但同一Mapper中的增删改，会清空二级缓存（为了防止脏数据）。从这个角度讲，只有数据不频繁修改时，才适合使用二级缓存。

---
