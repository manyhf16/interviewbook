---
search:
    keywords: ['hibernate','核心接口']

---

# Hibernate有哪5个核心接口？

# 参考解答：

1. Configuration接口：用于读取hibernate配置，根据配置信息创建SessionFactory对象； 

2. SessionFactory接口：一个SessionFactory实例对应一个数据源，应用从SessionFactory中获得Session实例。SessionFactory有以下特点：
  * 它是线程安全的，这意味着它的同一个实例可以被应用的多个线程共享。
  * 它是重量级的，这意味着不能随意创建或销毁它的实例。如果应用只访问一个数据库，只需要创建一个SessionFactory实例，在应用初始化的时候创建该实例。如果应用同时访问多个数据库，则需要为每个数据库创建一个单独的SessionFactory实例。

3. Session接口：Session接口是Hibernate应用使用最广泛的接口。Session也被称为持久化管理器，它提供了和持久化相关的操作，如添加、更新、删除、加载和查询对象。Session有以下特点：
  * 不是线程安全的，因此在设计软件架构时，应该避免多个线程共享同一个Session实例。
  * Session实例是轻量级的，所谓轻量级，是指它的创建和销毁不需要消耗太多的资源。这意味着在程序中可以经常创建和销毁Session对象，例如为每个客户请示分配单独的Session实例，或者为每个工作单元分配单独的Session实例。
  * Session有一个缓存，被称为Hibernate的第一级缓存，它存放被当前工作单元加载的对象。每个Session实例都有自己的缓存，这个Sesion实例的缓存只能被当前工作单元访问。

4. Transaction接口：管理事务

5. Query和Criteria接口：执行数据库的查询。
Query和Criteria接口是Hibernate的查询接口，用于向数据库查询对象，以及控制执行查询的过程。Query实例包装了一个HQL查询语句，HQL查询语句和SQL查询语句有些相似，但HQL查询语句是面向对象的，它引用类句及类的属性句，而不是表句及表的字段句。Criteria接口则更彻底地实现了面向对象查询，将数据查询条件封装为一个对象，Criteria接口擅长执行动态查询（多条件组合）。


---