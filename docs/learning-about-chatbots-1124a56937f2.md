# 了解聊天机器人

> 原文：<https://medium.datadriveninvestor.com/learning-about-chatbots-1124a56937f2?source=collection_archive---------37----------------------->

![](img/94243ab195d71be8224eb29cf3c56fa6.png)

Photo by [rawpixel](https://unsplash.com/@rawpixel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

数据科学中最有趣的话题之一是自然语言处理，它让我感到困惑。想想计算机和几行代码如何能够计算和处理语言的复杂性是很有趣的。

聊天机器人是我觉得非常有趣的技术之一。当你打电话给信用卡公司、在线零售商询问商店地址，或者通过 [***多林戈***](https://www.duolingo.com/) (一款利用聊天机器人的交互质量来帮助人们学习新语言的应用程序)学习一门新语言时，许多人都熟悉自动响应，聊天机器人是一种通过提供高效和有效的响应来提升客户服务和提高用户参与度的好方法。

在一次 meetup 活动中，我通过谷歌的 dialog flow 学习了一种快速简单的创建聊天机器人的方法。通过创造各种意图，聊天机器人将能够理解用户所说的上下文。将实体添加到意图中，聊天机器人提取信息。

[](https://dialogflow.com/) [## 对话流

### 对话式用户体验平台。

dialogflow.com](https://dialogflow.com/) 

例如，使用实体，如果客户要求聊天机器人订购一件红色的小衬衫，机器人将理解动作词是“订单”，并且订单已被指定为颜色“红色”和尺寸“小号”。使用这种技术，人们可以通过预设各种意图和响应来制作一个快速而简单的聊天机器人，并且该聊天机器人可以很容易地集成到一个网站上。Dialogflow 利用谷歌的机器学习来理解文本和语音的上下文，其能力已经过数千个语音和文本样本的训练。

构建一个现成的聊天机器人是高效和有效的，然而，我很想知道我是否能够仅使用特定的语料库来构建一个聊天机器人，其中机器学习过程的全部知识完全基于一个来源。利用我最喜欢的 90 年代的情景喜剧，我试图只根据《宋飞正传》的剧本来建立一个聊天机器人训练。你可以阅读下面的博客:

[](https://towardsdatascience.com/seinfeld-with-tf-idf-a-blog-about-nothing-1732abcfd773) [## 宋飞与 TF-IDF:一个什么都没有的博客

### 在为我的班级项目分析 OKCupid 约会简介一周后，我想做一些有趣的事情，同时仍然…

towardsdatascience.com](https://towardsdatascience.com/seinfeld-with-tf-idf-a-blog-about-nothing-1732abcfd773) [](https://towardsdatascience.com/seinfeld-with-neural-network-a-blog-about-nothing-part-2-50ac642c705f) [## 宋飞与神经网络:一个关于虚无的博客(第二部分)

### 继续我科学研究所有数据的旅程，我终于进入了深度学习和人工智能的世界

towardsdatascience.com](https://towardsdatascience.com/seinfeld-with-neural-network-a-blog-about-nothing-part-2-50ac642c705f) 

这是我对 NLP 着迷的延续，包括我之前发布的与节目 Seinfeld 相关的博客，我想看看我是否能够建立一个只懂杰瑞·宋飞语言的聊天机器人，并以 Jerry 在节目中做出的相同方式做出回应。只用了几行代码，这个机器人还有很大的改进空间。

请随时查看我的 Github，获取这个实验的代码。

[](https://github.com/catherhuang/seinfeld_chatbot/tree/master) [## 凯瑟黄/宋飞 _ 聊天机器人

### 聊天机器人。在 GitHub 上创建一个帐户，为 catherhuang/seinfeld_chatbot 开发做出贡献。

github.com](https://github.com/catherhuang/seinfeld_chatbot/tree/master) 

因为这是一个初始阶段，所以创建聊天机器人的过程非常简单。从预处理开始，用语料库的其余部分来拟合输入文本。代码能够从提供的脚本中生成响应。尽管这是一个粗略版本的聊天机器人，我将继续完善代码，以获得更好的交互体验。