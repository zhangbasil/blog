---
title: CMS垃圾收集器
categories: 
    - java虚拟机
tags: 
    - JVM
    - CMS
---

### Concurrent Mark Sweep (CMS) Collector

- 标记清除
- 作用在老年代

### 工作原理

- 初始标记
- 并发标记
- 重新标记
- 并发清除

其中初始标记和重新标记需要 Stop The World

#### 并发标记
+ 由于用户线程和垃圾收集器线程共存，用户线程不在引用某个对象，而垃圾收集器线程已经标记过，则会产生浮动垃圾
+ 垃圾收集器线程扫描后是确定是垃圾，但是此时用户线程引用了这个对象，则这个对象就不能被回收

浮动垃圾，不影响程序在下次GC的时候就会回收，而第二种情况则是使用了三色标记算法来解决

#### 三色标记算法






More info: [CMS](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/cms.html)
