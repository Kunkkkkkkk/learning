1. 你觉得 Java 好在哪儿？

   ```
   1.跨平台性：通过jvm（java virtual machine，java虚拟机，即java运行的环境）。可以不同的平台上运行
   2.资源多：提供大量框架和类库，方便开发
   3.安全性高：内置了安全机制，如沙箱模型
   4.面向对象编程：代码方便模块化和重用
   5.社区支持：语言成熟，开发者社区庞大。
   ```

2. Java 的多态是什么意思？

   ```
   同一个行为（方法）有多个不同的表现形态，分为编译时多态和运行时多态，编译时多态是方法重写，运行时多态是方法重载。（重写是子类重写父类的方法，重载是同一个方法不同的参数方法体不同返回值也不同例如构造方法）。能提高代码的灵活性和可拓展性
   ```

3. Java 按值传递还是按引用传递？

   ```
   官方答案：The Java Spec says that everything in Java is pass-by-value. There is no such thing as “pass-by-reference” in Java. java中只有按值传递。
   首先先明确按值传递和按引用传递是什么：按引用传递比如说传递一个物理地址，也就是那个值的真身（我这样理解的），那么意味着接受的实参只是一个副本而不是真身。
   
   基本类型：那8个
   引用类型：数组、对象等
   
   在用到基本类型的值的时候，只是传一个分身，而那个值比如a并不会因为方法内的操作而改变
   在对引用类型的传递的时候，举个例子sort(a) a这里是一个数组，虽然a本身会改变，但是a本身就是一个引用类型，意思就是它本身就是一个值，但是指向对象在内存中的位置（不管什么物理位置还是什么），虽然指向的对象在方法内部被改变了，但是依旧是按值传递的
   ```

4. 接口和抽象类有什么区别？

   ```
   1.抽象类可以有抽象方法和具体方法，也可以有实例变量。接口只能有抽象方法，没有实例变量
   2.一个类可以实现多个接口，但是由于java单继承，只能继承一个抽象类
   3.接口强调功能的作用而不关心具体实现，抽象类注重is-a的层次结构（is-a就是 xxxx是xxx的一个老弟）
   ```

5. Java 为什么不支持多继承？

   ```
   避免了二义性，也叫钻石继承问题（即继承多个父类时，当多个父类里有方法名相同的部分，不知道调用哪一个），
   替代方法：用接口或者composition（组合类）来替代  下面弄了个例子
   ```

   ```java
   //组合类例子
   class Car{
   public void run(){
   开车
   }
   }
   class Plane{
   public void takeoff(){
   起飞
   }
   }
   class Vehicle{
   private Car car;
   private Plane plane;
   public void run(){
   car.run();
   }
   public Plane plane(){
   plane.takeogg();
   }
   }
   ```

6. 什么是序列化？什么是反序列化？

   ```
   序列化就是把对象转换为字节流类型 方便传输和存储
   反序列化就是把字节流恢复成对象类型
   例子就是input/outputstream input就是反序列化
   ```

7. 什么是不可变类？

   ```
   不可变类型和不可变类
   不可变类型比如int,string,float 他们创建出来之后值就不会变了，改变他的值之后内存地址也变了，也就是一个新的值了。
   不可变类是指一旦创建，对象字段无法更改的类。很适合用作hashMap和hashSet的键值对
   所有字段和类自身都是final，没有修改状态的方法（如setter）
   用处1.线程安全性，避免了建设同步机制2.不用担心对象被修改，简化了维护3.缓存和优化问题4.可以用作键值对
   ```

8. Exception 和 Error 的区别知道吗？

   ```
   Exception是程序可以处理的异常，分为两种，受检异常和运行时异常。受检异常时必须捕获或者声明抛出（声明就是在类名后throw，抛出是下面），运行时异常就是无需声明
   Error是严重的系统级错误，如内存不足这种
   ```

