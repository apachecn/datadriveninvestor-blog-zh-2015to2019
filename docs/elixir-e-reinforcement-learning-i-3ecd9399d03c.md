# 灵丹妙药和强化学习— I

> 原文：<https://medium.datadriveninvestor.com/elixir-e-reinforcement-learning-i-3ecd9399d03c?source=collection_archive---------11----------------------->

## 这个想法是利用 Deep-Q 学习和 Elixir 建立一个虚拟的自动驾驶汽车。

![](img/402d1b40e1d22ed643b22968f3806f04.png)

## 为什么要强化学习？

我一直对强化学习很感兴趣。在看了关于 AlphaGo 的纪录片后，我决定了解这一切到底是如何工作的。在看了一些文章、书籍、博客之后，我在 [**Udemy**](https://www.udemy.com/aprendizagem-reforco-deep-learning-pytorch-python/) 上找到了一门关于在虚拟自动驾驶汽车中使用 Phyton[**py torch**](https://pytorch.org)进行深度强化学习的课程。所以我决定用 [**仙丹**](https://elixir-lang.org) 语言做一个类似的项目。

## 为什么是长生不老药？

想用 VM Erlang 玩机器学习已经有一段时间了。使用只有几个 ML 库的语言来重建项目看起来是一个挑战。

[](https://www.datadriveninvestor.com/2019/01/23/deep-learning-explained-in-7-steps/) [## 深度学习用 7 个步骤解释-更新|数据驱动的投资者

### 在深度学习的帮助下，自动驾驶汽车、Alexa、医学成像-小工具正在我们周围变得超级智能…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/deep-learning-explained-in-7-steps/) 

## 该项目

该项目包括开发一个独立的虚拟汽车，或看起来像汽车的东西，离开屏幕的左上角，到达屏幕的右下角。汽车将不得不自主行驶，面对各种障碍并从中学习，直到到达目标。

基本上，在强化学习中，我们有一个在环境中互动的代理，并通过奖励来定义达到目标的行动。通过这些奖励，代理“学习”尽可能快地达到目标的最佳行动和路径。

所以我们首先需要建立我们的环境。在参加了 ElixirConf 2018 上的 [**介绍 Scenic，一个功能性 UI 框架**](https://www.youtube.com/watch?v=1QNxLNMq3Uw) **，** Boyd Multerer 的演讲后，我决定使用 Scenic 来构建 GUI。我们需要制造一辆有 3 个传感器的汽车，它将把数据返回给代理人，代理人可以做出必要的决定来达到目标。然后我们需要为我们的车建造障碍和街道。

## 安装药剂

显然，我们需要安装 Elixir 和 VM Erlang。你可以在这里按照 [**的指示**](https://elixir-lang.org/install.html) 。

## 安装布景

在安装 Scenic 之前，我们需要安装一些预依赖项。这里的 [**的说明很详细**](https://github.com/boydm/scenic_new?#install-prerequisites) 。安装完成后，我们可以执行下面的命令来创建我们的`autonomous_car`项目。

```
mkdir autonomous_car
cd autonomous_car
mix archive.install hex scenic_new
mix scenic.new .
```

现在，随着项目的创建，我们需要编辑 mix.exs 文件并正确设置项目依赖项。

```
defp deps do
  [
    {:scenic, “~> 0.10”},
    {:scenic_driver_glfw, “~> 0.10”},
  ]
end
```

完成后，保存 mix.exs 文件并运行:

```
mix deps.get
mix scenic.run
```

该项目将被编译，并将打开一个带有 Scenic 和 glfw 版本的屏幕。

完美，风景是活的。现在我们需要画出我们的汽车和它的传感器。我们将在项目的下一部分这样做。

[下一集](https://medium.com/@marceloreichert/elixir-e-reinforcement-learning-ii-6e55f7e85cfa) …