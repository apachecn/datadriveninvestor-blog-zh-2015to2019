# 算法时代与问题解决模式(上)

> 原文：<https://medium.datadriveninvestor.com/algorithms-era-and-problem-solving-patterns-part-1-d26e7450343b?source=collection_archive---------5----------------------->

![](img/eb0b6725dd3bd364ea12f4cafd456128.png)

对于新开发人员来说，解决问题是一个很大的挑战。我认为对大多数人来说，学习新的语法很容易。你学会了一种语言的语法，你就大功告成了。现在，你可以复制别人的代码或者按照一步一步的指示重新制作一个应用程序，但是最困难的事情是处理新的问题和新的挑战。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

不管技术如何(语言，平台..等等)你用。拥有强大的解决问题的技能真的很重要，这可以帮助你找到解决方案。面试中有很多关于算法的问题，所以我们关注面试中出现的问题。

# 目标

*   定义什么是算法
*   算法无处不在
*   设计一个解决算法的计划
*   讨论解决问题的模式“两个指针的问题”，“分而治之”，“频率计数器”

**注**

“我将这篇文章分为两部分，在第一部分，我们将更多地关注设计一个计划，一种解决问题的方法，在本文的下一部分，我们将关注解决问题的模式。让我们从定义算法开始”

什么是算法？

> 为完成某项任务而按特定顺序实施的一组步骤。

因此，简单来说，我们可以说，一个算法可以是一组数学步骤，我们需要去解决一个问题。例如，我们有这样一个问题“计算前 100 个质数？”。现在，我们必须采取一些措施来解决这个问题。

# 为什么我们关心算法

我们周围有一堆执行不同任务的算法。我们可以谈谈

*   *脸书的算法会在你的新闻提要上显示某些广告*
*   *谷歌的算法(用于文本搜索、语音搜索、根据输入过滤文档)*
*   *YouTube 算法(用于视频推荐和最热门视频)*
*   *自然语言处理(NLP)算法(生成书籍摘要，在 Twitter 上发布推文，提供文本自动完成，进行语音识别等)*
*   *寻找和选择路由器的网络算法*
*   *计算机视觉算法(用于人脸识别、二维码检测)*
*   *数据加密、解密和过滤算法。*

在编程中，无论我们是在做一个简单的任务还是构建一个复杂的应用程序，几乎我们做的每一件事都涉及某种算法。这是成为一个成功的问题解决者和开发者的基础

***我们逃不出算法*** 。那么，你如何在这方面做得更好呢？你知道，很多人认为这是人在解决问题时的好坏的本质。你可以说有些人天生更擅长解决问题，他们的思维可以解决问题，但这并不意味着我们变得没有希望，不去奋斗。

# 你是如何提高的？

这里有一个方法可以让你冷静地参加面试，并按照我在这里列出的一些步骤来解决问题。我已经提到了两件事

*1-设计一个解决问题的计划。所以，更多的是关于你如何解决问题，如何打破僵局。我会推荐几个步骤。*

*2-掌握常见问题解决模式。这是必要的，因为在面试中出现的许多问题可以分为不同的类别。如果你能确定其中的一些类别，那么你就可以采取一些步骤来编写代码。*

# 问题解决策略

这里有一个简单的方法，一套你可以记住的步骤，可以帮助你解决很多问题。是一个具体的东西一步一步的回头去参考。所以，这是步骤

**。理解问题**

**。探索具体的例子**

**。分解它**

**。解决或简化问题**

**。回顾并重新因子化**

# 理解问题

在你开始在船上打字或写作之前，后退一步，确保你理解了任务，这是非常重要的。所以，这里有一些我建议你问自己的问题。

*1-想法问题是基于什么，我可以用自己的话重述一下问题吗？2-进入问题的输入及其类型是什么？*

问题的解决方案应该产生什么样的预期结果？

我有足够的信息来解决问题吗？也就是说，你有输入，你能利用提供的信息得到预期的输出吗？5-在问题中，什么是重要的数据，我应该如何标记它们？

让我们应用这些步骤来解决一个简单的例子

写一个函数来检查左括号和右括号是否正确地嵌套在一个给定的字符串中，并返回一个布尔值

所以，假设有人在面试中问你这个问题。让我们一步步来解决这个问题。

请你用自己的话重述这个问题，我们可以说这是一个简单的功能

我想写一个函数，以正确的左右顺序确定一对括号。

**思考输入及其类型**

在我们的例子中，只有一个字符串类型的输入

**期望的输出是什么**

True 或 false(如果字符串包含正确的括号顺序，则返回 true，否则返回 false。)

**提供的信息是否足以解决问题**

在大多数情况下，这是真的，否则你可以问更多关于这个问题的问题，并澄清你的困惑。

**什么是重要的数据，我应该如何标记它们？**

假设我们的函数名是 checkNesting，那么我们将把 givenString 作为参数，把 true 或 false 作为我们返回的结果。

```
fun checkNesting (givenString:String):Boolean{
      return true/false
}
```

# 举一些具体的例子

最好举一些例子来帮助你理解这个问题。示例还提供了健全性检查，以明确您的解决方案是否可行。

