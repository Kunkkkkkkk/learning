###### 谈谈对spring的理解和认识

核心特性：IOC容器、AOP、事务管理、MVC框架

---

IOC容器：inversion of Control控制反转。就是把对象创建和依赖管理的控制权从代码中反转到spring容器中。让ioc容器来创建对象和管理生命周期。ioc的核心概念是bean和DI（dependence injection，可以字段注入，构造方法注入和setter注入【car和engine】，创建对象实例不用new。

```java
@Component
public class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }

```

AOP：允许开发者自定义横切关注点与业务逻辑分离，增强代码的模块化，里面设置通用操作如日志操作、事务管理、权限检查等。提高代码的可重用性和可维护性。

事务管理：Spring提供了一致的事务管理接口，支持声明式和编程式事务。

MVC框架：基于servlet狗降低Web框架，Model-View-Controller



###### AOP的理解

**1.@pointcut**

里面要空的方法体，在@Before啊这些通知上面也可以直接写切点表达式，使用pointcut的目的是提高代码的重用性

```java
@Pointcut("execution(String com.lyk.aopdemo.controller.AOPController.printWords(..))")
    public void printPointcut() {}

    //切点表达式execution
    @Before("printPointcut()")
    public void beforePrint(){
        log.info("beforePrint");
    }
```

切点表达式

`@Before("execution(* com.lyk.controller.UserController.createUser(..))")`

第一个*用来指定返回值类型

若要指定传参内容的方法

`@PointCut("execution(* *.*(String,int))")`

指定注释

`@Pointcut("@annotation(com.example.CustomAnnotation)")`

模糊查询那样的方法名开头

`@Pointcut("execution(* update*(..))")`

**2.joinpoint**

signature这个对象包含了被拦截方法的基本信息，比如方法名、返回类型、参数类型等。这个 `Signature` 对象不能直接操作方法本身，但可以用来获取与方法相关的各种信息。