---
title: JVM 面试题
categories: 
    - java虚拟机
tags: 
    - JVM
---

###### GC roots 有哪些



###### GC 算法有哪些

- Mark-Sweep(标记-清除)
  - 效率不高（如果java堆中包含大量对象，而且其中大部分都要被回收，这时必须进行大量的标记和清除动作，导致这两个过程的执行效率随着对象增多而降低）
  - 内存碎片（标记、清除后会产生大量不连续的内存碎片，会导致需要分配较大对象没有足够连续的内存而不得提前触发一次垃圾收集）
- Copying（拷贝）
  - 效率高，复制成本相等高（浪费空间）
  - 分配担保（老年代担保）
- Mark-Compact（标记-压缩）

###### 垃圾收集器有哪些

- ParNew 		Serial			 Parallel Scavenge
- CMS               Serial Old      Paraller Old
- G1                  ZGC 
- Epsilon          Shenandoah

###### 常见垃圾回收期组合参数

- -XX:+UserSerialGC = Serial New(DefNew) + Serial Old
  - 小型程序。默认情况下不会是这种选项，Hotspot会根据计算及配置和jdk版本自动选择收集器
- -XX:+UseParNewGC = ParNew + Serial Old
  - 这个组合已经很少用了（在某些版本中已经废弃掉了）
- -XX:UseConcMarkSweepGc = ParNew + CMS + Serial Old
- -XX:+UseParallelGC = Parallel Scavenge + Parallel Old （1.8默认垃圾收集器）
- -XX:+UseParallelOldGC = Parallel Scavenge + Parallel Old
- -XX:+UseG1GC = G1



###### CMS收集器有哪些问题

- 内存碎片 

  - 标记-清除 会产生内存碎片，老年代提前触发FGC
    - -XX:+UseCMSCompactAtFullCollection  内存碎片合并整理（停顿时间会变长）
    - -XX:CMSFullGCsBeforeCompaction   默认0   FGC多少次会被压缩

- 浮动垃圾

  - 三色标记（漏标）
    - 写屏障（write barrier）
      - Incramental Update （应用线程插入一条从黑色到白色对象的新引用）
  - Concurrent Mode Failure  PromotionFailed （当老年代内存不足应用线程的时候 会启用 Serial Old 收集器，用户会出现卡顿）
    - -XX:CMSInitiatingOccupancyFraction       默认92% 降低这个值让CMS保持老年代有足够的空间

  



