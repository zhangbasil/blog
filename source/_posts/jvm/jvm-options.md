---
title: JVM options
categories: 
    - java虚拟机
tags: 
    - JVM
---



java -XX:+PrintFlagsInitial 打印虚拟机是参数和初始值


### GC常用的参数

- -Xms<size>        设置初始化堆大小
- -Xmx<size>        设置最大堆大小
- -Xss<size>          set java thread stack size 设置线程栈大小
- -Xmn<size>        新生代大喜
- -XX:+UseTLAB      使用TLAB（Thread Local Allocation Buffer）线程的本地缓冲区，默认打开
- -XX:+PrintTLAB    打印TLAB的使用情况
- -XX:TLABSize        设置TLAB的大小
- -XX:+DisableExplicitGC 忽略手动调用GC的代码使得 System.gc()的调用就会变成一个空调用，完全不会触发任何GC
- -XX:+PrintGC
- -XX:+PrintGCDetails 打印gc日志
- -XX:+PrintHeapAtGC

-verbose:class 

- -XX:+TraceClassLoading

- -XX:+TraceClassUnLoading

- -XX:+PrintGCDetails 打印gc日志
- -XX:+UseParNewGC 使用ParNew垃圾收集器作为新生代



###  Parallel常用参数

- -XX:SurvivorRatio
- -XX:MaxTenuringThreshold=7 到达老年代的对象最大年龄值 PS 垃圾收集器默认是 15 
- -XX:PretenureSizeThreshold     大对象到底有多大
- -XX:+ParallelGCThreads        并发收集器的线程数，同样适用于CMS，一般设为和CPU核数相同
- -XX:+UseAdaptiveSizePolicy    自动选择各区大小比例



### CMS常用参数

- -XX:+UseConcMarkSweepGC     启用CMS收集器

- -XX:+ParallelCMSThreads           CMS线程数量
- -XX:CMSInitiatingOccupancyFraction   使用多少比例的来年的后开始CMS收集，默认是68%（近似值），如果频繁发生SerialOld卡顿，应该调小
- -XX:+UseCMSCompactAtFullCollection     在FGC时进行压缩
- -XX:CMSFullGCsBeforeCompaction         多次次FGC之后进行压缩
- -XX:<u>*CMSInitiatingPermOccupancyFraction*</u>   达到什么比例时进行Perm回收
- GCTimeRatio    设置GC时间占用程序运行时间的百分比



### G1 常用参数

- -XX:+UseG1GC
- -XX:MaxGCPauseMillis       
- -XX:GCPauseIntervalMillis     GC的间隔时间
- -XX:+G1HeapRegionSize   分区大小，建议逐渐增大该值，1 2 4 8 16 32   随着size增加，垃圾的存活时间更长，GC间隔更长，但每次GC的时间也会更长
- G1NewSizePercent  新生代最小比例，默认5%
- G1MaxNewSizePercent   新生代最大比例，默认60%
- GCTimeRatio     GC时间
- ConcGCThreads     线程数量
- InitiatingHeapOccupancyPercent  启动G1的堆空间占用比例

