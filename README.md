## 封装 继承 多态

## 重载和重写的区别

## Spring Boot和Spring Cloud的区别是什么

## 什么时候用Spring Boot，什么时候用Spring Cloud

## Spring Boot和Spring Cloud都有什么缺点

## 索引过多，会影响性能吗？

## MyBatis和MyBatis Plus有什么区别

## Nacos主要做什么

## spring自动装配原理

主要是通过@EnableAutoConfiguration注解来实现的，一般这个这个注解不需要我们手动实现，他会在程序启动时，自动从程序启动类的根目录下开始遍历目录下所有文件，找到@configuration注解的class，或者是@bean注解的class，通过反射装载到IOC容器中，如果是使用spring mvc则是通过xml文件装配bean，spring boot只需要class上添加@bean注解。

## spring的ioc和aop是什么

spring的核心就是ioc和aop，ioc是控制反转，aop是面向切面编程，ioc控制反转就是说我们平时创建一个对象是手动new出来，自己管理的，而ioc是将对象交给spring框架来管理，他是通过DI注入来实现的，spring框架在启动时会加载所有bean信息，将他们放在一个map集合中，每一个bean都有自己的生命周期（生成实例对象-->填充属性-->初始化信息-->aop-->生成代理对象）。

aop概念比较抽象，用通俗的例子来讲，比如我们有一个add函数接口，我们需要记录这个函数的执行耗时，通常我们会用current time来记录一个开始时间和一个结束时间来计算，如果每一个接口都这样做，会产生大量的冗余代码，特别是日志记录，但用aop我们可以通过注解的方式来减少代码冗余，常用的就是@after，@before,@around

## linux常用命令

mkdir 创建文件夹

touch 创建文件

rm -rf 删除

su 切换用户

sudu 管理员权限

vi或vim 修改文件

cat 查看文件

yum install 安装包

yum remove 删除包

yum -y updage 更新包

yum -y upgrade 更新包但不更新软件和系统

## String、String Buffer和String Build的区别，怎么保证线程安全

String、String buffer和String Build都是通过char类型数组实现的，只不过String添加了final修饰，所以String变量定义了后不可变，如果对String变量进行**频繁**的修改、拼接等操作，会产生大量的GC回收，很占用系统的资源。

String Buffer和String Build调用同一父类append方法，采用相同的扩容机制，保证了性能开销。

String Buffer是线程安全的，String Build是非线程安全的。String Buffer在所有操作类的方法上添加了synchronized来保证线程安全。

所以String Buffer要比String Build慢一些，在不考虑线程安全的情况下，尽量使用String Build。

## 什么是锁

锁是一种机制，在并发编程中，多个线程对同一资源进行争夺，导致线程不安全，为了解决这个问题，引入了抽象的锁概念，来对资源进行锁定。

jvm中一个对象的对象头包含gc状态、对象布局、类型、同步状态、哈希标识基本信息。

锁就是改变对象的对象头中的同步状态。

参考：（http://openjdk.java.net/groups/hotspot/docs/HotSpotGlossary.html ） object header

## 什么是死锁

在多线程编程中，多个线程对同一个对象使用了多把锁，造成了线程互相等待，程序不往下走了，一般称为死锁。

## synchronized原理是什么

在对方法或者是变量使用synchronized，class文件在编译后的字节码中会生成monitorenter和monitorexit两个指令，这两个指令会调用jvm中使用C++实现的trylock方法，再由该方法调用汇编指令调用系统低层接口实现锁的抢占，中间还会涉及锁升级一系列操作。

jvm中每个对象都包含对象头，对齐数据，实例数据，对象的锁信息都包含在对象头的mark word中，其中包含无锁、偏向锁、轻量级锁、重量级锁的信息，synchronized就是修改mark word中锁的信息。

## synchronized怎么用的

可以修饰方法，也可以修饰代码块。

## ==和equals的区别

==如果是基本类型比较的是栈中的值，如果是引用类型比较的是对象地址。

equals通常都会被从重写，所以比较的是对象的值。

## 讲一下final

final可以修饰类、变量、方法

被final修饰的类不可以被继承。

被final修饰的变量不可以改变，在声明变量是就需要赋值，如果是基本类型的话在初始化后不可以被修改，是引用类型的话可以修改引用的值，但不能指向新的引用。

被final修饰的的方法不可以被重写，但可以重载。

## 接口和抽象类的区别

接口的目的是定义规范，抽象类的目的是抽取公共代码实现代码复用。

接口中只有abstract方法，抽象类中abstract方法或普通方法都可以有。

接口可以被实现多个，抽象类只能被继承一个。

接口跟他的实现类的关系是like a，抽象类跟他的继承类的关系是is a。

## List和Set的区别

List是有序的，添加的值可以重复，可以为空，取数据可以用迭代器取也可以用下标取

Set无序的，添加的值不可以重复，取数据只能用迭代器取。

## ArrayList和LinkedList的区别

