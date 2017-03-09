---
search:
    keywords: ['springmvc','注解']

---

# springMVC常见注解?


# 参考解答:
|注解名称|含义
|-----|:-----:|
|@Controller |用来定义控制器类，并配合`<component-scan>`让spring扫描到并通过容器管理该类|
|@RequestMapping|用来映射请求路径，并可以定义路径参数，以及各种条件匹配|
|@RequestParam|当请求参数与方法参数名不一致时，通过这个注解来映射，它还可以指定请求参数能否为null，以及指定请求参数的默认值|
|@PathVariable|用来将路径参数映射至方法参数|
|@ModelAttribute|加在方法参数上表示该参数会存入Model加在方法上，表示方法的返回值会存入这次请求的Model|
|@SessionAttributes|用来指明哪些Model属性也会存入Session域|
|@ExectionHandler|用来映射控制器方法处理请求异常|
|@InitBinder|用来初始化控制器中的WebDataBinder，以提供数据类型转换和校验功能|
|@ControllerAdvice|用来作为所有控制器的通知类，用来实现全局的参数绑定，公共的Model属性，全局异常处理|

---