9. 面向对象编程和面向过程编程的区别？

   ```
   1.可重用性和可扩展性：OO由于封装继承多态的特效可重用性和可扩展性更强
   2.数据和行为的分离度：PP是数据和行为（函数）分离，数据大多是全局参数，强调数据的处理和操作，而OO是吧数据和行为封装在对象中。
   3.关注点：PP主要关注解决问题的步骤和过程，强调算法和过程控制，OO主要关注问题的实体和对象，把问题划分为多个对象，强调对象间的交互来解决问题
   ```

10. 重载与重写的区别？

    ```
    上面第二题我写了
    ```

11. 什么是内部类，有什么用？

    ```
    内部类是类中再定义的类，内部类可以访问外部类的成员变量和方法，就算再外部类中是private的。
    作用：将相关逻辑的类放在一起，让代码更简洁和回调处理方便
    有4大类：
    成员内部类：定义在外部类内部，可以访问外部类的所有成员。
    局部内部类：定义在方法或代码块内部，仅在该方法或代码块内可用。
    匿名内部类：没有名字的内部类，适合用于简化实现接口的单一方法或继承类的情况。
    静态内部类：使用 static 关键字定义，不需要外部类的实例即可创建，不能访问外部类的非静态成员。
    操作时和下面的深拷贝和浅拷贝有联系
    ```

12. JDK8 有哪些新特性？

    ```java
    1.lambda表达式和函数式接口
    2.方法引用：比如mybatisplus里经常用的例如User::GetName
    3.重复注解(还有其他的注解相关的改变)，例如在Config.class这个类里面加了一个@Repeatable(Configs.class)就是Configs是Config存放注解的容器。
    4.新的日期API：新 API 中的主要类
      特点：所有时间类不可变，让线程更安全；强类型减少了类型转换的错误
    LocalDate
    LocalTime
    LocalDateTime
    ZonedDateTime
    Period
    Duration
    Instant
    5.接口中可以有具体的实现方法：这里叫默认方法，以便实现该接口的类可以直接使用而不必重新定义。 default void defaultMethod(){}
    6.提供函数式接口 @FunctionalInterface
    函数式接口只能有一个抽象方法，但是静态方法和默认方法可以有多个，这个注解是让编译器来检查这个函数式接口是否符合函数式接口的规范，比如有多个抽象方法就会报错。
      主要的作用是配合lambda表达式和方法引用来时的代码更加简洁易读，下面有lambda和方法引用的具体代码讲解
    ```

    ```java
    接口
    @FunctionalInterface
    public interface MyFunctionalInterface{
      void interfaceMenthod();
    }
    ```

    ```java
    方法引用
    public class Myclass{
      psvm(){
        MyFunctionalInterface func = Myclass::Method;
        func.interfaceMenthod();
      }
      
      public static void Method(){
        sout("hello world")
      }
    }
    ```

    ```java
    lambda表达式
    就是()->具体要实现的
    MyFunctionalInterface func =()->sout("hello world")
    ```

13. String，StringBuffer，StringBuilder 的区别？

    ```
    String不可变，每次修改都是生成了一个新的对象
    StringBuffer和StringBuilder都是对原有对象的修改，builder的速度更快，一般不考虑线程安全的时候都用它（因为builder不能同步访问）
    要线程安全的情况下必须用buffer，适合多线程
    引用对象来拼接字符串都是用这几个，然后==为false
    用的是final来拼接不会使用
    ```

    ```java
    StringBuffer和StringBuilder对对象的修改过程（都是数组）
    psvm(){
      StringBuilder sb = new StringBuilder(10); //建一个容量为10的空间（可变化的）
      sb.append("hello");
      sout(sb);  //输出结果:hello
      sb.append(0,"world1");
      sout(sb);  //输出结果:world1hello   可以大于10
    	sb.delete(3,7);  // [前删后不删]
      sout(sb);  //输出结果: worello
    }
    ```

14. StringBuilder 内部是如何实现的？

    ```
    看上面
    ```

