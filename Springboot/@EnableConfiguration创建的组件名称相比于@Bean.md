1.`@Component`创建的就是类名，不过首字母小写

2.`@Bean`创建的就是方法名

```java
@Bean
public Cat Cat001(){
  return new Cat();
}
//就是001
```

3.`@EnableConfiguration` 是 <u>**类名-带路径的类**</u>   的形式

```
cat-com.example.demo.bean.Cat
```