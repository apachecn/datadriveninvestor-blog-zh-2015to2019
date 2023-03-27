# 通过滚动自己的来理解 JavaScript 中的 Array.map()

> 原文：<https://medium.datadriveninvestor.com/understand-array-map-in-javascript-by-rolling-your-own-842d6031f168?source=collection_archive---------0----------------------->

[![](img/ba7696b27ecda370a97a895b4f353a8c.png)](http://www.track.datadriveninvestor.com/181206BYellow)![](img/bd4b0a4a211c42967eceed673e2b520a.png)

Photo by [Muhammad Haikal Sjukri](https://unsplash.com/@pantiumforce?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> *本文是向新开发人员介绍在没有框架或任何其他“魔法”的情况下用 JavaScript 构建 web 应用程序的系列文章的一部分。* [*你可以在这里找到该系列的所有文章。*](https://medium.com/@tindleaj)

JavaScript 中的`Array.map()`函数是初涉函数式编程领域的初学者的常见绊脚石。在花费大量时间学习了 JavaScript 中所有不同类型的循环的来龙去脉之后，理解`map`的概念似乎很陌生。这篇文章将作为一个一般性的介绍，并且(希望)对于那些还没有接触过函数式编程的人来说，是进入强大的函数式编程世界的一个门户。如果你对深入探究 JavaScript 中的函数式编程感兴趣，一定要看看 Kyle Simpson 的[Functional Light JavaScript](https://github.com/getify/Functional-Light-JS)。如果你正在寻找一些简短、实用、切题的东西，请继续读下去。

# `Map`、`Maps`和`Mapping`

`Map`(不要与数据结构混淆，[‘Map’](https://en.wikipedia.org/wiki/Hash_table))是一个函数实用程序，我们可以用它来迭代一个数组，对每个值应用某种更改，并返回一个包含更改后的值的新数组。更一般地说，`mapping`只是一个值到另一个值的转换。如果我将数字`10`加上`5`，我就将值`10`映射到了`15`。对保存在一个列表(数组)中的所有值都这样做并返回一个新的列表将被认为是对列表的映射。

[](http://go.datadriveninvestor.com/BCL2019/matf) [## 2019 年最值得学习的编码语言——数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

go.datadriveninvestor.com](http://go.datadriveninvestor.com/BCL2019/matf) 

让我们来看一个代码示例:

```
const arrayToMapOver = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; function timesFive(value) { 
    return value * 5 
} const newArray = arrayToMapOver.map(timesFive);// newArray is now [5, 10, 15, 20, 25, 30, 35, 40, 45, 50] 
// arrayToMapOver is still [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

在这个例子中，我们从一组数字`1`到`10`开始。然后我们定义一个函数`timesFive()`，它接受一个`value`，并返回乘以 5 的值。接下来，我们采用在所有 JavaScript 数组上都可用的`Array.map()`方法，并使用它将`timesFive()`应用于绑定到变量`arrayToMapOver`的数组中包含的每个值。最后，我们将`map`方法的输出(也是一个数组)绑定到名为`newArray`的变量。

# 关于不变性的一句话

重要的是要注意，即使我们对包含在`arrayToMapOver`数组中的每个值都进行了`mapping`处理，原始值都没有改变。这与函数式编程的主要支柱之一“不变性”是一致的。不变性有点超出了本文的范围，但基本上它指的是数据不应该变异或改变的思想。相反，当我们需要修改现有数据时，我们应该以新的形式重新构建数据。在我们的例子中，我们不改变`arrayToMapOver`中的值，而是将`timesFive()`返回的值存储在`newArray`中。

# 滚动我们自己的`Map`功能

解释`map`的概念是一回事，但这是一个实用的介绍，所以让我们试着建立自己的。首先，我们需要定义函数的结构:

```
function ourMap(transformation, inputArray) {
    // our map function logic will go here 
};
```

我们来分析一下。我们的 map 函数不会作为方法附加到任何数组上，所以它需要两个参数:`transformation`和`inputArray`。`transformation`将是我们应用于第二个参数`inputArray`中每个值的函数。定义了函数签名后，让我们给我们的`map`添加一些逻辑:

```
function ourMap(transformation, inputArray) {
    // bind an empty array to a variable to hold our transformed
    // values 

    let outputArray = [];     return outputArray 
};
```

完美。我们将变量`outputArray`绑定到一个空数组，这样我们最终可以存储我们的输出值。我们还抢先返回了那个输出数组。它现在是空的，但我们很快就会有时间去填满它。出于个人喜好，我使用了`let`关键字来绑定`outputArray`，而不是`const`。这样做的唯一原因是`outputArray`必然会被修改(添加)，所以将其声明为`const`没有多大意义。

现在开始下一件事:

```
function ourMap(transformation, inputArray) {
    // bind an empty array to a variable to hold our transformed   
    // values     let outputArray = [];     // loop over the input array     for (let value of inputArray) {
       // apply our transformation here 
    }     return outputArray 
};
```

等等什么？一个`for loop`？我以为这是函数式编程？

# 为胜利而抽象

函数式编程的一个主要目的是为经常使用的功能提供抽象，以便让开发人员更清楚地理解代码。理论上，这种抽象简化了代码库，从长远来看更容易维护。但是，当你深入了解它时，任何在计算机上运行的代码在某种程度上都是由基本操作组成的，[包括](https://youtu.be/ecIWPzGEbFc?t=3431) `[assignment](https://youtu.be/ecIWPzGEbFc?t=3431)` [语句、](https://youtu.be/ecIWPzGEbFc?t=3431) `[if](https://youtu.be/ecIWPzGEbFc?t=3431)` [语句和](https://youtu.be/ecIWPzGEbFc?t=3431) `[loops](https://youtu.be/ecIWPzGEbFc?t=3431)`。函数式程序也不例外。

现在是最后一部分:

```
function ourMap(transformation, inputArray) {
    // bind an empty array to a variable to hold our transformed 
    // values 

    let outputArray = []; 

    // loop over the input array     for (let value of inputArray) { 
        // apply our transformation here         let transformedValue = transformation(value)         // put the transformed value in our outputArray outputArray.push(transformedValue) 
    }    return outputArray 
};
```

这里，我们简单地通过前面添加的便利的`for loop`获取`inputArray`中的每个值，并应用`transformation`参数(这是一个函数)。然后，我们将那个`transformedValue`放入我们的`outputArray`中。很快，我们成功了。`ourMap`的最后一行返回我们的`outputArray`,包含我们所有转换后的值。如果我们用`ourMap`实现替换之前的`Array.map()`方法，它应该完全一样:

```
function ourMap(transformation, inputArray) {
    // bind an empty array to a variable to hold our transformed 
    // values     let outputArray = []; 

    // loop over the input array     for (let value of inputArray) {
        // apply our transformation here         let transformedValue = transformation(value)         // put the transformed value in our outputArray outputArray.push(transformedValue) 
    }return outputArray 
}; const arrayToMapOver = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; function timesFive(value) { 
    return value * 5 
} const newArray = ourMap(timesFive, arrayToMapOver); // newArray is still [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]!
```

> 注意:“map”的这个实现并不完美，为了简单起见，您在“Array.map()”中所期望的一些 edge 功能已经被省略了。

就是这样！希望实现我们自己的`map`函数有助于真正了解`mapping`是如何工作的。如果你觉得这篇文章有用或有启发性，请考虑分享它。另外，如果你有兴趣看看函数式编程概念的其他实现，一定要看看 [Ramda 库](https://ramdajs.com/)。

感谢阅读。

*原载于 2018 年 12 月 11 日* [*tndl.io*](https://tndl.io/blog/understand-array-map/) *。*