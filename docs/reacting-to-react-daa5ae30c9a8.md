# 反应来反应去

> 原文：<https://medium.datadriveninvestor.com/reacting-to-react-daa5ae30c9a8?source=collection_archive---------54----------------------->

![](img/413d1c674b23d12d1f6d0a0713871447.png)

大约一个月前，我开始学习 JavaScript，三周后，我投身于 React，致力于创建一个简单的待办事项应用程序。在开始之前，我已经阅读了使用 React 的所有利弊；它很快，单向数据流使调试更有效，VirtualDOM 允许更快更灵敏的更新，但最大的缺点似乎是它有一个陡峭的学习曲线。因为我对编程相当陌生，而且这是我尝试的第一个框架/库，我觉得我无法准确估计 React 比其他框架更难掌握还是更难掌握，但我可以说这可能是我迄今为止尝试过的最令人沮丧的努力。

澄清一下，我认为 React 有潜力成为一个真正有用的工具，我只是需要先掌握它的窍门。现在我不会写我对 React 的看法，但我想谈谈为什么 React 的前几周让我如此沮丧(可能还有很多其他人)。React 实际上是蛋糕上的一团花哨的绒毛。它可以使构建和使用您的程序更有吸引力，更快，并最终成为一项巨大的资产，但同时，它可能看起来非常复杂和令人生畏，即使最终它都是基于您已经知道的概念构建的。这是我学习反应的大部分问题开始的地方。我陷入了混乱，忘记了在这一切之下，我本质上仍然在做 JavaScript。

我昨晚才意识到这一点。我正在为我的应用程序添加一个删除按钮，允许用户删除个人待办事项。我已经和一个技术代理在 Bloc 前端 Slack 频道上工作了一段时间，当我最终说“我认为我错过了一些基本的东西，因为我不明白这些东西在做什么。”代理回复说暂时忘记 React，专注于 JavaScript，你会用 JavaScript 做什么？这是我想出来的。

> delete todo(index){
> const todoDelete = this . state . todos . filter((todos，i) = > i！==指数)；this . setstate({ todos:todoDelete })；
> }

为了删除选定的待办事项，我需要创建一个过滤器，将我的“待办事项”数组与选定的“待办事项”进行比较，并返回与选定事项不匹配的所有内容。过滤器传递某些参数，并构造返回 true 的元素的新数组。一旦我用这些术语来看待它，它就不再是一个我认为我不理解的可怕的反应，它只是一个简单的过滤方法，我以前已经做过几百次了。然后我要做的就是设置状态，这样 React 就会用我们的新数组更新 UI。这种特殊情况的语法如下所示:

> this . setstate({组件中最初设置的状态:新的筛选列表})；

关于 React，我还有很多需要学习的地方，但是最好记住，感觉受到威胁比概念本身的实际难度更大。

— MxOliver