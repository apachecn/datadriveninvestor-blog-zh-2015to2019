# haskell——纯粹的函数式语言！

> 原文：<https://medium.datadriveninvestor.com/haskell-the-purely-functional-lang-dc97b8b87a83?source=collection_archive---------2----------------------->

[![](img/60cff867829614c08d9c9ad9eb03b8d6.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/f6672d8364fa40b4504bdc8ec346a46a.png)

正如这篇文章的标题所示，Haskell 是一种纯粹的函数式编程语言，你可能知道也可能不知道，这表明它将所有的计算都视为数学函数的求值。相反，不是告诉计算机*做什么*，而是告诉它*什么数据是*。

Haskell 的独特性归因于以下特性:

懒惰 —表达式只在需要时才被计算，因此我们可以计算潜在的无限值。

*副作用* —在 Haskell 中，函数结果只依赖于它们的输入，因此函数没有副作用，但是这种能力用输入-输出(IO)类型表示，因为在某些时候，我们无论如何都需要改变状态。我们稍后将通过一个例子来更好地理解 IO 类型。

> [DDI 编辑推荐—学习路径:Haskell:函数式编程和 Haskell](http://go.datadriveninvestor.com/haskell1/matf)

*多态性*——通常指采取多种形式。数据类型可以是多态的，函数也是如此。`data Tree a = Leaf a | Node (Tree a) (Tree a)`。树是多态数据类型的一个例子，因为它可以是整数、字符串、字符或任何东西的树。函数`id :: a -> a`是多态的，因为它接受任何类型的输入并返回该值。

*简洁* — Haskell 具有高度的抽象性，并使用了许多高级概念。因此，用 Haskell 编写的程序往往更短，可读性更好，也更容易维护。

以下面的示例函数(pure 和 IO)为例，它们都返回一个大写的字符串。

*纯功能:*

```
capitalize :: String -> String
capitalize []       = []
capitalize (x : xs) = toUpper x ++ capitalize xs
```

纯函数的放大:

1.  **型签名**

`capitalize :: String -> String`表示大写函数接受一个字符串作为输入并返回一个字符串。在大多数情况下，声明类型签名并不是强制性的，因为 Haskell 能够执行 ***类型推断*** ，但建议将其作为一种良好的实践，因为这对于文档来说也是必要的。

**2。模式匹配**

```
capitalize []       
capitalize (x : xs)
```

`String`只是`[Char]`的语法糖，也就是说，一个字符串就是一个字符列表。列表数据类型有两个构造函数:`empty` case 和`cons` case，写成`data [] a = [] | a : [a]` ((x : xs)翻译成 x 为头，xs 为尾)。列表类型有两个可能的值，空列表和非空列表，因此我们有必要声明所有可能的返回值，因此是模式匹配。数据类型将在下一篇文章中详细阐述，所以现在不要太担心。

*模式匹配包括指定一些数据应该符合的模式，然后检查是否符合，并根据这些模式解构数据—*Miran lipo vaa

正如您所料，在一个空列表上调用一个像`capitalize`这样的函数会返回一个空列表，因为没有数据可以操作。同样的情况也被称为`edge condition`。

下一个案例迎合了实际的字符列表，在这种情况下，我们注意到了强大的`recursion`。

**3。递归**

`capitalize (x : xs) = toUpper x ++ **capitalize xs**`

如前所述，纯函数式语言是关于告诉计算机数据是什么，而不是如何达到某种结果；而递归对于实现这一点是非常重要和必要的。递归在这种情况下很重要的另一个原因是因为`toUpper`函数接受单个字符作为输入，并产生大写的字符。它的签名写为`toUpper :: Char -> Char`。

回想一下，对于`capitalize`函数，输入和输出都是字符列表，因此对一个字符执行`toUpper`是不够的，我们不能对整个字符串执行`toUpper`，因为这将产生类型错误！因此，在这种情况下，递归是我们的理想解决方案。我们将链表头 toUpper 的结果和递归调用的结果连接起来。

```
*Lib> capitalize “dee” 
“DEE”
```

上述函数调用被评估为:

```
capitalize “dee” 
== toUpper 'd' ++ capitalize “ee”
== 'D'         ++ capitalize “ee” 
== 'D'         ++ (toUpper 'e' ++ capitalize "e")
== 'D'         ++ ('E' ++ capitalize "e")
== 'D'         ++ ('E' ++ toUpper 'e' ++ capitalize [])
== 'D'         ++ ('E' ++ 'E' ++ [])
== 'D'         ++ "EE"
== "DEE"
```

如果我们希望递归函数终止，前面提到的边界条件非常重要。没有它，程序仍然可以编译，但是当调用`capitalize`函数时，会产生一个不吸引人的输出:

```
"DEE*** Exception: src/Lib.hs:12:1-47: Non-exhaustive patterns in function capitalize
```

*IO 功能:*

```
capitalize' :: *IO* [*Char*]
capitalize' = do
    str <- getLine
    return (map toUpper str)
```

大写的签名表明它属于类型`IO [Char]`或`IO String`，因此它返回一个`IO String`动作。我们使用`do block`捆绑多个 IO 操作。

`getLine`功能属于`IO String`类型，用于“拾取”输入。绑定`getLine`到`str`对于拆箱接收到的输入是必要的，也就是从 IO 字符串展开字符串。

地图功能有一个签名`(a -> b) -> [a] -> [b]`。据说 Haskell 函数只接受一个参数，但是从 map 函数的签名中，我们看到它至少接受两个参数:函数`(a -> b)`和变量`a`。现在说什么😕？矛盾吧？一会儿就清楚了。

揭开谜底:**高阶函数** (HOF)是将输入或输出作为一个函数的函数。属于 HOF 类的 Curried 函数是那些可以接受一个以上参数的函数。我们的`map`函数是一个典型的定制函数。让我们来看看如何。

我们可以将`map`的签名重写如下:`((a -> b) -> [a]) -> [b]`并将其称为部分应用的函数，这是一个采用我们遗漏的尽可能多的参数的函数。

*使用部分应用程序(调用参数太少的函数，如果你愿意的话)是一种快速创建函数的好方法，这样我们可以将它们传递给另一个函数，或者用一些数据播种它们*

当我们`map` `toUpper`处理一个字符串时，我们对字符串中的每个字符都应用了 toUpper。例如`map toUpper “dee”`返回`DEE`。但是`capitalize`的类型是`IO [Char]`；我们有了`[Char]`，我们如何附上`‘IO’`？。简单！`return`函数属于`a -> IO a`类型，表示 return 接受任何类型的变量，并将其作为 IO 操作返回。

能走到这一步真了不起！Haskell 很有趣，而且基本上是自动化的😉如你所见！开始学习 Haskell 可能会很困难，因为它纯粹是功能性的，但是正如你所知道的；熟能生巧。不要绝望！有足够的工具可以用来学习 Haskell，例如 [Hackage](https://hackage.haskell.org/) ，详尽的文档和中心包。[学你一个哈斯克尔就好了！Miran Lipovač也是一本适合初学者的好书。您也可以关注这个针对新手的 Haskell 系列文章，让我们一起学习一些概念。](http://learnyouahaskell.com/)