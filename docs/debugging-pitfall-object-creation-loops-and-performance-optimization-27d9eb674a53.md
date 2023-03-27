# 调试陷阱:对象创建、循环和性能优化

> 原文：<https://medium.datadriveninvestor.com/debugging-pitfall-object-creation-loops-and-performance-optimization-27d9eb674a53?source=collection_archive---------23----------------------->

![](img/3afa1ee327d9b32e178b5bce4e11173e.png)

Not those kind of loops! Photo by [Oliver Hale](https://unsplash.com/photos/2cYueJxEDz8?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/roller-coaster?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

作为一名计算机科学导师，我通常告诉我的新生不要太担心性能优化，首先要专注于理解你在做什么，让你的程序工作。这通常也是我在自己的程序中最初的做法，但是在有些情况下，我并不总是持这种观点。作为一名游戏开发人员，我当然需要将性能放在心上，但是我曾经处理过一个重要的实例，在这个实例中，一小段看似微不足道的代码在一个商业的非游戏应用程序中造成了严重的性能问题。

我们的团队正在为一个客户的企业级 web 系统进行重大更新，其中最重要的功能之一是向大量收件人发送群发电子邮件。其中一些电子邮件会发送给超过 10，000 人。正如电子邮件自动化中常见的那样，每封电子邮件都需要将收件人姓名和其他相关但特定于收件人的信息填充到邮件中。如果我没记错的话，我们使用 Java 的 JavaMail API 工具来构造和发送消息。

在用户接受度测试期间，一个客户端用户向我们的团队通报了一个严重的缺陷:有时生成一封电子邮件并发送给一个大的收件人列表需要五分钟或更长时间(同样，我指的是成千上万的收件人)。编写这部分代码的开发人员不在，所以在接到我们的客户联络员的电话并与他面谈后，我开始自己查看代码。

我在其他地方写过一些我的调试技术，比如使用系统日志和创建自己的日志记录语句，以及如何使用 bug 跟踪器(或者创建自己的跟踪器，你可以在[https://medium . com/@ cloudyheavengames/a-winning-technique-to-make-you-a-powerful-debugger-73 C2 DDA 088 f 0](https://medium.com/@cloudyheavengames/a-winning-technique-to-make-you-a-powerful-debugger-73c2dda088f0)上读到)，所以我不会过多地讨论我使用的实际过程。通过大量使用系统的日志功能，以及了解处理电子邮件的代码的大致位置，我对在哪里查找问题有了一个很好的想法。

具体的原因不是很明显，新的编码人员可能不会想到。正如我们团队成员的经验水平所证明的那样，甚至更有经验的编码人员也可能落入这个微妙的陷阱。该问题与循环和对象创建有关。正如我提到的，对于每个用户来说，blast 电子邮件的基本主体是相同的，但是我们只是替换了每个收件人的姓名和其他信息。为了完成这项任务，我们使用了一个循环来遍历收件人列表中的每个用户，并创建和发送个人电子邮件。在伪代码中，该过程如下所示:

*对于(列表中的每个用户 I)*

*{*

*   创建一个邮件消息对象，我们称之为消息对象
*   *使用收件人的名字*为问候语创建一行文本
*   *为标准消息的剩余部分创建一段文本*
*   *连接问候文本和标准消息，形成完整的消息文本*
*   *将 messageObject 的文本设置为我们的完整消息*
*   *将消息对象的附件设置为标准文件(对每个收件人都一样)*
*   *将 messageObject 发送到邮件服务器进行投递，收件人为用户 I*

*}*

当然，由于我从事该项目的时间，并且因为我没有代码的副本或所有权，这些不是确切的细节，但是这个描述非常接近算法。

你觉得这段代码有问题吗？我们的方法可能适用于一些邮件，但是对于大量的收件人列表呢？花一分钟考虑一下，然后继续读下去…

好，注意我们在括号内的第一行代码中做了什么。我们创建一个消息对象。在 JavaMail API 中，这可能是一个 MimeMessage 对象(如果你想要更多关于 API 的细节，请查看[https://javaee.github.io/javamail/docs/api/](https://javaee.github.io/javamail/docs/api/))。如果我们有 10，000 个接收者，我们将创建一个对象 10，000 次，在每次循环迭代结束时销毁它，然后返回到循环的顶部，再次创建基本相同的对象。对于每个收件人，邮件的所有内容都是相同的，除了带有收件人姓名和实际收件人地址的问候语。那么为什么我们需要创建一万次全新的 MimeMessage 对象呢？如果您查看 MimeMessage 的文档(您可以在[https://docs . Oracle . com/javaee/6/API/javax/mail/internet/mime message . html](https://docs.oracle.com/javaee/6/api/javax/mail/internet/MimeMessage.html)阅读它)，您会注意到我们有设置消息接收者和消息文本的方法*(分别是 setRecipients()* 和 *setText()* )。我们在每次循环迭代中为标准文本创建一个新字符串也是在浪费时间。

因此，更好的解决方案可能是在循环外部创建消息对象和标准文本，然后在循环内部创建特定的问候行，然后在循环内部设置接收者并发送消息。新代码可能看起来像:

*创建新的消息对象*

*用标准消息文本创建字符串*

*设置消息对象的附件*

*对于(列表中的每个用户 I)*

*{*

*   *使用收件人的名字*为问候语创建一行文本
*   *连接问候文本和标准消息，形成完整的消息文本*
*   *将 messageObject 的文本设置为我们的完整消息*
*   *将 messageObject 发送到邮件服务器进行投递，收件人为用户 I*

*}*

在 Java 中创建和销毁对象需要时间。对于小规模的标准操作，您可能不会注意到这一点，但是当您像我们讨论的那样大规模地工作时，这一点就会累积起来。如果你感兴趣，我还找到了开发者 Andre Spiegel 写的一篇关于这个主题的文章，他在文章中做了一个用 Java 创建对象的定时测试:[http://drmirror.net/2013/06/06/object-creation/](http://drmirror.net/2013/06/06/object-creation/)。他指出，新版 Java 已经得到了更好的优化，因此这个过程不需要花费太多时间。但是，请记住，您可能正在为一个不总是使用最新版本 Java 的客户工作，这种情况经常发生在政府或非盈利客户身上，或者您正在更新和处理的项目中有很多旧的遗留代码。将整个系统迁移并测试到更新的软件版本需要大量的工作和计划，有时没有时间或资源来冒险长时间关闭系统。此外，Java 并不是创建和销毁对象的唯一语言，所以仅仅因为 Java 的虚拟机得到了改进，并不意味着其他语言也是如此。

总而言之，调试并不总是关于跟踪灾难性的崩溃。有时，看似微不足道的优化会对某个特性是否可用产生巨大的影响。所以在极端情况下运行程序时要小心，比如有大量用户，尤其是在处理循环的时候！

# 有关系的

已标记的[编码](http://cloudyheavengames.com/tag/coding/)、[计算机科学](http://cloudyheavengames.com/tag/computer-science/)、[调试](http://cloudyheavengames.com/tag/debugging/)、[游戏开发](http://cloudyheavengames.com/tag/game-development/)、 [java](http://cloudyheavengames.com/tag/java/) 、[编程](http://cloudyheavengames.com/tag/programming/)。将[永久链接](http://cloudyheavengames.com/debugging-pitfall-object-creation-loops-performance-optimization/)加入书签。

*原载于 2018 年 9 月 18 日*[*【cloudyheavengames.com】*](http://wp.me/p6x8lb-ah)*。*