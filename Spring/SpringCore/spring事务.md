`@Transactional`

当一个方法被`@Transactional`注解标注时，Spring会在运行时为该类生成一个代理对象。这个代理对象会拦截对标注方法的调用，在方法执行前开启事务，方法执行完毕后提交事务或在出现异常时回滚事务。



当在一个类中自己调用了一个带事务的方法，这时候默认的 方法使用是用的this，也就是实例对象，这个调用不会通过代理对象，而是直接调用了实际的方法实现。这意味着Spring的事务拦截器不会被触发，事务也就不会正常开启或提交/回滚。

我们得通过代理对象调用这个方法。在Spring框架中，通常可以通过以下两种方式获取代理对象：

- **自注入**：通过Spring容器注入自身类的代理对象。比如，在类中添加`@Autowired`注解并注入自己：

  ```java
  java
  复制代码
  @Autowired
  private YourClassName self;
  
  public void someMethod() {
      self.createOrderId(voucherId, voucher); // 通过代理对象调用
  }
  ```

- **使用`AopContext`**：通过`AopContext.currentProxy()`方法获取当前对象的代理对象：

  ```java
  java
  复制代码
  public void someMethod() {
      ((YourClassName) AopContext.currentProxy()).createOrderId(voucherId, voucher); // 通过代理对象调用
  }
  ```

如果是impl里面 ，更建议使用接口的代理对象，

即`UserService uuuu= (UserService)AopContext.currentProxy().void();`

**接口优先**: 如果你的`Service`实现类实现了接口，并且你没有特殊需求，建议通过接口类型注入代理对象。这符合Spring的设计原则，并且更灵活。