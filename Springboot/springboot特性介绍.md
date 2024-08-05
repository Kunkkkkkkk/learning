

简化应用的配置和创建

##### 1.可以【快速创建spring应用】，之前SSM需要导很多包，配置很多文件

##### 2.【内置servlet容器】比如tomcat，jetty等

```
原来Web开发都是基于servlet开发，把项目打成一个war包放到tomcat等webapp目录下，在运行tomcat的时候就会顺带着启动。
war包的结构大致如下
myproject.war
├── META-INF/
│   └── MANIFEST.MF
├── WEB-INF/
│   ├── classes/
│   │   └── [编译后的 Java 类文件]
│   ├── lib/
│   │   └── [项目依赖的库文件]
│   └── web.xml
├── [前端页面]
│   ├── index.html
│   ├── styles/
│   │   └── style.css
│   ├── scripts/
│   │   └── app.js
│   └── images/
│       └── logo.png
└── [其他资源文件]
```

直接把项目打成jar包，在java环境直接java-jar就启动了

##### 3.starter（场景启动器），

后面有自定义starter 

之前的时候，比如要实现json、web、异步请求、文件上传阿里云，需要导入一大堆东西，现在只要一个starter，就是pom里的依赖坐标，比如之前mybatis要导入一堆东西，这里只要在pom文件里面导入一个mybatis依赖就行

##### 4.自动配置

【约定大于配置】：因为大多数情况下，默认约定已经可以足够。

只需要引入起步依赖，框架会根据默认决定进行配置，比如配置端口号这些，然后可以通过application.yml文件来自定义一些配置来覆盖默认的配置

##### 5.提供了生产级的特性

1.可以通过内置的工具来监控指标和健康检查（比如查看是否存活）

2.<u>允许外部化配置</u>（等下看看）

可以在项目程序运行时修改配置而不用重新打包

```
想象一下，已经打成了jar包，这时候要修改内部的配置，那么需要打开源码，修改了之后重新打成jar包再重新上线。很麻烦，可以直接在外面写一个application.yml，然后重启jar包
```

```
将项目打包：清理项目并将其打包成一个 JAR 文件或
mvn clean package
/path/to/your/external/
├── my-spring-boot-app.jar
└── application.yml
像这样启动jar包的时候，会优先加载外部的配置文件
```

##### 6.不会生成垃圾代码，不用写一大堆xml文件

