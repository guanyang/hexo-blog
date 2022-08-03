---
title: LockSupport实战
catalog: true
comments: true
indexing: true
header-img: ../../../../img/default.jpg
top: false
tocnum: true
date: 2022-08-03 17:24:44
subtitle: LockSupport类可以阻塞当前线程以及唤醒指定被阻塞的线程
tags:
- 多线程
categories:
- Java
---

## 概要
- `LockSupport`类可以阻塞当前线程以及唤醒指定被阻塞的线程。
- 主要是通过`park()`和`unpark(thread)`方法来实现阻塞和唤醒线程的操作的。

## 原理
- 每个线程都有一个许可(permit)，permit只有两个值1和0，默认是0。
- 当调用unpark(thread)方法，就会将thread线程的许可permit设置成1(注意多次调用unpark方法，不会累加，permit值还是1)。
- 当调用park()方法，如果当前线程的permit是1，那么将permit设置为0，并立即返回。如果当前线程的permit是0，那么当前线程就会阻塞，直到别的线程将当前线程的permit设置为1.park方法会将permit再次设置为0，并返回。

>注意：因为permit默认是0，所以一开始调用park()方法，线程必定会被阻塞。调用unpark(thread)方法后，会自动唤醒thread线程，即park方法立即返回。

## 常用方法
```java
public static void park(Object blocker); // 暂停当前线程
public static void parkNanos(Object blocker, long nanos); // 暂停当前线程，不过有超时时间的限制
public static void parkUntil(Object blocker, long deadline); // 暂停当前线程，直到某个时间
public static void park(); // 无期限暂停当前线程
public static void parkNanos(long nanos); // 暂停当前线程，不过有超时时间的限制
public static void parkUntil(long deadline); // 暂停当前线程，直到某个时间
public static void unpark(Thread thread); // 恢复当前线程
public static Object getBlocker(Thread t); //阻塞的对象，方便线程dump时查看具体信息
```

## 总结
1. `LockSupport`不需要在同步代码块里，区别于`wait`和`notify`，所以线程间也不需要维护一个共享的同步对象了，实现了线程间的解耦。
2. `unpark`函数可以先于park调用，所以不需要担心线程间的执行的先后顺序。
3. 因为中断的时候`park`不会抛出`InterruptedException`异常，所以需要在park之后自行判断中断状态，然后做额外的处理。
4. `blocker`的作用是在dump线程的时候看到阻塞对象的信息

