# API 101:什么是 API？

> 原文：<https://medium.datadriveninvestor.com/api-101-what-even-is-an-api-bd4bba29b47e?source=collection_archive---------9----------------------->

![](img/14c415a0265b24f7d9fa0f66426182e6.png)

Sending a request to an API

API 到处都是，但它们实际上是什么呢？你如何创造一个？最佳实践是什么？

在接下来的几个月里，我将通过这个 API 系列来阐述这些东西。首先，让我们了解一下基本情况。

[](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) [## 雅虎财经 API |数据驱动投资者的 6 种替代方案

### 长期以来，雅虎金融 API 一直是许多数据驱动型投资者的可靠工具。许多人依赖于他们的…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) 

简单来说，API 就是客户端和服务器之间的接口。客户端向服务器发送数据请求。在后台，服务器获取请求的信息并做出响应。

数据可能来自各种地方。它可以是一个数据库、一个文件甚至是另一个 API。

所以 API 是允许客户端与服务器交互的东西。客户可以是任何东西。android 应用程序、网站、桌面应用程序或命令行程序。

这就是 API 如此有用的原因之一。当你实现 API 时，你必须指定契约(响应和请求的结构)，只要你遵守这个契约，谁将使用你的 API 并不重要。

这意味着您可能有一个与 API 交互的 web UI，但是没有什么可以阻止您以后实现应用程序。你的后端根本不需要改变。

API 的另一个强大的方面是客户端不关心服务器的实现。合同为王。服务器如何收集和存储契约指定的数据完全取决于后端的实现者。

![](img/14c415a0265b24f7d9fa0f66426182e6.png)

A client sends a request to a waiting server

![](img/759ea8f018e48b2f267d98082f9397c1.png)

The server fetches the data

![](img/c6521c95110a4d4f61329a7928b0efd4.png)

The server responds with the data according to the contract specified by the API

# 使它更加具体

让我们举一个经典待办事项清单的具体例子。假设我们想要为待办事项列表服务构建一个 API。也就是说我们需要详细说明合同。

首先，我们需要告诉客户端如何查询特定资源的 API。在这里，资源是特定数据的表示。在我们的例子中，待办事项列表可能是一种资源。

该请求可能如下所示:

```
GET https://todo.johanneandersen.me/todolist
```

这里的`GET`指定了发送哪种 HTTP 请求。稍后将详细介绍。`/todolist`指定了我们需要数据的资源。

然后，我们需要指定您期望得到的响应，可能是这样的:

```
{
	"id": integer,
	"items": [
		{
			"id": integer,
			"title": string,
			"created_datetime": dd-MM-YYYYT00:00:00,
			"completed": boolean,
			"completed_datetime": dd-MM-YYYYT00:00:00
		}
	]
}
```

所以作为一个想要查询 API 的程序员，当你向`[https://todo.johanneandersen.me/todolist](https://todo.johanneandersen.me/todolist)`发送 GET 请求时，你完全知道会发生什么

这只是皮毛，在接下来的文章中，我将深入探讨什么是 REST API 以及如何设计它。我们还将研究身份验证、授权和分页。在探索这些主题的过程中，我们将构建我们的待办事项 API。作为奖励，我还将研究 GraphQL 和 Postman 的提示和技巧。

感谢您的阅读，下次见！

下一篇文章→ [**API 101:设计超级 REST API**](https://medium.com/@JohanneA/api-101-designing-kick-ass-rest-apis-39e0027e1d3a)