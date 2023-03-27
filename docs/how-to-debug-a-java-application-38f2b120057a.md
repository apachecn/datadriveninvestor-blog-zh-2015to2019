# 如何调试一个 Java 应用？

> 原文：<https://medium.datadriveninvestor.com/how-to-debug-a-java-application-38f2b120057a?source=collection_archive---------1----------------------->

*这个故事最初发表在我的博客@linqz.io* [*这里*](https://www.linqz.io/2018/07/how-to-debug-a-java-application.html) *。*

![](img/90d45d354ec392bfa57c12a5e51f574f.png)

How to figure out the root cause of faulty code execution in production environment?

对基于 Java 的应用程序进行故障排除或“调试”是一个高技能软件工程师的特征之一。要准确地识别一个软件工程师有多熟练，可以归因于他在软件应用程序中发现问题的速度。

记录到日志文件中的异常更容易发现，因此在这篇博客中我省略了它们。当我们知道了根本原因，找到解决方案就容易了。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

应用程序会对系统产生“涟漪效应”,有时可能会波及到整个应用程序。比方说，您的应用程序运行在 tomcat 中，并使用 san 挂载(假设它是硬挂载)。如果 mount 消失(或者没有响应), tomcat 将停止服务请求。但是为什么呢？

下面是答案:

当 mount 变得无响应时，读/写线程进入挂起状态，这使得当前运行的 tomcat 线程处于忙碌/等待状态，随着时间的推移，随着读/写 mount 请求的增加，将会有一段时间 Tomcat 的所有线程都将进入忙碌-等待状态。

因此，Tomcat 停止服务，客户端开始接收 **503-服务不可用**。

让我们讨论一下有助于发现问题的交易工具:

## 调试主机上的问题:

1.  **lsof** (仍在消耗内存的打开文件指针列表)

运行下面的命令将列出打开的文件指针，如果这个列表保持不变，那么很可能您的应用程序没有正确地关闭流，因此操作系统仍然持有它，因此机器上可用的内存由于没有被释放而减少。

涟漪效应-->因为如果这个列表越来越大，将导致进程可用内存的减少，并可能开始导致应用程序中的垃圾收集，最糟糕的情况是操作系统可能会由于内存不可用而终止 java 进程。

```
$ **sudo lsof | { head -1;  grep deleted;}**
COMMAND      PID          USER   FD      TYPE             DEVICE     SIZE/OFF       NODE NAME
XXXXX     3342        tomcat    5w      REG                8,1            0     108573 /var/tmp/data/0_00000 (**deleted**)
java      139971        tomcat   61r      REG                8,1           10    8471874 /var/tmp/ABC.csv (**deleted**)
java      139971        tomcat   69r      REG                8,1       148003    8472018 /var/tmp/XYZ.mp3 (**deleted**)
```

2.**顶部**

通过这个命令，您可以监视系统资源、进程、它们的使用情况等等。如果您理解这个命令的输出，它将帮助您调试各种各样的问题。

例如，您有一台启用了超线程的 4 核计算机，实际上有 8 个内核，因此，如果您的平均负载高于 10，则该计算机会超负荷工作，这将在内部导致过多的线程上下文切换，从而在内部影响性能。

根据公式 **N*(1+WT/ST)** 在应用程序中使用的线程数量，其中 N 是 CPU 的数量，WT 是等待时间，ST 是执行时间，如这里的[**所示**](http://www.ibm.com/developerworks/java/library/j-jtp0730.html) **。**

`**wa**`值，即 CPU 等待 I/O 完成所花费的时间。这将告诉你，你的 IO 太多了，你的硬件或应用程序需要改进。

`**nice**`值来确定一个进程的优先级。具有高“好”值的进程获得低优先级，低“好”值意味着高优先级。

这里对顶层命令输出的详细描述是 [**。**](https://www.booleanworld.com/guide-linux-top-command/)

3) **netstat** 命令/ **ss** 命令

此网络统计命令用于监控网络连接的传入和传出，查看路由表、接口统计等。它在网络故障排除和性能测量方面非常有用。

Recv-Q，Send-Q，这两个值告诉我们有多少数据在该套接字的队列中，等待读取(Recv-Q)或发送(Send-Q)。

**接收方**上的 Recv-Q** 高—当接收缓冲区填满时，TCP 关闭接收窗口，禁止发送方发送。发送方发送的数据不能超过接收方 TCP 在其接收窗口中公布的数据。这可能会导致发送方应用程序线程冻结。**

**高 Send-Q** on **Sender** —这意味着操作系统级别的另一端 TCP 实现已被卡住，并已停止为我的数据包发送 ACK，这通常是操作系统级别的问题(尽管这种可能性很小)*。*

[**Wireshark**](https://www.wireshark.org/)TCP/UDP 转储可以用来做网络包分析。

3) **dmesg -T** 命令

`**dmesg**`命令缓冲区为内核记录的硬盘、Cpu、以太网等提供了许多不同类型的消息和日志。

该命令记录无法正常工作的硬件/异常行为/固件/驱动程序/时间等相关问题。这些问题有时会影响应用程序的平稳运行。如果您无法解决任何问题，请使用`**dmesg**`查找硬件错误。

可以用来监视/识别特定主机上的问题的其他著名工具和系统有[**【Ganglia】**](http://ganglia.info/)**/**[**Icinga**](https://www.icinga.com)**。**

## 调试主机上的应用程序:

现在让我们讨论调试应用程序的各个步骤。下面附上一些助手工具，可用于调试请求/应用程序的各个方面(您可以根据自己的要求自由修改和使用它)。

[](https://github.com/root0109/ApplicationDebugHelper) [## root 0109/ApplicationDebugHelper

### 这包含了一组调试问题的帮助工具，这些工具必须初始化为和…

github.com](https://github.com/root0109/ApplicationDebugHelper) 

a) **数据库调试:**

1.  您可以使用[***DBQueryStatsManager.java***](https://github.com/root0109/ApplicationDebugHelper/blob/master/src/my/test/DBQueryStatsManager.java)来收集查询统计数据，如果您使用的是普通的旧 JDBC，或者如果您使用的是 ORM，它们有自己的连接/查询统计报告。例如在冬眠时

```
setting below attribute<persistence>
    <persistence-unit name="my-persistence-unit">
        ...
         <properties>
            <property name="**hibernate.generate_statistics**" value="**true**" />
             ...
        </properties>
    </persistence-unit>
</persistence>
```

2. [***显示全部流程列表***](https://dev.mysql.com/doc/refman/8.0/en/show-processlist.html)

这是识别长时间运行的查询的另一种方法，检查各种 mysql 线程状态等。这为识别有问题的查询/表格提供了重要信息，稍后可以详细查看这些信息。

3) ***数据库锁定查询/表:***

对于 Mysql:设置下面的属性来记录执行缓慢的日志，

```
set global log_slow_queries = 1;
set global slow_query_log_file = <some file name>;
```

或者，您可以在`my.cnf/my.ini`选项文件中设置该选项

```
log_slow_queries = 1; 
slow_query_log_file = <some file name>;
```

b) **垃圾收集器日志**:

总是在 tomcat 应用程序的启动脚本中添加下面的 GC 选项，以便可以记录垃圾收集的详细信息。

```
**-Xloggc:/var/tmp/gc_20180811.txt -XX:-PrintGC -XX:+PrintGCTimeStamps -XX:+PrintGCDetails -XX:-PrintTenuringDistribution**
```

gcViewer 是分析 GC 日志的好工具，你可以从[这里](https://sourceforge.net/projects/gcviewer/)下载。

大多数应用程序开发人员更喜欢使用 G1GC，而不知道垃圾收集的复杂性。G1GC(尽管是最优选的)对于任何位于用户浏览器路径中的 JVM 都是优选的，而 ParallelGC 对于具有更多异步处理的应用程序是优选的。

Eric Abbott 在 G1GC 上写了一篇漂亮的文章，对于所有想了解和微调 G1GC 的人来说，这是一篇必须阅读的文章。这里的链接是[](https://product.hubspot.com/blog/g1gc-fundamentals-lessons-from-taming-garbage-collection)**。**

**c) **挂载相关问题(不可用/断开)****

**大多数负载平衡应用程序使用 mount(nfs/sftp 等)在负载平衡实例之间共享文件数据。很多时候，这些挂载被卡住或停止响应，这导致应用程序线程处于挂起状态(如开始给出的示例中所解释的)。**

**下面是 nfs 装载的一个示例，可以按如下方式检查其连接性:**

```
# on server
**systemctl start nfs-server**

# on client
mount node1:/mnt/media /mnt/media
**df -h** #works fine here

# on server
**systemctl stop nfs-server**

# on client
**nfsstat -m** #shows the list of nfs mounts
/my_enterprise host0026:/data/my_enterprise
 Flags: rw,sync,relatime,vers=4.0,rsize=8192,wsize=8192,namlen=255,**hard**,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,clientaddr=20.20.20.7,local_lock=none,addr=20.20.20.26**df -h #this command will hang
ls /mnt/media #this command will hang**
```

**d)线程转储**

**线程转储是理解 JVM 中运行线程状态的重要工具。线程转储有助于分析线程争用和死锁情况，更多信息可以在这里 找到 [**。**](https://dzone.com/articles/how-analyze-java-thread-dumps)**

**有许多方法可以进行线程转储，下面是不打开 tomcat 服务器端口的最干净的方法:**

```
$ tail -f /<path to tomcat logs>/catalina.out >> ~/thread-dump-1 &
$ sudo -u tomcat-user kill -3 <pid>
$ kill %1
$ less ~/thread-dump-1
```

**Tomcat 管理器:**

**Tomcat web 应用程序管理器提供请求连接器信息，这有助于调试 Tomcat 工作线程耗尽、内存泄漏等问题。**

**例如，在给定的时间点，下面的连接器信息告诉我们这个 tomcat 有足够的线程来服务请求。当最大线程数等于当前线程忙计数时，用户将开始接收`503 Service Unavailable`,因为没有可用的 tomcat 工作线程来服务。**

```
**"http-nio-8080"**
Max threads: 1000 Current thread count: 163 Current thread busy: 4 Keep alive sockets count: 24
Max processing time: 2290247 ms Processing time: 2051071.2 s Request count: 70904137 Error count: 533477 Bytes received: 102431.25 MB Bytes sent: 72495.65 MB
```

**f) **正则表达式:****

**由于灾难性的回溯，正则表达式有时花费太多时间。您可以首先在应用程序中监控正则表达式匹配的执行时间。如果你发现它过分使用[https://regex101.com](https://regex101.com)找到幕后正则表达式匹配。**

**虽然我不建议这样做，但有时取消长时间运行的正则表达式是更好的选择。在这里 查看 Stackoverflow 上提到的在规定时间 [**后取消操作的方法。**](https://stackoverflow.com/questions/910740/cancelling-a-long-running-regex-match)**

**g) **内存/缓存问题:****

**总是缓存经常使用并且在一段时间内变化不大的内容，不要缓存所有内容。始终定期记录缓存的统计信息，即缓存中的条目数、缓存占用的内存等，以便您了解使用了多少内存，并帮助避免内存不足错误。**

****其他问题:****

**文件编码:**

**Windows 和 Unix 有不同的文件编码，很多时候它们会导致问题。例如，Windows 使用 CRLF 行结束符，而 Unix 只使用 LF 行结束符。**

**你可以在这里阅读更多关于这个[](https://www.networkworld.com/article/3107972/linux/windows-vs-unix-those-pesky-line-terminators.html)**。****

****没有什么可以打败远程调试(如果规模不是问题)，如果您被允许远程调试部署在生产环境中的应用程序，您可以遵循下面提到的步骤:****

****[](https://stackify.com/java-remote-debugging/) [## 真实世界中的 Java 远程调试实用指南

### 对远程服务器上的问题进行故障排除，尤其是在生产环境中，并不是一件容易的事情。有时它涉及…

stackify.com](https://stackify.com/java-remote-debugging/)**** 

****本文是基于我多年来在基于 Java 的企业应用程序上积累的经验。可能有更多的调试步骤，更多的工具等，上面的编译是一个小的检查列表，它可能不是一个全面的列表，因为每个应用程序在设计方面都不同，一些应用程序占用内存，一些 IO 或一些 CPU 等。****

****我已经排除了记录到日志文件中的调试异常，因为根据错误发生的行号，它们更容易被发现(对于开发人员来说)。希望有帮助。****

****有问题吗？建议？评论？****

****下一步是什么？ [**在 Medium 上关注我**](https://medium.com/@vaibhav0109) 成为第一个阅读我故事的人。****