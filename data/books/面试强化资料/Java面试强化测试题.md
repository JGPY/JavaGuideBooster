## Java面试强化测试题

### Java基础
1、集合类以及集合框架；HashMap与HashTable实现原理，线程安全性，hash冲突及处理算法；ConcurrentHashMap <br>
2、进程和线程的区别？ <br>
3、Java的并发、多线程、线程模型？ <br>
4、什么是线程池，如何使用? <br>
5、数据一致性如何保证？ <br>
*注意点：* <br>
Synchronized关键字，类锁，方法锁，重入锁；<br>
6、Java中实现多态的机制是什么？ <br>
7、如何将一个Java对象序列化到文件里？ <br>
8、说说你对Java反射的理解？ <br>
9、同步的方法；多进程开发以及多进程应用场景？ <br>
10、在Java中wait和seelp方法的不同？ <br>
*注意点：* <br>
最大的不同是在等待时wait 会释放锁，而sleep 一直持有锁。wait 通常被用于线程间交互，sleep 通常被用于暂停执行。 <br>
11、synchronized 和volatile 关键字的作用和区别？ <br>
*注意点：* <br>
volatile 本质是在告诉jvm 当前变量在寄存器（工作内存）中的值是不确定的，需要从主存中读取；
synchronized 则是锁定当前变量，只有当前线程可以访问该变量，
其他线程被阻塞住。 <br>
(1).volatile 仅能使用在变量级别；synchronized 则可以使用在变量、方法、和类级别的 <br>
(2).volatile 仅能实现变量的修改可见性，并不能保证原子性；synchronized 则可以保证变量的修改可见性和原子性 <br>
(3).volatile 不会造成线程的阻塞；synchronized 可能会造成线程的阻塞。 <br>
(4).volatile 标记的变量不会被编译器优化；synchronized 标记的变量可以被编译器优化 <br>
12、服务器只提供数据接收接口，在多线程或多进程条件下，如何保证数据的有序到达？ <br>
13、ThreadLocal原理，实现及如何保证Local属性？ <br>
14、String StringBuilder StringBuffer对比？ <br>
15、你所知道的设计模式有哪些？ <br>
*注意点：* <br>
（Java 中一般认为有23 种设计模式，我们不需要所有的都会，但是其中常用的几种设计模式应该去掌握。下面列出了所有的设计模式。
需要掌握的设计模式我单独列出来了，当然能掌握的越多越好。 <br>
总体来说设计模式分为三大类： <br>
创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。 <br>
结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。 <br>
行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。
）
16、Java如何调用c、c++语言？ <br>
17、接口与回调；回调的原理；写一个回调demo； <br>
18、泛型原理，举例说明； <br>
*注意点：* <br>
解析与分派； <br>
19、抽象类与接口的区别；应用场景；抽象类是否可以没有方法和属性； <br>
20、静态属性和静态方法是否可以被继承？是否可以被重写？以及原因？ <br>
21、修改对象A的equals方法的签名，那么使用HashMap存放这个对象实例的时候，会调用哪个equals方法？ <br>
22、说说你对泛型的了解？ <br>
23、Java的异常体系？ <br>
24、如何控制某个方法允许并发访问线程的个数？ <br>
25、动态代理的区别，什么场景使用？ <br>
26、Dex加载过程和优化方式？ <br>
27、Jvm和Gc机制？ <br>

### 叙述下令你印象最深刻的项目；
*注意点：* <br>
1、明确项目是做什么的  <br>
2、明确项目的价值。
*注意点：* <br>
（为什么做这个项目，它解决了用户什么痛点，它带来什么价值？）  <br>
3、明确项目的功能。
*注意点：* <br>
（这个项目涉及哪些功能？）  <br>
4、明确项目的技术。
*注意点：* <br>
（这个项目用到哪些技术？） <br>
5、明确个人在项目中的位置和作用。
*注意点：* <br>
（你在这个项目的承担角色？）  <br>
6、明确项目的整体架构。  <br>
7、明确项目的优缺点,如果重新设计你会如何设计。  <br>
8、明确项目的亮点。
*注意点：* <br>
（这个项目有什么亮点？） <br>
9、明确技术成长。
*注意点：* <br>
（你通过这个项目有哪些技术成长？）

### Java基础
1、List 和 Set 的区别？  <br>
2、HashSet 是如何保证不重复的？  <br>
3、HashMap 是线程安全的吗，为什么不是线程安全的（最好画图说明多线程环境下不安全）?  <br>
4、HashMap 的扩容过程？   <br>
5、HashMap 1.7 与 1.8 的 区别，说明 1.8 做了哪些优化，如何优化的？  <br>
6、final finally finalize 区别？  <br>
7、强引用 、软引用、 弱引用、虚引用？  <br>
8、Java反射？  <br>
9、Arrays.sort 实现原理和 Collection 实现原理？  <br>
10、LinkedHashMap的应用？  <br>
11、cloneable接口实现原理？  <br>
12、异常分类以及处理机制？  <br>
13、wait和sleep的区别？ <br>
14、数组在内存中如何分配

