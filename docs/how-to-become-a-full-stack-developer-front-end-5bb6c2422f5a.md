# 如何成为全栈开发人员—前端

> 原文：<https://medium.datadriveninvestor.com/how-to-become-a-full-stack-developer-front-end-5bb6c2422f5a?source=collection_archive---------16----------------------->

[![](img/dc480a82a4487080ccc863f0600dedf1.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/74fd03e4a90b11fe1bb9cbd35a7e681a.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 内容

系列文章:

*   [简介](https://medium.com/datadriveninvestor/how-to-become-a-full-stack-developer-intro-8419c9aa342d)
*   第一部分— [HTML，CSS —可视化部分](https://medium.com/@antmihlin/how-to-become-a-full-stack-developer-html-369fb58cc221)
*   第 2 部分—前端开发
*   第 3 部分— [后端开发](https://medium.com/@antmihlin/how-to-become-a-full-stack-developer-backend-53c0330eaa64)

现在你知道如何使用 CSS 和 HTML 了。不如我们现在就开始编程吧！

正如在过去的文章中提到的，前端应用程序工作在客户端(网络浏览器)。大多数网页都使用三种基本技术。HTML 是一种结构，CSS-styles，JS interactive。

本文将对 Javascript 进行概述。

## 向页面添加 javascript

Js 将所有的动态添加到网页中。例如动画、事件和许多许多其他东西。

Javascript 通过以下方式与 HTML 交互:

标签事件:

```
<button onClick="alert('Thank you for clicking')" >Click me!</button>
```

在结束 body 标记之前插入脚本:

```
<body>
 ...
  <script>
    alert('The script is working.');
  </script>
</body>
```

或外部文件:

```
<body>
 ...
  <script src="some-external-file.js">
    alert('The script is working.');
  </script>
</body>
```

## **基础知识**

首先，walk JS 是一种编程语言。因此具有其他语言所具有的特征。此外，它还具有与 HTML 页面的交互。所有的 HTML 元素都是可读的，并且可以从 JS 获得。

基于原型继承范式的 Javascript。

> 所有的编程语言都有内置的数据结构，但是每种语言的数据结构都不一样。本文试图列出 JavaScript 中可用的内置数据结构，以及它们有哪些属性；这些可以用来构建其他数据结构。只要有可能，就与其他语言进行比较。检索自: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

六种基本数据类型:布尔、空、未定义、数字、字符串、符号。和反对。

更多关于这一点可以在这里 发现 [**。**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

## **功能元件**

```
// Comments
/*
   Or long comments
*/// Variables
var someVariable = 'data asssigned to variable';// Functions
function someFunction(){
  //Some actions here
}// Classes
class GoodClass {
  anyProperty = 'data asssigned to property';
  anyMethod(){
    //Any action
  }
}//Loops
for( var i of numbersArray ){
  //Repetative actions
}
```

## **文档对象模型**

所有的 HTML 元素都按照层次顺序存储在 DOM 中。

元素`<div id="orangeDog">Text</div>`可由`document.getElementById('orangeDog');`到达

例如，文本颜色可以这样改变`document.getElementById('orangeDog').style = 'red';`

这是最基本的。对于更深层次的知识，强烈推荐考虑 [**这本书**](http://javascript.info/) 包括习题。它从基础开始，逐步向您介绍 JavaScript。

## **成为一名优秀的前端开发人员需要什么？**

在完成这本书之后，你现在是一个前端开发人员。现在的问题是训练和实践。

从小页面开始。在第一阶段，你可以复制一些现有的网站或元素。

当你对 JS，HTML，CSS 有了一定的了解之后，你就可以进行更复杂的任务了。然后尝试在一些公司找到一份初级工作，或者为朋友或家人建立一个网站。职场有助于提升能力。

## 工作要求是什么？

通常，它看起来像:

*   HTML，CSS，JS(包括 ES6)，Jquery，Sass 或更少
*   前端框架之一:Angular，React
*   创建交互式、快速动态网页应用的网页开发技术
*   使用 Git 的经验
*   具有 Webpack、Gulp 或其他构建/捆绑 JS 应用程序所需工具的经验
*   Photoshop 基础
*   投资组合。甚至可能是很小的例子。

增加机会的技能:

*   单元测试
*   Wordpress 或其他流行的 CMS
*   对整个网络开发过程有很好的理解

## **库/框架**

[角度](https://angular.io/guide/quickstart)或[反应](https://reactjs.org/docs/getting-started.html) —最常用于单页应用。第二种是目前需求量最大的。

[Jquery](https://jquery.com/) —方便对元素、动画、AJAX 的操作

[Lodash](https://lodash.com/) —在 JS 中操作数据的有用函数

[Bootstrap](https://getbootstrap.com/docs/4.1/getting-started/introduction/) —带有样式的可重用 HTML 块

[字体牛逼](https://fontawesome.com/start) —图标库

## **有用的工具**

Chrome 开发工具——浏览器中的开发工具。

[Git](https://git-scm.com/) —代码版本控制

[NodeJs](https://nodejs.org/en/docs/) —基于 Javascript 的服务器。有许多有用的模块

NPM—NodeJs 模块的包管理器。

[吞咽](https://gulpjs.com/)或 [Webpack](https://webpack.js.org/) —打包并缩小代码。需要安装节点。

[Github](https://github.com/) —存储/分享你的代码，发现他人的源代码。

[Codepen](https://codepen.io) — HTML、CSS、JS 在线编辑器。