## spring 相关笔记

#### 1 总体架构

[spring总体架构](https://blog.csdn.net/sunchen2012/article/details/53939253)

##### spring context 总结


1. `AnnotationConfigApplicationContext`和`@Configuration`和 `@Bean`

```Java
// 1.@bean注解声明bean,可以很方便的利用第三方的API构建spring bean
@Bean
   public Book book(){
       return  new Book();
   }


//2.@Configuration 注解将当前class定义为一个spring 的配置类bean，AnnotationConfigApplicationContext通过加载配置类bean，来加载其中的bean实例，从而替换掉spring的XML配置
//2.1优点，方便简洁，更加舒服
//2.2可以采用@Import和@ImportResource导入其他的bean配置类或者XML文件
//2.3可以在该类上加上@Enable*实现spring的注解配置
//2.4@AutoWired 注入bean的reference
//2.5 @Value 注入基本数据类型
@Configuration
@EnableCaching
@ImportResource("classpath:beans.xml")
public class CacheConfig {

    @Bean
    public Book book(){
        return  new Book();
    }

    @Bean
    public CacheManager cacheManager(){
        SimpleCacheManager cacheManager = new SimpleCacheManager();
        cacheManager.setCaches(Arrays.asList(new ConcurrentMapCache("sampleCache")));
        return cacheManager;
    }
}

//AnnotationConfigApplicationContext类实例化spring的ApplicationContext


// 方式一，构造函数加载
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(CacheConfig.class，*config.class);

// 方式二,动态加载
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
 //动态加载configuration
 context.register(BeanConfig.class, CacheConfig.class);
 context.refresh();

 // 方式三,scan 扫描,小坑：scan时，需要在对应的bean上加上@Componet注解
 AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
       context.scan("com.mercury.spring");
       context.refresh();

```