### Java 并发
1、synchronized 的实现原理以及锁优化？  <br>
2、volatile 的实现原理？  <br>
3、Java 的信号灯？  <br>
4、synchronized 在静态方法和普通方法的区别？  <br>
5、怎么实现所有线程在等待某个事件的发生才会去执行？  <br>
6、CAS？CAS 有什么缺陷，如何解决？  <br>
7、synchronized 和 lock 有什么区别？  <br>
8、Hashtable 是怎么加锁的 ？  <br>
9、HashMap 的并发问题？  <br>
10、ConcurrenHashMap 介绍？1.8 中为什么要用红黑树？  <br>
11、AQS 12、如何检测死锁？怎么预防死锁？  <br>
13、Java 内存模型？  <br>
14、如何保证多线程下 i++ 结果正确？  <br>
15、线程池的种类，区别和使用场景？  <br>
16、分析线程池的实现原理和线程的调度过程？  <br>
17、线程池如何调优，最大数目如何确认？  <br>
18、ThreadLocal原理，用的时候需要注意什么？  <br>
19、CountDownLatch 和 CyclicBarrier 的用法，以及相互之间的差别?  <br>
20、LockSupport工具  <br>
21、Condition接口及其实现原理  <br>
22、Fork/Join框架的理解  <br>
23、分段锁的原理,锁力度减小的思考  <br>
24、八种阻塞队列以及各个阻塞队列的特性

### Spring
1、BeanFactory 和 FactoryBean？  <br>
2、Spring IOC 的理解，其初始化过程？  <br>
3、BeanFactory 和 ApplicationContext？  <br>
4、Spring Bean 的生命周期，如何被管理的？  <br>
5、Spring Bean 的加载过程是怎样的？  <br>
6、如果要你实现Spring AOP，请问怎么实现？  <br>
7、如果要你实现Spring IOC，你会注意哪些问题？  <br>
8、Spring 是如何管理事务的，事务管理机制？  <br>
9、Spring 的不同事务传播行为有哪些，干什么用的？  <br>
10、Spring 中用到了那些设计模式？  <br>
11、Spring MVC 的工作原理？  <br>
12、Spring 循环注入的原理？  <br>
13、Spring AOP的理解，各个术语，他们是怎么相互工作的？  <br>
14、Spring 如何保证 Controller 并发的安全？

### Netty
1、BIO、NIO和AIO？ <br>
2、Netty 的各大组件？ <br>
3、Netty的线程模型？  <br>
4、TCP 粘包/拆包的原因及解决方法？  <br>
5、了解哪几种序列化协议？包括使用场景和如何去选择？  <br>
6、Netty的零拷贝实现？  <br>
7、Netty的高性能表现在哪些方面？

### 分布式相关
1、Dubbo的底层实现原理和机制？ <br>
2、描述一个服务从发布到被消费的详细过程？ <br>
3、分布式系统怎么做服务治理？ <br>
4、接口的幂等性的概念？ <br>
5、消息中间件如何解决消息丢失问题？ <br>
6、Dubbo的服务请求失败怎么处理？ <br>
7、重连机制会不会造成错误？ <br>
8、对分布式事务的理解？ <br>
9、如何实现负载均衡，有哪些算法可以实现？ <br>
10、Zookeeper的用途，选举的原理是什么？ <br>
11、数据的垂直拆分水平拆分？ <br>
12、zookeeper原理和适用场景？ <br>
13、zookeeper watch机制？ <br>
14、redis/zk节点宕机如何处理？ <br>
15、分布式集群下如何做到唯一序列号？ <br>
16、如何做一个分布式锁？ <br>
17、用过哪些MQ，怎么用的，和其他mq比较有什么优缺点，MQ的连接是线程安全的吗？ <br>
18、MQ系统的数据如何保证不丢失？ <br>
19、列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题？ <br>
20、zookeeper的选举策略？ <br>
21、全局ID？ <br>

### 数据库
1、mysql分页有什么优化？ <br>
2、悲观锁、乐观锁？ <br>
3、组合索引，最左原则？ <br>
4、mysql 的表锁、行锁？ <br>
5、mysql 性能优化？ <br>
6、mysql的索引分类：B+，hash；什么情况用什么索引？ <br>
7、事务的特性和隔离级别 ？<br>

### 缓存
1、Redis用过哪些数据数据，以及Redis底层怎么实现？ <br>
2、Redis缓存穿透，缓存雪崩？ <br>
3、如何使用Redis来实现分布式锁？ <br>
4、Redis的并发竞争问题如何解决？ <br>
5、Redis持久化的几种方式，优缺点是什么，怎么实现的？ <br>
6、Redis的缓存失效策略？ <br>
7、Redis集群，高可用，原理？ <br>
8、Redis缓存分片？ <br>
9、Redis的数据淘汰策略？<br>

### JVM
1、详细jvm内存模型？  <br>
2、讲讲什么情况下回出现内存溢出，内存泄漏？   <br>
3、说说Java线程栈  <br>
4、JVM 年轻代到年老代的晋升过程的判断条件是什么呢？  <br>
5、JVM 出现 fullGC 很频繁，怎么去线上排查问题？  <br>
6、类加载为什么要使用双亲委派模式，有没有什么场景是打破了这个模式？  <br>
7、类的实例化顺序？  <br>
8、JVM垃圾回收机制，何时触发MinorGC等操作？  <br>
9、JVM 中一次完整的 GC 流程（从 ygc 到 fgc）是怎样的？  <br>
10、各种回收器，各自优缺点？
*注意点：* <br>
重点CMS、G1  <br>
11、各种回收算法？ <br>
12、说下OOM错误，stackoverflow错误，permgen space错误？ <br>



---
### 搬运工信息
Author:Jason Lou <br>
Email:vip.iotworld@gmail.com <br>
Blog:https://blog.csdn.net/qq_21508727 <br>
Github:https://github.com/JGPY/JavaGuideBooster <br>
---