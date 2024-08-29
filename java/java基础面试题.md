###### 深拷贝和浅拷贝：

一个是新的对象，一个还是引用指向被拷贝的对象。注意对象内的对象是引用还是新建。3种深方法：1.实现cloneable方法 2.把要拷贝的对象序列化，然后再反序列化 3.手动递归对象和引用类型字段



###### GC回收new出的对象的时机：

1.gc内部有算法，引用计数法，当改对象被引用的数为0时被清除

2.可达性，从根对象（方法区的静态属性和局部变量）出发可以通过引用链到达该对象则说明可达，反之不可达就会清理

3.重写finalize方法。（不推荐，执行时间不定）



###### 反射在框架里面的应用场景

1.JDBC 连接数据库时使用 Class.forName()通过反射加载数据库的驱动程序

`Class.forName("com.mysql.cj.jdbc.Driver")`

2.spring 早期用xml文件配置bean

- 将程序中所有XML或properties配置文件加载入内存
- Java类里面解析xml或者properties里面的内容，得到对应实体类的字节码字符串以及相关的属性信息
- 使用反射机制，根据这个字符串获得某个类的Class实例
- 动态配置实例的属性



###### 注解的原理和作用域

基于反射原理，在编译过程或通过编译器插件或者是注解处理器，生成额外的代码和文件（相当于一小串注解变成了一大串代码），然后在运行的时候，反射机制获取到字节码对象，然后通过得到所有方法再使用isAnnotation(注解名)查看是否包含某个注解，然后getAnnotation拿到注解的实例对象，然后通过这个对象调用注解中的方法。

作用域：类、方法、字段



###### try{return “a”} fianlly{return “b”}这条语句返回啥

finally里面的会覆盖try里面的，return b



###### ==和equals

字符串：==比较对象地址，equals比较包含内容

非字符串：如果不重写的话==和equals一样的





###### StringBuilder StringBuffer

都是用来减少修改字符串过程产生大量对象

两个作用一样，原理都是构造一个可变数组

buffer线程安全，用作多线程

单线程大量操作用builder，速度更快一点，开销少



###### 1.8新特性

1.流stream

2.并行流是什么：将源数据分为多个子流进行多线程操作，最后操作的结果再汇总成一个流对象。

是通过forkjoin池来给每一个cpu来分配任务的



###### 怎么把对象从一个jvm传递到另一个jvm

1.redis存储等数据库共享场景

2.使用序列化和反序列化

3.消息队列比如RabbitMQ



###### 怎么自己实现序列化和反序列化

java自带的不好的点：

1.因为java自带的序列化是使用Objectinput Stream，可读性不好，简单的例子就是在redis存储数据以及RabbitMq传消息到交换机

2.然后因为是java自带的，没有协议，所以无法跨语言。

3.在使用readObject的时候他会反序列化所有实现serializable接口的所有对象，很不安全

4.从redis的例子可以看到，仅仅一个hello通过java自身的反序列化后得到一大串，占用的空间太大了

一般使用protobuf或者fastJson，protobuf压缩的性能比较好。



###### 单例模式，以及用volatile和synchronized来实现双重检查锁定的单例模式

```java
单例模式：即只能有一个实例对象，会给一个全局访问点
public class Singleton{
  private static Singleton singlepoint; //唯一的实例对象
  private Singleton(){} //私有修饰构造方法，使得外部无法创建对象
  public void showMessage(){
    sout("hello from singleton")
  }
  public static Singleton getInstance(){ //全局访问点
    if(singlepoint==null){
      singlepoint = new Singleton();
    }
    return singlepoint;
  }
}
```

volatile的作用：1.让变量在多线程可以被看见 2.禁止jvm运行时指令重排序，确保读写顺序

```java
双重检查锁定
public class Singleton{
  private static volatile Singleton singlepoint; //唯一的实例对象
  private Singleton(){} //私有修饰构造方法，使得外部无法创建对象
  public void showMessage(){
    sout("hello from singleton")
  }
  public static Singleton getInstance(){ //全局访问点
    if(singlepoint==null){
      synchronized(Singleton.class){ //以免两个进程都到了这里，然后出问题
				    if(singlepoint==null){  //两个线程都到了，一个拿了锁一个等待，然后拿了锁的那个创建了单例对象解锁了但是还没有返回，然后等待的那个这时候解锁了如果没有这个非空判断它又会创建一个单例对象
      singlepoint = new Singleton();
    }}}
    return singlepoint;
  }
}
```



###### 代理模式和适配器模式

代理模式比如在同一个类里面一个方法到调用另一个带着@Transaction事务注解的方法，这时候直接使用他就相当于this.事务方法，这时候就相当于一个普通方法不会开启事务，因为AOP代理机制：一个带有`@Transactional`注解的方法被调用时，Spring的事务代理会拦截这个方法调用，并在调用前开启事务，调用后提交或回滚事务。

适配器模式就是使接口兼容