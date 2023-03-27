# 让 vs Var，简单回答

> 原文：<https://medium.datadriveninvestor.com/let-vs-var-a-simple-answer-3cf8c941f4e4?source=collection_archive---------5----------------------->

JavaScript 中我一直难以理解的一个概念是`let` 和`var`的区别。它们都声明了一个保存某个值的变量。它们都可以在全局或局部范围内使用。它们都允许变量值被改变。有一天，我意识到我只是在编码时交替使用它们，而不是为了特定的目的选择一个。知道这种缺乏理解只会强化糟糕的编码习惯，我开始真正理解关键词`let` 和`var`。所以`let`要搞清楚到底是怎么回事！(原谅我的双关语。)

![](img/0cf3b0c20044309d87999c2d15901b64.png)

# 定义

[MDN 定义](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) `let` 和`var` 如下:

> ` let '允许您声明范围仅限于使用它的块、语句或表达式的变量。这与“var”关键字不同，后者全局定义变量，或局部定义整个函数的变量，而不考虑块范围。

基于这个定义，`let` 似乎比`var`有更有限或更明确的范围。由于作用域是`var` 是局部的，“不管块作用域”，所以会作用域到整个函数。所以`var` 的位置肯定没什么大不了的，因为如果我在范围内，我就是好的。当使用`let`时，我需要确保我在正确的块中声明了我打算使用的变量。我必须更仔细地编码。这仍然没有给我我正在寻找的完整的图片，就像告诉我什么时候使用一个而不是另一个。在代码示例中检查它们的不同行为将更全面地说明这一点。

# 提升

Var 提升是 JS 中的一个重要概念，基于 [JS 是一种编译语言](https://github.com/getify/You-Dont-Know-JS/blob/master/up%20%26%20going/ch3.md)的事实。它是一种快速编译的语言，但还是被编译了。就在运行之前，JS 引擎确保所有东西都在它的位置上。它看到你在程序中途使用了`var x = 2`，所以它在程序的顶部为你声明了`var x`。然而，当使用`let`时，提升似乎有点不同。我们可以看到这个简单代码的不同之处:

```
var x;
let y;console.log(x); // undefined
console.log(y); // undefined
```

我所做的只是声明了`x`和`y`，没有设置任何值。当在两者上使用`console.log()`时，它们返回`undefined`。这是有道理的。引擎发现，的确，我们有一个`x`和`y`变量，但是它们是`undefined`，因为我没有给它们任何值。现在我要移动`var x`:

```
let y;console.log(x); // undefined
console.log(y); // undefinedvar x;
```

有了这个改变，我甚至在声明之前就试图打印`x` ，这应该会引起一些问题。但是由于 var 的提升，一切都变得很好。在编译代码时，`x` 的声明被吊到程序的顶部。所以`console.log(x);`还是返回`undefined`。但是，当我用`let y`做同样的事情时会发生什么呢？

```
console.log(x); // undefined
console.log(y); // error!var x;
let y;
```

由于 var 提升，我仍然从`console.log(x);`得到`undefined` ，但是我从`console.log(y);`得到了一个大大的错误信息: `ReferenceError: y is not defined`。所以 var 吊装在`let`上确实不起作用。因为我没有按照正确的顺序写代码，引擎很生气。我应该在尝试使用变量`y`之前声明它。真为我感到羞耻！

在这个例子中，`let`的使用引入了一种严格模式。当我写了糟糕的代码时，引擎会找我麻烦。想象一下，一个程序有 1000 行长，有 10 倍多的变量。作为开发人员，在调试时看到一条`undefined` 消息或一条详细的错误消息会更有用吗？

# 添加值

看来`let`更加明确的范围实际上可能是有用的。我决定尝试另一个例子，这次给`x` 和`y`赋值。首先，我用`var`试了一下:

```
var x = 2;function add(){
 return x + y;
}
console.log(add()); // NaNvar y = 3;
```

为什么我得到了`NaN`的回应？`NaN` 表示“不是数字”，所以我的函数没有返回数值。

-我声明了变量`x`，并给了它一个值 2。
-我写了我的函数来添加`x`和`y`的值。
-我执行了`add()`函数，并用`console.log()`
将其返回值打印到控制台上-我的问题来了！我在调用函数`add()`后声明了`y`的值，所以它在知道 3 的值存在之前就运行了。

这个函数实际上返回了什么？它认为什么是“不是一个数字”？Var 提升本应开始发挥作用，将`var y`提升到程序的顶部，但在执行`add()`时被`undefined` 取消。所以函数其实返回了`2 + undefined`，肯定不是数字。我将把我的语句`var y = 3;`移到程序的顶部，一切都会正常运行。

如果我用`let` 代替，会发生什么？

```
let x = 2;function add(){
 return x + y;
}
console.log(add()); // error!let y = 3;
```

这次我得到了一个错误信息:`ReferenceError: y is not defined`。基于这些信息，我应该看看我的`y`变量在哪里。
-我在`add()`函数
中引用了-我的问题来了！我在调用了`add()`函数之后声明了`y`的值，所以在执行的时候没有定义`y`。

看到调试过程有多快了吗？因为我用了`let`而不是`var`，所以我得到了一个错误而不是`NaN`。详细的错误消息从一开始就为我指出了正确的方向，让我可以快速找到并修复代码中的问题。

当然，没有人应该或愿意编写这样的代码。每个人都知道不要在执行了一个函数之后，在使用它的地方声明一个变量和它的值。但是错误是会发生的！在巨型程序中，当多个开发人员一起进行更改时，代码放错位置是必然会发生的。这就是“调试”这个术语存在的原因。所以，就像我之前说的，您更愿意有一个消息`undefined` 或`NaN` 还是一个详细的错误消息？

# 我的结论

我最初带着这样一个问题着手这项调查，“什么时候我应该使用`let`而不是`var`？”我做了调研后的回答是“一直”。当然，你可以继续用`var`代替`let`；但是，您必须注意您正在声明的变量的范围，以及 JS 引擎将如何提升它。或者，你可以依靠`let` 而不是`var`。这确实迫使我格外小心地使用正确的位置和语法——但无论如何我都应该这样做。

在 ES6 中引入`let` 就像在 JS 中加入生活质量一样简单。使用`let` 鼓励你注意语法以避免出错。它还在调试时提供了更多有用的信息。使用`let` 而不是获得`undefined`，意味着我将获得一个详细的错误消息，比如`ReferenceError: x is not defined`。

我敢肯定，有许多人更喜欢`var` ，他们会说，“好吧，这就是`var` 的工作方式，所以处理它吧。”你可以。或者，你可以让你的代码在语法上更加甜美，并使用`let`。

# 资源

-[https://www . vojtechruzicka . com/JavaScript-raising-var-let-const-variables/](https://www.vojtechruzicka.com/javascript-hoisting-var-let-const-variables/)-[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)-
-[https://github . com/getify/You-Dont-Know-JS/blob/master/up % 20% 26% 20 going/up](https://github.com/getify/You-Dont-Know-JS/blob/master/up%20%26%20going/ch2.md)