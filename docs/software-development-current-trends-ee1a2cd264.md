# 软件开发:当前趋势

> 原文：<https://medium.datadriveninvestor.com/software-development-current-trends-ee1a2cd264?source=collection_archive---------20----------------------->

科技行业正经历前所未有的繁荣。数十亿美元的公司每天都在大力投资革新技术。那么，一个普通的工程师如何应对当前的趋势呢？

查看一些由你最喜欢的科技公司验证的不容错过的当前趋势，并在竞争中保持领先..！！

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

# **Dropbox:微服务通信层**

当微服务语言不通的时候，它们之间是如何沟通的？为此，谷歌已经推出了一个名为 [gRPC](https://grpc.io/) 的框架，它比 Json 更快更高效。

但是，Dropbox 领先一步，在 gRPC 的基础上开发了内部通信基础设施。现在屏住呼吸！它不仅负责通信，还将处理所有的服务器内部认证、授权、服务发现、日志记录、监控、跟踪、截止日期、断路、运行时调试等等！？ [**做此检查..**](https://blogs.dropbox.com/tech/2019/01/courier-dropbox-migration-to-grpc/)

![](img/fdc81a3e9be1b159f1b70f3ae176126f.png)

# 网飞:多数据库同步层

每个数据库都是为一个特殊的用例设计的。大多数时候，我们需要相同数据的不同用例。为此，开发人员必须使用各种数据库，并需要在它们之间同步数据。这成为一个主要的技术挑战，通常使用基于事件或基于作业的机制。

但是，网飞设计了一个多数据库统一架构，这将是一个编排层以上的几个数据库。这一层将负责所有的同步功能。 [**看看这个...**](https://medium.com/netflix-techblog/implementing-the-netflix-media-database-53b5a840b42a)

![](img/57e23a252474e9b63aae113128293270.png)

# **Lyft:工作流管理平台**

通常，所有的系统都非常复杂，有如此多的工作流。了解任何工作流管理平台吗？！检查新的[阿帕奇气流](https://airflow.apache.org/)。

尽管它是一项新兴技术，Lyft 仍在生产中使用它来以编程方式创作、安排和监控工作流程。丰富的用户界面使得可视化生产中运行的管道、监控进度以及在需要时解决问题变得容易。 [**看看这个..**](https://eng.lyft.com/running-apache-airflow-at-lyft-6e53bb8fccff)

![](img/d571a4bcda09e0ef8be1b0340d59993c.png)

# Reddit:负载平衡器-网络层转移

负载平衡是后端架构的主要组成部分。通常，负载平衡是在 TCP 层(L4)完成的，以实现快速的 ip 转换。但是，现在它被移到了应用层(L7)。这看起来是反直觉的，因为它将在计算上更加昂贵，并且将产生更多的延迟。但是，它可以读取请求，做出更好的路由决策，从而节省大量网络成本。

看起来很奇怪，对吧？！但像 Reddit 这样的大公司正在痛苦地将他们的堆栈从 HAProxy(L4)转移到 Envoy(L7)。 [**看看这个..**](https://redditblog.com/2018/12/18/envoy-proxy-at-reddit/)

![](img/690bd093528cfa7be9a5bfde40254e41.png)

# #5 优步:机器学习——开发你自己的测试案例

机器学习算法的主要挑战是什么？！生成训练数据，对吗？！。如果算法学会自己生成训练数据会怎么样？！那不是很神奇吗？这就是优步正在努力的方向。 [**做此检查...**](https://eng.uber.com/poet-open-ended-deep-learning/)

![](img/baa30f01ad72addc12b01f39820a5cee.png)

这篇博文到此为止。我有意保持简短，以涵盖所有主要趋势。一定要让我知道你对它的想法！