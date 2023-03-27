# Java Futures 和 Kotlin 协同例程的比较

> 原文：<https://medium.datadriveninvestor.com/java-futures-and-kotlin-co-routines-a-comparison-4c8fa1e55407?source=collection_archive---------1----------------------->

![](img/0c7efe81d83f1b52cb3c345e47986071.png)

Photo by [Omar Flores](https://unsplash.com/@omarg247?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 背景

## 异步编程

异步编程帮助我们并行执行许多任务。请务必阅读我关于这个主题的其他帖子:

[](https://medium.com/@suchakjani/a-case-for-non-blocking-jdbc-part-one-caeadc80fb7c) [## 非阻塞 JDBC 案例(一)

### 背景

medium.com](https://medium.com/@suchakjani/a-case-for-non-blocking-jdbc-part-one-caeadc80fb7c)  [## 非阻塞 JDBC 的一个例子(下)

### 你需要多少关系？Oracle 数据库管理员

medium.com](https://medium.com/@suchakjani/a-case-for-non-blocking-jdbc-part-two-a8d803f6ed69) 

## Java 异步编程

Java 中的异步编程已经走过了漫长的道路。Java 的未来一直在不断改进，并且是许多代码库的支柱。Java 流以 Java 未来为基础。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

## 科特林异步编程

Kotlin 是由 Idea 的人们创建的一种新语言。Android 已经张开双臂接受了它。这里有一个链接可以帮助我们理解“为什么？”

[](https://blog.plan99.net/why-kotlin-is-my-next-programming-language-c25c001e26e3) [## 为什么 Kotlin 是我的下一门编程语言

### 一首你从未听过的语言颂歌

blog.plan99.net](https://blog.plan99.net/why-kotlin-is-my-next-programming-language-c25c001e26e3) 

Kotlin 有一个称为协程的方面，它有助于异步编程。

## 例子

在这篇文章中，我们将编写一些 Java 未来和 Kotlin 协同程序的例子。

# Java 未来

Java 的未来是围绕未来接口构建的。它们帮助我们了解 Java 中异步编程的各个方面。

 [## 未来(Java SE 12 和 JDK 12)

### 接口 archive searcher { String search(String target)；}类 App { ExecutorService executor =...归档搜索器…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/Future.html) 

我们现在将编写一系列的类。

## 工作管理器

```
package future.tryout;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.CompletionStage;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class WorkManager {

    private ExecutorService es = Executors.*newCachedThreadPool*();

    CompletionStage<Result> workForTime(int millis) {
        CompletableFuture<Result> future = new CompletableFuture<>();
        es.submit(()->{
            try {
                Thread.*sleep*(millis);
                future.complete(Result.*of*(millis, true, "Worked for " + millis + " milliseconds"));
            } catch (InterruptedException e) {
                future.complete(Result.*of*(millis, false, "Error : " + e.getMessage()));
            }
        });
        return future;
    }
}
```

Workmanager 通过在工作任务完成之前休眠给定的毫秒数来创建模拟真实工作任务的虚拟工作器。

然后它返回一个“结果”对象。这项工作被包装在一个“完成阶段”中。这将有助于我们将不同的任务联系起来。

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html) 

**注意:**根据 Java API，当我们睡眠时，我们也必须捕捉或抛出一个“Interruptedexception”。

## 结果

```
package future.tryout;

import lombok.Value;

@Value(staticConstructor = "of")
class Result {
    int time;
    boolean success;
    String message;
}
```

有三个字段的简单数据类

1.  int time —我们等待的时间，以毫秒为单位
2.  布尔成功——工作是否成功
3.  字符串消息—来自工作任务的消息

在这里使用 Lombok 来减少 java 样板代码。

[](https://www.baeldung.com/intro-to-project-lombok) [## 龙目岛项目简介| Baeldung

### Lombok 是我经常放入项目构建的第一个工具。我无法想象自己…

www.baeldung.com](https://www.baeldung.com/intro-to-project-lombok) 

## 未来示例

```
package future.tryout;

import java.util.Optional;
import java.util.concurrent.CompletionStage;

public class FutureExamples {

    private WorkManager manager = new WorkManager();
```

主示例类。

我们创建了 workmanager 实例，应该可以开始了。

**注:**

1.  这绝不是 Java 未来可以使用的所有方法的详尽列表。请查看 Java API 并确定您需要什么
2.  这些只是使用这些期货方法的可能方式的例子。

## 然后运行

```
public CompletionStage<Void> workWithRun(int time1, int time2) {
    return
        manager
        .workForTime(time1)
        .thenRun(() -> {
            manager.workForTime(time2);
        });
}
```

第一个例子是*，然后运行*。

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html#thenRun%28java.lang.Runnable%29) 

这里有两个参数，时间 1 和时间 2。一旦我们完成时间 1 的工作，我们想运行时间 2。

注意这里的*然后 Run* 返回一个带有 Void 的 CompletionStage。它不返回我们的“结果”对象。对于某些用例来说，这可能没问题。

让我们看看能否在下一个方法中返回一个结果。

## 然后应用

```
public CompletionStage<CompletionStage<Result>> workWithApply(int time1, int time2) {
    return
        manager
        .workForTime(time1)
        .thenApply(
            result -> manager.workForTime(time2) // If we wanted we could do something with result here
        );
}
```

这是一个*应用*的例子

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html#thenApply%28java.util.function.Function%29) 

如果我们还想返回 time2 任务的结果，我们可以使用*应用*。正如上面所看到的，我们得到的回报是 a 将第二个任务结果包装在两个完成阶段中。

让我们在下一个例子中看看我们是否能在这方面有所改进。

**然后撰写**

```
public CompletionStage<Result> workWithCompose(int time1, int time2) {
    return
        manager
        .workForTime(time1)
        .thenCompose(
            result ->  manager.workForTime(time2) // If we wanted we could do something with result here
        );
}
```

这是一个 *thenCompose* 的例子

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html#thenCompose%28java.util.function.Function%29) 

如上所述，我们得到的回报是在一个完成阶段有结果。

如果您使用过 streams api，这类似于一个*平面图*

 [## 流(爪哇东南 12 和 JDK 12)

### 流管道可以顺序或并行执行。这种执行模式是流的一个属性…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/stream/Stream.html#flatMap%28java.util.function.Function%29) 

**然后接受两者**

```
public CompletionStage<Void> workWithAccept(int time1, int time2, int time3) {
    return
        manager
        .workForTime(time1)
        .thenAcceptBoth(
            manager.workForTime(time2), (result, result2) -> {
                if (result.isSuccess() && result2.isSuccess()) {
                    manager.workForTime(time3);
                }
            });
}
```

这是一个*接受两个*三个任务的例子

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html#thenAcceptBoth%28java.util.concurrent.CompletionStage,java.util.function.BiConsumer%29) 

这里我们执行三个任务，但是和以前一样，我们仍然只得到一个 void CompletionStage。让我们看看我们是否能在这方面有所改进并得到一个结果。

**然后合并**

```
public CompletionStage<Optional<CompletionStage<Result>>> workWithCombine(int time1, int time2, int time3) {
    return
        manager
        .workForTime(time1)
        .thenCombine(manager.workForTime(time2),(result, result2) -> {
            if (result.isSuccess() && result2.isSuccess()) {
                return Optional.*of*(manager.workForTime(time3));
            }
            return Optional.*empty*();
        });
}
```

这是一个*然后将*与三个任务相结合的例子

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html#thenCombine%28java.util.concurrent.CompletionStage,java.util.function.BiFunction%29) 

这里我们执行三个任务，并得到最后一个任务的结果。

**例外情况**

如果我们想知道是否有一个异常，然后我们想在任何 CompletionStage 上处理这个异常，那该怎么办呢？

当在结果完成阶段完成时，我们可以使用*。以上所有例子都是如此。*

```
(void, exception) -> {
   if (exception == null) {
     // triggering stage completed normally
   } else {
     // triggering stage completed exceptionally
   }
 }
```

 [## 完成阶段(Java SE 12 和 JDK 12)

### 方法形式是创建延续阶段的最常见方式，它无条件地执行一个计算，即…

docs.oracle.com](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/concurrent/CompletionStage.html#whenComplete%28java.util.function.BiConsumer%29) 

# 科特林协程

Kotlin 协程在 Kotlin 的异步编程方面帮助了我们。请务必浏览一下这里的指南

[](https://kotlinlang.org/docs/reference/coroutines/basics.html) [## 基础知识- Kotlin 编程语言

### 本节介绍基本的协程概念。运行下面的代码:import kot linx . coroutines . * fun main(){…

kotlinlang.org](https://kotlinlang.org/docs/reference/coroutines/basics.html) 

我们现在将编写一系列的类。

## 工作管理器

```
package coroutine.tryout

import kotlinx.coroutines.delay

internal class WorkManager {

    suspend fun workForTime(millis: Int): Result {
        *delay*(millis.toLong())
        return Result(millis, true, "Worked for $millis milliseconds")
    }
}
```

Workmanager 通过在工作任务完成之前休眠给定的毫秒数来创建模拟真实工作任务的虚拟工作器。

*deplay* 是一个特殊的*挂起函数*，它不阻塞线程，但是*挂起*协程，它只能从协程中使用。

[](https://kotlinlang.org/docs/reference/coroutines/basics.html) [## 基础知识- Kotlin 编程语言

### 本节介绍基本的协程概念。运行下面的代码:import kot linx . coroutines . * fun main(){…

kotlinlang.org](https://kotlinlang.org/docs/reference/coroutines/basics.html) 

## 结果

```
package coroutine.tryout

data class Result(val time: Int, val isSuccess: Boolean, val message: String)
```

有三个字段的简单数据类

1.  int time —我们等待的时间，以毫秒为单位
2.  布尔成功——工作是否成功
3.  字符串消息—来自工作任务的消息

热爱数据类！

**注意** : Java 可能很快会有一个类似的概念，即记录类

 [## JEP 359:记录(预览)

### 用记录增强 Java 编程语言。记录为声明类提供了一种紧凑的语法…

openjdk.java.net](https://openjdk.java.net/jeps/359) 

## 协同示例

```
package coroutine.tryout

import kotlinx.coroutines.async
import kotlinx.coroutines.coroutineScope

class CoroutineExamples {

    private val manager = WorkManager()
```

主示例类。

我们创建了 workmanager 实例，应该可以开始了。

**注:**

1.  这绝不是我们可以在 Kotlin 协程中使用的所有函数的详尽列表。请查看 CoRoutines API 并确定您需要什么
2.  这些只是使用这些协程方法的可能方式的例子。

## 两种功能同步运行

```
suspend fun workWithTwoTimes(time1: Int, time2: Int): Pair<Result, Result> {
    return *coroutineScope* **{** val result1 = manager.workForTime(time1) // work1
        val result2 = manager.workForTime(time2) // work2 after work1
        Pair(result1, result2)
    **}** }
```

这里，我们在一个协程中执行两个任务，并在一个 pair 类中返回这两个任务的结果。

## 两种功能并行运行

```
suspend fun workWithTwoTimesParallel(time1: Int, time2: Int): Pair<Result, Result> {
    return *coroutineScope* **{** val work1 = *async* **{** manager.workForTime(time1) **}** // Async work1
        val result2 = manager.workForTime(time2) // work2 while work1 is working
        val result1 = work1.await() // non-blocking wait
        Pair(result1, result2)
    **}** }
```

这里我们并行执行两个任务，然后在 Pair 类中返回两个任务的结果。没有更多的。太棒了。

## 三种功能同步运行

```
suspend fun workWithThreeTimes(time1: Int, time2: Int, time3: Int): Triple<Result, Result, Result> {
    return *coroutineScope* **{** val result1 = manager.workForTime(time1) // work1
        val result2 = manager.workForTime(time2) // work2 after work1
        val result3 = manager.workForTime(time3) // work3 after work2
        Triple(result1, result2, result3)
    **}** }
```

这里，我们在一个协程中执行三个任务，并在一个三元组类中返回任务的三个结果。

## 三种功能并行运行

```
suspend fun workWithThreeTimesParallel(time1: Int, time2: Int, time3: Int): Triple<Result, Result, Result> {
    return *coroutineScope* **{** val work1 = *async* **{** manager.workForTime(time1) **}** // Async work1
        val work2 = *async* **{** manager.workForTime(time2) **}** // Async work2 while work1 is working
        val result3 = manager.workForTime(time3) // work3 while work1 and work2 are working
        val result1 = work1.await() // non-blocking wait
        val result2 = work2.await()// non-blocking wait
        Triple(result1, result2, result3)
    **}** }
```

这里，我们在一个协程中并行执行三项工作，并在一个三重类中返回任务的三个结果。

**注:**

1.  java 中的“async/await”即“wait/lock/notify/join”是 Java 中涉及线程同步的线程阻塞范例。
2.  kotlin 中的“async/await”解释为:“在不阻塞线程的情况下等待该值的完成”
3.  如果我们不关心结果，我们可以使用 *launch* 来代替 *async*
4.  我们能在 Java 中做类似的事情吗，比如执行一个任务，当任务完成时，在不阻塞线程的情况下得到一个通知？是的，我们可以选择使用任何基于事件/消息的框架，如 Vert.x、Akka Actors、Play 等…

## 试验

```
package coroutine.tryout

import io.kotlintest.specs.StringSpec
import kotlin.system.measureTimeMillis

class CoroutineExamplesTimeTest : StringSpec(**{** val coroutineExamples = CoroutineExamples()
    val time1 = 300
    val time2 = 200
    val time3 = 100

    "workWithTwoTimes should return result time1 and result time2" **{** val time = *measureTimeMillis* **{** coroutineExamples.workWithTwoTimes(time1, time2)
        **}** *println*("workWithTwoTimes in $time ms")
    **}** "workWithThreeTimes should return result time1, time2  and  time3" **{** val time = *measureTimeMillis* **{** coroutineExamples.workWithThreeTimes(time1, time2, time3)
        **}** *println*("workWithThreeTimes in $time ms")
    **}** "workWithTwoTimesParallel should return result time1 and result time2" **{** val time = *measureTimeMillis* **{** coroutineExamples.workWithTwoTimesParallel(time1, time2)
        **}** *println*("workWithTwoTimesParallel in $time ms")
    **}** "workWithThreeTimesParallel should return result time1, time2  and  time3" **{** val time = *measureTimeMillis* **{** coroutineExamples.workWithThreeTimesParallel(time1, time2, time3)
        **}** *println*("workWithThreeTimesParallel in $time ms")
    **}

}**)
```

如上所述，我们将使用 *measureTimeMillis* 作为一个模块来测试我们的暂停任务功能。

[](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.system/measure-time-millis.html) [## 测量时间毫秒

### 编辑描述

kotlinlang.org](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.system/measure-time-millis.html) 

上面的测试应该是不言自明的。

## 测试输出

```
workWithTwoTimes in 509 ms
workWithThreeTimes in 612 ms
workWithTwoTimesParallel in 304 ms
workWithThreeTimesParallel in 307 ms
```

我们得到的结果如上。

运行两个任务我们用 509ms，并行运行两个任务我们用 304 ms，有道理。

运行三个任务我们用 612ms，并行运行三个任务我们用 307 ms，同样有道理。

# 裁决

科特林协程很有意义。它们似乎很容易使用，因此开发应该更简单。

你怎么想呢?欢迎在下面的评论区添加任何评论/建议/更正。

谢谢你的时间。

# 密码

所有代码都在这里签入

[](https://gitlab.com/suchakjani/coroutines) [## Suchak Jani / coroutines

### 测试 Java Futures 和 Kotlin 协程

gitlab.com](https://gitlab.com/suchakjani/coroutines)