15. 包装类型和基本类型有什么区别？

    ```
    基本类型如:int,char这种
    包装类型如:Integer,Character  可以为null
    基本类型存贮在栈里，包装类型存贮在堆里
    堆是一个完全二叉树（具体我不懂）
    栈因为地址是连着的，所以寻址很快，剩下堆和栈在下面说
    ```

    ```
    栈的只是虚拟地址连在一起而不是物理地址。cpu有专门的寄存器来直接操作栈，但堆要间接寻址。
    在并发计算的时候，每一个线程有自己独享的栈内存，没有多线程的竞争问题，但是堆内存是所有线程共享的。栈是先进先出，内存的分配和施放速度很快，但是在堆里面的内存分配和施放机制很复杂。
    ```

16. JDK 和 JRE 的区别？

    ```
    JDK java development kit  包括了开发工具和JRE
    JRE java runtime environment  包括了JVM和运行时需要的类库，是为了运行那些已经变写好的java代码
    ```

17. 用过哪些 JDK 提供的工具？

    ```
    javac，java，javadoc，jdb（调试器），javap（反编译器），jps（用来查看进程的信息）
    ```

18. Java 中 hashCode 和 equals 方法是什么？它们和 == 各有什么区别？

    ```
    hashcode()是直接返回int类型的hash值，equals（）比较的是两个对象的引用是否指向的是同一个对象（内存中的同一个地址）。
    
    ==可以比较基本类型（值）和引用类型（地址），但是equals只能比较引用类型
    ```

19. hashCode 和 equals 有什么关系吗？

    ```
    equals相同的话，那么hashcode一定相等
    但是hashcode相等但是equals不一定相同，只能说明他们存贮在散射存储结构中的同一个位置（比如hash表里面有很多个水桶，每个水桶里能存储很多数据）：其实这里是因为hash表的有限性和对象的潜在无限性，所以不同对象有相同的hash值的情况不可避免，这种情况叫做哈希冲突，但是即便这种情况下还是能区分的，这里使用的是  链地址法   ，就是会在内部使用一个链表来存储这些hash冲突的元素，在查找元素的时候会遍历这些链表，用equals方法来找到正确的值
    
    所以hashcode和equals方法，重写了equals()方法的话，那么必须重写HashCode()方法，比如String类里就重写了
    
    ```

20. 动态代理是什么？（和AOP一起理解）

    ```
    Java 动态代理是一种设计模式，允许在运行时为接口创建代理对象，这些代理对象可以在调用目标方法前后执行特定的操作（如日志记录、权限检查、事务管理等）。
    ```

    

21. JDK 动态代理与 CGLIB 区别？

    ```
    1.jdk代理类必须实现接口，cglib可以不实现
    2.jdk生成代理类是内部自动生成， cglib通过asm字节码库生成代理类和多个用来增强效率的类
    3.jdk是代理类实现了目标类的接口，cglib是代理类把目标类当成父类继承
    4.jdk里的代理是通过反射来调用方法实现AOP，cglib是直接调用父类的方法来实现AOP
    ```

22. 注解是什么原理？

    ```
    注解是结合反射来运行的，相当于一个标识，不做具体的操作，是由反射来完成的，反射机制检测到注解开始赋值
    ```

    

23. 反射用过吗？（加一个例子）

    ```
    在编译的时候不知道要创建哪个类，只有运行时才能知道。 动态获取类的信息
    ```

24. SPI 有了解过吗？

    ```
    Service provider interface
    允许服务动态替换和插拔
    ```

    ```java
    //定义一个支付接口 
    public interface PaymentService(){
      void pay(double num);
    }
    //写两个实现类微信和支付宝,这里省略
    WeChatPay AliPay
     
    //然后写一个配置文件META-INF/services/com.example.PaymentService
    com.lyk.WeChatPay
    com.lyk.AliPay
    
    //可以直接使用服务加载
    psvm{
      ServiceLoader<PaymentService> loader =   ServiceLoader.load(PaymentService.class)
      for(PaymentService service:loader){
        service.pay(100.0);
      }
    }
    /*
    alipay:100元
    WeChatpay:100元
    */
    ```

