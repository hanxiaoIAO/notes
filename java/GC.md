[toc]

## GC

### GC 垃圾分类

强引用 StrongReference：非垃圾。new 创建的对象，及时抛出 OOM 异常，也不进行回收

软引用 SoftReferance：内存不足会回收

弱引用 WeakReference：下一次 GC 回收

虚引用 PhantomReference：任何时候都可能被垃圾回收器回收。无法通过虚引用得到一个对象，为一个对象设置虚引用的唯一目的是能在这个对象被回收时收到一个通知。

### GC 对象存活判断

垃圾收集主要针对堆和方法区。主要采用的方式为：1. 引用计数法 2.可达性分析法

### GC 垃圾回收算法

标记-清除：缺点是效率不高，会产生大量不连续的内存碎片，导致无法给大对象分配内存。

复制算法：缺点是内存的有效使用率太低。

标记-整理/标记-压缩：不会产生内存碎片，但内存移动频繁，效率低。

分代收集：综合利用，新生代使用复制算法和老年代使用标记-整理

方法区回收：

## GC 的几个概念

minor GC：在新生代进行的收集

major GC：在老年代进行的收集

full GC：同时作用于新生代和老年代

Stop-The-World：导致系统全局停顿

### Stop-The-World 的原因

Full GC 为了保证引用更新的正确，Java会暂停其他所有线程，native 可以执行，但不能和 JVM 交互。内存消耗越大，耗时越多。

## GC 垃圾收集器

### Serial 收集器

Serial 收集器即串行收集器，只用一个线程去回收。最古老，做稳定以及效率高的收集器。

新生代老年代均使用串行回收。新生代采用复制算法，老年代采用标记-压缩。

使用：

​	-XX:+UseSerialGC 

### ParNew 收集器

相当于 Serial 收集器的多线程版本。新生代使用并行回收。

使用：

​	-XX:+UseParNewGC  ParNew收集器

### Parallel收集器

感觉更像是 ParNew 收集器的升级版，可以通过参数启动自适应调解策略，以提供最合适的停顿时间或者最大吞吐量，控制 GC 时间和比例。

使用：

​	-XX:+UseParallelGC

### Parallel Old 收集器

Parallel 收集器的升级版，老生代使用并行回收。

使用：

​	-XX:+UseParallelOldGC

### CMS 收集器

老年代基于 “标记-清除实现”，过程包括:1. 初始标记 2. 并发标记 3. 重新标记 4. 并发清除。新生代使用 ParNew 的收集方式。

该收集器以获取最短回收停顿时间为目标，应用于 b/s 架构服务端，缺点是会产生大量空间碎片。

使用：

​	-XX:+UseConcMarkSweepGC

### G1 收集器

目前最新的收集器。该收集器的 Java 堆内存中的新生代和老年代不是物理隔阂，而是划分成多个大小相等独立区域，其中新生代老年代为几个独立区域的集合，区域可以不连续。

该收集器新生代使用 ParNew 的收集方式，老年代使用标记-压缩的方式。

使用：

​	-XX:+UseG1GC

#### -XX：+ UseStringDeduplication

尝试消除重复字符串，仅适用于G1 GC 算法。

[JVM消除重复自负参数-XX:+UseStringDeduplication的优缺点 - JAXenter](https://jaxenter.com/duplicate-strings-158567.html)

## 参考文档

 [Java垃圾回收机制（GC策略）](https://www.cnblogs.com/Mufasa/p/11226913.html)

[GC算法 垃圾收集器](https://www.cnblogs.com/ityouknow/p/5614961.html)

