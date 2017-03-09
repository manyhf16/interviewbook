---
search:
    keywords: ['spring','依赖注入','di']

---




# spring中依赖注入的方式？

# 参考解答

* spring中依赖注入主要方式有set注入和构造注入。
* 另外还可以通过@Autowired @Resource @Value 进行注入，它们可以分别用于set方法注入、构造方法注入和field属性注入。
* 最后，spring中的DefaultListableBeanFactory提供了容器外的bean属性的织入

# 例如
xml格式的set注入：
```xml
<property name="属性名" ref="要注入的bean id"/>
```
xml格式的构造注入：
```xml
<constructor-arg index="构造方法参数下标" ref="要注入的bean id"/>
```
xml格式的值注入（也属于set注入和构造注入）：
```xml
<property name="属性名" value="属性值"/>
<constructor-arg index="构造方法参数下标" value="参数值"/>
```
---