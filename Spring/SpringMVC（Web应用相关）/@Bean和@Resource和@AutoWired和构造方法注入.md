`@Resource`注解本身不能创建新的Bean。它的主要作用是将已经存在于Spring容器中的Bean注入到目标类的字段、方法或属性中。`@Resource`用于依赖注入，而不是Bean的定义或创建。

```
@Configuration
public class MvcConfig implements WebMvcConfigurer {
    @Resource
    private StringRedisTemplate stringRedisTemplate;
```

`StringRedisTemplate`已经作为一个Bean存在于Spring容器中，Spring会根据其配置自动创建并管理这个Bean。

你需要的是使用这个已经存在的`StringRedisTemplate` Bean，所以使用`@Resource`将其注入即可。





resource和autowired都是字段注入。resource按名称也就是后面的，但是找不到会按类型，也可以指定一个name在注解里，autowired是按类型

```java
private UserService_前 userService_后;
```

autowired爆黄色的原因就是可能存在多个同类型的，会导致模糊注入。

一个例子

```java
@Resource
private StringRedisTemplate abc;

```

这里会按abc去找，找不到再按StringRedisTemplate找



---



autowired是字段注入

字段（成员变量）

```java
@Component
public class MyService {
    
    @Autowired
    private UserService userService; // 这里的 userService 是 MyService 类的成员变量

    public void doSomething() {
        userService.performAction(); // userService 是被注入的 UserService 类的实例
    }
}

```





#### 1.可维护性

使用构造函数注入可以使依赖关系更加清晰，并且如果有未满足的依赖，构造函数会立即抛出异常，提醒开发者修正，而不是在运行时遇到空指针异常。

#### 2.字段的完整性

使用字段注入时，依赖项的注入是在对象已经被实例化后才进行的。这意味着在对象的构造过程中，字段可能仍然为空，导致部分逻辑不能在对象构造时安全地使用这些依赖。

而构造注入是在对象刚创建就注入了

#### 3.对于不可变对象

更利于那些可变的对象，更灵活，而对于不可变对象，则构造方法注入更好用

#### 4.是否便于单元测试

```java
public class MyServiceTest {

    @Test
    public void testDoSomething() {
        // 创建 UserService 的 mock 对象
        UserService mockUserService = mock(UserService.class);
        
        // 通过构造函数注入依赖
        MyService myService = new MyService(mockUserService);

        // 执行测试
        myService.doSomething();

        // 验证 mock 对象的行为
        verify(mockUserService).performAction();
    }
}

```

而字段注入是私有的，不好单元测试