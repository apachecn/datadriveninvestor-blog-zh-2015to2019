# Heroku CI 并行测试运行采用最佳测试套件分割——如何运行并行 dynos

> 原文：<https://medium.datadriveninvestor.com/heroku-ci-parallel-test-runs-done-with-optimal-test-suite-split-how-to-run-parallel-dynos-79903d9a0ec6?source=collection_archive---------17----------------------->

Heroku 为团队提供了现成的 CI 解决方案。他们可以在 dyno 实例中为您的项目运行测试。更有趣的是，您可以将并行 dynos 作为 CI 构建的一部分来运行。这允许您在并行 dynos 上分割测试，以更快地完成 CI 构建并节省时间。

![](img/c56cfcff51c8209fc946ca89a99f04f5.png)

Heroku 对每个 dyno 的运行时间收费。这意味着，您可以将测试套件拆分到多个 dyno 上，而不是在单个 dyno 上运行您的慢速测试套件，并支付或多或少相同的费用，从而显著减少项目的 CI 构建时间。

# 如何从 Heroku CI 开始

如果您或您的公司已经在 Heroku 创建了一个团队，那么您可以使用 Heroku CI 并在那里为您的项目运行测试。

在 Heroku，你可以为你的一个项目打开你的团队和特定的管道。您会发现有一个*测试*选项卡，您可以在其中启用 Heroku CI。

您还需要在项目的存储库中保存一个 *app.json* 文件。该文件包含在 Heroku 上运行项目所需的信息。我们将在 *app.json* 文件中添加 Heroku CI 所需的额外配置。

为了使用 Heroku CI 并行测试运行，我们需要启用它。您必须请求 Heroku 支持人员为您的项目激活它。这个特性允许为您的 CI 构建运行多达 32 个并行 dynos。

您还可以观看更详细的视频中的所有步骤，或者从本文中复制一些示例。

下面我将向你展示如何在 Heroku CI 上为 Ruby 和 JavaScript 项目分割测试的例子。

# 如何在 Ruby on Rails 项目中为测试套件运行并行 dynos

我们可以动态地将 RSpec、Minitest 或其他测试运行程序中编写的 Ruby 测试拆分到并行的 dyno 上，所有的 dyno 将在相似的时间完成工作，这样我们就可以尽快得到测试套件是绿色还是红色的结果。为此，我们将使用[backpack Pro](https://knapsackpro.com/?utm_source=medium&utm_medium=blog_post&utm_campaign=how-to-run-parallel-dynos-on-heroku-ci-to-complete-tests-faster)工具及其[队列模式进行动态测试套件分割](https://youtu.be/hUEB1XDKEFY)。使用 *quantity* 键，我们可以设置想要使用多少个并行 dynos 来运行我们的*脚本测试*命令。

```
{
  "environments": {
    "test": {
      "formation": {
        "test": {
          "quantity": 2
        }
      },
      "addons": [
        "heroku-postgresql"
      ],
      "scripts": {
        "test": "bundle exec rake knapsack_pro:rspec"
      },
      "env": {
        "KNAPSACK_PRO_TEST_SUITE_TOKEN_RSPEC": "rspec-token"
      }
    }
  }
}
```

我们还可以为我们的 CI 构建更改 dyno 大小。如果您运行需要更多 CPU 或内存的复杂测试，您可以向 *app.json* 添加 *size* 参数来定义 [dyno 类型](https://devcenter.heroku.com/articles/dyno-types)。

```
{
  "environments": {
    "test": {
      "formation": {
        "test": {
          "quantity": 1,
          "size": "performance-l"
        }
      }
   }
}
```

# 针对赛普拉斯 E2E 测试套件，在并行 Heroku CI dynos 上运行 JavaScript 测试

端到端测试(E2E)通常需要很多时间，因为点击网站的多个场景非常耗时。在多个 dynos 上拆分 Cypress 测试套件将帮助我们节省大量时间，并保持 CI 快速构建。

我们可以使用[@ backpackage-pro/cypress](https://github.com/KnapsackPro/knapsack-pro-cypress)项目。它使用[背包 Pro 队列模式](https://knapsackpro.com/?utm_source=medium&utm_medium=blog_post&utm_campaign=how-to-run-parallel-dynos-on-heroku-ci-to-complete-tests-faster)。

这是你的 *app.json* 的配置

```
{
  "environments": {
    "test": {
      "formation": {
        "test": {
          "quantity": 2
        }
      },
      "addons": [
        "heroku-postgresql"
      ],
      "scripts": {
        "test": "$(npm bin)/knapsack-pro-cypress"
      },
      "env": {
        "KNAPSACK_PRO_TEST_SUITE_TOKEN_CYPRESS": "example"
      }
    }
  }
}
```

如果你想了解更多关于 Cypress 的知识，那么查看一篇文章中的视频[在并行 CI 节点上用 Cypress 运行 javascript E2E 测试](https://docs.knapsackpro.com/2018/run-javascript-e2e-tests-faster-with-cypress-on-parallel-ci-nodes)。

# 摘要

赫罗库词是赫罗库的一大补充。如果你已经使用 Heroku，你可以很容易地利用 dynos 并保持 CI 的低成本，因为你只需为 dyno 的使用付费。最棒的是，您可以使用测试套件的子集运行许多并行 CI dynos，从而为您的工程团队节省大量时间。您可以了解更多关于[backpack Pro 如何通过更快的 CI 构建帮助您节省时间](https://knapsackpro.com/?utm_source=medium&utm_medium=blog_post&utm_campaign=how-to-run-parallel-dynos-on-heroku-ci-to-complete-tests-faster)。

*原载于*[*docs.knapsackpro.com*](https://docs.knapsackpro.com/2018/how-to-run-parallel-dynos-on-heroku-ci-to-complete-tests-faster)*。*