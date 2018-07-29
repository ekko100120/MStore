# SpringMVC总结

***
#### 1 SpringMVC常用注解
**@Controller**

通过@controller标注即可将class定义为一个controller类

**@RestController**

组合注解@Controller和@ResponseBody

**@RequestMapping**

- **value** 	表示需要匹配的url的格式

- **method**    表示所需处理请求的http 协议(如get,post,put,delete等)


```
@RequestMapping(value = "/member/add",method = RequestMethod.POST)
```
- **params**	格式为”paramname=paramvalue” 或 “paramname!=paramvalue”。 表示参数必须等于某值，或者不等于才进入此映射方法。不填写的时候表明不限制。所以当请求/testParams.do?param1=value1&param2=value2 的时候能够正确访问到该testParams 方法：


```
@RequestMapping (value= "testParams" , params={ "param1=value1" , "param2" , "!param3" })
    public String testParams() {
       System. out .println( "test Params..........." );
       return "testParams" ;
    }
```


- **headers**	用来限定对应的reqeust请求的headers中必须包括的内容，例如headers={"Connection=keep-alive"}, 表示请求头中的connection的值必须为keep-alive。当请求/testHeaders.do 的时候只有当请求头包含Accept 信息，且请求的host 为localhost 的时候才能正确的访问到testHeaders 方法：

```
@RequestMapping (value= "testHeaders" , headers={ "host=localhost" , "Accept" })
    public String testHeaders() {
       return "headers" ;
    }
```

- **produces**
指定返回的内容类型，仅当request请求头中的(Accept)类型中包含该指定类型才返回
```
@RequestMapping (value= "testProduces" , produces="text/plain;charset=utf-8")
@RequestMapping (value= "testProduces" , produces="application/json;charset=utf-8")
@RequestMapping (value= "testProduces" , produces="application/xml;charset=utf-8")

```

**@DeleteMapping**

映射HTTP的delete请求，等同于`@RequestMapping(value = "/member/add",method = RequestMethod.DELETE)`，以下同理

**@GetMapping**

**@PostMapping**

**@PutMapping**


**@RequestParam**

- **value** 对应表单name空间的值
- **required**	是否允许为空
- **defaultValue**	默认值

```
@RequestMapping ( "requestParam" )
   public String testRequestParam( @RequestParam(required=false) String name, @RequestParam ( "age" ) int age) {
       return "requestParam" ;
}
```

**@PathVariable**

获得地址栏中传的参数 例如：

```
@RequestMapping(value="/{groupId}.do")
public void detail(@PathVariable long groupId){
    groupRepository.selectOne(groupId);
}
```

**@RequestBody**

用来将指定的客户端发送过来的请求参数的数据格式转换成Java实体


```
@RequestMapping(value = "/xxxxx.do")
public void create(@RequestBody() String host){
    System.out.println("-----------" + host);
}
```

**@ResponseStatus**
返回一个指定的http response状态码。


```
@ResponseStatus(reason="no reason",value=HttpStatus.BAD_REQUEST)
@RequestMapping("/responsestatus")
public void responseStatusTest(){

}
```

**@CookieValue**
可以把Requestheader中关于cookie的值绑定到方法的参数上。

例如有如下Cookie值：

　　JSESSIONID=415A4AC178C59DACE0B2C9CA727CDD84，即把JSESSIONID的值绑定到参数cookie上。


```
@RequestMapping("/displayHeaderInfo.do")  
 public void displayHeaderInfo(@CookieValue("JSESSIONID") String cookie)  {  
 }
```

**@ExceptionHandler**

@RequestMapping("/exception")
 public void ExceptionTest() throws Exception{
    throw new Exception("i don't know");
 }    
 @ExceptionHandler
 public String handleException(Exception e,HttpServletRequest request){  
    System.out.println(e.getMessage());  
    return "helloworld";  
 }
```
****

#### 1 SpringMVC 拦截器(Interceptor)，过滤器(filter)，监听器(Listener)


**比较:**
![拦截器VS过滤器VS监听器](/pic/拦截器_监听器_过滤器.bmp)

##### 1.拦截器
**原理:**
```
大部分时候，拦截器方法都是通过代理的方式来调用的。Struts2的拦截器实现相对简单。当请求到达Struts2的ServletDispatcher时，Struts2
会查找配置文件，并根据配置实例化相对的拦截器对象，然后串成一个列表（List），最后一个一个的调用列表中的拦截器。Struts2的拦截器是可
插拔的，拦截器是AOP的一个实现。Struts2拦截器栈就是将拦截器按一定的顺序连接成一条链。在访问被拦截的方法或者字段时，Struts2拦截器链
中的拦截器就会按照之前定义的顺序进行调用。
```


**构建步骤:**

1. 通过注解注册定义的拦截器，并通过@Componet定义为spring bean
2. 自定义一个实现了Interceptor接口的类，或者继承抽象类HandlerInterceptorAdapter,根据反射机制获取method注解数据。
3. 在配置类中重写addInterceptors接口添加拦截器和配置拦截路径

```Java
@Configuration
@ComponentScan(basePackages = "com.mecury.boot")
public class AppConfiguration implements WebMvcConfigurer {

    @Autowired
    private HandlerInterceptor handlerInterceptor;
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(handlerInterceptor).addPathPatterns("/**");
    }

```
***
##### 2.监听器
[监听器概述](https://blog.csdn.net/reggergdsg/article/details/52891311)

[Annotation监听器](https://blog.csdn.net/erbao_2014/article/details/68924231?locationNum=9&fps=1)

[常用监听器](http://chenjumin.iteye.com/blog/2249833)


***
##### 3. 过滤器


[https://blog.csdn.net/reggergdsg/article/details/52821502](https://blog.csdn.net/reggergdsg/article/details/52821502)


[https://blog.csdn.net/zzp448561636/article/details/77745502](https://blog.csdn.net/zzp448561636/article/details/77745502)