ArrayList是基于动态数组实现的，使用ArrayList查询比较快，因为他在内从中是连续存储，我们随机访问的速度很快，但是插入数据会很慢，因为他要对数据进行移动。

LinkedList是基于链表实现的，他的查询比较慢，但是插入很快，因为他在内存中是分散存储的，每添加一个元素都会保存指向下一个元素的地址，访问的话需要遍历所有的元素。

## HashMap和HashTable的区别

HashMap和HashTable的底层都是通过数组+链表实现的，具体的是数组长度超过64链表长度超过8，这时候会转换为红黑树。

HashMap是非线程安全的，HashTable是线程安全的，他有synchronized方法修饰。

## ConcurrentHashMap

ConcurrentHashMap是通过synchronized+CAS+红黑树实现的，他的所有操作都是通过CAS实现，除非出现hash冲突会使用synchronized锁，所以他的锁粒度更细，效率更高，能保证线程安全的情况下性能更高。

## 索引的原理

MySql中有Hash索引和BTREE索引
hash索引是在创建索引时会生成一张hash表，将索引列的数据hash运算后存放在这张表里（顺序排序），下一次查找时根据条件hash运算到hash表中查找，可以很快的得到hash值对应的数据地址位置，不需要全表遍历。
BTREE索引则是用的b+树数据结构

## synchronized锁优化，锁粗化，锁消除

## 什么是自旋锁

自旋可以理解为一种轮询，线程会不断循环去尝试查看目标资源的锁有没有释放，如果释放了那么就获取，如果没有那么将进入下一轮循环。

## 什么是偏向锁

在无锁状态下，只有一个线程进来争夺锁资源，jvm将线程id写入对象头markword中，如果后续来争夺资源的锁id为同一个锁，那么这时候可以称之为偏向锁。

jvm在启动后，默认延迟4秒后启动偏向锁（可以设置jvm参数修改），后续所有新建对象的对象头中，锁状态默认为偏向锁（1 01）。

如果给锁状态为无锁的对象（0 01）添加synchronized关键字，对象会直接从无锁（0 01）升级为轻量级锁（1 00）。

## 什么是轻量级锁

在资源处于偏向锁状态下，出现了多个线程争夺锁资源的情况下，偏向锁将升级为轻量级锁。

## 什么是重量级锁

有多线程处于自旋状态，而且自旋个数超过cpu核数的一半或者是自旋次数超过10次，线程id进入等待队列，轻量级锁升级为重量级锁（1 10)

## synchronized和volatile的区别是什么

## 为什么要用volatile

volatile的特点就是当一个线程修改一个被volatile修饰的变量的值时，会被其他线程立刻感知到。

volatile只能保证在多线程情况下对共享变量读写数据具有原子性，其他情况下不能保证原子性。

## 说一说Java内存模型

## 说一说Java并发包

## failfast和failsafe区别

## 什么是copyOnWrite

## 什么是AQS

## 什么是CAS

在有多个线程对同一资源进行争夺的情况下，我们不想对这个资源进行锁定，而是通过其他方式来限制，同时只有一个线程能资源争夺成功，而其他修改失败的线程将会不断重试，直到修改成功。这种方式称之为cas。

## 什么是乐观锁

乐观锁相对悲观锁，每次获取资源不会对其上锁，在修改资源时会判断期间有没有其他线程修改了资源。乐观锁的一种实现方式就是cas。

## 什么是悲观锁

在一个线程获取资源时总会认为资源会被其他线程修改，所以每次获取资源都会上锁，这样的话，想要修改资源的线程就会被一直阻塞，直到获取到锁。

## 乐观锁和悲观锁是怎么实现的，区别是什么

## 什么是行级锁

## 什么是表级锁

## 什么是共享锁

## 什么是排他锁

## 什么是gap锁

## 什么是next key lock

## 数据库的隔离级别有哪些

## 说一说数据库的索引

## 什么是聚簇索引

## 什么是非聚簇索引

## 什么是最左前缀

## 索引如何实现的

## 什么是哈希索引

## 什么是B+树，如何实现的

## B+树里面的存储是怎么存的

## 为什么要用B+树

## 什么是回表

## 什么是分布式锁

## 分布式锁如何实现的

## 数据库，redis，zookeeper实现分布式锁的区别是什么，各自有什么优缺点

## 为什么要使用redis

redis可以做数据缓存、分布式锁、消息队列，还支持事务，持久化，集群方案。

## 什么是分布式缓存

一个服务端负责管理，多个客户端存储数据，根据一致性算法确定数据存储的节点。

## redis和memcache有什么区别

## zookeeper怎么实现分布式锁

## 什么是zookeeper

## 什么是cap

## 为什么cap不能同时存在

## 什么是base理论

## 分布式系统如何保证数据一致性

更新缓存、删除缓存

先更新数据库再删缓存

先更新缓存再删数据库

延迟双删

引入消息队列保证一致性

## 分布式数据一致性有哪些算法

## 什么是paxos算法

