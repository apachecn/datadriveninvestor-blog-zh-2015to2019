# 来说说经验吧

> 原文：<https://medium.datadriveninvestor.com/lets-talk-experience-90fd03b3b54f?source=collection_archive---------22----------------------->

## 或者为什么对每件事都知道一点点比对一件事知道很多要好

![](img/5ca98f810d29106fdee81e656e98b315.png)

by [Artem Sapegin](https://unsplash.com/@sapegin?utm_source=medium&utm_medium=referral) from [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你曾经在寻找一份编程工作，我敢打赌你已经看过很多要求“X 年 Y 框架经验”的广告。我甚至还没有谈到某个框架或技术几年前才出现，而招聘人员要求有 5 年以上的经验的情况(不幸的是，这种情况并不少见)。让我们考虑一些相对合理的经验需求，并弄清楚要求某种特定工具的经验有多大意义。

# 情况

为了描绘一幅更加丰富多彩的画面，我们将想象我们想要构建一个新的软件产品，并且在进行一些分析之后，我们决定将平台 A 作为我们的主要开发工具。太好了！那么，我们现在需要什么？当然是一些开发者。是的，但是我们对他们有什么要求呢？显然，首先想到的是，他们必须对您选择的平台有一定的经验。对吗？不一定。啊？让我想想。

# 需要考虑的事情

首先，我们不否认使用一个特定的平台通常需要了解一些定义其运行方式的特定规则。例如，如果您必须编写一个 Node.js 程序，您需要了解事件循环的工作方式，如果您没有至少一些关于监督器和监督树的基本知识，您将无法创建一个像样的 Erlang 应用程序。然而，一旦你知道了关键的概念，剩下的大部分就是习惯的问题了，这不一定需要几年的时间去养成。想想帕累托原则:使用某个特定工具的 80%效果来自于它的 20%特性，其中大部分是一些主要的概念和规则。

接下来，这不仅很奇怪，而且非常矛盾:通常花费多年时间使用特定的工具或技术并不意味着跟上它的最新发展。相反，正如他们所说的:你可以设计一个应用程序，并在一段时间内维护它，而不用升级它所基于的平台的版本。结果，五年过去了，你肯定获得了多年的平台经验，唯一的问题是它不再是同一个平台:你甚至有可能很难阅读使用新版本工具编写的程序([比较一些 ES5 代码与 ES6 aka ES2015](https://codeburst.io/es5-vs-es6-with-example-code-9901fa0136fc) ，这只是一个版本的差异)。当然，工具越年轻就越不稳定，但是即使是成熟的平台(包括专有平台)也不容易从一个主要版本到另一个版本发生根本性的变化。

如果这些理由对你来说还不够，想想那些以一个平台开始，然后不得不将开发切换到另一个平台的公司。这里有一个简短的列表给你，所以你不必谷歌它:

*   Twitter: [从 Ruby on Rails 到主要基于 JVM 的语言(Java / Scala)](https://techcrunch.com/2008/05/01/twitter-said-to-be-abandoning-ruby-on-rails/) ，
*   Groupon: [再次将他们的后端从 RoR(抱歉，Rails，我还是有点爱你)切换到 Node.js](https://siliconangle.com/2013/11/11/how-groupon-web-traffic-moves-from-legacy-ruby-on-rails-to-node-js/) ，
*   Pinterest: [切换客户端模板渲染反应](https://medium.com/@Pinterest_Engineering/how-we-switched-our-template-rendering-engine-to-react-a799a3d540b0)，
*   AirBnB: [frontend 从 Prototype.js 到 Backbone.js 反应](https://www.slideshare.net/spikebrehm/the-evolution-of-airbnbs-frontend)，
*   沃尔玛:[从 Java 和服务器端渲染转移到 Node.js 和 React](https://www.informationweek.com/devops/programming-languages/walmart-agility-enabled-with-reactjs-nodejs/d/d-id/1328676) ，
*   诸如此类。

现在，我并不是说您一定会遇到这些公司所面临的相同的性能/可伸缩性相关的问题，(尽管，谁知道呢，让我们保持信心)，然而这个列表只是冰山一角:数以千计的其他(较小的)软件项目不得不在这个或那个点上依赖于他们选择的开发语言或平台。所以，请想一想:如果有一天你不得不做出类似的决定，你是希望你的开发人员拥有特定于该工具的经验，还是成为多面手？虽然以主平台或编程语言为中心会让你损失很多钱，但因此而改变整个开发团队的需求很容易对你的企业造成致命影响，尤其是如果它是一家初创企业。

# 结论

那么，我想说什么呢？那段经历不重要？如果我们谈论的是业内的一般经验的话，确实如此。然而，更不重要的是对特定产品的体验:这仅仅是因为将更广泛的知识应用于特定领域比概括某个工具的一些通常很窄的限制更容易，以便解决边缘情况和预测可能的问题。

是否意味着你应该只雇佣高级开发人员？绝对不是，因为如果你这样做了，你可能在试图建立决策的结构(也称为层次结构)时会有困难:一群经验水平相对平等的高级开发人员可能会花几天时间争论谁的设计建议更好，即使有人说思想在冲突中茁壮成长，但它更经常地在途中死去。所以，找一个你可以信任的高级开发人员做设计决策，找一些初级/中级开发人员在实现方面支持他。并确保提供足够的咖啡。😃