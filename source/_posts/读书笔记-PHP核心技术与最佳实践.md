---
title: 读书笔记-PHP核心技术与最佳实践
date: 2019-07-13 23:59:40
cover: https://images.pexels.com/photos/2766334/pexels-photo-2766334.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500
tags:
- php
- 读书笔记
---

# 面向对象思想的核心概念

##### 异常与错误处理

PHP里面，遇到任何自身错误都会触发一个错误，而不是抛出异常，PHP遇到非正常代码，通常会触发错误，而不是抛出异常，所以这种错误是不能用异常捕获的。 **PHP只有手动抛出异常后才能捕获。**

##### PHP中的错误处理机制

php错误有很多种：warning,notice,deprecated,fatal error。PHP无法自动抛出异常，必须手动进行，可以用set\_error\_handler接管，进而主动抛出异常。

# 面向对象的设计原则

###### 单一职责原则

single responsibility principle,SRP

就一个类而言，应该只有一个引起它变化的原因。

避免相同的职责分散到不同的类中，避免一个类承担太多职责



##### 接口隔离原则

interface segregation principle,ISP

客户端不应该依赖它不需要的接口

类间的依赖关系应该建立在最小的接口上

##### 开放-封闭原则

open-close principle，OCP

open for extension，模块的行为必须是开放的，支持扩展的，而不是僵化的

close for modification，在对模块的功能进行扩展是，不应该影响或大规模地影响已有的模块

##### 里氏替换原则

Liskov Substitution Principle，LSP

子类型必须能够替换掉它们的父类型、并出现在父类能够出现的任何地方

##### 依赖倒置原则

上层模块不应该依赖于下层模块，它们共同依赖于一个抽象

抽象不能依赖于具体，具体应该要依赖于抽象

# 正则表达式基础与应用



# PHP网络技术及应用

HTTP（Hyper Text Transfer Protocol，超文本传输协议），是一个应用层协议，由请求和响应构成，是一个标准的客户端服务器模型。HTTP通常承载于TCP协议之上（80端口），有时也承载于TLS或SSL协议层之上（HTTPS，443端口）。HTTP协议是一个无状态的协议，同一个客户端的这次请求和上次请求没有对应关系。

##### HTTP协议是如何工作的

客户端发送一个请求（request）个服务器，服务器在接受到这个请求后将生成一个响应（response）返回给客户端。一次HTTP操作称为一个食物，其工作过程可分为4步。

1. 客户机于服务器需要建立连接，单击某个超链接，http协议的工作开始
2. 客户机发送一个请求给服务器
3. 服务器接到请求后，给予响应的响应信息
4. 客户端接受服务器返回的信息并显示在用户的显示屏上，然后客户机于服务器断开连接

###### 请求

请求由3部分组成：请求行，消息报头，请求正文

请求行： Method Request-URI HTTP-Version CRLF

###### 响应

响应也由3部分组成：状态行，消息报头，响应正文

状态行：HTTP-Version Status-Code Reasion-Phrase CRLF

###### 报头

普通报头、请求报头、响应报头、实体报头

Host

User-Agent

Accept

Cookie

Set-Cookie

Cache-Control

Referer

Content-Length

Accept-Encoding

###### HTTP应用，模拟灌水机器人

1. cURL库
2. file\_get\_contents
3. socket系列函数
4. 等等

###### 垃圾请求防御

1. IP限制（ip无法伪造）
2. 验证码
3. Token和表单
4. 审核机制

cURL步骤