25. 泛型有什么用？泛型擦除是什么？

    ```java
    泛型可以增强代码的重用性和可读性和类型转换的安全性,检测类型让你不乱传参数
    class A<T>{
     	//这里只是演示，代码没吊用
      public void out(T t){
        sout{t}
      }
    }
    
    泛型只是编译期的技术，所以在运行时无法获取到泛型的类型
    泛型擦除的按下面的例子
    class B<T>{
      T t ;
    }
    擦除之后
    class B{
      object t;
    }
    
    总的来说：简化了JVM的实现（因为擦除之后不需要在对特殊类型进行处理），然后更好地向后兼容（泛型擦除可以让泛型和非泛型代码兼容）。但是会引起安全问题（ClassCastException强制转换异常），因为在运行的时候获取不到泛型的类型。
    ```

26. 泛型的上下界限定符有了解过吗？

    ```java
    上界：List<?extends 具体的类> lst
      不能单个添加该类或者该类的子类，因为不知道该集合内是什么类型的。
      这里是动物园的案例，动物园里面有狗和猫
     public static void processAnimals(List<? extends Animal> animals) {
            for (Animal animal : animals) {
                animal.makeSound();
            }
        }
    这里只是方便作为形参的时候不用再细分
    下界：List<? super Cat> lst
      同上
    ```

27. 深拷贝和浅拷贝？

    ```java
    拷贝的知识
    拷贝分为【引用拷贝】【对象拷贝】，深浅拷贝都是【对象拷贝】
      
    引用拷贝：
    psvm{
      Teacher t1 = new Teacher();
      Teacher t2 = t1;
      sout{t1};
      sout{t2};
    }
    //输出结果: 
    //1  com.test.Teacher@28a418fc
    //2  com.test.Teacher@28a418fc
    因为这里是直接把t1的内存地址赋给t2。
    
    
    对象拷贝：
    psvm{
      Teacher t1 = new Teacher();
      Teacher t2 = (Teacher)t1.clone();
      sout{t1};
      sout{t2};
    }
    //输出结果: 
    //1  com.test.Teacher@28a418fc
    //2  com.test.Teacher@28abcde1
    说明t2是新的对象，成员变量和t1一样而已
    
      
      // 浅复制时：
            // Object object = super.clone();
            // return object;
    
            // 改为深复制：
            Student student = (Student) super.clone();
            // 本来是浅复制，现在将Teacher对象复制一份并重新set进来
            student.setTeacher((Teacher) student.getTeacher().clone());
            return student;
    
    
    总结：深拷贝就是在拷贝对象的时候对该对象引用的对象进行了对象拷贝了一个罢了
    ```

28. Integer 缓存池知道吗？

    ```java
    即在 [-128,127]内的数是在缓存里面，直接使用而不会再创建一个对象，而超出这个界限就会重新创建
    其中也涉及到自动装箱
    自动装箱：就是java中基本类型和包装类的相互转换，称为装箱和拆箱
    例如
      Integer a = 10;
    	int b = a ;   //自动拆箱
    	Integer c = b;//自动装箱
    但是equals不会自动装箱和拆箱，比如
        int i5 = 917;
            Integer i6 = 917;
            System.out.println(i5 == i6);
            System.out.println(i5.equals(i6));
    下面的连编译都过不去，因为equals需要同类型对象和相同的值
    ```

    ```java
    至于这个范围，可以用 == 来判断，因为 == 比较的是否是同一个对象，equals比较的是对象的值
     Integer i1 = 127;
            Integer i2 = 127;
            System.out.println(i1 == i2);  //true
    
            Integer i3 = -128;
            Integer i4 = -128;
            System.out.println(i3 == i4);  //true
    
            Integer i5 = -150;
            Integer i6 = -150;
            System.out.println(i5==i6);   //false
    
            Integer i7 = 130;
            Integer i8 = 130;
            System.out.println(i7 == i8); //false
    
            Integer i9 = new Integer(127);
            Integer i10 = new Integer(127);
            System.out.println(i9 == i10);//false 这里虽然在范围内,但是是直接创建不同的对象
    ```

