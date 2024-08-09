```java
@Configuration
public class EQconfig {

    // fanout交换机
    @Bean
    public FanoutExchange fanoutExchange() {
        return new FanoutExchange("hmall.fanout");
    }

    // fanout队列
    @Bean
    public Queue fanqueue() {
        return new Queue("fanout.queue");
    }

    // 绑定 fanout交换机 和 fanout队列
    @Bean
    public Binding binding1(@Qualifier("fanqueue") Queue queue, @Qualifier("fanoutExchange") FanoutExchange exchange) {
        return BindingBuilder.bind(queue).to(exchange);
    }
}

```

上面的依赖注入是根据 `@Qulifier`注解来区分注入的参数的，这样方便代码的可读性和维护性。

另一种方法就是我们平时的直接传入唯一的组件命名，那一种仅限于单人小项目。