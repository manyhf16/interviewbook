---
search:
    keywords: ['spring','生命周期','init','destroy','lazy']

---


# spring 生命周期方法相关问题
1. 请描述spring中 lazy-init属性的作用和优缺点 
2. 描述init-method 和destroy-method的作用
3. 描述factory-method的作用


# 参考解答

1）lazy-init 是让bean懒惰实例化，默认情况下spring容器创建，那么单例bean也会被创建；如果设置了lazy-init=true 那么就意味着该bean 不会在spring容器创建时创建，而是当它第一次被用到（getBean）时被创建。

* 优点是按需使用，可以加快容器的启动速度、节省容器内存
* 缺点是如果bean之间建立了依赖关系，那么依赖链上的所有bean都必须是lazy-init的，例如service（非lazy） 依赖 dao（lazy），这时候service是不懒惰的，它也会同时导致dao被创建，从而让lazy失去了效果
因为以上缺点，实际开发时，lazy-init的应用范围很小

2）对于单例bean，init-method 和destroy-method 都会生效，分别在bean实例化之后和容器销毁之前被调用；对于prototype bean 仅有 init-method会生效

3）factory-method 用来让spring管理哪些不能通过new关键字创建实例的那些类，例如Calendar 只提供了getInstance静态方法来创建Calendar实例，这时候就配置factory-method="getInstatnce"让spring得知该用哪个静态方法来创建它

---