# 如果我说你可以避免锁在 Java 里呢？第二部分

> 原文：<https://medium.datadriveninvestor.com/what-if-i-say-you-can-avoid-locking-in-java-part-2-a8afa7efa37f?source=collection_archive---------0----------------------->

继续第一部分，这个博客更多的是关于如何编写无锁代码，以及编写这样的代码需要什么条件？

没有人期望大型应用程序是完全无锁的。通常，我们从整个代码库中识别出一组特定的无锁操作。例如，在具有无锁操作的无锁队列中，诸如`push`、`pop`，或许还有`isEmpty`，等等。

在基于 Java 的应用程序中可能的方法有

*   原子读取-修改-写入操作
*   顺序一致性

# 原子读取-修改-写入操作

原子操作是以一种看起来不可分割的方式操纵内存的操作，即没有线程可以观察到操作的一半完成。

最常见的 RMW 操作(读-修改-写)是[比较和交换](https://en.wikipedia.org/wiki/Compare-and-swap) & [获取和添加](https://en.wikipedia.org/wiki/Fetch-and-add)。

```
**JDK7 - AtomicInteger (CompareAndSwap operation)**public final int addAndGet(int delta) {
    int current, next;
    do {
        current = get();
        next = current + delta;
    } while (!compareAndSet(current, next));
    return next;
}**JDK 8 - AtomicInteger (FetchAndAdd operation)** 
public final int getAndIncrement() 
{
     return unsafe.getAndAddInt(this, valueOffset, 1);
}
```

CAS 基于乐观方法工作，它预计会有一些失败，所以它会重试操作，所以理论上如果没有争用，它应该会很快工作。

在许多情况下，[原子取加](http://en.wikipedia.org/wiki/Fetch_and_add)指令可能比传统加载产生更好的性能(更多关于取加[在这里](https://blogs.oracle.com/dave/atomic-fetch-and-add-vs-compare-and-swap))。因此，在 JDK 8 中它优于 CAS。

# **顺序一致性**

顺序一致性意味着所有线程都同意内存操作发生的顺序，并且该顺序与程序源代码中的操作顺序一致。

实现顺序一致性的一个简单但不切实际的方法是禁用编译器优化，并强制所有线程在单个处理器上运行。即使线程在任意时间被抢占和调度，处理器也不会看到它自己的内存效果乱序。

# 总结一下

编写无锁代码时，请始终牢记以下要点:

*   从交易的角度考虑，记住谁拥有什么数据。要使用的典型编码模式是将工作放到一边，然后使用上面提到的 RMW 操作，通过单个原子写操作将每个更改“发布”到共享数据。
*   确保并发写入者不会相互干扰，也不会干扰并发读取者，并特别注意任何删除或移除并发操作可能仍在使用的数据的操作。

无锁编程的优点是，如果您挂起一个线程，它永远不会阻止其他线程作为一个组通过它们自己的无锁操作取得进展。

你可以在这里阅读更多关于无锁编程的内容:

*   [编写无锁代码:修正队列](http://collaboration.cmc.ec.gc.ca/science/rpn/biblio/ddj/Website/articles/DDJ/2008/0810/080901hs01/080901hs01.html)
*   【Xbox 360 和微软 Windows 的无锁编程考虑。