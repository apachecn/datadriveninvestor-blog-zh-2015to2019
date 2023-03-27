# HashiConf 2018 洞察概要

> 原文：<https://medium.datadriveninvestor.com/the-brief-summary-of-hashiconf-2018-insights-e2a471809167?source=collection_archive---------24----------------------->

[![](img/470461fd7115b7be6636b48da0b8d556.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/00a96e511b4d11514d98b41ba82d74c9.png)

[旧金山的 HashiConf 2018](https://www.hashiconf.com/) 为 HashiCorp 的开源和企业平台、产品和工具带来了许多新闻和更新。我们在这里总结一下。

HashiCorp 是 IT 行业的领导者之一，它坚信 DevOps 的基础设施即代码原则，并在其整个产品堆栈中实施该原则。 [Terraform](https://www.hashicorp.com/terraform) 、游民、执政官、金库、游牧者和 [Hashi Stack](https://www.hashicorp.com/) 的其他部分使企业能够在公共云、本地虚拟服务器甚至裸机集群上构建与云无关的高度可用且安全的基础设施。IT Svit 在我们的运营中积极使用 Terraform，我们很高兴看到这一工具的改进和进一步发展。

# Terraform 0.12 新的 HCL 功能

随着越来越多的公司认识到 Terraform 的重要性以及它为什么会流行起来，HCL 或 HashiCorp 配置语言变得越来越流行。然而，随着用例场景数量的增加，各种改进的空间凸显出来。这一客户反馈带来了各种改进，并在 [Terraform 0.12](https://www.hashicorp.com/blog/terraform-0-1-2-preview) 中发布。该版本为 HCL 带来了许多新功能，并提高了稳定性、一致性和灵活性。

# 远程计划和应用简介

[远程规划和应用](https://www.hashicorp.com/blog/terraform-remote-operations)是一组新功能，支持更透明的 Terraform CLI 与底层 CI/CD 系统和开发人员工作流的交互。这对于决定迁移到 Terraform Enterprise 的[公司尤其有用，因为他们可以从他们习惯的 CLI 中充分利用所有可用的企业级服务。](https://hireukraine.me/service/business-transformation-and-coe/)

# 通过免费的 Terraform 状态存储实现协作

三个关键组件对于 Terraform 协作至关重要:

*   **状态文件管理。** Terraform 状态文件应安全存储、版本化和锁定
*   **在集中地点**计划和应用。Terraform 计划和应用最好在一个中央服务器上运行，以支持同行之间的协作
*   **可共享模块注册表**。团队应该能够自由地重用各种 Terraform 模块

Terraform 面临的第一个也是最大的挑战是状态文件管理的简易性。哈希公司宣布对他们的新服务——[免费状态文件存储](https://app.terraform.io/signup)进行有限的测试。该服务将提供以下好处:

*   无限用户
*   无限工作空间
*   保险库加密
*   根据单独的操作锁定

该公司随后计划推出这项收费服务，但定价方案尚未最终确定。然而，它承诺，即使付费层将是相当负担得起的，免费层将不会提供任何重大的限制。HashiCorp 似乎非常希望加强全球 Terraform 用户之间更广泛的合作，我们渴望看到他们将如何实施这一解决方案。

# HashiCorp Vault v1.0 预览版

HashiCorp Vault 是行业公认的秘密存储和管理领域的领导者。[跳马 1.0](https://www.hashicorp.com/products/vault/)

自 2015 年首次发布以来，已经走过了漫长的道路。现在，这是一个深入且功能丰富的安全平台，被世界领先的公司广泛采用。最新版本使管理员能够以集中的方式批量管理用户、机密和数据。截至 2018 年，该平台已做好生产准备，提供了涵盖众多使用案例的详细和即时文档，完善的工作流程和简单的学习曲线。

# 自动解封保险库

当使用开源 Vault 版本时，手动解封有些受限。社区一直要求 HashiCorp 为该产品的开源版本启用 Vault Enterprise 的自动解封功能。它是在 1.0 中完成的，目前适用于 AWS、GCP、Azure 和阿里巴巴，对其他云平台的支持将很快推出。

# Vault 1.0 中的新功能

Vault 的最新版本中引入了许多新功能:与 Kubernetes 的更高级集成、对 [Helm charts](https://itsvit.com/blog/what-is-helm-and-why-you-should-love-it/) 的支持、对批处理和无服务器计算的批处理令牌的支持，以及其他改进。

# 哈希公司领事 1.4 获得预览版

Consul 是 HashiCorp 的一款优秀产品，它使服务网格能够确保跨云中或本地的任何平台的各种服务的安全连接和轻松配置。Consul 1.4 版本拥有全面可用的 [Consul Connect](https://www.hashicorp.com/blog/consul-1-2-service-mesh) ，以及支持分布在多个数据中心的操作的新功能。该公司最近增加了与 Kubernetes 和[特使](https://www.hashicorp.com/blog/consul-1-3-envoy)的本地领事集成，以实现在 Kubernetes 集群中自动和安全地发现和配置各种服务。

# 强调本地 Kubernetes 支持

HashiCorp 了解他们的客户希望能够将 Hashi Stack 的产品与其他流行的平台和工具相集成。2018 年致力于为地形、执政官、金库和特使提供[本地库伯内特支持](https://www.hashicorp.com/blog/first-class-kubernetes-support-for-hashicorp-products)，正如我们在上面强调的。这种对 HashiCorp 堆栈与其他 DevOps 工具集成的持续强调，为软件工程团队的日常操作提供了更多的灵活性和多功能性，我们非常重视这种努力。

# 关于 HashiConf 2018 见解的最终想法

还有许多其他公告没有包括在 HashiConf 2018 的简要概述中，例如，Nomad 的持续开发和未来推出的 [HashiCorp Learn 平台](https://www.hashicorp.com/blog/hashicorp-learn-platform-with-vault)。该服务旨在培训 Hashi Stack 用户最大限度地利用他们的 Vault、Terraform、Consul 和 Nomad 工具，我们希望您会发现它很有用。

IT Svit 在我们的项目中广泛使用 Terraform、Consul 和 Vault，因此我们很高兴看到 HashiCorp 永无止境的追求完美。随着每一个新版本的推出，他们的产品变得更加有用、安全、创新和高效。您对 HashiCorp 产品有什么体验？请在下面的评论中分享你的想法！