# 高度可伸缩系统的串行化技术

> 原文：<https://medium.datadriveninvestor.com/serialization-techniques-for-highly-scalable-systems-a8bf2130fe7f?source=collection_archive---------0----------------------->

这个故事最初发表在我的博客@linqz.io [这里](https://www.linqz.io/2018/03/serialization-techniques-for-highly-scalable-systems.html)。

在构建架构(微服务或任何其他类型)时，最常见的发送/共享数据对象的方法是 ***公共消息队列*** 和***HTTP API***，它们由项目的每个元素公开和使用。

对于高性能的流量，需要快速、可扩展和可互操作。通过网络发送 Java Serializable Object/JSON/XML 值在早期似乎是一个好主意，因为大多数语言为通信流的每一端都提供了现成的编码/解码，但对于大规模来说不再可行。

事情是这样的，如果你看一看这个过程有多长或者物体的大小，你会被**震惊**。对于高流量、总是可用的&稍微复杂的系统来说，将大部分时间花在 JSON 解析上并不罕见(除了 I/O 调用)。

在比较序列化格式时，我们可以观察到三个量化值。

*   序列化时间
*   反序列化时间
*   序列化大小

# Java 序列化的问题

*让我们一步步了解对象是如何序列化和反序列化的。*

所以当一个对象被序列化时

*   首先，它写出序列化流魔术数据，即 STREAM_MAGIC 和 STREAM_VERSION 数据(静态数据),以便 JVM 可以在必要时反序列化它。STREAM_MAGIC 将被“AC ED ”,而 STREAM_VERSION 将是 JVM 的版本。
*   然后写出与实例相关的类的元数据(描述)。它包括类的长度、类的名称、serialVersionUID(或串行版本)、各种标志以及这个类中的字段数量。
*   然后递归写出超类的元数据，直到找到 java.lang.object。
*   一旦写完元数据信息，它就从与实例相关的实际数据开始。但是这一次，它从最顶层的超类开始。
*   最后，它将与实例相关联的对象的数据从元数据写入实际内容。所以这里它开始为包含的类写元数据，然后像往常一样递归地写它的内容。

这里可以很容易地推断出，一个小对象在序列化时有时会比原始对象增长 20 倍。然后传输这个序列化的对象实际上会花费更多的时间。

# **外部化/XML/JSON 序列化的问题**

Java `**Externalizable**`接口(或者 Hadoop `**Writable**`工作原理类似)提供了`readExternal(ObjectInput in)`和`writeExternal(ObjectOutput out)`来控制什么序列化，什么不序列化。因此，它提供了非常需要的控制，如何/哪部分对象被序列化和反序列化。

Json/XML 的优势在于它是人类可读的，提供数据的服务可以直接在浏览器上使用。

XML 是强类型的，提供了人和机器的可读性，但是它非常慢，不安全，消耗大量的磁盘空间，并且它作用于公共成员和公共类，而不是私有或内部类。

首先也是最重要的，在 JSON 中没有针对 JSON 调用的错误处理。JSON 的另一个主要缺点是，如果与不受信任的服务或不受信任的浏览器一起使用，它可能会非常危险，因为 JSON 服务会返回一个包装在函数调用中的 JSON 响应，该响应将由浏览器执行。如果与不受信任的浏览器一起使用，它可能会被黑客攻击，这使得宿主 Web 应用程序容易受到各种攻击。

# 为什么是 proto buf/FlatBuffers/Thrift/Avro 等？

与 java 序列化/json/xml 相比，flat buffer/proto buf/Thrift/Avro 等工具有很多优势:

*   尺寸更小(至少 3 到 10 倍)
*   更快(快 20 到 100 倍)
*   打字
*   为您的所有服务提供一个通用界面，您只需更新您的。原型或。节俭还是。avro 并与使用它的服务共享，只要有该语言的库
*   [自描述](https://en.wikipedia.org/wiki/Self-documenting)(即如果没有外部规范，就无法说出字段的名称、含义或完整的数据类型)
*   处理类及其成员的版本问题
*   简易语言互用性

# 结果

在大多数情况下，你喜欢什么样的系统或多或少是个人喜好的问题。我会根据问题做出决定

> 我必须处理的数据有多大的可变性？
> 
> 需要多大的性能/流量？
> 
> 我需要像 Avro 这样的松类型系统还是像 flatbuffer 这样的强类型系统？
> 
> 它需要人类可读吗？
> 
> 我需要版本控制吗？向后兼容？

如果使用强类型系统有意义，我会这样做，因为我非常喜欢尽早得到关于错误的通知。

然而，如果需要非常灵活的数据结构，走另一条路可能更有意义。

因此，您可以看到选择取决于许多因素，很多时候 json/xml 序列化可以解决问题，但是当您谈论处理数百万 API 调用和系统的高可伸缩性/互操作性时，您必须寻找更健壮的系统。

你可以在这里读到更多

*   [https://en . Wikipedia . org/wiki/Comparison _ of _ data _ serialization _ formats](https://en.wikipedia.org/wiki/Comparison_of_data_serialization_formats)
*   https://google.github.io/flatbuffers/
*   【https://developers.google.com/protocol-buffers/ 
*   [https://thrift.apache.org](https://thrift.apache.org)
*   [https://avro.apache.org/docs/current/](https://avro.apache.org/docs/current/)

有问题吗？建议？评论？

下一步是什么？ [**在媒体上关注我**](https://medium.com/@vaibhav0109) 成为第一个阅读我的故事的人。