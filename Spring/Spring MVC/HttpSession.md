SpringMVC中 HttpSession可以被Spring自动注入，我们直接使用这个对象

这个是与当前controller请求相关的对象

在我们使用controller的时候，可以传入一个HttpSession对象

```java
@PostMapper("/login")
public Result login(@RequestBody LoginDTO loginDTO,HttpSession session){
}
```

我们可以用session来实现登入验证的原理（**即跨请求（即controller里面的每一个方法）共享**）

A:tomcat会自动把session里的id放进cookie，然后每次请求都会带着这个cookie，然后我们就可以根据这个id拿到session（***比如HttpServletRequest可以通过getSesstion方法拿到***），然后通过里面的方法来拿到存储在session里面的东西来实现验证或者其他操作。

---

常用的方法

`Object getAttribute(String name)`获取会话中的属性值

`void setAttribute(String name, Object value)`设置属性值（有点像redis kv结构）

`void removeAttribute(String name)` 删除属性值

---

如果你去看源码（120%不会去看），你会发现，wtf？HttpSession不是接口吗，为什么能直接使用方法。没毛病还是Spring的自动注入 😋

---

`HttpSession`参数通常不需要使用注解进行标注，因为Spring MVC能够自动解析并注入`HttpSession`对象。