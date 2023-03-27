# 为什么会有这么多 JavaScript 框架？

> 原文：<https://medium.datadriveninvestor.com/why-are-there-so-many-javascript-frameworks-d5ecb525cda0?source=collection_archive---------7----------------------->

![](img/ef21be8eeb0bab1542542f0467c6a3ca.png)![](img/ebc404f446fda7bfe6f1f4fb3c3e27cd.png)

有很多 JS 框架。为什么有这么多，我们是怎么到这里的？它们之间有什么联系？

# 开始

JavaScript 是网景公司的 Brendan Eich 在 1995 年用 10 天时间创造出来的。最初它将基于 Scheme 或 Lisp，但在最后一刻采用了类似 Java 的语法(这是当时的热门新事物，Netscape 与拥有 Java 的 Sun 达成了协议)。其结果与 Java 毫无关系，但出于市场营销的原因，这个名字还是被取了下来。

1996 年，JS 被标准化为 ECMAScript。以及网景的 JavaScript，Macromedia/Adobe 有 ActionScript，微软有 JScript 和所有以不同的不兼容方式扩展的 JS。还有 [E4X](https://developer.mozilla.org/en-US/docs/Archive/Web/E4X/Processing_XML_with_E4X) 向 JS 添加了 XML 文字(现在已经死了，但是了解 React/JSX 的人会觉得很熟悉)。

[](https://www.datadriveninvestor.com/2019/01/17/the-technologies-poised-to-change-the-world-in-2019/) [## 准备在 2019 年改变世界的技术-数据驱动的投资者

### 很难想象一项技术会像去年的区块链一样受到如此多的关注，但是……

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/17/the-technologies-poised-to-change-the-world-in-2019/) 

这些大公司坐下来，就前进的道路达成了一致…开玩笑，他们没有，相反，他们花了接下来的十年为他们自己的版本而战。他们*终于*在 2009 年走到了一起，并就 ECMAScript 5 达成了一致。现在 [TC39](https://www.ecma-international.org/memento/tc39-rf-tg.htm) 每年 6 月商定标准，最近一次是 [ES2018](https://www.ecma-international.org/ecma-262/9.0/index.html) 。

我们将回头来看这些新的、快速发展的标准变得多么重要，但首先:当网络从学术工具变成每个家庭的实用工具时，JS 是一堆停滞不前的竞争版本。

# 第一次 JS 大战:平台

剧透:这场“战争”的赢家是 jQuery。

回到 21 世纪初，浏览器领域是一个很难开发的平台。没有模块，没有组件(除非你算上 [IE 的行为](https://msdn.microsoft.com/en-us/library/ms531079(v=vs.85).aspx?f=255&MSPPError=-2147217396))，不一致的 DOM，不一致的事件——任何丰富的交互都可能意味着 Flash(和 ActionScript)。

大多数开发人员想要两件基本的东西:

*   代码可移植性:在 IE、Netscape、Opera、Safari 等平台上运行的一致的 JS
*   组件:编写一次日期选择器，然后重用它。或者甚至使用别人现成的

这一时期的 JS 库将为开发人员提供一个标准的开发接口，并添加一组编写组件的约定。

代价是所有的标准化都需要大量的代码——加载多个框架很慢，而且大多数框架互不兼容。

只能有一个！

虽然有很多这样的框架(包括但不限于 [Script.aculo.us](https://script.aculo.us/) 、 [Prototype](http://prototypejs.org/) 、 [MooTools](https://mootools.net/) 、 [Dojo](https://dojotoolkit.org/) 、[下划线](http://underscorejs.org/)、 [Yahoo UI](https://yuilibrary.com/) 和 [jQuery](https://jquery.com/) )，但一旦其中一个占据了市场主导地位，并且大多数组件都依赖于它而不是其他任何一个，那么胜利就是板上钉钉的事情。

这是一个相当大的胜利，因为几年来 jQuery 是如此的普遍，以至于许多人把 jQuery 和 JS 视为一回事。但这并不是故事的全部…

# 建筑应用

jQuery 只是一个平台——一堆用于 DOM 操作和事件的标准工具。开发人员还想要其他东西:

*   构建整个应用程序的一致模式
*   具有数据绑定的可重用 HTML
*   路由和状态管理

jQuery 并没有真正帮助解决这些问题，但是很多其他框架做到了。

模板和数据绑定框架提供了一种重用 HTML 用户看到的。早期的例子有 [jQuery.tmpl](https://github.com/BorisMoore/jquery-tmpl) (后来的[jsRender](https://github.com/borismoore/jsrender))[车把](http://handlebarsjs.com/)和[小胡子](https://github.com/janl/mustache.js/)。

还有一些库框架，比如 Twitter 的 [Bootstrap](https://getbootstrap.com/) ，它提供了一堆基于 jQuery 的基本组件和一致的风格。随着时间的推移，很多都已经建立起来了，所以你可以将 jQuery 与 jsRender 和 Bootstrap 一起构建一个应用程序。

你要有 JS 代码来获得一个项目(比如你网站上的一个产品，叫做*模型*)，一个 JS 框架来呈现它(用 HTML 和数据绑定，叫做*视图*)，以及一些方法来把它们连接起来。可能是模型视图控制器(MVC)或者模型视图表示(MVP)或者……姑且称之为模型视图*什么的*，或者 MV*。你可以在 [Todo MVC](http://todomvc.com/) 中轻松地比较它们。

早期 MV*框架的例子有 [knockout.js](http://knockoutjs.com/) 和 [Backbone.js](http://backbonejs.org/) 。

统一整个方法的框架开始出现，例如 [AngularJS](https://angularjs.org/) 或 [Ember](https://www.emberjs.com/) 。

然后 Node.js 就发生了。

# JS 工具的时代

大多数 ide 和开发工具都是桌面应用程序，通常用 C++或 Java 之类的语言编写。每天在 JS 中工作的开发人员中有技能和时间编写桌面工具的人非常少。那里的大多数工具(如 Bridge.NET 的 [GWT](http://www.gwtproject.org/) 、T21 的[和 CoffeeScript 的](http://bridge.net/))都倾向于桌面到网络(分别将 Java、C#和 Ruby/Python 转换成 JS)。

Node.js 改变了这一切——突然间，整天写 js 的开发人员也可以轻松地用 JS 编写他们的工具了。这种可访问性意味着有大量新工具和新框架可以利用它们。

特别是，这些工具侵蚀了对*平台* JS 库的需求:你可以依靠 [Babel](https://babeljs.io/) 或 [TypeScript](https://www.typescriptlang.org/) 将你的代码转换成旧浏览器仍能运行的代码，而不是在 jQuery 之上编写(每个用户都需要一份 jQuery)。*打包程序 l* ike [Browserify](http://browserify.org/) 、 [WebPack](https://webpack.github.io/) 或 [RollupJS](https://rollupjs.org/) 可以打包并处理你的 JS 文件，只发送给你的用户他们所需要的，仅此而已。

可以说，这个时期的赢家是 [React](https://facebook.github.io/react/) 。React 在名为 [JSX](http://buildwithreact.com/tutorial/jsx) 的 HTML 和 JS 的嵌入式混合中提供了可重用的 HTML 和数据绑定，并使用基于节点的工具将其转换为普通 JS，该 JS 与名为*虚拟 DOM* (或 VDOM)的页面的极快副本一起工作。很容易就有一整篇博文深入细节，但是与旧的模板库相比，React 是*快*，用 JSX 写起来很容易。

这种方法的最新发展是像 [Stencil JS](https://stenciljs.com/) 这样的系统，其中*所有东西*都由 JS 构建工具编译成普通 JS，根本没有客户端框架。许多框架现在都包含了基于节点的命令行工具，用于构建最终的 JS。

最后， [npm](https://www.npmjs.com/) 和 [Bower](https://bower.io/) 出现了，方便下载和维护组件。不幸的是，它们实际上并不能帮助将文件放入你的 JS 应用程序，所以你需要一个模块导入器，比如 [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) 、 [SystemJS](https://github.com/systemjs/systemjs) 或 [CommonJS/RequireJS](http://requirejs.org/docs/commonjs.html) 来做这一点。

# 分叉、断裂和固执己见的框架

不需要所有的模块都依赖于一个单一的框架，并且大多数框架都有足够的组件库来生存，一个框架来统治所有模块的压力已经消失了。

在 MV*方面， [Angular 2](https://angular.io/) 进化利用了 TypeScript，但 [Aurelia](http://aurelia.io/) 在不同的方向上分裂出来(为 AngularJS 用户提供更多的直接升级)。

React 最初有一个有问题的许可，不是每个开发者都想依赖脸书的知识产权。它也相当固执*——它以自己的方式做一些事情(没有好坏之分，只是有点特殊),这意味着它并不总是与他人友好相处。使用相同 VDOM 理念的竞争对手出现了，如 [Preact](https://github.com/developit/preact) 、 [Inferno](https://github.com/infernojs/inferno) 和 [Vue.js](https://vuejs.org/) (Vue.js 也跳过了对 JSX 的依赖)。*

*React(和大多数 VDOM 框架)并不做所有的事情，所以与提供应用程序其余部分的其他框架结合，例如用于状态管理的 [Redux](https://redux.js.org/) 或用于反应事件的 [RxJS](https://rxjs-dev.firebaseapp.com/) 。*

*Bower 输掉了包经理的战斗，这很不幸，因为(虽然它更快)npm 是为桌面节点项目设计的。在 web 中，需要一个额外的步骤来展平和解析每个模块的单个版本。npm 不这么做，所以需要像 [Yarn](https://yarnpkg.com/) 这样的包装器。*

*甚至 Node.js 也破裂了，发明者瑞安·达尔离开并创建了 [Deno](https://www.youtube.com/watch?v=M3BM9TB-8yA) 。*

# *JS 的演变*

*在这一切发生的同时，IE 失去了市场主导地位，ECMA 僵局打破，JS 标准再次开始移动。竞争意味着浏览器需要变得更好以保持市场份额，这与 90 年代的浏览器大战不同(`<blink>` vs `<marquee>`有人知道吗？)这一次推动的是更快的 JS 和所有浏览器都能支持的特性(大部分)。新功能发布成为年度发布，并停止使用版本号，所以在 ES5 和 ES6 之后，我们切换到 ES2016、ES2017 等等。*

*这些特性改变了游戏规则:*

*谷歌开始推动这些功能(特别是 web 组件和 Shadow DOM)来帮助使用它们，并填补那些还不被支持的功能。其他 web 组件助手包括 [Skate.js](https://github.com/skatejs/skatejs) 。*

*VDOM 没有原生支持(可能永远不会)，但 React 的最新改进利用了新的异步功能，使其无缝快速。*

*文字字符串和 HTML 模板的组合允许一个类似 VDOM 的模型，即*是一些浏览器原生支持的。例子包括 [HyperHTML](https://github.com/WebReflection/hyperHTML) 和 [lit-html](https://github.com/Polymer/lit-html) 。**

# *移动的*

*移动是现在大多数人与互联网互动的方式。您的 web 应用程序在移动设备上运行良好变得越来越重要。*

*移动设备的连接时断时续，速度很慢，处理能力也差很多。JS 贵得不成比例。很长一段时间，本地移动应用被视为解决这一问题的唯一办法。2012 年，标准将是孤立的网络和本地移动体验。*

*解决这个问题的一个办法是像 [React Native](https://facebook.github.io/react-native/) 、 [Ionic](https://ionicframework.com/) 或 [Cordova](https://cordova.apache.org/) 这样的工具包，它可以让你将你的 JS 代码编译成原生应用。然而，并不是每个人都会安装你的应用。*

*AMP 是功能的最小子集。这是有限的，但保证加载速度很快。谷歌在搜索中优先考虑 AMP 结果，使其成为内容网站(如新闻)的一个好选择。*

*另一种选择是使用服务人员等新功能，逐步下载丰富的功能。渐进式网络应用程序(PWA)可以做几乎所有本地应用程序能做的事情，没有安装开销。你必须在设计应用时考虑到移动目标，使用 [PRPL 模式](https://developers.google.com/web/fundamentals/performance/prpl-pattern/)或类似的模式。*

*关于 PWA 的一个很好的例子，请查看 Twitter Lite 。*

# *我们现在在哪里？*

*之所以有这么多框架，是因为*可以有*这么多框架。JS 框架是专门化的、可移植的，并且通常是可互换的。不要担心选择了错误的框架——你总是可以(而且几乎肯定会)在以后改变它。门柱在移动，2009 年的市场与 2019 年大不相同。*

*应该学习哪些框架？你想要多少就有多少；只要确保你理解了底层的 JS。例如，如果你使用 React 来了解 VDOM 是如何工作的，了解 JSX 会发生什么，以及这种方法有什么妥协/好处。学习底层机制并不总是能帮助你更快地完成项目或使项目更好，但它总会让你在未来变得更有能力。*

**原载于 2019 年 5 月 21 日*[*https://www.evolutionjobs.com*](https://www.evolutionjobs.com/uk/media/why-are-there-so-many-javascript-frameworks-188799/)*。**