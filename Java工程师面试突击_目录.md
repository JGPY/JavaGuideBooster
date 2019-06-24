### <a name="3">Java工程师面试突击_目录</a>

#### <a name="31">[消息中间件](./Java工程师面试突击/消息中间件)</a>
&ensp;&ensp;&ensp;&ensp; • [1. 如何进行消息队列的选型](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [2. 引入消息队列后如何保证其可用性](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [3. 为什么消息队列里消费到了重复数据](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [4. 发到消息队列的数据不见了](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [5. 如何保证从消息队列拿到的数据按照顺序执行](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [6. 几百万消息在小消息队列里积压了几小时](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [7. 如果让你开发一个消息中间件,你会怎么设计架构](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [8. 消息队列相关问题的面试技巧](./notes/待整理.md)<br>

#### <a name="32">[分布式搜索](./Java工程师面试突击/分布式搜索)</a>
&ensp;&ensp;&ensp;&ensp; • [1. 分布式引擎架构是怎么设计的,为什么是分布式的](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [2. 分布式搜索引擎写入和查询的工作流程](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [3. 分布式搜索引擎在几十亿数据量级的场景下如何优化查询性能](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [4. 你们公司分布式搜索引擎是怎么部署的](./notes/待整理.md)<br>
&ensp;&ensp;&ensp;&ensp; • [5. 分布式搜索引擎相关问题的面试技巧](./notes/待整理.md)<br>

#### <a name="33">[分布式缓存](./Java工程师面试突击/分布式缓存)</a>
&ensp;&ensp;&ensp;&ensp; • [1. 分布式缓存第一个问题]()<br>
&ensp;&ensp;&ensp;&ensp; • [2. redis线程模型,为什么单线程还是有很高的效率]()<br>
&ensp;&ensp;&ensp;&ensp; • [3. redis有哪些数据类型,分别在什么场景下使用比较合适]()<br>
&ensp;&ensp;&ensp;&ensp; • [4. redis过期策略,手写LRU]()<br>
&ensp;&ensp;&ensp;&ensp; • [5. 怎么保证redis是高并发和高可用]()<br>
&ensp;&ensp;&ensp;&ensp; • [6. 怎么保证redis挂掉之后再重启数据可以恢复]()<br>
&ensp;&ensp;&ensp;&ensp; • [7. redis cluster集群模式的原理]()<br>
&ensp;&ensp;&ensp;&ensp; • [8. 一般如何应对缓存雪崩以及穿透问题]()<br>
&ensp;&ensp;&ensp;&ensp; • [9. 如何保证缓存与数据库双写时的数据一致性]()<br>
&ensp;&ensp;&ensp;&ensp; • [10. redis的并发竞争该如何解决]()<br>
&ensp;&ensp;&ensp;&ensp; • [11. 你们公司生产环境的redis集群的部署架构是什么样的]()<br>
&ensp;&ensp;&ensp;&ensp; • [12. 分布式缓存面试题的回答技巧]()<br>

#### <a name="34">[分布式系统](./Java工程师面试突击/分布式系统)</a>
&ensp;&ensp;&ensp;&ensp; • [1. 为什么要把系统拆分为分布式,为啥要用dubbo]()<br>
&ensp;&ensp;&ensp;&ensp; • [2. dubbo的工作原理,注册中心挂了可以继续通信嘛]()<br>
&ensp;&ensp;&ensp;&ensp; • [3. dubbo都支持哪写通信协议以及序列化协议]()<br>
&ensp;&ensp;&ensp;&ensp; • [4. dubbo支持哪写负载均衡,高可用以及动态代理策略]()<br>
&ensp;&ensp;&ensp;&ensp; • [5. SPI是啥意思,dubbo的SPI机制原理]()<br>
&ensp;&ensp;&ensp;&ensp; • [6. 基于dubbo如何做服务治理、服务降级以及重试]()<br>
&ensp;&ensp;&ensp;&ensp; • [7. 分布式接口的幂等性如何保证,比如不能重复扣款]()<br>
&ensp;&ensp;&ensp;&ensp; • [8. 分布式系统中的接口调用如何保证顺序性]()<br>
&ensp;&ensp;&ensp;&ensp; • [9. 如何设计一个类似dubbo的rpc框架,架构上如何考虑]()<br>
&ensp;&ensp;&ensp;&ensp; • [10. zookeeper一般都有哪写使用场景]()<br>
&ensp;&ensp;&ensp;&ensp; • [11. 什么是分布式锁,对比redis和zk两种分布式锁的优劣]()<br>
&ensp;&ensp;&ensp;&ensp; • [12. 说说你们的分布式session方案,怎么做的]()<br>
&ensp;&ensp;&ensp;&ensp; • [13. 分布式事务方案,有啥坑]()<br>
&ensp;&ensp;&ensp;&ensp; • [14. 一般如何设计一个高并发的系统架构]()<br>

#### <a name="35">[数据库](./Java工程师面试突击/数据库)</a>
&ensp;&ensp;&ensp;&ensp; • [1. 如何分库分表]()<br>
&ensp;&ensp;&ensp;&ensp; • [2. 如何系统不停机迁移到分库分表]()<br>
&ensp;&ensp;&ensp;&ensp; • [3. 如何设计可动态扩容缩容的分库分表方案]()<br>
&ensp;&ensp;&ensp;&ensp; • [4. 分库分表后全局id如何生成]()<br>
&ensp;&ensp;&ensp;&ensp; • [5. MySQL读写分离的原理,主从同步如何解决]()<br>



---
### 搬运工信息
Author:Jason Lou <br>
Email:vip.iotworld@gmail.com <br>
Blog:https://blog.csdn.net/qq_21508727 <br>
Github:https://github.com/JGPY/JavaGuideBooster <br>
---
