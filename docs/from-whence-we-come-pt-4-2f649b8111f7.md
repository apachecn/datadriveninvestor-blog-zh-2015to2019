# 我们从哪里来。四

> 原文：<https://medium.datadriveninvestor.com/from-whence-we-come-pt-4-2f649b8111f7?source=collection_archive---------5----------------------->

[![](img/07374afea3e40d6217fb01cbcc502c9f.png)](http://www.track.datadriveninvestor.com/1126A)

## 抓住榆树，驶向未来

![](img/e69aaea03ef8e5aec6d51167e60a833d.png)

Elm logo

web 是用 HTML、CSS 和 JavaScript 编写的。都是 2018 年 23 岁左右。当时最前沿的个人电脑技术有 32MB 的内存(孩子们，那是兆字节，相当于千兆字节的 1/1000)，还有一种叫做(让我看看我的笔记)通用串行总线(USB)的东西。

现在，七部《星球大战》电影之后，电脑变得更小、更快……并且仍然用 JavaScript 渲染网络。

也许是时候改变一下了。也许是能让速度更快的东西？多核处理器已经存在十多年了，JavaScript，这给了你什么想法吗？

> “我不断遇到的问题是如此愚蠢，”他说。“例如，试图将一幅图像放在一个框的中央，或者在多个网页上重复使用视觉元素是非常困难的。我开始痴迷于解决这些基础问题。”— [埃文·察普利茨基，2015 年](https://www.seas.harvard.edu/audiences/alumni/stories/2015/10/alumni-profile-evan-czaplicki-ab-12)

![](img/1380475e40842729f292f77e3d2d9d56.png)

Evan Czaplicki (from his Twitter page, [@czaplic](https://twitter.com/czaplic))

2012 年， [Evan Czaplicki](https://github.com/evancz) 写了一篇[的论文](https://elm-lang.org/assets/papers/concurrent-frp.pdf)，描述了并发函数式反应式编程(FRP)及其实现，以轻松创建响应性图形用户界面。他用一种编程语言实现了他关于并发 FRP 的想法，即纯功能(即由函数组成)图形界面设计，他称之为 [Elm](https://elm-lang.org/) 。

(Czaplicki [已经远离了 FRP](https://elm-lang.org/blog/farewell-to-frp) ，所以我在这里就不赘述它的特性了。)

六年来，Elm 已经发展到包括 Mac 和 Windows 的安装程序，一个 [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) ，一个将你的代码转换成 HTML 或 JavaScript 的编译器，以及一个[在线代码编辑器](https://ellie-app.com/)。

不过，了解内情的人似乎喜欢 Elm 有两个主要原因:

## [实践中无运行时错误](https://softwareengineering.stackexchange.com/questions/337295/what-is-the-benefit-of-having-no-runtime-exceptions-like-elm-claims)

错误可能会抛出一个“[结果](https://guide.elm-lang.org/error_handling/result.html)或者“[也许是](https://guide.elm-lang.org/error_handling/maybe.html)”(是的，真的)，但那些只是值；他们不一定会停止这个项目。你可以存储它们，你可以把它们收集到一个数组中，你可以在你想的时候把它们当作错误来处理。

Elmers(我不知道他们是不是这么称呼自己，但我现在肯定是这么称呼他们的)很快指出，这并不意味着“永远没有运行时错误”，这只是意味着避免了生产代码中可能未被发现的小错误，不像其他一些语言可能以“Java”开头，以“JavaScript”押韵。

## 可以想象的最有用的错误消息

[https://twitter.com/GregorySchier/status/732830868562182144](https://twitter.com/GregorySchier/status/732830868562182144)

Elm 是[静态类型的](https://stackoverflow.com/questions/1517582/what-is-the-difference-between-statically-typed-and-dynamically-typed-languages):变量的类型在编译时就知道了。在程序运行之前，你必须有话直说，有浮点运算。Elm 还支持类型注释，在这里您可以向编译器指定您的意图，如果您错过了一个输入错误或试图创建一个无限循环，编译器将会非常有用地明确指出哪里出错了，在哪里，以及它认为您正在尝试做什么。

所以！让我们看一些代码。

## 别人的六面骰子滚筒

抱歉，[埃迪的 6 面骰子滚动器](https://medium.com/datadriveninvestor/from-whence-we-come-97a375810d01)粉丝，但这不是我的代码，这只是我在[guide.elm-lang.org](https://guide.elm-lang.org/effects/random.html)找到的榆树随机函数的一个例子。

```
import Browser
import Html exposing (..)
import Html.Events exposing (..)
import Random

-- MAIN

main =
  Browser.element
    { init = init
    , update = update
    , subscriptions = subscriptions
    , view = view
    }

-- MODEL

type alias Model =
  { dieFace : Int
  }

init : () -> (Model, Cmd Msg)
init _ =
  ( Model 1
  , Cmd.none
  )

-- UPDATE

type Msg
  = Roll
  | NewFace Int

update : Msg -> Model -> (Model, Cmd Msg)
update msg model =
  case msg of
    Roll ->
      ( model
      , Random.generate NewFace (Random.int 1 6)
      )

    NewFace newFace ->
      ( Model newFace
      , Cmd.none
      )

-- SUBSCRIPTIONS

subscriptions : Model -> Sub Msg
subscriptions model =
  Sub.none

-- VIEW

view : Model -> Html Msg
view model =
  div []
    [ h1 [] [ text (String.fromInt model.dieFace) ]
    , button [ onClick Roll ] [ text "Roll" ]
    ] 
```

[你可以在这里用 Elm 的官方在线代码编辑器运行这段代码，包括必要的 HTML。](https://ellie-app.com/37gXN5G4T2sa1)

这里有一些事情引起了我的注意:

*   即使有括号，也很少。这就像 Czaplicki 先生小时候被一个 Lisp 编译器吓到了。但是没有，比如说，函数参数之间的描述大部分是用空格完成的。
*   它是以[模型-更新-视图](https://guide.elm-lang.org/architecture/)范式组织的。

> **型号** —您的应用程序的状态
> 
> **更新** —一种更新状态的方式
> 
> 查看——一种以 HTML 格式查看你的状态的方式

这对于任何经历过前四周的人来说都很熟悉，除了我们称之为模型-视图-控制器。不过，这是同一个领域模型，并且已经融入到语言中。来自 guide.elm-lang.org[的](https://guide.elm-lang.org/architecture/):

> 这种建筑似乎在榆树自然出现。早期的 Elm 程序员在他们的代码中不断发现相同的基本模式，而不是有人“发明”它。团队发现这对新开发人员来说特别好。代码最终证明是架构良好的。有点恐怖。

话虽如此，我发现很难解析。可能我只是习惯于 JavaScript，但是我不得不在代码和文档之间来回翻动，以弄清楚，例如，什么是保留字，什么是声明函数的名称。

那么榆树最好吗？至少是更好了吗？说到底，Elm 只是另一个工具。对于它被设计来做的工作来说，它是整洁和高效的，但前提是你花时间去学习它。显然，它不能做所有的事情:你可以建立一个在线聊天客户端，甚至可能是一个聊天机器人。但是即使你*可以*使用热胶枪而不是锤子，如果你在盖房子，你会需要一把锤子。

也就是说，你肯定能造出像[这种射线投射器](http://krisajenkins.github.io/elm-rays/)一样酷的东西。