---
search:
    keywords: ['struts2','使用步骤']

---

# Struts2的应用，它的功能有哪些？ 使用步骤？

# 参考解答：

Struts2 可以用来开发基于MVC的web应用程序。 Struts2有如下的主要功能：

 1) 基于MVC(Model-View-Controller)设计模式，基于aop拦截器来处理用户请求，使用Action控制器来联系模型和视图
  
 2) 提供了一套标签库，用来创建动态页面
 
 3) 简化了请求参数接收和类型转换、作用域变量传输、支持多种视图技术、解耦了servlet API，让开发和测试更为容易
 
 4) 提供web应用程序开发时所需要的通用功能，例如：表单重复提交、国际化支持等
 
 
 # 使用步骤：
 
1) 首先在struts.xml中配置一个action：
```xml
<struts>
  <package name="test" namespace="/hello" extends="struts-default">
    <action name="helloworld"  class="com.xx.action.HelloAction" method="execute">
      <result name="success">/WEB-INF/list.jsp</result>
    </action>
  </package>
</struts>
```
其中`<action>`标签用来配置路径和java类的映射关系，`<result>`标签用来配置视图路径。

2) aciton类可以是普通的java类或继承了ActionSupport的java类，例如：
```java
public class HelloAction{
    private String name;
    public String getName(){
        return this.name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String execute(){
      System.out.println("进入了HelloAction");
      return "success";
    }
}
```
3)  向该action的发送请求：`/hello/helloworld.action?name=zhangsan`，这时name参数会被struts赋值给HelloAction的name属性。

4)  根据action方法的返回值找到`<result>`标签，来确定要转发的视图是 list.jsp

5)  在视图中可以使用 `<s:property value="name"/>` 来获取HelloAction中name属性值显示生成html

---