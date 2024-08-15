`@Resource`注解本身不能创建新的Bean。它的主要作用是将已经存在于Spring容器中的Bean注入到目标类的字段、方法或属性中。`@Resource`用于依赖注入，而不是Bean的定义或创建。

```
@Configuration
public class MvcConfig implements WebMvcConfigurer {
    @Resource
    private StringRedisTemplate stringRedisTemplate;
```

`StringRedisTemplate`已经作为一个Bean存在于Spring容器中，Spring会根据其配置自动创建并管理这个Bean。

你需要的是使用这个已经存在的`StringRedisTemplate` Bean，所以使用`@Resource`将其注入即可。