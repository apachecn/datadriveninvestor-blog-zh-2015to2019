# 致系统架构师:如何更好地设计系统

> 原文：<https://medium.datadriveninvestor.com/to-system-architects-how-to-design-a-system-better-3625cbac7e09?source=collection_archive---------3----------------------->

![](img/2cf491e5287dee34b7b969ae4ce21ece.png)

*作者毕玄。*

作为一名[系统架构师](https://www.careerexplorer.com/careers/systems-architect/?spm=a2c41.13644021.0.0)，也拼写为 systems architect，我本人在阿里巴巴，我一直觉得教授系统设计实际上远比教授 [Java](https://www.java.com/en/) 编程技巧更难。事实上，我早就觉得一堂关于系统设计的课很容易变成一堂我们只讨论理论却得出令人失望的结果的课。

我经常听人说，即使是没有多少系统设计经验的人也可以很容易地教会如何设计一个系统，但这与事实相差甚远。但是因为这样的说法，我一直觉得做这方面的培训师有点泄气。然而，过去一年的一些情况给了我勇气在内部提供一个私人培训项目，结果很受欢迎。我认为我是从这个培训项目中获益最多的人:我组织了我的想法，从与受训者的互动中学到了很多，并且更好地抽象和总结了系统设计的方法论。可以说，系统设计的课程是我和我的学员共同创造的，给了我所有很好的反馈和输入。

我为系统设计培训设定了以下目标:

*   掌握概念框架，了解系统设计的套路。[系统设计](https://medium.com/the-andela-way/system-design-in-software-development-f360ce6fcbb9?spm=a2c41.13644021.0.0)——也称为系统设计或[系统架构](https://www.lix.polytechnique.fr/~golden/systems_architecture.html?spm=a2c41.13644021.0.0)——不仅仅是简单地绘制结构图的方框。你必须遵循一定的程序来更好地设计系统。
*   拓宽你的知识面。在系统设计中，你必须全面地考虑事物，以便更好地权衡利弊。因此，通过系统设计训练来拓宽你的知识面是很重要的。

为了实现这些目标，我将在授课前分析以下问题:

*   我想提出的概念框架是什么？
*   我怎样才能让受训者更好地掌握和使用概念框架，而不仅仅停留在理论上？

过去，我没有仔细考虑系统设计的概念框架。事实上，许多系统设计模板是一种概念框架，但是如果你不理解它们，它们就很难应用。在这篇博客中，我希望帮助你不要犯我过去犯过的同样的错误。

[](https://www.datadriveninvestor.com/2018/09/22/infographic-journey-to-the-clouds/) [## 信息图:云之旅|数据驱动的投资者

### 聪明的企业领导者了解利用云的价值。随着数据存储需求的增长，他们已经…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2018/09/22/infographic-journey-to-the-clouds/) 

# 系统设计程序

我回顾了我过去的系统设计，发现我最好的工作是在设计系统的整个过程中遵循一个常规。在这个过程中，我的思维过程和设计工作遵循以下顺序:

系统设计的目的>系统设计的目标>以目标为中心的核心设计>根据核心设计制定的设计原则>各子系统和模块的详细设计

# 系统设计的目的

系统设计的目的是为了系统设计的预期用途。在从事系统设计时，许多人不清楚他们为什么要设计一个新的系统，或者他们为什么要为一个现有的系统设计重构或进化。这不太好。漫无目的的系统设计可能导致一系列偏差，也可能导致与设计初衷和目的背道而驰的结果，例如，必须通过设计新系统或重组或升级现有系统来解决单一问题。当然，请记住，一个伟大的架构师应该能够向该领域中不同技能水平的人以及不同背景的人解释系统设计。只有在系统架构师理解并向团队的所有成员阐明系统设计的目的之后，团队才能更好地实现系统设计。

# 系统设计的目标

接下来，重要的是考虑基于系统设计目的制定可测量目标的可行性，以最小化最终系统实现和系统设计的原始目的之间的偏差。相信你们很多人可能会遇到最终系统实现与设计偏差很大的情况。这主要是因为实施系统的整个团队没有为系统设计制定可测量的目标，也没有在系统设计中体现这些目标。

# 目标为中心的核心设计

这一步涉及如何在设计过程中通过你的技术专长、视角、综合考虑，以及主观的权衡原则和你解决问题的思路来实现你的系统设计目标，这些都是形成最终核心设计的关键要素。在整体设计过程的核心过程中，您将制定新的目标来衡量您的设计的最终实现。您需要将这些目标添加到系统设计中，这样您就可以可视化最终实现和原始设计之间的偏差。

# 基于核心设计制定的设计原则

完成核心设计后，您可以制定设计原则，并确保这些原则在后续的子系统和模块的详细设计中得到遵守和反映。这样做可以使整个系统设计更加一致，集成性更好。

# 每个子系统和模块的详细设计

您会发现详细设计子系统和模块并不复杂，这是一项在前面的步骤之后缩小范围的任务，而不是重新设计主系统设计。程序员通常擅长解决问题，所以我认为良好的数学能力是程序员的首要要求，因为数学是一门典型的解决问题的学科。

其核心是，我关于如何让你掌握和应用系统设计的概念框架的想法是分享——在我阐述每个步骤的过程中——我过去在系统设计中的错误和实践经验。对我来说，我认为只有具有丰富实践经验的架构师才有能力提供系统设计方面的培训课程。

在整体流程的应用部分，这里采用的方法是让每个人按照同一个概念框架来阐述自己的体系，通过互动来相互对齐，让这种做法成为一种习惯。

在简要描述了每一步之后，我想详细说明前三步。

# 系统设计的逐步阐述

# 系统建设的目的

确定系统设计的目的是系统设计的第一步，也是最重要的一步。如果一开始就没有设定目标，你在接下来的步骤中肯定会出错。许多制度设计的一个典型问题是缺乏对制度建设的目的和意图的深入分析。

系统设计是设计一个新系统或对现有系统的体系结构进行重大改造或升级的过程，它服务于一个明确的目的。通过分析系统构建的目的，可以避免壁虎带来的问题。系统建设要体现服务层或系统用户层的挑战或问题，而不是满足你自己的个人需求。通过目的分析，您还可以确保在整个系统设计过程的后续步骤中实现目的。

通过分析系统建设的目的，你可以很容易地确定一个具体的模式和系统的深度，这是两个看似肤浅但实际上相当实际的概念，显示了你所做的一项工作的影响范围。影响可能涉及您所在的团队、部门、业务单位(BU)、业务团队(BG)、跨 BG 业务模块、整个团队，甚至您所属的社会。这里的准则是寻求事实背后的真相。也就是说，我不建议你沉迷于谈论理论而对系统设计束手无策。相反，我建议你让我们参与所有的设计。

从我早期开发[高速服务框架(HSF)](http://www.programmersought.com/article/7324712963/?spm=a2c41.13644021.0.0) 的经历中，我得出结论，我对系统建设缺乏明确的目的导致我犯了几个严重的错误。一个典型的错误发生在我为动态系统架构重组 HSF 的过程中。如果我当时分析了我努力的目的和意图，我会发现我的工作完全是出于我个人钻研技术的意图，而不是为了解决 HSF 用户面临的服务挑战或问题。我的这个错误与我之前谈到的整个过程开始时的问题有关。当许多技术工程师仅仅为了满足技术需求而开始进行重大的系统重组时，也会出现这种情况。我曾经接受过阿里巴巴一位高管的指导，他建议我在从事一项工作之前，一定要弄清楚这项工作的目的和原因。这帮助我认识到，在开始工作之前，通过清楚地了解动机，我可以摆脱许多复杂的技术细节。

由于我在 HSF 和阿里巴巴数据库开发方面的经验，我能够更好地理解我在开发阿里云的[容器服务](https://www.alibabacloud.com/product/container-service?spm=a2c41.13644021.0.0)，以及调度服务和主动[地理冗余](https://www.atlanticmetro.net/geo-redundancy-not-simple-think/?spm=a2c41.13644021.0.0)应用程序的后续工作的目的。与此同时，我也能够将我的工作定位于解决阿里巴巴服务挑战的需求。

在大多数情况下，系统设计的需求是由系统设计者之外的其他人提出的。也就是说，架构师应该能够将确定的需求转换为设计，也就是说，他需要知道是否根据需求或请求来构建新系统或重建或升级旧系统，并且他或她还需要能够理解系统构建的目的。只有这样，架构师才能向技术团队解释系统设计的动机，让他们理解系统设计的价值和意义。

我认为，在进行制度设计之前，我们需要明确分析制度建设的目的，以确保制度建设有价值和意义，并确保制度设计的目标能够实现。

# 系统建设的目标

在明确分析制度建设的目的后，我们需要将目的转化为一系列可衡量的目标，以确保最终实施的制度符合制度建设的目的。我相信你们中的许多人可能会遇到设计的系统和实现的系统之间的不一致，这是由于缺乏可测量的目标。

让我举两个例子:

*   2011 年，我的团队开始构建一个集装箱化的系统，以应对预期不断增长的服务器成本，目标是通过使用现有服务器的一半来支持相同的服务量。
*   2013 年，我的团队开始构建主动地理冗余系统，以提高服务的灾难恢复能力。后来，我们发现了主动地理冗余的更多好处，这些好处在最初的系统设计的构建目的中没有计划到。例如，主动地理冗余支持云资源的[弹性利用](https://www.michaeldiamond.com/understanding-leverage-elasticity/)，并加速基础设施技术的发展。在最初的设计阶段，我们设定的目标是在中国的多个地点(地点之间的距离大于 1 公里)部署服务，以承载流量，并在 30 秒内将流量从地点 A 切换到地点 B。

有了明确且可衡量的系统建设目标，我们可以:

*   以有针对性的方式将系统设计导向目标，避免偏差。

也就是你想建一个系统来监控系统建设效果。这是系统设计难题中最重要的一块，但却很容易被忽略。例如，我们展示了容器化集群中支持服务的服务器数量和支持的服务数量，我们还将这两个数字与未容器化集群中的数字进行了比较。我们还为主动地理冗余构建了一个控制系统，以显示系统部署状态和流量切换状态。我们只有通过建立一个系统来监控系统建设的目标是否达到，才能确保所构建的系统满足我们最初的动机。否则，我们可能在制度实施后与制度建设的目的背道而驰。因此，在系统建设过程中，必须建设监控系统。

基于目的制定目标的过程在理论上并不复杂，但容易被忽略，从而导致系统设计过程中的问题。关键是制定可衡量的目标，并建立一个系统来监测实现目标的进展情况。

# 与目标实现相关的核心问题

为了实现系统设计的可测量目标，我们需要确定核心问题，并通过系统设计解决这些问题。

我想根据我的经历来谈谈这个话题。

我们从一开始就有一个清晰的 HSF 开发目标，可测量的目标是一次支持大约数亿个服务调用。然而，由于我们当时有限的技术能力，我们提炼的核心问题与实际情况有很大差异，这导致我们不断重组和修改 HSF。因此，我永远不会相信一个技术能力差的人能成为一个好的建筑师，因为建筑师需要扎实的技术才能以理性的方式绘制出结构图的方框。

对于那些只关注盒子的人来说，绘画的过程表面上看起来很简单。在最初的 HSF 设计中，我们确定了如何实现一个用户友好和服务定义的[远程过程调用](https://searchapparchitecture.techtarget.com/definition/Remote-Procedure-Call-RPC) (RPC)框架的核心问题，但我们忽略了如何支持数亿次交互式调用的问题，以及服务化后服务研发中会出现哪些问题(如复杂的故障排除)&。例如，在 HSF 启动后才发现的中间负载平衡问题导致了 HSF 架构的重新设计，而这个问题本来应该由知识更广泛的架构师从一开始就发现。

事后看来，要实现 HSF 设计的目标，我们需要解决以下核心问题:

*   一个支持上亿服务交互的用户友好的 RPC 框架
*   服务间软件负载平衡
*   服务交互的故障排除

事后看来，我们在 T4(容器化)阶段制定了明确的目的和相关目标，并适当细化了问题，在此期间，我们解决了如何在一台服务器上运行 20 个应用程序的核心问题。T4 会议期间出现的大多数问题都与核心问题的设计方案有关。我将在下一个关于基于核心问题的系统设计的主题中讨论这一点。

在开发主动地理冗余时，我们还制定了明确的目的和相关目标。尽管我们尝试在中国多个城市同时传输流量，并在几十秒内切换流量，但我们无法消除主动地理冗余应用中存在的物理距离所导致的网络延迟。为了在主动地理冗余应用中实现动态流量交换，我们需要解决以下核心问题:

*   我们如何在本地区域内分割流量并实现整个请求处理过程？
*   在实施主动地理冗余后，我们如何确保数据一致性？

经过近几年我们在统一调度方面的努力，系统设计的概念框架已经日趋成熟，所以我们在这方面有明确的目的和目标。结合我们遇到的实际情况，实现统一调度需要解决以下核心问题:

*   我们如何实现一个在线服务资源调度系统来满足各种资源需求？
*   我们如何尽可能地扩展统一资源池，以解决与池相关的问题，如资源竞争、资源盗窃和不同的资源规格？
*   我们如何将在线服务调度系统和离线任务调度系统互连起来？
*   当在线服务和离线任务以混合模式部署时，我们如何解决资源竞争？

前面的案例表明，当可度量的目标被映射到技术层面时，解决核心问题需要技术技能。对于工程类型的项目和产品，工程经验在解决这些核心问题时也是必不可少的，并且是对架构师能力的直接衡量。

# 为解决核心问题而设计

我们在设定了系统建设的目的和可衡量的目标，确定了核心问题之后，就可以开始设计解决核心问题了。许多技术工程师倾向于直奔主题，对设计部分抱有更高的期望，而没有任何目的、目标或核心问题。结果，最终实现的系统无法解决服务挑战，或者不能按预期运行，因此我强烈建议系统设计人员遵循指定的过程。

我将根据我的案例谈谈如何设计来解决核心问题。我之前的经历揭示了我在系统设计中犯了相当多的错误，遇到了很多复杂的取舍，但我的经历也让我逐渐明白了一个称职的架构师应该具备的能力。

## HSF 设计

在 HSF 设计的初始阶段要解决的第一个核心问题是构建一个易于使用的 RPC 框架，能够支持每天数以亿计的服务调用。

我忽略了易用性的问题，因此在最初的版本中犯了一个错误，但幸运的是，纠正错误并没有花费太多成本。在这个版本中，要将 Spring bean 发布为 HSF 服务或调用 HSF 服务，我需要编写一个文件来描述要发布或调用的服务，并将该文件放在 JBoss 的目录中。尽管这种方法似乎并没有干扰编码过程，但它会导致一系列复杂的问题，比如在哪里编写文件，以及如何在部署过程中自动将完成的文件放入目录中。在第二个版本中，这个方法被修改为通过使用 Spring bean 来发布和调用服务。尽管修改后的方法产生了依赖于 HSF 的服务代码，但它标准化了维护和部署过程。因此，要进行适当的设计，我们不仅需要全面考虑如何实现一个系统，还需要考虑如何使用该系统以及如何运行和维护该系统。

我在 HSF 开发中犯的第二个错误与 RPC 框架有关，它能够支持每天数以亿计的服务调用。这个错误给了我编码生涯中最大的教训，甚至完全改变了我在后续设计项目中的技术选择风格。在从事 HSF 开发之前，我从未构建过日访问量超过 100 万次的系统，也不知道日访问量上亿次的系统会有什么不同。在 HSF 的初始版本中，JBoss Remoting 被选为通信框架，只是因为我们使用 JBoss 作为 web 容器。但是这个版本在一个主要系统上线的时候出现了严重的故障，导致整个网站的反应大大变慢。经过一整天的故障排除，我们无法确定原因，不得不执行回滚，但我们确信故障一定是由 HSF 启动引起的。我们在回滚一周后确定了原因。JBoss Remoting 将远程调用的默认超时时间指定为 60s，而后端系统在处理一些服务时速度较慢，导致共享处理线程池被填满，从而降低了网站响应速度。这个错误让我意识到，要设计一个高访问量的系统，我需要清楚系统的处理机制，因为小问题可能会不受控制地升级，在繁重的访问负担下导致故障。因此，高访问量的系统对可控性的要求很高，这使得这类系统不同于其他访问量一般的系统。可控性并不意味着您必须编写完整的代码，而是您必须清楚开源代码的逻辑(如果使用的话)。为了纠正这个错误，我为 HSF 编写了一个专用的基于 Mina 的通信框架，以特殊的方式处理连接方法和线程池。在我随后的 HSF 改造和其他技术改造项目中，我一直遵循技术可控性的原则。

当我之前谈到核心问题时，我提到了 HSF 设计期间核心问题的细化是有问题的，导致负载平衡和服务化后故障排除方面的大量返工。这些错误是可以避免的，面向服务框架的开发人员不再会犯这些错误。

[负载均衡](https://www.alibabacloud.com/product/server-load-balancer)在早期版本中是由硬件负载平衡器实现的，这导致了几个问题。一个问题是必须配置要调用的服务的虚拟 IP 地址，例如，通过使用中央配置服务器。另一个问题是，HSF 使用持久连接，当虚拟 IP 地址用于连接到后端集群时，这进一步导致了复杂的问题。例如，当后端集群发布重启操作时，连接的分布可能会变得非常不均匀，从而导致故障。

除了前面两个问题，另一个导致我们改造 HSF 的问题是，当时使用的硬件负载平衡器已经达到了最大流量，这是必然会发生的，会使网站崩溃。为了消除这种高风险并解决前面两个问题，我们决定通过设计基于软件的服务注册、发现和寻址来彻底改造 HSF，这是服务框架系统的典型结构。

事后看来，有缺陷的负载平衡功能是由我们对具有高访问量的系统的不全面考虑造成的。

我们最初的设计没有考虑售后服务故障排除。因此，我们不得不投入大量人力来解决问题，但效率很低。为了改进故障诊断，我们尝试了 Google 的 Dapper，但在实现上花了很多时间。

HSF 还存在其他设计问题。例如，最早的通信协议没有版本号，这使得后续升级期间的兼容性处理变得复杂。更棘手的问题是多语言支持。

HSF 是我设计的第一个高访问量的核心系统。由于我当时的技术能力不足，我犯了无数的错误，造成了无数的修改，故障和修复，但我取得了很大的进步。回想起来，我很感谢我的主管，他给了我很大的包容和支持。我在 HSF 设计的经历让我认识到，一个建筑师必须在技术选择上有深厚的技术功底，在设计方案上有广博的知识，要综合考虑开发、部署、运营、O&M 来解决设计的核心问题。

## T4 设计

我在提炼 T4 的核心问题时没有遇到很多困难，但在旨在解决核心问题的设计中犯了明显的错误。

为了在服务器上运行比在虚拟机上更多的应用程序进程，我们通过黑客手段隔离了进程。尽管应用程序仍能正常运行，但当应用程序在一个小范围内启动并建立了用户基础后，这种黑客方法会使枚举变得困难。只有在找到 LXC 之后，我们才解决了这个问题。

我们在 T4 阶段也遇到过很多类似的问题，比如如何控制磁盘空间限制，最初都是用镜像的方法处理的。然而，在磁盘空间超额销售的情况下，镜像方法并不友好，所以我们求助于 dir 配额方法，这种方法花了我们一个多月的时间来实现，因为我们必须编写。在线应用程序的 cp 文件。

我在 HSF 设计中所犯的错误大多是因为我缺乏深厚的技术功底，而我在 T4 设计中所犯的错误大多是因为我当时技术视角的狭隘。我认为，一个称职的建筑师应该在感兴趣的技术领域具有开放的视角，拥有足够的工程知识和该领域的学术知识，以便在一定的约束条件下选择适当的技术来实现设计的目的和目标。我曾经写过一篇关于如何拓展我们技术视角的文章。

## 主动地理冗余设计

回想起来，我的主动地理冗余设计更像是一个基于我以前的经验做出选择的过程，错误率是可控的。因此，我将谈论如何在约束条件下进行权衡，以解决主动地理冗余设计的核心问题。

主动地理冗余设计的核心问题是请求封闭和数据一致性。为了解决这些问题，我们参考了一些工程案例，但发现我们的情况完全不同。

在这里，我将介绍在设计主动地理冗余时必须做出的一些选择，以便您可以思考和讨论它们。我就不说我选择的逻辑了。

*   流量或数据拆分的规则是什么？拆分应该基于买家，卖家，还是产品？
*   流量卸载规则与数据库和表分片规则之间的关系是什么？关系是松耦合还是强绑定？
*   我们应该同步部分数据还是全部数据？
*   应该在什么层面(比如 CAP)保证数据一致性？
*   我们应该以双区域还是三区域模式部署主动地理冗余，以及我们应该如何确定区域分布？
*   实施主动地理冗余需要多长时间，一年、两年还是三年？

如果您对主动地理冗余设计感兴趣，您可以在互联网上搜索更多信息。

在未来，我将详细阐述我在过去几年直到最近在设计统一调度系统和基于云的系统方面的工作。

# 合格架构师的能力总结

让我总结一下架构师必须具备的以下能力，以定义系统设计的目的和可测量的目标，提炼与设计相关的核心问题，并解决这些问题:

*   了解服务挑战，并将服务挑战映射到技术挑战或抽象技术。
*   具备所需的知识，全面考虑从开发、部署、运行到维护的整个过程。
*   拥有选择技术的能力、深厚的技术技能和开放的技术视角。
*   基于合理的原则，在约束条件下进行权衡。

综上所述，我认为“建筑师”不是一个笼统的称谓。一个人要成为一名合格的建筑师，尤其是一名工程建筑师，需要付出大量的努力，需要长期的实践，也需要大量经验的积累。

就我而言，系统设计是我在工作中接受培训的最复杂的课题。我很感谢我的同事们，他们以前参加过我的一个系统设计培训课程，并在我关于系统设计的写作和讨论中帮助过我。通过所有这些工作，我意识到系统设计实际上是一项相当实际的工作，它需要的技能可以随着时间的推移而训练和学习。

# 原始资料

[](https://www.alibabacloud.com/blog/to-system-architects-how-to-design-a-system-better_595386?spm=a2c41.13644021.0.0) [## 致系统架构师:如何更好地设计系统

### 阿里巴巴科技 2019 年 9 月 24 日 3469 作者毕轩。作为一名系统架构师，我本人在…

www.alibabacloud.com](https://www.alibabacloud.com/blog/to-system-architects-how-to-design-a-system-better_595386?spm=a2c41.13644021.0.0)