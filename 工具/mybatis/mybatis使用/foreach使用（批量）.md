```java
    void insert(List<DishFlavor> list);


<insert id="insert" parameterType="com.sky.entity.DishFlavor">
    insert into dish_flavor(dish_id,name,value) values
<foreach collection="list" item="df">
   (#{df.dishId},#{df.name},#{df.value})
</foreach>
</insert>
```

这里的list就是传的参数





`<foreach collection="ids" item="id" separator=" OR ">`



在一个list，根据这个删除多个时，相比于上面的or，更推荐使用in

```
where id in 
<foreach collection="ids" item="id" open="(" ,separator=",",close=")" >
#{id}

```

