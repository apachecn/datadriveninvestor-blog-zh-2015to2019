# 超越 Java 8:开发者的视角

> 原文：<https://medium.datadriveninvestor.com/going-beyond-java-8-a-developers-perspective-ea6a6a93ddc1?source=collection_archive---------7----------------------->

![](img/39f5b32e9a3c97bd1bf892446c4f4eca.png)

*由阿里巴巴集团资深技术专家陈利炳(雷娟)主持，GitHub*

Python、JavaScript 和其他编程语言变得越来越流行。然而，以前占主导地位的语言 Java，尽管失去了一些偏爱，但在主要编程语言的不同排名中仍然保持着头把交椅。它仍然是主流企业应用程序开发的第一语言。自从 Java 8 发布以来，Java 已经引入了许多有用的新语言特性和工具来帮助提高性能。然而，许多程序员还没有升级到 Java 8 以后的版本进行开发。本文从开发人员的角度描述了 8 以后版本中的 Java 语言特性。

[](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) [## 雅虎财经 API |数据驱动投资者的 6 种替代方案

### 长期以来，雅虎金融 API 一直是许多数据驱动型投资者的可靠工具。许多人依赖于他们的…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) 

第一，Java 8 在大多数 Java 程序员眼中无疑是一个里程碑式的版本。它最著名的特性是流和 Lambda 表达式，这使得函数式编程成为可能，并使 Java 重获新生。这就是为什么尽管 Oracle 停止了更新，但许多云供应商仍然给予 Java 8 巨大的支持，以保持长期活跃。

[安装阿里云 Java SDK>>](https://www.alibabacloud.com/help/doc-detail/52740.htm?spm=a2c41.13869702.0.0)

很多程序员没有升级到 Java 8 以后的版本进行开发，这也是我们在以后版本中解决语言特性的原因。本文关注开发，跳过垃圾收集(GC)、编译器、Java 模块和平台。这些主题可以在其他文章中讨论。以下功能在代码编写中发挥了作用。

Java 13 即将发布，从 Java 9 到 Java 13 的 Java 版本全部覆盖。Java 版本经过了调整，因此引入了一个版本的预览，随后是基于用户反馈的增强和改进。在本文中，我们不会特别指出哪个版本具有哪些功能。你可以把它们看作是 Java 8 以后所有版本的混合特性。本文的参考资料来源是 Java 官方网站上的 Features 和 Pluralsight 部分对每个 Java 版本的详细介绍。

# Var —局部变量类型推理

Java 支持泛型，但是如果类型很长，并且您不太关心它，那么就使用 var 关键字。这大大简化了您的代码。Java IDE 可以很好地与 var 一起工作，所以您不会遇到频繁的代码提示。

```
Map<String, List<Map<String,Object>>>  store = new ConcurrentHashMap<String, List<Map<String,Object>>>();
        Map<String, List<Map<String,Object>>>  store = new ConcurrentHashMap<>();
        Map<String, List<Map<String,Object>>>  store = new ConcurrentHashMap<String, List<Map<String,Object>>>();
  //lambda
  BiFunction<String, String, String> function1 = (var s1, var s2) -> s1 + s2;
        System.out.println(function1.apply(text1, text2));
```

将 confd 文件复制到 bin 目录并启动 confd。

```
sudo cp bin/confd /usr/local/bin
confd
```

在实践中，您可能会遇到一些小的限制，比如将值赋给空值。但这些都不是大问题，所以你现在就可以开始了。

# 过程句柄

我们只是偶尔用 Java 调用系统命令。当然，我们大多使用 ProcessBuilder 来实现。另一个特性是增强的 ProcessHandle，它提供其他进程的更新。ProcessHandle 帮助获取所有进程、特定进程的启动命令和启动时间等等。

```
ProcessHandle ph =  ProcessHandle.of(89810).get();
System.out.println(ph.info());
```

# 集合工厂方法

你还在用新方法创建 ArrayList 和 HashSet 吗？你可能落后于形势。直接使用工厂方法。

```
Set<Integer> ints = Set.of(1, 2, 3);
List<String> strings = List.of("first", "second");
```

# 字符串类的新 API

这里不可能列出所有的新 API，但是掌握几个重要的 API 就足以让您摆脱第三方 StringUtils。以下 API 是:repeat、isEmpty、isBlank、strip、lines、indent、transform、trimIndent、formatted。

# 支持 HTTP 2

使用 OkHTTP 3 更容易，但是如果您不想要其他开发包，而更喜欢使用 HTTP 2，这不是问题。Java 支持 HTTP 2，以及同步和异步编程模型。同样，代码也基本相同。

```
HttpClient client = HttpClient.newHttpClient();
        HttpRequest req =
                HttpRequest.newBuilder(URI.create("https://httpbin.org/ip"))
                        .header("User-Agent", "Java")
                        .GET()
                        .build();
        HttpResponse<String> resp = client.send(req, HttpResponse.BodyHandlers.ofString());
        System.out.println(resp.body());
```

# 文本块(JDK 13)

在早期版本中，您必须键入长文本并避免双引号。可读性差。例如:

```
String jsonText = "{"id": 1, "nick": "leijuan"}";
```

使用文本块的新方法:

```
//language=json
  String cleanJsonText = """
        {"id": 1, "nick": "leijuan"}""";
```

简单多了吧？专注于写你的代码，也不用担心双引号转义，或者拷贝共享转换。

等等，你在 cleanJsonText 前面加的`//language=json`是什么？这是 IntelliJ IDEA 的一个特点。你的文本块是语义的。将`//language=json`添加到 HTML、JSON 或 SQL 代码中，您会立即得到代码提示。嘘...我只能把这个小技巧分享给我的好朋友。

文本块还支持基本的模板特征。将上下文变量引入文本块，键入%s 并调用格式化方法。你的任务完成了。

```
//language=html
    String textBlock = """
    <span style="color: green">Hello %s</span>""";
    System.out.println(textBlock.formatted(nick));
```

# 开关的改进

# 箭头标签

切换箭头“-->”的引入消除了使用如此多的中断的需要。下面是一些示例代码。

```
//legacy
    switch (DayOfWeek.FRIDAY) {
        case MONDAY: {
            System.out.println(1);
            break;
        }
        case WEDNESDAY: {
            System.out.println(2);
            break;
        }
        default: {
            System.out.println("Unknown");
        }
    }
    //Arrow labels
    switch (DayOfWeek.FRIDAY) {
        case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
        case TUESDAY -> System.out.println(7);
        case THURSDAY, SATURDAY -> System.out.println(8);
        case WEDNESDAY -> System.out.println(9);
    }
```

# 切换表达式

这意味着开关有返回值。下面是一些示例代码。

```
//Yielding a value
    int i2 = switch (DayOfWeek.FRIDAY) {
        case MONDAY, FRIDAY, SUNDAY -> 6;
        case TUESDAY -> 7;
        case THURSDAY, SATURDAY -> 8;
        case WEDNESDAY -> 9;
        default -> {
            yield 10;
        }
    };
```

关键字 yield 表示开关表达式的返回值。

# 使用这些功能

所有这些特性看起来都很好，但是当我们还在使用 Java 8 时，我们如何使用它们呢？除了考虑这些特性，我们还能做什么？别担心。有人找到了解决办法。

该项支持透明地将所有 JDK 12+语法编译成 Java 8 VM。换句话说，在 Java 8 上运行这些语法不成问题。即使在 Java 8 环境中，所有这些特性都是可用的。

如何使用它们？这一切都非常简单和容易。

首先，下载最新的 JDK，比如 JDK 13，并将 jabel-java-plugin 添加到依赖项中。

```
<dependency>
            <groupId>com.github.bsideup.jabel</groupId>
            <artifactId>jabel-javac-plugin</artifactId>
            <version>0.2.0</version>
  </dependency>
```

然后，调整 Maven 的编译器插件，将源码设置为你需要的 Java 版本，比如 Java 13。目标和版本可以设置为 Java 8。IntelliJ IDEA 能够自动识别，不需要调整。

```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>13</source>
                    <target>8</target>
                    <release>8</release>
                </configuration>
</plugin>
```

现在，开始享受使用这些功能的愉快体验吧。

# 摘要

在这篇博客中，我们已经讨论了 Java 中一些最流行和最有用的特性。一些有用的特性，比如 API 调整，在本文中没有提到。但是，您可以通过我们的博客或论坛与我们的社区分享它们。

# 原始资料

[](https://www.alibabacloud.com/blog/going-beyond-java-8-a-developers-perspective_595669?spm=a2c41.13869702.0.0) [## 超越 Java 8:开发者的视角

### 本文从开发人员的角度描述了 Java 版本 8 以后的特性，强调了如何…

www.alibabacloud.com](https://www.alibabacloud.com/blog/going-beyond-java-8-a-developers-perspective_595669?spm=a2c41.13869702.0.0)