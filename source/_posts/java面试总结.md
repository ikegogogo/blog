---
title: java面试总结
date: 2020-03-01 23:11:08
cover: https://images.pexels.com/photos/3706707/pexels-photo-3706707.jpeg?cs=srgb&dl=silhouette-of-man-standing-on-grass-field-during-night-time-3706707.jpg&fm=jpg
tags:
- java
- 面试
---



### 零、写简历

简历可以先写，写完多自己看看，自己问问，做优化或调整。内容可以多看看目标岗位的【工作要求】。我写简历用到的网站：超级简历。

### 一、面试准备

1. 复习面试知识点：主要参考《JAVA核心知识点整理.pdf》 云盘：链接:https://pan.baidu.com/s/11YfQ_2ZH5ygK35GLlJLFgw  密码:3v51

2. 详细阅读相关知识点：

   jvm：详细看：[深入理解Java虚拟机：JVM高级特性与最佳实践（第3版）](https://item.jd.com/12607299.html)，特别注意GC，垃圾收集器，内存模型。

   spring：相关内容及aop，ioc原理。

   redis：详细看：《Redis设计与实现 数据库技术丛书.epub》链接:https://pan.baidu.com/s/1tyH5uUhz4NGpt72c5M9h2g  密码:gz4x

   mysql：基础知识，数据库引擎，索引，优化等。及《mysql实战45讲》：链接:https://pan.baidu.com/s/12-W5u2nLvnWoti1sFMKvpQ  密码:kf2p

   zookpper：https://www.bilibili.com/video/av79704007?p=9
   kafka：链接:https://pan.baidu.com/s/1GAFTrO_UDzvto9jhCIoADQ  密码:7jfj

   RabbitMQ：链接:https://pan.baidu.com/s/1lSGPbJegvCFnmD8lbj61Xg  密码:bxfz

   dubbo、spring cloud：

3. 算法题：参考 http://leetcode-cn.com/



### 二、面试问题记录

ps：一些我简单写了答案，不一定准群

综述：hashmap线程安全、源码相关问得最多，其它主要集中在：多线程 ，线程安全，锁，spring，jvm，gc，mysql，redis，mq。

###### JD：

hashmap为何会线程不安全。源码解读：
https://www.jianshu.com/p/b37b2f9fba4e
https://www.jianshu.com/p/8b6eb2fd15ab 
resize(): https://blog.csdn.net/u013494765/article/details/77837338?utm_source=distribute.pc_relevant.none-task 
hashmap，ConcurrentHashMap 1.7，1.8扩容的区别 
nginx底层原理
nginx如何做限流：Nginx为我们提供了请求限制模块（ngx_http_limit_req_module）、基于令牌桶算法的流量限制模块（ngx_stream_limit_conn_module），可以方便的控制令牌速率，自定义调节限流，实现基本的限流控制
缓存
redis缓存击穿，空值解决方案
redis定时清除，缓存击穿解决方案：加锁，使用redis setnx获取锁，如果获取锁失败则sleep后继续循环调用自己。
tcp/ip协议一台单网卡机器最多支持多少连接
mq，kafuka，自己用到的cmq与其他mq的区别，分布式mq的顺序是如何保证的：
如何保证MQ的顺序性？
nio Selector了解吗，select和epoll的区别 ：https://blog.csdn.net/m0_37524661/article/details/87916779，https://blog.csdn.net/yijie__shusheng/article/details/89536604。
grpc简介优点缺点：https://studygolang.com/articles/21897?fr=sidebar 

##### PA：

jpa原理，怎么实现不用写sql的，如何连表查询，如何动态查询。
mybatis了解吗
jdk里面线程安全的类了解吗
spring boot 启动时做了什么

hashmap，ConcurrentHashMap :  https://www.jianshu.com/p/1197e4717194
为什么一个调用一个service方法，方法再调用内部带注解的方法注解不生效：
当外部通过@Autowired注解得到一个TestClass对象时，其实得到的是一个Spring包装过的代理对象
spring 在扫描bean的时候会扫描方法上是否包含@Transactional注解，如果包含，spring会为这个bean动态地生成一个子类（即代理类，proxy），代理类是继承原来那个bean的。此时，当这个有注解的方法被调用的时候，实际上是由代理类来调用的，代理类在调用之前就会启动transaction。然而，如果这个有注解的方法是被同一个类中的其他方法调用的，那么该方法的调用并没有通过代理类，而是直接通过原来的那个bean，所以就不会启动transaction，我们看到的现象就是@Transactional注解无效。
集合有哪些：主要有 3 种:set(集)、list(列表包含 Queue)和 map(映射)。
锁有哪些：我的回答：乐观锁，悲观锁，ReentrantLock 与 synchronized。其实还有很多。
区别：1，ReentrantLock 通过方法 lock()与 unlock()来进行加锁与解锁操作，与 synchronized 会
被 JVM 自动解锁机制不同，ReentrantLock 加锁后需要手动进行解锁。为了避免程序出
现异常而无法正常解锁的情况，使用 ReentrantLock 必须在 finally 控制块中进行解锁操作。2，ReentrantLock 相比 synchronized 的优势是可中断、公平锁、多个锁。这种情况下需要
 使用 ReentrantLock。

cms了解吗：CMS收集器(多线程标记清除算法)，G1收集器
Garbage first 垃圾收集器是目前垃圾收集器理论发展的最前沿成果，相比与 CMS 收集器，G1 收 集器两个最突出的改进是:
1. 基于标记-整理算法，不产生内存碎片。
2. 可以非常精确控制停顿时间，在不牺牲吞吐量前提下，实现低停顿垃圾回收。

java类加载过程，有哪些类加载，怎么自定义加载器
redis主要用途
redis底层数据结构了解吗
redis怎么实现一个队列
zk了解吗
设计模式了解吗，用到了哪些
Spring Bean 作用域，spring 生命周期，controller，service默认生命周期类型是什么。
spring 有什么特点，为何要用它
数据库锁有哪些？https://www.php.cn/mysql-tutorials-418309.html
临键锁、间歇锁边界锁了解吗？https://blog.csdn.net/zcl_love_wx/article/details/82382582
innodb如果update语句的where没有索引，会用什么锁：InnoDB这种行锁实现特点意味着：只有通过索引条件检索数据，InnoDB才使用行级锁，否则，InnoDB将使用表锁！
索引，前缀索引的特性
分布式ID用什么生成的，什么原理
ThreadLocal用过没

##### SF：

==和equals的区别：==比较值是否相等，引用类型比较引用地址是否相等。equals比较内容是否相等。
zk用过没
内存泄露会是什么导致的：静态类的使用，资源连接的使用（io，数据库等连接），监听器的使用。
jvm调优一般会用到什么工具
spring中用到了哪些设计模式
synchronized用到类和字节码的区别：synchronized(this)：因为this是当前对象本身，所以锁定只对你自己new了并调用那个对象有用，所以另外一个人如果要new并调用，则和这个不是同一个锁，因为this变了。synchronized(类的名.class)：每个类在jvm里面只有一个唯一的字节码，所以.class是唯一的，无论多少对象，共用此同一把锁。
序列化是什么，什么地方会用到

##### ZX：

用到的cmq和其他mq的区别
数据库调优策略有哪些：表设计，索引，sql
如果用了like查询能命中索引吗
redis的nio模型知道吗
分布式锁怎么实现的：说了redis实现方式，以及redis的问题，可能有锁无法解锁等问题，也说了用zk实现
hashmap有什么问题
nginx作为负载均衡，如果一台挂了怎么办：答：没详细研究过，运维处理的，我猜是和哨兵模型或者zk的选举一样吧
有没有遇到数据库特别大的情况，怎么处理的
分库分表
线程池有哪些，各有什么区别
springboot有什么特点，有了什么springboot的框架或组件
我们系统架构是怎么样的：答：从nginx->api tomcat->微服务。
微服务怎么治理和通信的，用的什么协议
分布式事务怎么实现的

##### coding:

tcp什么情况下会重发
跳表
hashMap的key如果是对象，需要注意什么：HashMap的key最好不要存储对象，大部分环境都是String。
如果要存储对象，要注意重写下equal和hashcode方法
mq怎么保证不丢失消息的，什么情况下会丢失消息：https://blog.csdn.net/u011277123/article/details/104258340 

二面：
undolog特别长多，怎么实现的快速commit
mysql什么情况下会用到临时表
explan filesort怎么出现
垃圾收集器有哪些，cms垃圾收集时机，有几个阶段
ConcurrentHashMap负载因子为1时有什么问题，同时有多个线程resize时怎么办
ConcurrentHashMap的size()是怎么样的
mysql为啥时b+树，不是红黑树
mysql分裂
线程池
treemap是什么数据结构
三面：
mq消息如何保证唯一性，发送和接受都只有一条，不会因为网络波动重复发送等场景影响
http2.0的区别
grpc的通讯模式
spring私有方法如何让事务注解生效：aspectJ
spring 事务怎么实现嵌套事务的： https://www.jianshu.com/p/2f79ee33c8ad

##### MT：

上了一个jar包，cpu过高怎么排查
nginx的底层原理，为何相比其它服务器性能更好。https://www.cnblogs.com/chenjfblog/p/8715580.html 
redis和mysql的io模型是什么：redis 单线程多路复用模型，：https://www.cnblogs.com/technologykai/articles/10823927.html 。 mysql使用线程池模型
grpc协议增加一个字段后，怎么实现新旧版本兼容性的
tomcat容器了解吗
100个人,排一列,奇数出列,剩下的人以此类推,最后一人在第一次排列第几位
实现一个二分查找
类加载机制，双亲委派模式，以及在其它场景的应用，如tomcat容器里面运行两个web服务，它怎么隔离加载相同类的
如果自己实现一个锁需要注意些什么特性：
mysql分布式锁实现方式
分布式锁要解决的问题
可以保证在分布式部署的应用集群中，同一个方法在同一时间只能被一台机器上的一个线程执行。
这把锁要是一把可重入锁（避免死锁）
这把锁最好是一把阻塞锁（根据业务需求考虑要不要这条）
这把锁最好是一把公平锁（根据业务需求考虑要不要这条）
有高可用的获取锁和释放锁功能
获取锁和释放锁的性能要好

##### TT：

程序员买咖啡
在公司楼下的咖啡厅上，每一杯美式咖啡的售价为 5 元；程序员在排队购买咖啡，一次购买一杯。
每位程序员只买一杯咖啡，然后向你付 5 元、10 元或 20 元。你必须给每个程序员正确找零。
注意，一开始你手头没有任何零钱，并且每位程序员急于回去写代码因此不能等待后边有零钱了再找。
如果你能给每位程序员正确找零，返回 true ，否则返回 false 。
lfu缓存淘汰算法
数据库sql它是怎么选择使用哪一个索引的

