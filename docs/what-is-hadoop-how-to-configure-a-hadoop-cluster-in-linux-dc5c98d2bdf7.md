# Hadoop 是什么？如何在 Linux 中配置 Hadoop 集群？

> 原文：<https://medium.datadriveninvestor.com/what-is-hadoop-how-to-configure-a-hadoop-cluster-in-linux-dc5c98d2bdf7?source=collection_archive---------2----------------------->

## Hadoop 演示&在 Linux 中配置 Hadoop 的逐步指南。

# 简介:

在大数据世界中，每当我们谈论数据库、服务器和处理时，我们脑海中浮现的第一个工具是 **Hadoop** 。如果你是大数据分析领域的新手，你迟早会遇到 Hadoop，因为它在大数据领域有自己的意义。由于其出色的性能、特性和灵活性，它被广泛应用于大数据领域。那么 Hadoop 是什么呢？

在这篇文章中，我将演示如何在 Linux 中配置 Hadoop 集群。

# Apache Hadoop:

描述 Hadoop 有多种定义，但我发现最准确的定义如下。

> Hadoop 是一个开源软件框架，用于在商用硬件集群上存储数据和运行应用程序。它为任何类型的数据提供大容量存储、巨大的处理能力以及处理几乎无限的并发任务或工作的能力。

![](img/99278ff4ce896dd478399ccd6d9e5dc4.png)

Hadoop 是不断增长的大数据技术生态系统的中心，这些技术用于支持高级分析、数据挖掘和机器学习应用。Apache Hadoop，该技术是作为 Apache 软件基金会的一个开源项目的一部分开发的。Hadoop 被称为大数据的支柱，因为它具有很大的灵活性，可以与许多其他大数据工具集成，如 Apache Hive、Apache Ignite、Presto、Impala、Apache Druid 等。

让我们详细讨论 Hadoop 的组件和其他令人惊叹的功能。

# Hadoop 的组件:

Hadoop 有四个主要的核心组件，让它物有所值。每个组件都执行一项特定的任务，这项任务对于为大数据分析而设计的计算机系统至关重要。

## 分布式文件系统:

这也是 Hadoop 独一无二的原因之一，Hadoop 分布式文件系统(**【HDFS】)**允许数据以一种易于访问的格式存储在大量链接的设备上。将设备连接在一起并相互共享资源的过程称为集群。无论集群中连接了多少设备，它们都将通过一个 U.I .和一个端口连接到同一个分布式文件系统。

## MapReduce:

Hadoop 出色性能的另一个原因是其组件 MapReduce。MapReduce 是根据该模块执行的两个基本操作而命名的——从数据库中读取数据，将其转换为适合分析的格式(map ),以及执行数学运算，即计算客户数据库中 30 岁以上男性的数量(Reduce)。每当 MapReduce 进程运行时，它就被称为 Job。映射器和缩减器代码可以用 Java 和 Python 编写，并且可以通过 Hadoop 轻松运行，但是，要在 Python 上运行，需要一个“hadoop streaming jar”文件。

## Hadoop 常见:

另一个组件是 Hadoop Common，它提供了用户的计算机系统(Windows、Unix 或其他任何系统)读取存储在 Hadoop 文件系统下的数据所需的工具(用 Java 编写)。

## 纱线:

Hadoop 最后也是最重要的组件是另一个资源协商器(YARN)。YARN 负责管理存储数据和运行分析的系统资源。我们可以将资源分配给 Hadoop 集群中的不同进程。Yarn 有三个不同的调度器，以不同的方式调度作业， **FIFO(先进先出)**，**公平调度器&产能调度器。**

YARN 中有很多细节需要讨论，但这是另一个博客的主题。

# **为什么 Hadoop 很重要？**

*   **能够快速存储和处理大量任何类型的数据。**随着数据量和种类的不断增加，尤其是来自社交媒体和物联网(IoT)的数据，这是一个关键的考虑因素。
*   **计算能力。** Hadoop 的分布式计算模型处理大数据速度快。使用的计算节点越多，处理能力就越强。
*   **容错。**保护数据和应用程序处理免受硬件故障的影响。如果一个节点出现故障，作业会自动重定向到其他节点，以确保分布式计算不会失败。自动存储所有数据的多个副本。
*   **灵活性。**与传统的关系数据库不同，您不必在存储数据之前对其进行预处理。您可以存储任意多的数据，并决定以后如何使用。这包括文本、图像和视频等非结构化数据。
*   **成本低。**开源框架是免费的，使用商用硬件来存储大量数据。
*   **可扩展性。**只需添加节点，您就可以轻松扩展系统以处理更多数据。几乎不需要管理。

在这一点上，我希望你了解 Hadoop，以及它在大数据中被广泛使用的独特之处。现在让我们继续讨论 Linux 中的 Hadoop 集群部署。

# 在 Linux 中配置 Hadoop 集群:

配置多节点 Hadoop 集群非常简单易行。请按照下面的说明操作。

1.  首先确保安装了 Java (open jdk)版本 8，如果没有，打开 gnome-terminal 并输入命令“sudo apt-get install open JDK-8-JDK”。
2.  在~/中设置 PATH 和 JAVA_HOME 变量。bashrc 文件

```
export JAVA_HOME=/usr/local/jdk1.7.0_71
export PATH=PATH:$JAVA_HOME/bin
```

3.在主系统和从系统上创建一个系统用户帐户，以使用 Hadoop 安装。以 root 用户“su root”身份登录，然后创建一个用户..

```
useradd hadoop
(after executing it, set the password).
```

4.为了做到这一点，请确保您的主节点知道其他节点的 ip 和主机名

```
# vi /etc/hosts
enter the following lines in the /etc/hosts file.

192.168.1.109 hadoop-master 
192.168.1.145 hadoop-slave-1 
192.168.56.1 hadoop-slave-2
```

5.在每个节点中设置 ssh，这样它们就可以相互通信，而不需要任何密码提示。

```
# su hadoop 
$ ssh-keygen -t rsa 
$ ssh-copy-id -i ~/.ssh/id_rsa.pub tutorialspoint@hadoop-master 
$ ssh-copy-id -i ~/.ssh/id_rsa.pub hadoop_tp1@hadoop-slave-1 
$ ssh-copy-id -i ~/.ssh/id_rsa.pub hadoop_tp2@hadoop-slave-2 
$ chmod 0600 ~/.ssh/authorized_keys 
$ exit
```

6.安装 Hadoop 2.7，因为它与其他工具没有任何兼容性问题。[在这里安装 Hadoop 2.7 Binar 表单](https://archive.apache.org/dist/hadoop/core/hadoop-2.7.0/)。下载后，解压文件

```
tar -xzf hadoop-2.7.0.tar.gz
```

7.在~/中设置 PATH 和 HADOOP HOME 变量。bashrc 文件。

```
export HADOOP_HOME=<path to hadoop's directory>
export PATH=PATH:$HADOOP_HOME/bin
```

8.配置主节点

```
$ vi etc/hadoop/masters

hadoop-master
```

9.配置从属节点

```
$ vi etc/hadoop/slaves

hadoop-slave-1 
hadoop-slave-2
```

10.在主节点上格式化 Namenode。转到 Hadoop 的 bin 目录并键入..

```
./hadoop namenode –format
```

最后，在完成上述所有程序后，启动 hadoop 服务。

```
$ cd $HADOOP_HOME/sbin
$ start-all.sh
```

在这一点上，希望您已经部署了多节点集群，这就是这篇博客的内容。**谢谢:-)**