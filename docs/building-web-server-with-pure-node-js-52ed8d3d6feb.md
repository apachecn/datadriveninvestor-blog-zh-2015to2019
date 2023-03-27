# 用 pure Node.js 构建 web 服务器

> 原文：<https://medium.datadriveninvestor.com/building-web-server-with-pure-node-js-52ed8d3d6feb?source=collection_archive---------2----------------------->

Node.js 构建 web 服务器应用有很多框架。下面我补充几个最知名的。

[](https://expressjs.com/) [## Express — Node.js web 应用程序框架

### Express 是一个最小且灵活的 Node.js web 应用程序框架，它为 web 和…

expressjs.com](https://expressjs.com/)  [## KOA——node . js 的下一代 web 框架

### Koa 是由 Express 背后的团队设计的一个新的 web 框架，它的目标是成为一个更小、更有表现力、更…

koajs.com](https://koajs.com/) [](https://hapijs.com/) [## 哈皮网

### 编辑描述

hapijs.com](https://hapijs.com/) 

然而，如果我们不想使用它们中的任何一个呢？我们可以使用 pure Node.js 构建一个 web 服务器，当然，这些框架让我们的生活变得更加轻松。就我个人而言，我经常主要使用 Express framework，但从现在起我将尽可能使用纯 Node.js API，特别是对于小项目:)这只是因为这些框架给我们的项目添加了许多依赖，所以它导致了巨大的 **node_modules** 。

![](img/760a28e7084ad98760f19f9c7fc4f204.png)

node_modules becomes really huge in projects if you use many frameworks and libraries

通过使用内置模块，可以同样轻松地构建简单的 web 应用程序或服务器，使我们的应用程序更加轻量级，更易于管理/维护。

如果你习惯于阅读代码胜于文字，这里有一个在 Node.js 上构建的没有任何框架的简单 web 服务器应用程序[你也可以从这个链接在 GitHub 上查看。](https://github.com/hcoz/pure-nodejs-web-server)

```
const http = require('http');/** handle GET request */function getHandler(req, res, reqUrl) {res.writeHead(200);res.write('GET parameters: ' + reqUrl.searchParams);res.end();}/** handle POST request */function postHandler(req, res, reqUrl) {req.setEncoding('utf8');req.on('data', (chunk) => {res.writeHead(200);res.write('POST parameters: ' + chunk);res.end();});}/** if there is no related function which handles the request, then show error message */function noResponse(req, res) {res.writeHead(404);res.write('Sorry, but we have no response..\n');res.end();}http.createServer((req, res) => {// create an object for all redirection optionsconst router = {'GET/retrieve-data': getHandler,'POST/send-data': postHandler,'default': noResponse};// parse the url by using WHATWG URL APIlet reqUrl = new URL(req.url, 'http://127.0.0.1/');// find the related function by searching "method + pathname" and run itlet redirectedFunc = router[req.method + reqUrl.pathname] || router['default'];redirectedFunc(req, res, reqUrl);}).listen(8080, () => {console.log('Server is running at [http://127.0.0.1:8080/');](http://127.0.0.1:8080/');)});
```

首先，我使用 Node.js 的 HTTP API 中的`createServer()`方法创建一个 HTTP 服务器，在它的请求监听器部分，我检测请求并重定向相关函数。

如你所见，我有三个功能，分别是`getHandler()`、`postHandler()`和`noResponse()`。他们正在处理相关的 URL 请求。URL 和函数对作为`{ method/url: function }`存储在`router`对象中。

然后，我使用 [WHATWG URL API](https://nodejs.org/api/url.html#url_the_whatwg_url_api) 解析 URL。其中一个原因是，我可以获得许多 URL 功能，如路径名、主机、来源等，我可以轻松处理，而无需费力的字符串操作。之后，我构造了请求键`req.method + reqUrl.pathname`,用于搜索相关函数。

最后，从`router`中找到相关的函数，通过传递`request`和`response`对象来调用它。如果对象中没有相关的函数，那么我调用默认的函数，在我们的例子中是`noResponse()`。

下面是我用 pure Node.js 创建一个简单 web 服务器的方法，在我看来，在没有任何框架的情况下从事技术工作，理解它的基础知识也很重要。

您可以阅读这个 [MDN 文档](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node_server_without_framework)来获得一个纯 Node.js 服务器的扩展示例。当然， [Node.js API](https://nodejs.org/api/) 是帮助你的最重要的文档！

此外，您可以查看我的语义命令行应用程序项目的[服务器端，了解 pure Node.js 服务器的更详细实现。另外，如果你想了解更多，请阅读我关于这个项目的文章。](https://github.com/hcoz/sem-cli-server)

**我的其他一些文章:** 1。 [Chrome Devtool 提示](https://medium.com/@hco/chrome-devtool-tips-48bd7c19e9c4)
2。使用 React Context API
3 创建多语言网站。[非常基础的云服务和 AWS](https://medium.com/datadriveninvestor/very-basics-of-cloud-services-and-aws-4bfa0cad6daa)
4。[一个带 Node.js 的语义命令行应用](https://medium.com/@hco/a-semantic-command-line-application-88ac785d31aa)