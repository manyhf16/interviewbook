---
search:
    keywords: ['spring','依赖注入','di']

---



# spring中循环注入？

# 参考解答

如果出现如下情况:
类A的构造中引用了类B，而类B的构造中引用了类A，这时候是会出现无限循环的情况，Spring初始化容器会抛异常。

解决方法是将构造注入改造为set方法注入，spring会尽可能晚地处理set依赖关系，换句话说，spring会先构造bean的实例，再进行依赖注入，最后调用生命周期相关方法。

---

