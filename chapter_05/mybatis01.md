---
search:
    keywords: ['mybatis']

---


# 简述mybatis的工作原理及运用？

# 参考解答
mybatis 是一个持久层框架，它封装了jdbc，简化了对数据库增删改查的操作，它支持各种sql语句和存储过程，将参数和结果映射为java中的基本类型、Map对象或POJO对象。

## 工作原理：

1. 加载配置：配置来源于两个地方，一处是配置文件，一处是Java代码的注解，将SQL的配置信息加载成为一个个MappedStatement对象（包括了传入参数映射配置、执行的SQL语句、结果映射配置），存储在内存中。
2. SQL解析：当API接口层接收到调用请求时，会接收到传入SQL的ID和传入对象（可以是Map、JavaBean或者基本数据类型），Mybatis会根据SQL的ID找到对应的MappedStatement，然后根据传入参数对象对MappedStatement进行解析，解析后可以得到最终要执行的SQL语句和参数。
3. SQL执行：将最终得到的SQL和参数拿到数据库进行执行，得到操作数据库的结果。
4. 结果映射：将操作数据库的结果按照映射的配置进行转换，可以转换成HashMap、JavaBean或者基本数据类型，并将最终结果返回。

## 使用经验：
1. MyBatis适用于需要对SQL完全控制的场合，通常这么做可以对SQL进行进一步优化，可以获得更好的性能
2. MyBatis自带的分页实现是逻辑分页，只适用于数据量非常少的情况，更多情况下应该使用自己的物理分页SQL取代它

> POJO 即(Plain Old Java Objects) 可视为java bean，实体类的同义词。