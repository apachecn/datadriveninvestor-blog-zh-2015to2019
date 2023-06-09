# 应用于机器学习的软件质量特征

> 原文：<https://medium.datadriveninvestor.com/software-quality-characteristics-applied-to-machine-learning-366347949081?source=collection_archive---------1----------------------->

## 黑客工作，直到它不工作

![](img/1666b1715ccde74a8f8d5c1235616ec8.png)

Photo by [Ales Nesetril](https://unsplash.com/@alesnesetril?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着我在软件开发和机器学习方面获得越来越多的经验，每隔几年，我都喜欢重温史蒂夫·麦康奈尔(Steve McConnell)的《代码全集 2》(Code Complete 2)，这是一本 1000 页的实用软件工程杰作。

如果所有的计算机工程本科生都被要求参加一个学期的使用 Code Complete 2 的课程，并且初级到中级程序员在他们的职位开始时有两个星期的工资，并且在一些更真实的世界经验之后每年至少提供几天时间来重温和思考软件开发的想法，那么软件开发的状态将会得到极大的提高。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

我将概述软件质量的重要性，软件的具体外部和内部特征，以及它们如何应用于机器学习的过程。

# 为什么软件质量很重要？

## 砍

软件开发的流行概念或焦点是通过“黑客”编写代码来构建东西，而没有提到软件质量或定义的过程，如测试或维护。里程数可能因程序员个人的天赋而异，但“黑客”不可扩展到更大的团队、更复杂的系统以及现实世界中活生生的业务问题。

我觉得特别幽默的是黑客马拉松，有些会持续一整夜，或者在“创业巴士”这样的环境中进行，同时含有大量咖啡因。我个人认为黑客马拉松接近真正的软件工程，就像看科幻小说接近科学研究一样。在任何真实的生产环境中，调试、测试、维护或少量扩展一个拼凑起来的代码系统所需的时间和精力很容易是快速编写它所需的最初努力、时间和思考的 10 倍。

## 航天飞机代码

我发现这篇关于二十多年前航天飞机中的软件过程和代码开发的文章尤其令人难忘。

*   [他们写对了东西](https://www.fastcompany.com/28121/they-write-right-stuff)
    —《快公司》杂志，1996 年 12 月 31 日

在无情的太空环境中运行航天飞机的软件中的任何错误都可能轻而易举地价值数百亿美元，值得许多人付出时间和努力，以及真实人类的实际生活，因此黑客行为是荒谬的，拥有强大的软件构建、测试和维护方法至关重要。

> 对软件进行升级，使航天飞机能够通过全球定位卫星导航，这一变化只涉及程序的 1.5%，即 6366 行代码。这一变化的规格长达 2500 页，比一本电话簿还厚。当前程序的规格有 30 卷，40，000 页。”

这种紧密运行的需求和规范会产生一些令人难以置信的无错代码。想想这句话:

> …程序的最后三个版本——每个版本都有 420，000 行——每个版本都只有一个错误。这个软件的最后 11 个版本总共有 17 个错误。同等复杂程度的商业程序会有 5000 个错误。

当然，商业软件开发不需要这些规范的这么低的错误水平，因为大多数生产环境比太空中的航天飞机宽容得多，可以容忍更多的错误。事实上，编写这种低错误代码的成本实际上对于商业软件中的大多数上下文来说没有经济、财务或商业意义，因为开发人员资源是昂贵的，并且他们的成本必须由与该开发相关的收入和盈利能力来调节。

无论如何，意识到这样的错误率是很重要的，同时也要注意软件质量的特征。

## 软件质量的外部和内部特征

在我阅读和重读《代码全集 2》的过程中，有一个特别的想法一直伴随着我，那就是软件质量的特征。

存在着:

*   与软件质量用户相关的外部特征
*   与软件开发人员相关的内部特征

在我的日常工作中，我编写代码，管理系统和人员，设计整个技术堆栈的流程。由于跨堆栈的许多系统都是封装的，并且通过 API 与定义明确的交互协议弱耦合，因此我同时作为外部用户和内部开发人员与软件进行交互，通常涉及我自己编写的代码。

如今，机器学习已经被整合到整个技术体系中，成为软件开发的一个组成部分，软件质量方面的许多想法也可以在机器学习的背景下加以考虑。我将列举软件质量的外部和内部元素，并简要评论它们如何应用于机器学习。这些定义来自《代码全集 2》，“第 20 章:软件质量景观”，但是机器学习(ML)的解释是我自己的。

由于软件质量的特性并不是完全相互独立的，因此在外部和内部特性之间，以及它们之间，可能会有大量的重叠。类似地，也可能有重叠和重复的“机器学习解释”。

![](img/5a5a19839d3e82d6651be0bc9fceba67.png)

Photo by [Banter Snaps](https://unsplash.com/@bantersnaps?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 软件质量的外部特征

软件的最终用户关注的是软件的外部特征。对于机器学习环境,“最终用户”可以指:

*   那些使用已经开发的代码的，这些代码用于在机器学习管道的部分中执行定义的过程
*   下游预训练模型的实际使用

代码的开发与软件或 ML 的内部质量有关。

## 1.正确性

*   **一个系统在规格、设计和实现上没有错误的程度。**

**ML 上下文**
我们可能需要制定与 ML 模型将在生产中使用的上下文密切相关的训练集。仅仅让机器学习模型产生高置信度的正确答案是不够的，因为它可能已经针对不同的上下文进行了训练。

有趣的是，当软件失败时，更容易检测和理解，即使它涉及语义错误，而不仅仅是立即导致错误的明显语法错误。

相比之下，ML 过程的正确性可能依赖于指定数据、解释定量准确度/精度度量的含义以及理解与数据原始上下文的任何细微偏差的整个流程。此外，训练过程可能完全不透明，尤其是在非常深的神经网络中。因此，深入了解需求、培训数据和生产环境非常重要。

## 2.复用性

*   **用户学习和使用系统的容易程度**

**ML 上下文**

Keras 之类的框架在这里非常有用。这里的可重用性可能是对比较训练集的陈述，也可能是对训练代码或分类器的可重用性的陈述。

可重用性可能需要对问题域和训练集有深入的理解，但是特征集越低，预训练模型的可重用性就越高。例如，在卷积神经网络中，可能存在来自 ImageNet 的高度可重用的分类器的低级训练权重，例如用于检测边缘的模型。

## 3.效率

*   **最少使用系统资源，包括内存和执行时间。**

**ML 上下文** 许多 ML 模型被优化以用作分类器，而不需要太多甚至任何训练。

具有预训练权重的可导入模型可以被视为将用于训练的大量资源封装到权重的精确规范中。

## 4.可靠性

*   **系统在需要时执行其所需功能的能力低估了条件——具有较长的平均故障间隔时间。**

**ML Context** 

这里的问题是可靠性和故障不一定与系统崩溃有关。甚至准确性度量也可能难以辨别，因为我们需要在准确性方面有很大的下降才能确定一个模型是否不再可靠。机器学习中的训练和分类本质上分别是统计的和概率的，因此什么构成了可靠性可能难以辨别。

## 5.完整

*   系统防止未经授权或不当访问其程序和数据的程度。

**ML Context** 这在生成式对抗网络(GANS)中尤为重要，在这种网络中，即使注入一点点有意设计的数据，也可能完全扰乱实际训练。

为了完整性，以下所有内容实际上必须被认为是紧密耦合的:数据、代码和分类器。

## 6.适应性

*   **一个系统无需修改即可用于除了专门设计的应用或环境之外的应用或环境的程度。**

**ML Context** 由于分类的维度要小得多，所以这在诸如边缘检测器之类的低级特征集中可能更加相关。适应性也可以是具有足够大的训练数据集的函数。

## 7.准确(性)

*   **系统建成后没有错误的程度，尤其是在定量输出方面。准确性不同于正确性；这是对一个系统的工作做得有多好的决定，而不是它的构建是否正确。**

**ML Context** 准确性在范围上更受限制，需要的解释更少，因此许多标准的统计技术无需深入思考或进一步的上下文化就可以使用。

## 8.稳健性

*   在无效输入或压力环境条件下，系统持续运行的程度。

**ML 上下文** 与理解训练模型的上下文特别相关。例如，有一个关于视觉分类器的案例研究，该分类器被训练用于辨别狗和狼。该系统被证明是高度准确和稳健的。然而，事实证明，狼通常在背景中有雪，所以实际上，ML 分类器是用于检测雪的，并且在背景中没有雪的情况下不会非常健壮。

![](img/d1afc42894cc075ec34af0b9965e8a53.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 固有特性

软件的“开发者”不是最终用户，而是对内部软件特性的关注。这里的 ML 开发人员可能是接触代码以训练分类器的人，也可能是定义训练集并参与开发整个 ML 管道的人。

## 1.可维护性

*   修改软件系统以改变或增加功能、提高性能或纠正缺陷的容易程度。

**ML Context
亚马逊 SageMaker 从平台的角度来看可能是有用的。**

这里的可维护性也可以指清理和暂存数据、输入缺失值、培训、验证、测试以及重新部署的整个管道和过程。

## 2.灵活性

*   **除了专门设计的用途或环境之外，您可以在多大程度上修改系统的用途或环境**

这可能更多地是数据和过程的函数，而不是分类器的训练。努力封装和松散耦合管道中的流程，例如数据清理和暂存、培训和测试，以帮助修改系统来满足不同的需求。

## 3.轻便

*   **您可以轻松修改系统，使其在与专门设计的环境不同的环境中运行**

**ML Context** 像 Amazon Sagemaker Neo 这样的平台支持重新编译成不同的 ML Context，甚至提供内置的加速，而不需要开发者做任何工作。

苹果允许在 TensorFlow 中训练模型，然后将其移植到苹果的核心 ML 工具包中。在许多方面，可移植性不是问题，并且有许多工具提供支持。主要问题是，它需要一个升级和开发操作层来使代码可以跨系统移植。

## 4.复用性

*   **您可以在其他系统中使用系统部件的程度和难易程度。**

**ML Context
分类的较低级部分可以重复使用。**

## 5.可读性

*   阅读和理解系统源代码的容易程度，尤其是在详细陈述级别。

**ML 上下文** 代码越简单，可读性越高。这就是为什么我真的很喜欢 Keras 非常干净简单的用法。基本上，只需要几行 Python 代码就可以完成指定、训练、测试和部署。

问题是可读性可能会掩盖许多较低级别的过程和实际的上下文，例如训练集的性质，可读性实际上可能是一种负担。

## 6.易测性

*   你可以对一个系统进行单元测试和系统测试的程度；您可以验证系统满足其要求的程度。

**ML Context** 这里可能还有更多关于用于测试的度量标准的“解释”，比如学习曲线、准确度、精确度、召回率等等。易于测试的 ML 模型实际上可能提供虚假的舒适性，即使测试结果看起来不错。

## 7.易懂

*   **你在系统组织和详细陈述层面理解一个系统的容易程度。与可读性相比，可理解性在更一般的层面上与系统的一致性有关。**

ML 上下文
这里的权衡是，ML 代码的可读性越强，它在抽象中的位置就越高。因此，从高层次的角度来看，这可能是可以理解的，但可能隐藏了许多重要的关键过程。