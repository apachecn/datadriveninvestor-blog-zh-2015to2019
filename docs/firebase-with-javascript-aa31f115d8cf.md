# 使用 Firebase 和 Javascript 构建应用程序

> 原文：<https://medium.datadriveninvestor.com/firebase-with-javascript-aa31f115d8cf?source=collection_archive---------4----------------------->

![](img/7f2909eb29195479ed4c642f41ef6c45.png)

Firebase 提供实时数据库、网络存储、认证等。在这篇博客中，我将解释如何使用 firebase 实时数据库来读写数据。为此，我们将创建一个简单的板球运动员列表应用程序来添加球员的详细信息，并在屏幕上显示详细信息。该应用程序在[故障](https://lucky-sea.glitch.me/)中运行。

> 我们去做一些吧！

**设置环境！**

1.  进入 [firebase 控制台](https://console.firebase.google.com)并添加新项目。
2.  选择 web 应用程序。
3.  复制该片段并将其粘贴到您的 HTML 文件中。
4.  转到“数据库”选项卡，打开“规则”选项卡，将“写入和读取”属性中的“假”更改为“真”。因此，可以在没有身份验证的情况下访问数据库。

第一步:创建一个简单的前端

创建姓名和角色输入标签，用于输入板球运动员的序号、姓名和角色。然后，一个 div 标记显示板球运动员的编号、姓名和角色

**第二:写入数据**

单击“添加”按钮后，输入标记中的数据必须写入数据库。

在上面的代码中，输入标签值存储在变量中，并被推入数据库。推送后，数据将会是这样的，

![](img/fe8fd32585b76b8bfbbe810e861fb32c.png)

**第 3:读取数据**

在这种情况下，将从数据库中读取数据，并使用 HTML 显示它。

在上面的代码中，一旦数据库中有值，就会开始读取数据，并且将检索到的值追加到 HTML 中可用的 div 标签中。

> 呜呜呜。博雅！

在明天的博客中，我将向你展示如何更新和删除。如果可能的话，会在 firebase 展示更多精彩的东西。不要错过那些！

[谷歌开发者](https://medium.com/u/991272e72e68?source=post_page-----aa31f115d8cf--------------------------------) [谷歌云](https://medium.com/u/4f3f4ee0f977?source=post_page-----aa31f115d8cf--------------------------------)

[](https://medium.com/@dineshsmart101.dm/build-an-app-using-firebase-and-javascript-e01d36c05ef2) [## 使用 Firebase 和 Javascript 构建应用程序—第 2 部分

### 昨天我写了一篇关于如何从 firebase 数据库读写数据的博客。在这篇博客中，我将…

medium.com](https://medium.com/@dineshsmart101.dm/build-an-app-using-firebase-and-javascript-e01d36c05ef2) 

第四天。那 1 博客，明天见！