29. 能说下类加载过程吗？

    ```
    首先.java后缀文件javac【编译】成.class文件，然后开始【加载】：读取字节码文件到内存当中，生成class对象；【验证】再开始验证文件格式和字节码，保证安全性和正确性以及防止对JVM产生损害；再开始【准备】：为静态变量分配内存空间，为默认值设0（占坑）；然后开始【解析】：即将类中的类、接口、方法等符号引用解析成直接引用：可以认为符号引用只是一个字符串，直接引用就是真实的地址；【初始化】：开始为前面占坑的静态变量赋值和执行静态代码块。
    ```

30. 双亲委派知道不？来说说看？

    ```
    一个类加载器要类加载，会往上让父类来加载，父类让更上面的父类来加载，一直递归直到父类无法完成请求时，子类才尝试加载
    ```

31. BigDecimal 有了解过吗？

    ```java
    1.可以表示任何精度和大小
    2.尽量使用String来创建对象，不要用double
      因为double是 IEE754 来确定精度的，二进制无法准确表示10进制的某些数字，比如十进制的0.1在二进制里是无限不循环
       BigDecimal bdFromDouble = new BigDecimal(0.1);
            System.out.println("BigDecimal from double: " + bdFromDouble);
    //输出结果：BigDecimal from double: 0.1000000000000000055511151231257827021181583404541015625
    
    正确写法:   BigDecimal bdFromDouble = new BigDecimal("0.1");
    3.可以自定义设置精度和舍入的模式
      //有8种Roundingmode，常用的有2种，一种是四舍五入ROUND_HALF_UP，另一种是直接舍去ROUND_DOWN
      BigDecimal date1 = new BigDecimal("2.003091020030429").setScale(5,ROUND_HALF_UP) //保留五位，四舍五入模式
    ```

32. new String("yupi") 一共创建了几个对象？（String详解）

    ```java
    2个
    首先new了一个String对象放在堆内存里面，然后yupi无论字符串池里面有没有都会再创建一个新的堆对象
    
    String a = "abc";：
    字符串 "abc" 会被放入字符串池中。
    如果池中已存在 "abc"，则直接返回引用。
    否则，将在池中创建新的 "abc" 对象。
    String a = new String("abc");：
    创建一个新的 String 对象，在堆内存中。
    即使池中存在 "abc"，也会创建一个新的堆对象。
    这个新对象的内容与池中的 "abc" 一致，但引用不同。
    ```

    ```java
    == 当只有基本数据类型时才比较值
    而string不是基本数据类型
    String是常量，拼接或者什么都是创建一个新对象
    String str1 = "hello"; 
    String str2 = "hello";
    String str3 = new String("hello");
    String str4 = new String("hello");
    String str5 = "hellohello";
    String str6 = str1 + str2;
    System.out.println(str1 == str2); //true
    System.out.println(str2 == str3); //false
    System.out.println(str3 == str4); //false
    System.out.println(str2.equals(str3));//true
    System.out.println(str3.equals(str4));//true
    System.out.println(str5.equals(str6));//true
    System.out.println(str5 == str6);//false
    ```

    ```java
    String s1 = "helloworld"; 
    String s2 = "hello";
    String s3 = "world";
    String s4 = "hello" + "world";
    String s5 = s2 + s3;
    String s6 = new String("helloword");
    String s7 = "hello" + new String("world");
    System.out.println(s1 == s4); //true 这里这两个都在缓存池里，所以拼接之后还是同一个内存里的
    System.out.println(s1 == s5);	//false
    System.out.println(s1 == s6);	//false
    System.out.println(s1 == s7);	//false
    ```

    

