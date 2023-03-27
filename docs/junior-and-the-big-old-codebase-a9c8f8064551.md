# Junior 和大的旧代码库

> 原文：<https://medium.datadriveninvestor.com/junior-and-the-big-old-codebase-a9c8f8064551?source=collection_archive---------4----------------------->

![](img/1fa84e419cc3a0b9f6f190e927c1919c.png)![](img/aea9c1fe2be05edc1337b8f1dd9fcc11.png)

Photo by [Tracy Adams](https://unsplash.com/photos/TEemXOpR3cQ?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

几个月前，大学毕业的我加入了 [Wix](https://www.wix.com/) 做前端开发。之前，作为一名学生，我在一家小型初创公司工作，并独自从头构建了大部分功能。我了解大部分流程，参与了大部分决策，基本上掌握了代码库和产品。

兴奋之余，我想在我的新职位**上开始写代码。然后，我发现我的新团队正在从事一个由 40 名程序员开发的历时 4 年的项目，拥有数百万活跃用户和超级复杂的用例。**

对我来说，最可怕的部分是，我将要工作的代码库是建立在两个巨大的核心项目之上的，以 AngularJS 作为主要框架。此外，这些与许多用 ReactJS 编写的迷你项目相结合，处理产品中不熟悉的部分。就连运行配置也和老的不一样了(npm vs. grunt)！

我心想，我怎么才能理解这个复杂的系统呢？!'我如何学习在本地运行每个项目？怎么考？在不了解产品及其边缘案例的情况下，我如何知道在哪里添加新代码或定位 bug 的来源？这太难了。

因此，在一段时间探索系统、犯错误和处理一些不同的案例和问题之后，以下是我发现对我有效的一些步骤:

**成为用户**

在为了修复一个错误或开发一个新特性而钻研代码之前，试着**成为一个用户！**首先，我试着从用户的角度使用这个系统。这样，我发现了产品的主要流程。只有到那时，我才能问我周围已经了解该产品的人一些“更聪明”的问题。

**找导师**

找一个伙伴，一个了解这个系统的导师。在 Wix，作为培训计划的一部分，我被分配给一个伙伴，这对我很好，尤其是在我的第一天。以下是一些要问的问题:

1.  **系统设计和结构** —请他们向您解释应用程序的高层结构。然后，试着识别系统的部件，它们是主要的组件，每个文件夹包含什么等等。我发现把它画出来，然后和我们刚刚提到的伙伴一起回顾它是很有用的。
2.  **系统中的方向** —询问他们如何在系统中找到特定的点。找到添加新代码的正确位置或定位 bug 源的常用方法是什么？
3.  **了解向谁询问什么** —了解你的团队，确保你知道每个问题需要向谁询问。从技术上来说，我发现“责怪饭桶”这个选项对我很有效。它告诉我，有人参与了这部分代码，应该知道如何回答我的问题(或者至少把我介绍给其他知道的人)。

![](img/1405246c3ec98c102ecbb44caa713ae9.png)

Photo by [Kobu Agency](https://unsplash.com/photos/7okkFhxrxNw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/mentor?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

**使用测试作为文档(或者——测试如何能让我避免产品中的错误？)**

在 Wix，我们实践 [TDD](https://en.wikipedia.org/wiki/Test-driven_development) 方法。作为一个新手，我发现测试文件是理解代码特定部分的极好资源。**为什么？**

1.  如果测试设计得好，它们将向我们介绍该地区的主流。例如，如果用户想要注册到您的系统，他们需要在浏览器中输入 URL，点击“注册”按钮，输入全名、电话、电子邮件和密码。然后，系统会保存他们的详细信息，他们就可以登录系统了。以“用户注册到系统”作为描述的 E2E 测试将向我展示所有的流程和这个流程中涉及的所有组件。
2.  你可以通过系统的单元测试来理解边缘案例(如果用户没有填写注册表单中的 email 字段会发生什么？).
3.  测试可以防止你破坏代码。当你试图修复一个 bug 或者写一些新的代码，但是你并不真正了解产品的所有用例，如果你没有被测试覆盖，你可能会犯一些错误。幸运的是，测试会失败，你会明白有些事情是错误的。对我来说，我发现这是信任我的代码的好方法。

**代码评审**

1.  我发现代码审查是识别隐藏功能和一些技术决策的最佳方式，这些决策在我加入之前就已经做出了。评审者可以根据他们的经验和对项目的熟悉程度向我介绍一些我遗漏的东西。
2.  代码评审对于初级评审人员来说也是很好的。要求参与其他人的代码评审，看看他们是怎么做的，学习标准等等。然后，给另一个初级或中级开发人员做代码评审。通过这种方式，您可以了解其他人的想法和编码实践，并对代码的不同部分更加熟悉。

**问。就问**。任何人，从开发人员到产品经理、营销或设计师。询问任何对产品或代码有所了解的人。不要羞于重复自己。再次问同样的问题是完全正常的。当你第一次开始的时候，要记住很多东西。反正对我来说，给自己写备忘录和笔记是有帮助的，不会忘记。

**这需要时间。让我们耐心点！祝你好运！**

## 来自 DDI 的相关故事:

[](https://medium.com/datadriveninvestor/deep-learning-explained-in-7-steps-9ae09471721a) [## 用 7 个步骤解释深度学习

### 和猫一起

medium.com](https://medium.com/datadriveninvestor/deep-learning-explained-in-7-steps-9ae09471721a) [](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4) [## 数据科学和软件工程哪个更有前途？

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

medium.com](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4)