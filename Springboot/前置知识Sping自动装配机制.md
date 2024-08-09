Spring自动装配是Spring框架提供的一种特性，它可以让Spring自动处理bean之间的依赖关系，而不需要在Spring配置文件中显式地声明每一个依赖。自动装配可以基于注解或XML配置进行。

```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {

    @Autowired
    private ServiceA serviceA;

    @Autowired
    private ServiceB serviceB;

    public void doSomething() {
        serviceA.doSomething();
        serviceB.doSomething();
    }

    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        AppConfig appConfig = context.getBean(AppConfig.class);
        appConfig.doSomething();
    }
}

@Component
class ServiceA {
    public void doSomething() {
        System.out.println("ServiceA is doing something.");
    }
}

@Component
class ServiceB {
    public void doSomething() {
        System.out.println("ServiceB is doing something.");
    }
}
```

**`@Autowired`** 注解用于自动装配依赖。Spring容器会自动查找类型匹配的Bean（`ServiceA`和`ServiceB`），并将它们注入到`AppConfig`类中的相应字段。这样，`serviceA`和`serviceB`就<u>**不需要显式地创建和管理，而是由Spring容器自动注入。**</u>

