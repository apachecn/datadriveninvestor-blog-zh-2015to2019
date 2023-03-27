# Android 协同程序入门

> 原文：<https://medium.datadriveninvestor.com/getting-started-with-coroutines-on-android-c99407c3bd9c?source=collection_archive---------2----------------------->

[![](img/4c75af2699c26bf20ab39b41db9a36f1.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/7ae7abbc1fc6e56add5f9fd9f0e10f25.png)

Android 上的线程从一开始就是一个难题。从您的第一个 NetworkOnMainThreadException 到一个滞后的 RecyclerView，我们的应用程序中都至少有一个线程问题。

在 Android 上写异步代码有很多种方法。AsyncTask 被推荐了一段时间，然后被滥用，现在是许多笑话的笑柄。加载器被引入，如果你能弄清楚它们的 API，它们就能完成任务。IntentService 是处理脱离主线程的一种便捷方式，但是它带来了包和接收器的负担。RxJava 仍然被认为是线程的黄金标准，但最终超出了大多数应用程序的实际需求。

Kotlin 最近介绍了用协程处理异步行为的最新方法。协程类似于 C#和 Javascript 等语言中的 async / await。我不是这两种语言的专家，但这是别人告诉我的。协程的强大之处在于，它们允许开发人员编写读起来像是同步的异步代码。

Android 上协程最常见的用例之一是从网络获取数据。虽然像 Retrofit 这样的库可能已经有了一些像`enqueue()`这样的方法的线程意识，但是它们迫使我们编写大量的回调代码。回调在简单的时候很好，但是当需要不止一个回调时，或者当多个调用需要并行发生时，很容易导致混乱。RxJava 将是一个很好的库，但是仅用于网络就像用喷火器点燃生日蜡烛一样。

# 入门指南

要在 Android 上开始使用协程，首先需要引入以下依赖项。

```
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.1.1")
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.1.1")
```

这些库让您可以访问 coroutines API 和代表 Android 上主线程的特殊调度程序。其他流行的 UI 框架也支持协程，比如 JavaFx 和 Swing。

现在我们有了我们需要的工具，我们可以开始使用它们并打破东西。由于我们想在示例中做一个网络请求，我们还将引入 [OkHttp](https://github.com/square/okhttp) 和 [Moshi](https://github.com/square/moshi) (这两个必须知道来自 Square 的库)。

# 打电话

我们将创建一个 WebService 类，负责从 [JSONPlaceholder API](https://jsonplaceholder.typicode.com/) 获取 Todo。WebService 应该返回一个成功或失败的网络结果，我们将用一个密封的类对其建模。响应的主体也应该使用 Moshi 解析成一个 Kotlin 数据类。

代码看起来应该非常简单。没有回调，也不用担心我们在哪个线程上。我们正在返回一个用`suspendCoroutine`函数构建的协程，它有一个延续作为参数。当我们想从协程返回值时，我们调用 continuation。我们返回的值被包装在一个结果类中，这使得我们的代码是成功还是失败变得很明显。这个函数和同步函数的唯一区别是关键字`suspend`。如此标记的函数能够在不阻塞线程的情况下挂起，这对于获得 60fps 的平滑 UI 非常重要。

由于关键字`suspend`，我们不能像普通函数一样调用这个函数。要调用一个挂起的函数，我们必须向 Kotlin 编译器提供函数将要运行的范围。我们的方法是创建一个协同作用域。

(CoroutineScopes 和 CoroutineContexts 对我来说仍然有点困惑，但是我有一个我知道有效的方法，所以如果你知道更好的方法来完成我将要展示的内容，请告诉我。)

# 从活动中调用

我们需要定义我们的范围。我们将从 IO Dispatcher 调用网络，并用主 Dispatcher 调用 UI。两个调度程序都将与一个名为`Job`的对象相结合。据我所知，作业是一个允许协程被取消的对象。此活动的作业因暂停而取消，因此当活动暂停时没有正在运行的任务。

我们能够脱离主线程，从 IO dispatcher 调用网络，回到主线程并更新 UI。这样做的代码非常简单，如果多加练习，可能会更简单。

Kotlin 协程是一个非常强大的工具，在生态系统中快速移动。最佳实践仍在被发现，我肯定还在学习。如果你对我发布的代码有任何意见或建议，请在下面的评论中告诉我。

感谢阅读！