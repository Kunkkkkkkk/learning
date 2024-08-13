**注解总结**



**@RestController** :放在controller层上面，restcontroller = controller + responsebody,返回一个JSON文本的数据，Spring MVC的默认返回是model and view



**@Slf4j** :在Java类中使用**@Slf4j**注解后，不需要手动创建Logger对象，Lombok会自动生成一个名为**log**的静态Logger成员变量，使得你可以通过这个**log**对象来记录日志，而无需每次都创建一个Logger实例。在controller层里面例如 [log.info](http://log.info)( “新建用户:{}”,user);



**@param**



**@EnableCaching** :用于启用应用程序中的缓存功能。它的作用是告诉Spring框架启用缓存机制，允许你将方法的结果缓存起来，以提高应用程序的性能。可以帮助你轻松地启用和配置缓存功能，提高应用程序的性能，并通过声明性的方式管理缓存，以减少重复计算和数据查询的开销。它通常在需要缓存数据的应用程序中使用，特别是在处理大量数据或频繁访问的情况下，以提高效率。



**@Cacheable** : 注解在方法上，表示该方法的返回结果是可以缓存的。也就是说，该方法的返回结果会放在缓存中，以便于以后使用相同的参数调用该方法时，会返回缓存中的值，而不会实际执行该方法。



**@CacheConfig**: @CacheConfig(cacheNames = "department")**@CacheConfig** 是Spring框架中用于配置缓存的注解之一，用于为类提供默认的缓存配置。在你的示例中，**@CacheConfig(cacheNames = "department")** 表示为标注了这个注解的类配置了一个默认的缓存名，即 "department"。





**@CacheEvict** 是 Spring Framework 中的注解之一，用于配置缓存的清除（eviction）

![Pasted Graphic 31.png](blob:file:///47b89257-0913-4fac-bdd1-3af77a509950)

CacheEvict (allEntries = true)这里表示清楚条目里的所有条目





**@TableName:**@TableName是**mybatis-plus**中的注解，主要是实现实体类型和数据库中的表实现映射。不要将@TableName和@Table注解认为是一个，虽然功能相同，但是，@TableName是mybatis-plus中的注解，@Table是Hibernate中的注解。

![Pasted Graphic 32.png](blob:file:///305345c0-0707-4976-aed3-95d9327afd3a)



**@Service @Mapper：**加上该注解会将当前类自动注入到spring容器中，不需要再在applicationContext.xml文件定义bean了。 service写在实现层里





**@RequiresRoles(“”):** 	是apache shiro框架里的一个用于授权的注解之一。**@RequiresRoles("admin")** 是 Apache Shiro 框架中用于授权的注解之一。它的作用是要求当前用户必须拥有指定角色才能访问或执行标注了这个注解的方法。

添加角色的示例：

public class CustomRealm extends AuthorizingRealm {

  @Override

  protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {

​    // 查询当前用户的角色信息

​    Set<String> roles = new HashSet<>();

​    // 从数据库或其他数据源中获取用户的角色信息，并将其添加到 roles 集合中

​    roles.add("admin");

​    roles.add("user");

​     

​    SimpleAuthorizationInfo authorizationInfo = new SimpleAuthorizationInfo(roles);

​    return authorizationInfo;

  }



  // 其他 Realm 方法...

}





**@Resource和@Autowired:** 都是依赖注入



**@Requestbody和@PathVariable和@RequestParam:**

**数据库里bigint在controller里传参可以用Long**

![Pasted Graphic 27.png](blob:file:///de61eb0d-6476-41ee-b194-5fb94beca035)



![Pasted Graphic 28.png](blob:file:///7905c0e4-ac3a-43ae-9954-d9788ed2434b)

@PathVariable 标记这个参数是路径参数(前端传参数过来）

Query

![Pasted Graphic.png](blob:file:///b9759c70-29f8-49b9-b3d8-86dc5a14676d)

**(还有一个 Integer id)**





- **@RequestBody** 用于处理请求体中的数据，适用于接收复杂结构的数据。
- **@RequestParam** 用于从 URL 查询参数中获取数据，适用于获取简单的键值对参数。
- 你可以根据具体的需求和数据传输方式来选择使用哪个注解。通常，POST 请求使用 **@RequestBody** 处理请求体数据，而 **GET** 请求使用 **@RequestParam** 处理查询参数。

![Pasted Graphic_1.png](blob:file:///e6322550-f0ed-4929-af5f-5b576b44a1cc)





**@Mapping之类的**：括号里面的路径别看前端那个，看接口文档里的，没有接口文档就用F12里看头文件









**@Builder：Lombok那个备忘录里有**





**@Component:** 是 Spring 框架中的一个核心注解，用于将一个类标记为 Spring 托管的组件。这意味着 Spring 容器会自动创建该类的实例，管理其生命周期，并使它可以在应用中被注入和使用。

**@Component** 注解是 Spring 的核心注解之一，还有其他与之相关的注解，如 **@Service**、**@Repository** 和 **@Controller**，它们都是 **@Component** 的特例，专门用于标记不同种类的 Spring 组件，以便更好地表示它们的角色和用途。