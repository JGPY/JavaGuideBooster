## Java面试强化测试题

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
10、各种回收器，各自优缺点？ <br>
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