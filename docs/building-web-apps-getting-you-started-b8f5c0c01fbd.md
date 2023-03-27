# 构建 Web 应用程序:入门指南

> 原文：<https://medium.datadriveninvestor.com/building-web-apps-getting-you-started-b8f5c0c01fbd?source=collection_archive---------17----------------------->

![](img/09447935d4c829ce6e55d709bd598b51.png)

> 互联网是为每个人服务的。很高兴记住这一点。

web 开发入门时的难易程度是相对的。有些人很容易进入，有些人不会。这是一个精选的列表，列出了当你开始做一名前端 web 开发人员时应该做或知道的事情。几年前没有人告诉我这些事情，但是在投入之前知道这些真的很有帮助。

# 从网页开始:

## 1.超文本标记语言

不要直接尝试构建成熟的应用程序。一步一步来。

如果你是一名前端 web 开发人员，首先培养你的 HTML 和 CSS 技能是很重要的。这是必然的。所以从网页开始，用一些基本的 HTML 标签:

```
<!--divisions-->
<div>This is a logical division</div>
<span>This is a span element</span> <!--Headings--> 
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6><!--Headings stop at h6--> <!--Paragraphs-->
<p>This is a paragraph</p><!--Image-->
<img src="https://link-to-my-image" alt="alternative text"/>
```

这些是一些简单的标签。下面是一个 HTML 页面的基本结构(例如 learning.html)

```
<!DOCTYPE html>
<html>
    <head>
        <title>Title of my HTML page</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <p>This is my first paragraph</p>
    </body>
</html>
```

不知道 meta 标签是什么意思也没关系，随着时间的推移你会明白的。

还有一点，记住一些标签而不是全部是没问题的。如果你忘记了，网上有很多资源可以帮助你。学习[语义代码](https://www.lifewire.com/why-use-semantic-html-3468271)也是非常重要的。

## 2.半铸钢ˌ钢性铸铁(Cast Semi-Steel)

HTML 描述了网页的结构，基本上是网页的组成部分，而 CSS 有助于设计风格。使用 CSS，你可以调整字体大小，颜色，背景图片，图片大小等。CSS 也允许你做一些形式的动画(不要太投入，不要分心。关注价格。你很快就会熟悉它的。

您可以在 HTML 文件头中添加对 CSS 文件(例如 style.css)的引用，如下所示:

```
<!DOCTYPE html> 
<html> 
   <head> 
       <title>Title of my HTML page</title> 
       <meta charset="utf-8"> 
       <meta name="viewport" content="width=device-width, initial-scale=1"> 
       <link href="style.css" rel="stylesheet" />
   </head> 
   <body> 
       <p>This is my first paragraph</p> 
   </body> 
</html>
```

使用 CSS，我们可以将段落的颜色改为蓝色，

```
p{
   color: blue;
}
```

网上有帮助 HTML 和 CSS 的资源。

# 每当你陷入困境时就问:

刚开始，在某些领域停滞不前是绝对正常的。试着向谷歌“请教”答案。很有可能有人经历过你正在经历的事情，并找到了解决办法。如果这不起作用，请访问文档来源，如 [W3Schools](https://www.w3schools.com/) 或 [MDN](https://developer.mozilla.org/en-US/) 。

# 参加课程:

这一点非常重要。当你学习网络开发课程时，你学得更快，而且你学习的方法是正确的。在这些课程中，你会有项目。在那里，您将构建第一个真正的 web 应用程序。你可以在 [Udacity](https://udacity.com/) 、 [Pluralsight](https://app.pluralsight.com/) 、 [Treehouse](https://treehouse.com/) 、 [Udemy](https://udemy.com/) 或 [Lynda](https://lynda.com/) 上课。

# 学习 JavaScript:

Javascript 是万维网的三大核心技术之一。有很多基于 Javascript 的框架，适用于 web、移动甚至桌面。我的建议是，在采用这些框架或库之前，先把 Javascript 作为一种语言来学习。我在我的 [GitHub](https://github.com/AdoraNwodo/javascript-fundamentals) 上创建了一个存储库，在那里我分享了从初学者到高级水平的不同 javascript 概念的代码片段。网上也有很多资源可以帮助你学习 JavaScript。

# 在下载 bootstrap 或 materialize 之前了解 css:

这很诱人。我们都想节省时间，所以我们依靠这些顶级 CSS 框架来帮助处理诸如响应和基本修复之类的事情。事实是，如果你在没有真正了解基础知识的情况下就直接进入这些框架，那么这些框架真的会让人不知所措。所以，在使用这个你从网上读到的或者你的朋友告诉你的流行框架之前，先学习 CSS，创建一些样式表并自己设计一些样式。

# 下载引导程序和 Javascript 框架:

我不只是迷惑了你。框架非常好。他们让我们的生活变得更加轻松。唯一重要的是，在使用框架之前，我们理解了这些 web 技术的基础。

# 了解软件架构模式:

这并没有听起来那么难。它只是一个帮助你编写好的、可伸缩的和可维护的代码的框架。相信我，如果你学会并把它们应用到你的项目中，你会成为老板的。

# 使用好的文本编辑器:

有大量的文本编辑器和工具，我推荐几个。微软 VS 代码，Atom，JetBrains 开发工具，括号等。好的开发工具提供智能感知，在编码过程中帮助你，防止你犯大量的错误。

# 结交有助于你成长的新朋友:

这一点也很重要。我们和周围的人一样优秀。时刻想着成长，充满热情。向那些你知道开始时和你一样，现在做得更好的人伸出援手。你会学到新的东西，如果你想不断提高，你会达到的。

如果你喜欢这篇文章，请鼓掌。

*这篇文章最初出现在我的博客上，* [*Adora Hack*](https://adorahack.com)