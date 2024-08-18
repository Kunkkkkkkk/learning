例子 BeanUtil.copyProperties(user,UserDTO.class) 这个的返回值是UserDTO的一个匿名对象
	而原版的BeanUtils返回的是一个方法 	

常用的方法(和原版不同的)

---



`BeanUtil.copyProperties(要复制的对象，目标的类)` 直接把属性名相同的值赋值过去，在类转该类的DTO时很好用

---



`BeanUtil.beanToMap(对象)` 直接把对象转成Map类型，这里可以通过指定泛型来自定义类型

🌰:

```java
Map<String, Object> stringObjectMap = BeanUtil.beanToMap(userDTO);
```

这个方法有高级设置，针对于转化成指定的类型，比如说用StringRedisTemplate的时候，他的泛型是<String,String> 然后我们要存的对象里面的id属性是Long，而Long无法自动转换成String类型，报错。就可以指定

```java
 Map<String,Object> map = BeanUtil.beanToMap(userDTO,new HashMap<>(), CopyOptions.create()
                .setIgnoreNullValue(true)   //设置忽视控制
                .setFieldValueEditor((k,v)->(v.toString())));
//设置 field 和 value 的类型 (k,v)->(k.转换的,v.转换的) 没要求两个都要写
```

这里注意，假如是说要转换的对象里面有的值为null，可以使用 `v!=null?v.toString():""` 

---

`BeanUtil.fillBeanWith(map,new User(),是否忽略转换中的错误)` 直接把map类型的东西转成要的类

