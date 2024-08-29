###### java的线程和操作系统的线程一样吗

java底层调用了pthread_create，和操作系统一样的，一对一的线程模型。



###### java多线程安全注意哪些问题

原子性：即操作不可被中断或分割，从而避免了传统锁机制带来的性能开销。即无锁的原子操作，atomic就是使用了底层的 CAS操作确保了无锁操作的原子性。synchronized上锁用于那种特别高并发导致的哈希冲突等cas容易失败重启频繁的地方，共同保证了原子性。  【cas属于自旋锁】

可见性：volatile和synchronized，确保一个线程做的修改能被其他的线程看见。

有序性：线程观察其他的线程中的指令执行顺序，但是指令会重排序，java中使用了volatile和happens-before原则来保证指令的有序

happens-before: A happens-before 操作 B，那么 A 的结果对于 B 是可见的，并且 A 先于 B 执行。



###### 如何保证数据的一致性

1.事务管理，例如spring事务管理和mysql事务管理

2.加锁，synchronized或者ReentrantLock【记忆：读音retry】可重入锁来控制并发访问

3.在操作数据时带上版本号，用乐观锁机制保证数据的一致性



创建线程的方式以及优缺点

1.直接继承Thread类，通过重写run方法

优点：编写简单

缺点：无法再继承别的东西了

2.实现Runnable接口，重写run方法

优点：拓展性高可以继承，一个runnable可以供多个线程来创建

缺点：无法直接使用Thread类的方法

3.线程池（里面有很多API以后慢慢看）

```java
//单线程池
ExecutorService pool =Excutors.newSingleThreadExecutor();
//多线程池 10个
ExecutorService pools=Excutors.newFixedThreadPool(10)
  
  然后在线程池里面submit runnable的实现类就行
  pool.submit({}->{

      sout("这是一个线程"
    //这里是函数式接口
  })
```

缺点：程序复杂，再故障排查和调整配置时较为复杂

优点：可以重用预先创建的线程，不使用线程池得不断得创建线程和销毁，而线程池会把它回收到线程池里面，即【线程重用】，显著提高程序的性能。

4.Callable

```java
        Callable callable = new MyCallable();
        FutureTask<String> futureTask = new FutureTask<>(callable);
        Thread thread = new Thread(futureTask);
        thread.start();
        System.out.println(futureTask.get());

    }

}
class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        return "callable线程创建成功";
    }
}
```

优点：和runnable一样，适合多个线程使用同一份资源

缺点：和runnable一样，必须得Thread.currentThread()来访问现在的线程



###### 停止线程的方法

1.异常法

使用thread.interrupt()让他中断，然后在run方法里面加一个判断

```java
Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {


                try {int i = 0;
                    while (true) {
                        if (Thread.currentThread().isInterrupted()) {
                            throw new InterruptedException();
                        }

                        System.out.println(i++);
                      Thread.sleep(500);
                    }
                } catch (InterruptedException ex) {
                    throw new RuntimeException(ex);
                }
            }});
```

2.在目标线程sleep时直接对他thread.interrupt()

3.stop暴力，现在已弃用

4.和第一种差不多，一直while判断isinterrupt，true就return



###### 调用 interrupt 是如何让线程抛出异常的?

每一个线程里面有一个布尔值来标记是否中断，在sleep，join，wait这些阻塞的情况下中断时就会导致线程停止抛出异常，其他的情况下不会，只会标记.



###### 线程的状态有哪些

new :刚创建好但是还没有start

runnable：启动了start但是还没cpu调度或者正在运行

blocked： 获取不到锁（这时候别人在用）

waiting：必须要等别人notify或者notifyAll

timed_waiting:等待时间

terminated：完成，终止

- BLOCKED 是锁竞争失败后被被动触发的状态，WAITING 是人为的主动触发的状态 
- BLCKED 的唤醒时自动触发的，而 WAITING 状态是必须要通过特定的方法来主动唤醒



###### 如果有多个wait(),那么notify是唤醒哪一个？

notify的唤醒是任意的，但是也依赖于JVM，JVM里面的具体的实现不同，比如hotspot就是先进先出来唤醒



###### 怎么保证多线程的安全性

1.synchronizd关键字上锁

2.Lock接口：有更灵活的锁管理和更好的性能。比如他的实现类ReentrantLock可重入锁

3.Atomic类，即原子类，提供了如CAS这种硬件级原子操作

4.ThreadLocal,比如在微服务那里的，直接可以在线程里面传东西，每一个线程都有自己独立的本地变量

5.并发集合，比如ConcurrentHashMap这种

6.JUC工具类：java.util.concurrent底下的一些工具包，比如Semaphore信号量



###### java里面常见的锁，谈谈使用场景

1.内置锁synchronized。使用的最多，他里面分了好几个级别：无锁、偏向锁、轻量级锁、重量级锁。

2.ReentranLock：可重入锁，在里面有lock和unlock方法，允许重复获取锁和释放锁，有一个计数器，当重复获取时就加一，当释放时就减一，当计数器为0时才能真正地释放，更加灵活。他里面还有更多的功能，如公平锁和定时锁等等

3.乐观锁和悲观锁：悲观锁就是上述上了锁的，乐观锁就是无锁，每次对数据进行操作时对一个值进行判断，常用的是版本号。

4.自旋锁：CAS，看起来像是乐观锁，也是无锁原子性操作。但是如果在超高的并发情况下会导致不停地失败自旋重试占用cpu

5.读写锁：因为读的情况远比写入的情况多，就允许多个进程同时读取操作，但是只允许一个写入者，以提高并发性。



###### 用代码展示各个锁的使用







