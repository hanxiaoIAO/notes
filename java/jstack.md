**jstack Dump 日志文件中的线程状态**

dump 文件里，值得关注的线程状态有：

1. 死锁，**Deadlock（重点关注）** 
2. 执行中，Runnable  
3. 等待资源，**Waiting on condition（重点关注）** 
4. 等待获取监视器，**Waiting on monitor entry（重点关注）**
5. 暂停，Suspended
6. 对象等待中，Object.wait() 或 TIMED_WAITING
7. 阻塞，**Blocked（重点关注）** 
8. 停止，Parked





含义如下所示：

- Deadlock：死锁线程，一般指多个线程调用间，进入相互资源占用，导致一直等待无法释放的情况。

- Runnable：一般指该线程正在执行状态中，该线程占用了资源，正在处理某个请求，有可能正在传递SQL到数据库执行，有可能在对某个文件操作，有可能进行数据类型等转换。

- Waiting on condition

  ：等待资源，或等待某个条件的发生。具体原因需结合 stacktrace来分析。

  - 如果堆栈信息明确是应用代码，则证明该线程正在等待资源。一般是大量读取某资源，且该资源采用了资源锁的情况下，线程进入等待状态，等待资源的读取。
  - 又或者，正在等待其他线程的执行等。
  - 如果发现有大量的线程都在处在 Wait on condition，从线程 stack看，正等待网络读写，这可能是一个网络瓶颈的征兆。因为网络阻塞导致线程无法执行。
    - 一种情况是网络非常忙，几乎消耗了所有的带宽，仍然有大量数据等待网络读写；
    - 另一种情况也可能是网络空闲，但由于路由等问题，导致包无法正常的到达。
  - 另外一种出现 Wait on condition的常见情况是该线程在 sleep，等待 sleep的时间到了时候，将被唤醒。

- Blocked：线程阻塞，是指当前线程执行过程中，所需要的资源长时间等待却一直未能获取到，被容器的线程管理器标识为阻塞状态，可以理解为等待资源超时的线程。

- Waiting for monitor entry 和 in Object.wait()：Monitor是 Java中用以实现线程之间的互斥与协作的主要手段，它可以看成是对象或者 Class的锁。每一个对象都有，也仅有一个  monitor。从下图1中可以看出，每个 Monitor在某个时刻，只能被一个线程拥有，该线程就是 “Active  Thread”，而其它线程都是 “Waiting Thread”，分别在两个队列 “ Entry Set”和 “Wait Set”里面等候。在  “Entry Set”中等待的线程状态是 “Waiting for monitor entry”，而在 “Wait Set”中等待的线程状态是  “in Object.wait()”。