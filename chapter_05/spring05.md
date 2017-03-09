# Spring 中什么时候引起NoWritablePropertyException，什么时候出现could not open class path resource[ApplicationContext.xml]


# 参考解答

在使用set方法进行注入时，如果该set方法不存在，就会报NoWritablePropertyException异常；

第二个错误显然是构造Spring容器时，配置文件的路径没有写对。