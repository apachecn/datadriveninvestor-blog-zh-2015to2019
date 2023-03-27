# Java 8 流

> 原文：<https://medium.datadriveninvestor.com/java-8-stream-2f2a625b86c4?source=collection_archive---------1----------------------->

Java 8 的主要和流行的特性之一是 Java Stream.Java 流是一组工具或一组类，用于处理或操作 sequences.Java 有不同类型的集合，以不同的方式存储数据。我们可以把 Java 流看作一种声明式编程语言，可以用来查询不同类型的数据结构。

主要有两种类型的流操作，它们要么是中间操作，要么是终端操作。中间操作返回一个流，使我们能够在一个语句中链接多个中间操作(就像在 builder 模式中一样)。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

terminal 语句返回一个非流，它是一个 void 或其他组件。中间操作具有惰性执行，即中间操作不工作，除非流处理没有以终端操作结束。

![](img/18c44a75b456563239900a7067568583.png)

Photo by [chuttersnap](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

基本上，Java 流操作符要么接受 lambda 表达式，要么接受代码块。

使用 lambda 表达式的流

使用代码块

作为一个好的实践，最好使用 lambda 表达式，或者将执行操作的代码块添加到方法中，并在操作符中将其作为 lambda 表达式调用。我刚接触 streams 时面临的一个大问题是决定方法的返回类型。方法的返回类型基于流的输出。例如

*   如果操作符是一个终端操作符，它没有返回任何东西，我们可以使用一个 void 方法。
*   如果运算符是中间运算符，并且它返回整数流，则该方法必须是整数方法。

让我们看看一些流行的流操作符及其用法。

# **地图(x- > x)**

Map 是一个中间流运算符。该操作符的用途是操作流中的每个元素，并将每个值映射到一个新值。当我们必须将对象集合的类型从一种类型改变为另一种类型时，这很方便。

# **滤镜(x- > x < 2)**

Filter 是一个中间流运算符。其用途是仅过滤流中一组特定元素。这与 Sql 中的 where 子句非常相似。

# 减少((x，y)->x+y)

当我们使用整个流并产生单个值(如整个数组的和)时，我们使用这个中间流操作符。

# **forEach(x- > print)**

forEach 是一个终结操作。当我们想在流的最后对每个元素应用一个动作而不返回最终结果时，就使用这个方法。

# 收集(列表)

collect 是一个终端操作，用于将流中的元素收集到 java 集合中。

流的主要优点之一是，由于其可读的结构，代码变得更可读。由于流与方法有着密切的关系，代码变得更加建模和清晰。流通过简化复杂行为的表达减少了开发时间。因为 Streams 不像循环那样使用任何索引值，所以减少了开发中出现的错误。