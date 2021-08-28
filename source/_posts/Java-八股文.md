---
title: Java 八股文
date: 2021-06-12 16:34:59
tags: 
- Java
- 面试
- 八股文
categories: 面试知识点
comments: true
---

唉八股文，能背多少背多少吧。
<!-- more -->
[原文](https://blog.csdn.net/qq_23696693/article/details/108406217)

## Java 基础知识

### Object类相关方法

* getClass 获取当前运行时对象的 Class 对象
* hashCode 返回对象的 hash 码
* clone 拷贝当前对象，必须实现 Cloneable 接口。**浅拷贝**对基本类型进行值拷贝，对引用类型拷贝引用；**深拷贝**对基本类型进行值拷贝，对引用类型对象不但拷贝对象的引用害拷贝对象的相关属性和方法。两者不同在与深拷贝创建了一个新的对象。
* equas 通过内存地址比较两个对象是否相等，String 类重写了这个方法使用值来比较是否相等。
* toString 返回类名@哈希码的 16 进制。
* notify 唤醒当前对象监视器的任意一个线程。
* notifyAll 唤醒当前对象监视器上的所有线程。
* wait
  1. 暂停线程的执行
  2. 三个不同参数方法（等待多少毫秒；额外等待多少毫秒；一直等待）
  3. 与`Thread.sleep(long time)`相比，sleep 使当前线程休眠一段时间，并没有释放该对象的锁，wait 释放了锁。
* finalize 对象被垃圾回收器回收时执行的方法。

### 基本数据类型

* 整形: byte(8)、short(16)、int(32)、long(64)
* 浮点型: float(32)、double(64)
* 布尔型: boolean(8)
* 字符型: char(16)

### 序列化

Java 对象实现序列化要实现 Serializable 接口。

* 反序列化并不会调用构造方法。反序列的对象是由 JVM 自己生成的对象，不通过构造方法生成。
* 序列化对象的引用类型成员变量，使用 transient 修饰。
* 如果想让某个变量不被序列化，使用 transient 修饰。
* 单例类序列化，需要重写`readResolve()`方法。

### String、StringBuffer、StringBuilder

* String 由 char[] 数组构成，使用了 final 修饰，是不可变对象，可以理解为常量，线程安全；对 String 进行改变时每次都会新生成一个 String 对象，然后把指针指向新的运用对象。
* StringBuffer 线程安全；StringBuilder 线程不安全
* 操作少量字符串用 String；单线程操作大量数据用 StringBuilder；多线程操作大量数据用 StringBuffer。

### 重载与重写

* 重载: 发生在同一个类，方法名相同，参数的类型、个数、顺序不同，方法的返回值和修饰符可以不同。
* 重写: 发生在父子类中，方法名和参数相同，返回值范围小于等于父类，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类；如果父类方法访问修饰符为 private 或者 final 则子类就不能重写该方法。

### final

* 修饰基本类型变量，初始化后就不能够对其进行修改。
* 修饰引用类型变量，不能够指向另一个引用。
* 修饰类或方法，不能被继承或重写。

### 反射

* 在运行时动态地获取类的完整信息
* 增加程序的灵活性
* JDK 动态代理使用了反射

### JDK动态代理

* 使用步骤
  1. 在创建接口及实现类
  2. 实现代理处理器`InvokationHandler`，实现`invoke(Proxy proxy, Method method, Object[] args)`
  3. 通过`Proxy.newProxyInstance(ClassLoaderLoader, Class[] interfaces, InvocationHandler h)`获得代理类
  4. 通过代理类调用方法

### Java IO

* 普通 IO，面向流，同步阻塞线程。
* NIO，面向缓冲区，同步非阻塞。

## Java 集合框架

### List (线性结构)

* ArrayList Object[] 数组实现，默认大小为 10，支持随机访问，连续内存空间，插入末尾时间复杂度 O(1)，插入第 i 个位置时间复杂度 O(n-i)。扩容，大小变为 1.5 倍，Arrays.copyOf(底层为 System.ArrayCopy)，复制倒新数组，指针指向新数组。
* Vector 类似 ArrayList，线程安全，扩容默认增长为原来的两倍，还可以指定增长空间长度。
* LinkedList 基于链表实现，1.7 为双向链表，1.6为双向循环链表，取消循环能更好地分清头尾。

### Map (Key, Value)

* HashMap
  1. 底层为数据结构，JDK1.8 是**数组 + 链表 + 红黑树**，JDK1.7 无红黑树。链表长度大于8时，转化为红黑树，优化查询效率。
  2. 初始容量为 **16**，通过`tableSizeFor`保证容量为 2 的幂次方。寻址方式，高位异或，**(n-1)&h** 取模，优化速度。
  3. 扩容机制，当元素数量大于容量 x 负载因子 0.75 时，容量扩大为原来的 2 倍，新建一个数组，然后转移到新的数组。
  4. 基于 Map 实现。
  5. 线程不安全。

* HashMap(1.7) 多线程循环链表问题
  1. 在多线程环境下，进行扩容时，1.7下的 HashMap 会形成循环链表。
  2. 则么形成循环链表: 假设有一 HashMap 容量为 2，在数组下标 1 位置以 A -> B 链表形式存储。有以线程对该 map 做 put 操作，由于触发扩容条件，需要进行扩容。这时另一个线程也 put 操作，同样需要扩容，并完成了扩容操作，由于复制到新数组是头部插入，所以 1 位置变为 B -> A 。这时第一个线程继续做扩容操作，首先复制 A ，然后复制 B ，再判断 B.next 是否为空时，由于第二个线程做了扩容操作，导致 B.next = A，所以在将 A 放到 B 前，A.next 又等于 B ，导致循环链表出现。

* HashTable
  * 线程安全, 方法基本是用 Synchronized 修饰
  * 初始容量为 11, 扩容为 2n+1
  * 继承 Dictionary 类。

* ConcurrentHashMap
  * 线程安全的 HashMap。
  * 1.7 采用分段锁的形式加锁; 1.8 使用 Synchronized 和 CAS 实现同步, 若数组的 Node 为空, 则通过 CAS 的方式设置值, 不为空则加在链表的第一个结点。获取第一个元素是否为空使用 Unsafe 类提供的 getObjectVolatile 保证可见性。
  * 对于读操作, 数组由 volatile 修饰, 同时数组元素为 Node, Node 的 K 使用 final 修饰, V 使用 volatile 修饰, 下一个结点也用 volatile 修饰, 保证多线程的可见性
