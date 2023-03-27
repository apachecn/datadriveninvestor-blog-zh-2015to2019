# 机器学习的容器化:TensorFlow、Kubernetes 和 Kubeflow

> 原文：<https://medium.datadriveninvestor.com/the-containerization-of-machine-learning-tensorflow-kubernetes-and-kubeflow-93bcdfb01ad5?source=collection_archive---------10----------------------->

![](img/466cab32d5ada5d69b6fec3633551e7d.png)

*原载于* [*CloudOps 的博客*](https://www.cloudops.com/blog/) *。*

机器学习(ML)是一种用于识别模式和预测未来概率的数据分析方法。这是人工智能研究的一部分。通过将带有预定答案的数据输入数学模型，计算机可以训练自己预测未来未知的输入集。

虽然 ML 迄今为止在解决特定任务方面取得了成功，但对具有更复杂参数的数据的分析需要可以通过简化操作大规模部署的模型。这种机器学习将使计算机能够从大量信息中找到解决方案并实现自动化。由于这些原因，预计到 2020 年[人工智能和人工智能将成为推动云计算采用的主要催化剂](https://www.forbes.com/sites/louiscolumbus/2018/01/07/83-of-enterprise-workloads-will-be-in-the-cloud-by-2020/#145840906261)。为了处理云中可用的大量信息，ML 需要大规模高效学习，并与云原生技术(尤其是容器化)集成。

为此，Google 最近宣布创建 Kubeflow，这是一个基于 Kubernetes 的可组合、可移植和可扩展的 ML 栈。它为 ML 模型提供了一个开源平台，可以将它们自己附加到容器中，与数据一起执行计算，而不是在叠加层中。

Kubeflow 有助于解决实现 ML 堆栈的固有困难。构建生产级 ML 解决方案需要导入、转换和可视化数据，然后构建、验证、训练和大规模部署模型。这些堆栈通常是用不同的工具构建的，这使得算法管理起来很复杂，结果也不一致。 [Kubeflow 1.0](https://kubernetes.io/blog/2018/05/04/announcing-kubeflow-0.1/) 提供的包将各种 ML 工具，特别是 TensorFlow 和 JupyterHub 吸收到一个堆栈中，可以很容易地通过 Kubernetes 在多云环境中传输。

**张量流**

Kubeflow 依靠开源编程系统 [TensorFlow](https://opensource.com/article/17/11/intro-tensorflow) 来构建机器学习模型。它的软件库使用张量几何结构以有状态数据流图的形式表达数据之间的线性关系。它抽象了硬件平台，允许模型在 CPU(中央处理器)、GPU(图形处理器)或 TPUs(张量处理器)上运行。总之，这些构成了低精度算术计算的高吞吐量的基础。这种灵活的架构允许 it 部门将来自各种对象的信息汇集在一起，从桌面到集群或服务器，以及移动设备和边缘设备。尽管使用起来困难且复杂，TensorFlow 非常适合创建复杂程度需要可移植和可扩展数据管理的 ML 模型。

**木星枢纽**

Kubeflow 直接从 [Jupyter](http://jupyter.org/hub) 笔记本上执行 TensorFlow 计算图形。Jupyter 笔记本是容器友好的，可以在 Kubernetes 或任何类型的开源基础设施上运行。它们为用户提供了易于实现的 ML 模型的环境和资源，而没有安装和维护的开销。他们的文档风格格式将代码和 markdown 都嵌入到同一个文件中，提供了计算的可见性。JupyterHub 允许工程师立即执行张量流图或存储以备后用，从而对张量流模型的配置进行更多控制。Kubeflow 依靠 JupyterHub 进行协作和交互式培训。

Kubeflow 的堆栈结合了其他几个解决方案，补充了 TensorFlow 模型的执行。Argo 用于调度工作流，SeldonCore 用于复杂推理和非张量流 Python 模型，Ambassador 用作反向代理。与 Kubernetes 集成，这个堆栈允许工程师有效地开发、训练和部署大规模的 ML 模型。

**Kubernetes**

Kubernetes 是一个可靠的开源容器编排工具。它将应用设计标准化为模块化、可移植、可扩展的微服务，可在不同环境中部署复杂的工作负载。它使用丰富的 API 来自动化众多的操作功能。Kubeflow 的平台利用 Kubernetes 来简化 TensorFlow 模型的操作，并使其执行云本地化。

*可移植性和可扩展性—* Kubernetes 允许将 TensorFlow 模型作为微服务进行模块化管理，使其具有高度的可移植性和可扩展性。它们可以在不同的环境、平台和云提供商之间轻松迁移。传统上，ML 堆栈是不可移动的，将模型及其相关依赖项从笔记本电脑移动到云集群的过程需要大量的重新架构。Kubeflow 允许这些算法在执行时尽可能快地访问数据。

*自动化和易操作性—* Kubernetes 通过提供丰富的声明式 API 库来管理微服务，帮助应用采用端到端自动化。Kubernetes 负责资源管理、工作分配和其他传统上耗时的运营问题。Kubeflow 允许工程师专注于编写 ML 算法，而不是管理他们的操作。

云中有大量可用的信息，但其范围尚未完全可供机器学习使用。Kubeflow 1.0 承诺 ML 有能力跟上云中数据的不断增长。它将 ML 集成到容器编排层，为模型提供了更好的易操作性、可伸缩性和可移植性。它提供了一个完整的容器化堆栈，可以快速而简单地进行部署。Kubeflow 1.0 允许计算机使用可靠而全面的堆栈，用更多的数据集来训练自己。[报名参加机器学习研讨会，了解更多信息。](https://www.cloudops.com/workshops/)

*这篇博文由 Syed Ahmed 撰写，最初发表于* [*CloudOps 的博客*](https://www.cloudops.com/blog/) *上* [*这里*](https://www.cloudops.com/blog/machine-learning-tensorflow-kubernetes-and-kubeflow/) *。*

[**注册订阅 CloudOps 每月简讯，了解最新的 DevOps 和云原生开发。**](https://www.cloudops.com/newsletter-signup/)