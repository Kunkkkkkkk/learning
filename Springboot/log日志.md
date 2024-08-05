核心starter里面导入了logging包

其他的starter都是系统启动好再配置所以有XXXAutoconfiguration

但是日志在一启动的时候就要有的。，所以他没有XXXAutoconfiguration，他是监听器

在配置里直接`logging.`



在控制台输出日志

```java
@RestController
public class LogController {
    @GetMapping("/log")
    public String log1() {
        Logger logger = LoggerFactory.getLogger(getClass()); //假如有多个方法都要使用日志，就可以把这一行放上面
        logger.info("日志进来了");
        return "log1";
    }
}
//访问的时候输出2024:08:215  INFO 26819 --- [nio-8080-exec-2] com.lyk.log.controller.LogController     : 日志进来了
```

这样很麻烦，lombok里的 `@Slf4j`，然后可以直接log.XXX(); 比如log.info（）

##### 日志格式

连starter都不是，直接在spring-boot核心的包里，通过检索注解可以找到

![image-20240802114443461](/Users/elfish/Library/Application Support/typora-user-images/image-20240802114443461.png)

假如我们只想修改日期的输出格式，可以 `logging.patten.dateformat`来修改



##### 日志级别

###### 1.级别

ALL  所有日志消息

TRACE  跟踪所有

----

上面很少用

DEBUG  开发调试细节

【INFO】  感兴趣的、关键的日志   <u>默认日志模式</u>

WARN  警告但不错误：比如版本太老了

ERROR  业务错误

FATAL  致命的系统错误

OFF  关闭所有日志

###### 2.修改日志级别

yml文件里

```yml
logging:
		level:
			root: debug   #root是所有的文件
```

```yml
logging:
		level:
			com/lyk/log/controller: debug  #具体的包
```

这时候，假如有多个包需要设置一样的等级，比如debug，这时候可以自定义把若干个包划分到一个组里

```yml
  group:
    abc:
      -
        com.lyk.log.controller
      -
      	com.lyk.log.mapper
```

在springboot里有**两个预先划分好的组 sql和web**，在做相关的开发要查看仔细信息可以直接打开

```yml
logging:
	level:
		sql:debug
```

----

##### 日志输出

```yml
loggeing:
	file：
		name：
		path：
```

不过我尝试了之后无法通过path来输出到指定位置，可以直接路径带文字名写在name里

###### 归档和切割

```yml
logging:
  logback:
    rollingpolicy:

      #file-name-pattern:   他的默认的格式是 日志文件名-时间-该天的第几个.gz压缩包格式
      max-file-size: 3KB  #同一天内大于3KB就自动切割变成新的
```

![image-20240802150141718](/Users/elfish/Library/Application Support/typora-user-images/image-20240802150141718.png)