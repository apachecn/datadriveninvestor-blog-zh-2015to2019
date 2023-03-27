# 一看就知道是本地人

> 原文：<https://medium.datadriveninvestor.com/react-native-at-a-glance-9cb1b296757b?source=collection_archive---------5----------------------->

我一直将 React Native 作为跨平台移动应用开发的工具。

![](img/a3eeca29ea402c6594ecf448630a4dd2.png)

脸书支持反动派。是用苹果的 Objective-C 写的。你用 Javascript 和 JSX 编写 RN 代码。RN 最酷的一点是，你的应用是真正的本地应用，而不是网络应用或混合应用。它在 IOS 和 Android 上都可以编译成本地代码。

我的观点是，React Native 是一个很好的方式，可以让视图和元素的 UI 在 IOS 和 Android 上工作相同。如果你的应用仅限于基本的功能，并且你有你想要的 RN 组件，那么 RN 是一个很好的解决方案。如果您的应用程序使用构建服务器端内容的 API，那么请认真考虑 RN，因为它在 HTTP 和 Javascript CRUD 方面很强。

让我们再深入一点。我在一个做图像人工智能识别和风格转换的应用程序上工作。React Native 在 Android 或 IOS 端都不支持这些新技术。

但是可以为 React Native 构建自己的 Swift 和 Java 组件。这就是问题所在。Swift 组件不会在 Android 上运行，Java 组件也不会在 IOS 上运行。所以你回到了依赖于平台的开发，而 RN 是缺乏的。

也可以将 RN 模块集成到现有的 Swift 和 Java 原生应用中。没错。您可以在现有的 IOS 和 Android 应用程序中添加常见的 RN 视图。

因此，在决定使用 React Native 时，您需要问自己这些问题:

1.  我的应用应该从 React 原生应用还是原生应用开始？
2.  React 是我需要的通用 UI 的一个很好的时间节省器吗？
3.  我需要为 IOS 和等同的 Android 写多少平台相关的模块代码？

**结论:**

如果你正在编写一个没有太多高科技平台依赖的应用程序，那么 React Native 应该可以工作。或者，如果你的应用程序使用大量的后端 API 来完成大部分工作，那么 RN 可能是一个很好的解决方案。但是如果你有一个复杂的应用程序，它使用了大量非 RN 支持的代码，那么你最好构建两个版本的应用程序，IOS 和 Android Native。

*原载于 2018 年 8 月 15 日*[*【www.bestcameraapps.com*](https://www.bestcameraapps.com/2018/08/react-native-at-glance.html)*。*