33. final、finally、finalize 各自有什么区别？

    ```
    final设置静态变量、类、方法。被设置的变量不可改变，类不可继承，方法不可重写
    finally是写在代码块前面，无论上面怎么样都会运行，例子try-catch-finally
    finalize是Object里的方法，是在回收对象前进行清理方法的（但是不一定会使用哦）
    ```

    ```java
    public class finalize {
        protected void finalize()throws Throwable{  //protected只是因为在object类里他就是protected
            System.out.println("finalize runing");
        }
    
        public static void main(String[] args) {
            finalize f = new finalize();
            f=null;
            System.gc();
            System.out.println(1);
        }
    }
    ```

    ```
    string转其他：
    
    基本数据类型时parseInt
    
    包装类是valueof
    
    其他转string：
    
    基本数据类型：包装类.toString
    
    包装类: 对象.toString
    ```

    

34. 为什么平时写代码的时候会遇到乱码？

    ```
    不同的编码格式
    ```

35. JDK9 把 String 中 char 数组改成了 byte 数组，你知道为什么吗？

    ```
    byte数组占用的内存更小
    ```

36. 在 Java 中如何操作调用外部可执行程序或系统命令？

    ```java
    1.Runtime.getRuntime().exec();
    例如Process process =Runtime.getRuntime().exec("cmd");
    2.ProcessBuilder.start(),用来执行多个命令的,先把命令放到一个集合里面
    List<String> command1 = new ArraysList<>();
    command1.add("cmd");
    command1.add("/bin/bash");
    
    ProcessBuilder pb = new ProcessBuilder(command1);
    Process p = pb.start()
    ```

37. 一个线程两次调用 start() 方法会出现什么情况？

    ```
    IllegalThreadStateException   一个线程只能启动一次
    ```

    ```
    线程的生命周期
    新建（New）、就绪（Runnable）、运行（Running）、阻塞（Blocked）和死亡（Dead）
    ```

38. 栈（Stack）和队列（Queue）有什么区别？ ps：栈和队列都有链表和数组两种方式的

    ```
    栈先进后出适合要回溯的地方，队列先进先出适合要顺序处理的地方
    ```

39. 什么是 Optional 类？

    ```
    在Java8之后的用来解决空指针错误的【容器】类
    表示一个对象既可能是null也可能非null
    ```

40. 什么是 Java 的 I/O 流？

    ```
    输入输出流，用于设备间的数据传输
    I/O流分为字节流byte和字符流character
    字节流是用来图片视频等，字符流文本
    ```

41. 什么是 Java 的网络编程？

    ```
    java提供类和接口来实现计算机网络通信
    常用的有
    URL URLConnection  http请求
    InetAddress ip地址
    socket 	客户端和服务器端的通信
    ServeScocket  服务器端用来监听客户端的请求
    ```

42. Java 的数据类型有哪些？

    ```
    基本数据类型：int ，short，Long，char，boolean ，float，double，byte  （String不是）
    
    引用数据类型：数组，集合，枚举，类，接口 String是一个类
    ```

43. 什么是自动装箱和拆箱？

    ```
    上面写了，拆箱就是把包装类类型赋值给基本数据类型的过程中自动类型转换
    拆箱就是反的
    ```

44. 什么是迭代器（Iterator）？

    ```java
    是一个接口，用来遍历集合内的元素
    有以下方法
    hasNext(); //检查还有没元素，经常结合for(hasNext())
    next();		//返回下一个元素
    remove();  //移除当前元素
    ```

45. 运行时异常和编译时异常有什么区别？

    ```
    运行时异常：比如ArithmeticExcepiton(算数异常)，OutOfIndexArrayException这些，不会强制捕获和处理
    编译时异常：常见的有IO异常，得throws或者try catch 来捕获，如果不捕获抛出则无法运行代码。
    
    ？为什么一定要捕获呢？
    1.告诉程序员潜在可能发生异常的地方
    2.防止程序在运行时因为未预见的异常而崩溃。提高代码健壮性
    ```

46. 解释 Java 中的继承。

    ```
    子类继承父类的非私有的成员变量和方法。
    继承只能单继承不能多继承，是因为避免钻石问题，但是可以多层继承。
    在子类的无参构造方法里，会自动隐性调用父类的无参构造方法。
    在有参构造方法里，若super（）不是在第一行，则会报错，因为子类的初始化会引用到父类的变量或者方法。
    初始化的时候只有父类初始化结束，子类才会开始调用构造方法初始化。
    ```

