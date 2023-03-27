# Centro 的 ChatOps/ChatBot

> 原文：<https://medium.datadriveninvestor.com/chatops-chatbots-at-centro-b671ba8245da?source=collection_archive---------17----------------------->

![](img/4832508702bed547d39ea1c0b79e2a89.png)

“white robot action toy” by [Franck V.](https://unsplash.com/@franckinjapan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 PDX 的志愿者活动期间，我和一些对在他们的组织中进行聊天感兴趣的人聊了聊。这是我写了一半的博文并对其进行最后润色所需要的动力。

## 为什么是聊天机器人？

先涛公司的团队一直在考虑做一个聊天机器人，但老实说，我们无意中发现了它，这将解释我们在路上遇到的一系列问题。当我们构建 AWS 基础设施时，我们设想了一个基础设施运营站点，允许用户自助请求。聊天机器人似乎是一个新奇的副业。有一天，我们在讨论聊天机器人应该是什么样子。我提到了一个我关注了一段时间的工具，叫做 [StackStorm](https://stackstorm.com) 。StackStorm 将自己定位为“事件驱动的自动化”工具，其理念是基础设施中的事件可以触发自动化工作流。(自动补救有人吗？)根据团队之前在其他公司的经验，这个想法似乎很可靠。你总是会发现你有一些烦人的问题，需要时间来解决。该工具还有一个 ChatOps 组件，因为当你想到它时，聊天消息只是另一种类型的事件。

长话短说，我们的一个团队成员出于好奇在 StackStorm 上做了一个 spike，很快就有了一个功能正常的聊天机器人，可以接受命令并执行它们。我们用 StackStorm 为 Marvin(我们的聊天机器人)构建了几个命令，我们立刻就坠入了爱河。主要优势。

*   Slack 是一个你可以在任何地方使用的客户端。聊天机器人的自动化程度越高，你就越有自由在任何地方工作。
*   聊天机器人是一种训练工具。人们可以通过搜索历史来了解一个特定的动作是如何完成的。
*   聊天机器人(如果你允许的话)可以让你的开发者自我授权
*   统一上下文。(如果你允许的话)聊天机器人可以成为运营/开发/数据库管理员使用**相同的**工具完成工作的地方。有共同的痛苦，共同的责任，以及对系统运作方式的共同理解。部署到生产环境看起来与部署到测试环境一样。

一旦你尝到了自动化工作流的滋味，每一个请求都会被放在显微镜下用一个简单的问题来观察；“为什么是我**做这件事，而不是开发人员要求计算机做这件事”。**

## 聊天机器人设置

StackStorm 是我们聊天机器人部署的核心。该工具为我们提供了开始编写命令所需的一切。该项目附带了 Hubot，但是除非你遇到问题，否则你不需要了解 Hubot 本身。StackStorm 设置有一个 [chatops 教程](https://stackstorm.com/2015/06/08/enhanced-chatops-from-stackstorm/)来了解如何设置它的细节。

StackStorm 工具由您创建的各种工作流组成。它使用来自 [OpenStack 项目](https://www.openstack.org)的 [Mistral 工作流引擎](https://docs.openstack.org/mistral/latest/)。它允许您将各个步骤联系在一起，以创建一个更大的工作流。它还能够启动工作流的独立分支，创建一些并行执行功能。例如，如果您的工作流依赖于在两个独立的数据库中植入数据，那么您可以并行化这些任务，然后在这两个独立执行的任务完成后让工作流继续(或者用 StackStorm 的说法“join”)。它可以是一个强大的选择，同时也是一个痛苦的选择。但是我们将在后面的文章中对此进行更深入的探讨。

然后，工作流被连接到 StackStorm 操作，这允许您使用命令行工具或聊天机器人来执行它们。动作定义是一个 YAML 文件，看起来像

```
---
  name: "create"
  pack: platform
  runner_type: "mistral-v2"
  description: "Creates a Centro Platform environment"
  entry_point: "workflows/create.yaml"
  enabled: true
  parameters:
    environment:
      type: "string"
      required: true
      description: "The name of the environment"
    requested_version:
      type: "string"
      default: "latest"
      description: "The version of the platform to deploy"
```

工作流和操作通过“包”打包在 StackStorm 中。可以把它想象成 StackStorm 中为产品提供相关功能的一个包。对我们来说，我们围绕应用程序对包进行分组，并为我们在多个包中执行的操作提供一些共享库。上面的动作来自**平台**包，它控制我们的主平台环境的管理。通过 [StackStorm Exchange](https://exchange.stackstorm.org) 可以获得许多社区支持的包。

最后，为了使它成为一个聊天命令，我们定义了一个别名。别名标识聊天中的哪些消息将触发相关联的动作。

```
---
name: "create"
action_ref: "platform.create"
description: "Creates a Platform environment"
formats:
  - "create platform environment named {{ environment }}( with dataset {{ dataset }})?( with version {{ requested_version='latest' }})"
ack:
  format: "Creating platform environment {{ execution.parameters.environment }}"
  append_url: false

result:
  format: "Your requested workflow is complete."
```

别名的**格式**部分是一个稍微修改过的正则表达式。随着命令变得越来越复杂，可选参数越来越多，解析起来有时会有点困难。 *{{ environment }}* 符号表示将传递给相关动作的参数。您还可以通过赋值将该参数设置为默认值，如*{ { requested _ version = latest } }*。这意味着如果用户没有指定 requested_version，“latest”将作为该参数的值被传递。在正则表达式和默认参数之间，您可以对用户可以指定的参数进行很多控制。您也可以使用多种格式来触发同一操作。您可以看到 **action_ref** 行将调用什么操作。它在一个*包*里。*动作名称*格式。

## StackStorm 带来了很多东西

对于每个命令的设置来说，这可能看起来很多，但实际上有 StackStorm 作为这个抽象层是非常好的。因为 StackStorm 实际上是一个事件自动化工具，它以 3 种不同的方式公开了您创建的这些工作流。

1.  聊天机器人允许你通过聊天工具执行命令。Hubot 支持许多聊天工具，我相信这些工具也可以转化为 StackStorm 支持。
2.  您创建的包和动作可以通过 StackStorm run 命令手动执行。当出现空闲停机时，这是非常有用的。命令语法是`st2 run platform.create environment=testing requested_version=4.3`，就像在聊天中一样，可选参数将获得默认值。
3.  StackStorm 应用程序还提供 API 访问。这使您能够从任何其他应用程序调用工作流。当有人需要做用户可能通过聊天机器人自己做的完全相同的事情时，这是非常好的。共享上下文的事情又出现了。

## 你通过聊天机器人运行什么？

简单来说，尽我们所能。每当有人不止一次要求做某件事时，我们就开始问自己，“我们是在给这个过程增加价值，还是只是看门人？”如果我们没有增加价值，我们把它放在聊天命令中。我们有一些例子。

*   创造环境
*   恢复环境
*   拍摄环境的数据库快照
*   缩放自动缩放组中的节点
*   执行 Jenkins 构建作业
*   扩展 Jenkins 工作实例计数
*   运行迁移
*   暂停 Sidekiq
*   重启服务
*   部署代码
*   将环境置于维护模式
*   打开功能切换
*   从 Consul 获取配置值
*   在 Consul 中设置配置值

总之，我们的环境中有超过 100 个聊天命令。

## 但是安全呢

是的，安全是一个东西。像大多数与安全相关的事情一样，你需要采取分层的方法。我们使用 SSO 来认证 Slack，所以这是第一层。第二层在我们创建的工作流中提供。你必须推出自己的 [RBAC](https://en.wikipedia.org/wiki/Role-based_access_control) ，但是大多数组织都有某种目录服务用于群组管理。特别是对于 Slack，RBAC 的实现可能有点混乱。y 你作为每个消息事件的一部分得到的聊天机器人变量包括用户的**用户名**，用户可以改变它。所以你真的需要获取用户的令牌，用令牌查找用户的信息，以获得帐户的电子邮件地址，然后使用它在你的目录服务中查找组信息。

我们还确保危险操作具有其他带外工作流控制。例如，您不能仅仅将一个分支部署到生产环境中。您只能部署 GA YUM 存储库中的 RPM。为了获得 GA 存储库的包，您需要从一个发布分支进行构建。发布分支的工件被提升到 GA，但是只有在提升确认发布分支有一个 PR 被批准到 master 之后。这些种类的带外检查对于一些敏感的动作是至关重要的。

对于某些操作，也需要基于推送的双因素身份验证。基于推送的选项是首选，因为您不想通过聊天提交双因素代码，这在技术上需要 60-120 秒。我们目前正在做这件事，所以请留意下一篇文章。

最后，有些事情你不能通过聊天机器人来做。没有人可以通过聊天破坏生产中的某些资源。即使是 OPS 也必须为这些命令使用不同的工具。有时候风险太大了。

## 陷阱

我们遇到的聊天机器人的一些陷阱。

*   我们没有为命令家族定义一个通用的词汇。例如，一个部署在任何地方都应该有非常相似的命名。但是因为我们没有定义具体结构，所以有些命令是`create platform environment named demo01`，有些是`create api environment demo01`。简单的省略`name`会让那些需要在平台空间和 api 空间中操作的人出错。
*   Mistral 工作流是一个强大的工具，但它可能有点麻烦。工作流还使用轮询机制在步骤之间移动。(步骤 1 完成，但步骤 2 直到轮询间隔出现且系统检测到步骤 1 完成后才开始)因此，在繁重的操作过程中，您可能会浪费大量时间来完成步骤，但在它们继续之前等待轮询成功。
*   尽早与所有团队分享 StackStorm 工作流程。授权他们在过程的早期创建他们自己的命令，在工具被特殊的用例弄得乱七八糟之前，这会使你犹豫是否将这项工作推给其他团队。
*   尽早建立常用动作库。您可以通过创建自定义包来实现，这样您就可以从任何包中调用这些操作。
*   谨慎使用 mistral 工作流程。这只是 runner StackStorm 提供的命令类型之一。我认为首选的执行方法，尤其是对于大型工作流，是将大部分执行放在脚本中，这样操作就变成了执行脚本。Mistral 工具很好，但是当您开始执行许多不同的步骤时，它会变得非常冗长。

# 结论

我们对聊天机器人的实现非常满意。无论从哪方面来说，它都不完美，但它让我们在浪费的辛苦工作中省回了很多时间。StackStorm 帮了大忙。 [StackStorm Slack](https://stackstorm.slack.com) 是很多开发者出没的地方，他们很棒。如果你有问题，他们非常乐意卷起袖子帮你解决。

虽然不够深入，但我希望这篇简短的文章能够帮助那些正在进行聊天机器人之旅的人。如有任何问题，请随时[联系我，或者在这里发表评论。](https://twitter.com/darkandnerdy)