1. 初始化 $ch = curl\_init()
2. 设置选项，包括URL  curl\_setopt($ch, CURLOPT\_URL, &quot;[http://www.php.net](http://www.php.net)&quot;)
3. 执行并获取HTML文档内容 $out = curl\_exec($ch)
4. 释放curl句柄 curl\_close()

###### Cookie于Session问答

1. cookie运行在客服端，session运行在服务器端，对吗？ 不完全对，cookie运行在客户端，由客户端进行管理，session虽然运行在服务端，但是sessionId最为一个cookie是存储在客户端的
2. 浏览器禁止cookie，cookie就不能用了，但session不会受浏览器影响，对吗？错。会影响，可通过URL传递session
3. 浏览器关闭后，cookie和session都消失了，对吗？错
4. session比cookie安全吗？错误

# PHP与数据库基础

pdo：php data objects，提供一个通用结构访问多种数据库，即抽象的数据模型支持连接多种数据库

事务的主要特性：

1. 原子性
2. 一致性
3. 独立性
4. 持久性

原子性:整个事务中的所有操作，要么全部完成，要么全部不完成，不可能停滞在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。

一致性:在事务开始之前和事务结束以后，数据库的完整性约束没有被破坏。

隔离性:隔离状态执行事务，使它们好像是系统在给定时间内执行的唯一操作。如果有两个事务，运行在相同的时间内，执行 相同的功能，事务的隔离性将确保每一事务在系统中认为只有该事务在使用系统。这种属性有时称为串行化，为了防止事务操作间的混淆，必须串行化或序列化请 求，使得在同一时间仅有一个请求用于同一数据。

持久性:在事务完成以后，该事务所对数据库所作的更改便持久的保存在数据库之中，并不会被回滚。

###### 数据库应用优化

数据库优化的思路：

避免在列上运算，会导致索引失效

使用join是，应该用小结果集驱动大结果集

注意like模糊查询的使用，避免%%

列出需要查询的字段，节省内存

使用批量插入语句节省交互

limit的技术比较大时使用between

不要使用rand函数获取多条随机记录

避免使用null

不要count(id)，而应该是count(\*)

1）应尽量避免在 where 子句中使用!=或\&lt;\&gt;操作符，否则将引擎放弃使用索引而进行全表扫描。

2）应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描，如：

select id from t where num is null

可以在num上设置默认值0，确保表中num列没有null值，然后这样查询：

select id from t where num=0

3）很多时候用 exists 代替 in 是一个好的选择

4）用Where子句替换HAVING 子句 因为HAVING 只会在检索出所有记录之后才对结果集进行过滤

禁止使用select \*、like %xxx

避免使用复杂的sql（不利于理解、优化和缓存）

不要在where索引字段上使用函数、变量、进行数学运算、（索引可能无法使用）

Or &amp; in 优先使用in

不要使用负向查询（not in、not like）

注意limit的效率

避免让mysql做复杂的数学运算

小心地使用trigger和store procedure

Explain select，尽量让where、group by、order by使用索引（最好是主键索引）

Update和delete改为select后explain看执行计划

视情况使用exist代替in

表连接注意连接顺序，用小表连大表，不要大表连小表

用到临时表的sql使用前注意查看db对临时表大小的限制(tmp\_table\_size)

用到文件排序时注意查看排序缓冲大小(sort\_buffer\_size)

不要在引擎不同的表上执行事务

数据库结构优化:

1）范式优化： 比如消除冗余（节省空间。。） 2）反范式优化：比如适当加冗余等（减少join） 3）拆分表： 分区将数据在物理上分隔开，不同分区的数据可以制定保存在处于不同磁盘上的数据文件里。这样，当对这个表进行查询时，只需要在表分区中进行扫描，而不必进行全表扫描，明显缩短了查询时间，另外处于不同磁盘的分区也将对这个表的数据传输分散在不同的磁盘I/O，一个精心设置的分区可以将数据传输对磁盘I/O竞争均匀地分散开。对数据量大的时时表可采取此方法。可按月自动建表分区。

4）拆分其实又分垂直拆分和水平拆分： 案例： 简单购物系统暂设涉及如下表： 1.产品表（数据量10w，稳定） 2.订单表（数据量200w，且有增长趋势） 3.用户表 （数据量100w，且有增长趋势） 以mysql为例讲述下水平拆分和垂直拆分，mysql能容忍的数量级在百万静态数据可以到千万 垂直拆分：解决问题：表与表之间的io竞争 不解决问题：单表中数据量增长出现的压力 方案： 把产品表和用户表放到一个server上 订单表单独放到一个server上 水平拆分： 解决问题：单表中数据量增长出现的压力 不解决问题：表与表之间的io争夺

方案： 用户表通过性别拆分为男用户表和女用户表 订单表通过已完成和完成中拆分为已完成订单和未完成订单 产品表 未完成订单放一个server上 已完成订单表盒男用户表放一个server上 女用户表放一个server上(女的爱购物 哈哈)

###### 存储引擎的选择

MyISAM: R/W \&gt; 100:1且update相对较少

并发不高，不需要事务

表数据量小

硬件资源有限

InnoDB：R/W较小，频繁更新大字段

表数据量超过1000w，并发高

安全性可可用性要求高

mysql瓶颈及应对措施

1. 增加mysql配置中的buffer和cache的数值
2. 使用第三方引擎或衍生版本
3. 迁移到其他数据库
4. 对数据库进行分区、分表操作，减少单表体积
5. 使用nosql等辅助解决方案，如memchched，redis
6. 使用中间件做数据拆分和分布式部署，如阿里巴巴的cobar
7. 使用数据库连接池技术

###### 范式与反范式

1. 核心业务使用范式
2. 若一致性需求-反ACID  原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）、持久性（Durability）
3. 空间换时间，冗余换效率
4. 避免不必要的冗余

# Memcached使用实践

memcached是高性能的分布式缓存服务器，数据存储在内存中，重启memcached或系统会导致数据全部消失，或内存容量达到指定值后，会使用lRU（Leatst Recently Used）算法自动删除不使用的缓存。memcached是一个多线程的缓存服务器，包括主线程（接受连接）和工作线程（处理连接请求）。

##### 特点：

- 协议简单
- 基于libevent的事件处理
- 内置内存存储方式
- 采用不互相通信的分布式

##### 方法：

- connect连接服务器
- addServer
- add添加一个缓存数据，如果存在会返回失败
- replace替换缓存数据
- set 设置一个key的缓存内容，add和replace的集合体
- get 
- delete
- flush
- getServerStatus
- getStatus

##### 过期

memcached为每个item设置一个过期时间，但不是到期就把item从内存中删除，而是访问item时如果到了有效期，才把item从内存中删除

##### LRU算法淘汰数据

当内存不够时，使用LRU算法淘汰旧的数据。淘汰规则是：从数据项列表尾部开始遍历，在列表中查找一个引用计数器为0的item释放掉，如果找不到引用计数器为0的，就找3小时没有访问过的。

##### 分布式布置方案

- 普通hash：通过hash函数把key转化为整数后，与服务器数量取模
- 一致性hash分布及增加虚拟节点改进算法

# Redis使用与实践



##### key命令

- exit key
- del key
- type key
- keys pattern
- expire key seconds：设置过期时间
- ttl key：返回过期时间
- randomKey 返回随机key，如果为空，返回空串
- rename oldKey newKey
- move key db-index

##### 支持的数据类型

- String
  字符串类型是redis最基础的数据结构，首先键是字符串类型，而且其他几种结构都是在字符串类型基础上构建的
  字符串类型实际上可以是字符串、数字、二进制（图片、音频），单最大不能超过512M
  使用场景：

  1. 缓存
     字符串最经典的使用场景，redis作为缓存层，mysql作为存储层，绝大部分请求数据都是redis中获取，由于redis具有支撑高并发特性，所以缓存通常能起到加速读写和降低后端压力的作用
  2. 计数器
     许多应用都会使用redis作为技术的基础工具，它可以实现快速技术、查询缓存的功能。
  3. 共享session
     处于负载均衡的考虑，分布式服务会将用户信息的访问均衡到不同服务器，用户刷新一次访问可讷讷个会需要重新登录，为了避免这个问题可以使用redis将用户session集中管理，在这种模式下只要保证redis的高可用和扩展性，每次获取用户更新或查询登录信息都直接从redis中集中获取
  4. 限速
     出于安全考虑，每次进行登录时让用户输入手机验证码，为了短信接口不被频繁访问，会限制用户每分钟获取验证码的频率

- Hash
  在redis中哈希类型是指键本身又是一种键值对结构
  使用场景:

  1. 哈希结构相对于字符串序列化缓存信息更加直观，并且在更新操作上更加便捷。

- list
  列表类型是用来存储多个有序的字符串，列表的每个字符串成为一个元素，一个列表最多可以存储2的32次方减1个元素。在redis中，可以对列表插入(push)和弹出（pop），还可以获取指定范围的元素列表。列表是一种比较灵活的数据结构，它可以充当栈和队列的角色。
  使用场景：

  1. 消息队列
     redis的`lpush+brpop`命令组合就可以实现阻塞队列，生产者客户端是用`lpush`从列表左侧插入元素，多个消费者客户端使用`brpop`命令阻塞式的抢列表尾部的元素，多个客户端保证了消费的负载均衡的高可用性。

  2. 使用技巧列表

     ```
     lpush+lpop=Stack(栈)
     lpush+rpop=Queue(队列)
     lpush+ltrim=Capped Collection(有限集合)
     lpush+brpop=Message Queue（消息队列）
     ```

- Set：查找删除时间复杂度为O(1)

- Sorted Set：查找删除修改时间复杂度为O(1)，适用于存储对象

  

支持排序：SORT key

##### 事务处理

保证一个客户端连接发起事务中的命令可以连续执行，而中间不会插入其他客户端连接的命令。

命令：muti   XXXX  exec

##### 持久化

- 内存快照（snapshotting,rdb）：保存内存快照可能阻塞其他客户端请求，影响性能，如果重启或宕机可能会丢失上次save之后的数据。
- 日志追加（append-only file,aof）：可有效降低数据丢失的风险，持久化文件可能过大。

##### 主从同步

优点：

- master可配置多个slave
- 多个slave连接到相同master，salve还可以连接其他slave
- 不会阻塞master
- 主从同步用来提交系统的伸缩性，比如多个salve用于读请求
- 在master服务器禁止数据持久化

同步原理：

设置好slave服务器后，slave自动和master建立连接，发送sync命令，master启动一个后台进程，将数据已快照方式写入文件，同时master主进程开始收集新的写命令并且缓存下来。master完成快照操作后，将数据文件发送给slave，slave将文件保存到磁盘，然后把数据加载到内存中。接着master把缓存的命令发送给slave。

##### 深入redis内核

内存淘汰：当内存不足时，有两种处理方式，启用虚拟内存（vm-enabled=yes），启用内存淘汰（maxmemory >0）。

淘汰算法：

- 随机淘汰：随机删除一个key
- LRU淘汰：删除一个最近最少访问的key
- TTL淘汰：删除一个最快过期的key

清除过期数据：

- 定时进行：每100毫秒进行一次清理数据操作
- 在用户获取数据时进行

##### Redis和Memcached的区别

- Redis和Memcache都是将数据存放在内存中，都是内存数据库。但是Memcache还可以缓存其他东西，比如图片、视频
- Redis不只支持简单的k/v类型的数据，同时还提供list、set、hash等数据结构的存储
- 虚拟内存，当物理内存用完时Redis可以将一些很久没有用到的value交换到磁盘
- 过期策略，memcache在set时就指定，例如`set key1 0 0 8`即永不过期，redis可以通过expire设定，例如：`expire name 10`
- 分布式，设定memcache集群，利用magent做一主多从；redis也可以做一主多从。
- 存储安全，memcache挂掉后，数据没了；redis可以定期保存在磁盘（持久化）
- 灾难恢复，memcache挂掉后数据不可恢复；redis数据丢失后可以通过aof恢复
- redis支持数据的备份，即master-slave模式的数据备份
- 应用场景不同：redis除了可以做nosql数据库之外，还能做消息队列、数据堆栈和数据缓存等。memcache适合于缓存sql语句、数据集、用户临时性数据、延迟查询数据和session等。