47. 什么是封装？

    ```
    面向对象的基本思想之一，将属性和方法封装在类里，对外提供接口，外界只能通过接口访问，隐藏内部细节
    ```

48. Java 中的访问修饰符有哪些？

    ```
    protected
    default 
    public
    private
    
    protected,default 是重点：区别在于在不在同一个包里可以调用
    public>protected>default>private
    ```

49. 什么是静态方法和实例方法的区别？

    ```
    静态方法里面没有this，也就是没有对象，想要调用成员变量必须得使用this。所以静态方法可以通过类名直接使用，而实例方法得通过对象使用
    ```

50. 说一下 for 与 for-each 的区别。

    ```
    for-each不需要考虑因为数组的越界带来的错误
    for-each是只读模式，无法修改
    ```

    

51. 为什么java里堆内存用的多

    ```
    1.堆内存的对象是共享的，数组，集合等数据结构等对象都是以堆内存存在的。
    2.生命周期更长，可以贯穿整个程序运行期间
    3.虽然在多线程计算时栈内存里是独占，没有安全性问题，内存的访问速度也更快，不过在多线程计算时要通信和资源数据共享，这时候就需要堆内存共享的对象了。
    ```

    ```
    1. 栈内存的用途
    栈内存用于存储局部变量和方法调用。每个线程都有自己独立的栈内存，所以在栈内存中的数据是线程安全的，不存在多线程竞争问题。栈内存的特点是：
    
    先进后出（LIFO）：栈是一个先进后出的数据结构，方法调用和返回遵循这个原则。
    生命周期短：局部变量和方法调用的生命周期很短，随着方法的结束，局部变量也会被释放。
    内存分配和释放速度快：由于栈的先进后出特点，内存分配和释放非常快。
    2. 堆内存的用途
    堆内存用于存储所有在程序运行时被创建的对象。这些对象可以在不同的方法之间共享，因此堆内存是所有线程共享的。堆内存的特点是：
    
    对象共享：所有线程可以访问堆中的对象，这使得对象可以在方法之间传递。
    生命周期长：对象的生命周期可以超出方法的范围，只要有引用指向该对象，它就不会被垃圾回收。
    内存管理复杂：由于堆内存中的对象生命周期不一致，内存的分配和释放机制比较复杂，需要垃圾回收机制来管理。
    为什么堆内存用得更多
    对象的创建和共享：
    在 Java 中，几乎所有的数据都是以对象的形式存在，而对象是分配在堆内存中的。
    对象在方法之间传递和共享，需要在堆内存中进行分配。
    生命周期管理：
    栈内存中的局部变量生命周期很短，只在方法执行期间存在。
    堆内存中的对象可以具有更长的生命周期，甚至可能贯穿整个程序运行期间。
    数据结构和集合类：
    Java 的集合类（如 List, Set, Map 等）和其他复杂的数据结构都是在堆内存中分配的。
    这些数据结构在许多应用中被广泛使用，需要大量的堆内存。
    线程间通信和共享：
    多线程编程中，线程之间的通信和共享数据依赖于堆内存中的对象。
    例如，共享缓冲区、任务队列等都需要在堆内存中分配。
    ```

52. 链表和数组的区别

    ```
    1.数组是连续存储，链表是各个元素之间通过指针指向链接
    2.数组访问某一个值，直接用下标，时间复杂度O(1),链表因为一个一个连着的，所以得O(n)
    3.数组删除添加某一个值，由于要前移后移，所以时间复杂度O(n),而链表只需要更改前后的指针O(1)
    ```

53. Map和conllection

```
只说几个经常用的
Map hashMap   pull()
collection List有序可重复 set无序不可重复  add()
set可以contains()
```

54. Object类里的getClass()方法

```
只会获取到当前实例所属的类，this.getClass()和super.getClass()都是获取当前类的类型
```