*   *从简单的例子开始。*
*   *继续更复杂的例子。*
*   *举一些空输入的例子。*
*   *尝试一些输入无效的例子。*

我们将为上面讨论的函数做一些例子

**简单示例**

*   检查括号("()")true
*   检查括号("(())")true
*   检查括号("()()")true

**更复杂的**

*   检查括号("(a(b))") true
*   检查括号("(123+(321+125))") true

E **空输入**

*   检查括号("")为空

**无效输入**

*   检查括号("(()()")false
*   检查括号(")(")false

如果输入为空或数据类型无效(Int 类型、double 类型..等)我们返回 null/false。在做出具体的例子后，我们进入下一步，将问题分解成更小的块

# 分解问题

> “将您的方法、解决方案分解成几个您可以遵循的步骤”

现在，在我们开始输入代码之前，我喜欢把问题分解成更容易理解的小部分。我的意思是采取问题的实际步骤并写下来，这并不意味着写完整的伪代码，只是写一些注释作为你需要采取的步骤的指南。写下你的步骤会很有用，这样你就可以向面试官展示，这些是我将要遵循的步骤，尽管我实际上已经完成了其中的 50%。

*   明确写出您需要采取的步骤，只是解决方案的基本组件，而不是步骤的详细版本。
*   因此，这迫使你在编写代码之前思考你的代码，并有助于在实现它之前发现任何误解或概念上的问题。

```
fun checkNesting(s: String): Boolean? {
    //  left and right parentheses should be equal
    //  So we can approach this as a counting problem
    //  count number of left and right parenthesis
    //loop over String,for each character
      //if we see a left parenthesis then Increment counter
      //if we see a right parenthesis then decrement counter
    //If at the end the counter is nonzero, then we don’t have a      properly nested string
}
```

# **求解或简化**

> “解决一个问题，如果你不能解决一个更简单的问题”

如果我们上面执行的所有步骤进展顺利，那么我们就可以为我们的解决方案编写代码了。有时你还没有准备好解决整个问题。大约 80%的时候你可能感觉良好，但是可能会有一件事让你感到困惑，你不知道如何去做。可能有两件或三件事情导致了混乱。所以，这就是简化的来源。这意味着试着忽略让你很难受的部分，以便把注意力集中在其他事情上。

*   *找到你正在尝试做的事情的核心难点*
*   *暂时忽略那个难度*
*   *写一个简化的解决方案*
*   专注于困难，尽量简化。

在我们上面写的解决括号问题的简单步骤中，我们并不关注左右括号的正确顺序。如果我们有一个字符串，像“)(”，它有相同数量的左括号和右括号，但顺序不正确，那么我们如何解决它？我们知道左括号在右括号之前，所以我们可以说，如果计数器变成负的，那么我们先有右括号。为了解决这个内部问题，我们可以这样写函数

```
fun checkNesting(s: String): Boolean? {
    //  left and right parentheses should be equal
    //  So we can approach this as a counting problem
    //  count number of left and right parenthesis
    //loop over String,for each character
      //if we see a left parenthesis then Increment counter
      //if we see a right parenthesis then Decrement counter
      //it’s not sufficient for counter to end at zero,it also has     to never be negative
      //if counter is negative then return false
    //If at the end the counter is nonzero, then we don’t have a properly nested string
}
```

现在，是时候将这些简单的步骤转换成实际的代码，使事情发生作用了。这是这个函数的实际实现。

```
fun checkNesting(givenString: String): Boolean {
    var count = 0
    for (i in 0 *until* givenString.length) {
        val ch = givenString[i]
        if (ch == '(') {
            ++count
        } else if (ch == ')') {
            --count
            if (count < 0) return false
        }
    }
    return count == 0
}
```

# 回顾过去，重新考虑

这是我们解决问题策略的最后一步。回顾你的代码，重构它或者只是分析它，是作为一个开发者学习和提高的最重要的事情。大多数时候，即使你是开发专家，也有重构代码的空间。查看其他人的解决方案并在您的代码中获得改进是非常有用的。这里有一些你可以问自己的问题。

*   你能检查结果吗？确保您的解决方案有效
*   你能改变结果吗？思考不同的方法
*   一眼就能看懂吗？当你在纸上、白板上或代码编辑器中查看时，你的解决方案有意义吗？
*   你能用这个方法解决其他问题吗？
*   你能提高代码的性能吗？
*   如果存在同样的问题，其他人是如何解决的？

所以上面的函数可以重构为

```
fun checkNesting(givenString: String): Boolean {
    var count = 0
    for (element in givenString) {
        if (element == '(') {
            ++count
        } else if (element == ')') {
            --count
            if (count < 0) return false
        }
    }
    return count == 0
}
```

这个函数可以进一步重构为

```
fun checkNesting(givenString: String): Boolean {
    var count = 0
    for (element in givenString) {
        when (element) {
            '(' -> ++count
            ')' -> {
                --count
                if (count < 0) return false
            }
        }
    }
    return count == 0
}
```

这些简单的步骤可以帮助您更好地理解技术问题，并让您有机会为问题提供更简洁和可靠的解决方案。