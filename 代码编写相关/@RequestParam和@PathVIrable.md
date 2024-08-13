**@RequestParam**

将请求参数绑定到你控制器controller的方法参数上



区别是url不同



//@PathVariable用法

@RequestMapping(value = "/test/{id}",method = RequestMethod.DELETE)

public Result test(@PathVariable("id")String id) 



//@RequestParam用法,注意这里请求后面没有添加参数

@RequestMapping(value = "/test",method = RequestMethod.POST)

public Result test(@RequestParam(value="id",required=false,defaultValue="0")String id) 

注意上面@RequestParam用法当中的参数。







作用就是当需要传多个不同参数的时候，比如多种参数的筛选，就需要@RequestParam

