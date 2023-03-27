# Python 中 Oozie 协调员工作的诀窍

> 原文：<https://medium.datadriveninvestor.com/recipe-for-a-oozie-coordinator-job-with-python-ee2da73cae22?source=collection_archive---------2----------------------->

![](img/ba4245ff6f86351fef18c1737ea91d75.png)

Another day at the workstation!

本文包含一个简短的教程，介绍如何用 Apache Oozie 设置一个递归 Python 脚本。Oozie 是 Apache Hadoop 的一个工作流调度器，它允许你定义和调度两种类型的作业:独立的“工作流”作业，它将在被明确触发时运行，以及“协调者”作业，它被设置为以定义的时间间隔运行——想想 [cron 作业](https://en.wikipedia.org/wiki/Cron),但是高度可用。注意，虽然 Oozie 没有明确支持 Python，但它支持[外壳动作](https://oozie.apache.org/docs/3.3.1/DG_ShellActionExtension.html)，这给了我们一个运行 Python 脚本的便捷方法。

**请注意，本教程假设您已经在集群上运行了 Oozie。**

[](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) [## 为什么数据将改变投资管理|数据驱动的投资者

### 有人称之为“新石油”虽然它与黑金没有什么相似之处，但它的不断商品化…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) 

我们这里的小脚本不会做太多事情——我将 Python 脚本功能的扩展留给读者作为练习！它应该让您了解如何搭建脚手架来重复运行脚本

1.  访问您的 Python 环境，
2.  从属性文件中接受参数，并
3.  以用户定义的时间间隔运行。

在本例中，Python 脚本将每隔 15 分钟简单地将“我住在旧金山”输出到 stdout(可以在 MapReduce 日志中找到)。它将城市作为一个包含在属性文件中的参数——这样，如果你想在将来逃到更便宜的地方，你可以很容易地更新你的位置…

事不宜迟，下面是设置和运行 Oozie coordinator Python 作业的方法:

# 佐料

1*coordinator . properties*—对于独立的“工作流”作业，该文件将被替换为“job.properties”。但是因为我们希望作业重复运行，所以我们需要 coordinator.properties 定义的额外参数。在这个文件中，您将定义集群配置和 HDFS 位置，并设置时间间隔变量。这里有一个例子:

```
oozie.coord.application.path=hdfs://[your-cluster-nameNode]/user/hdfs/hdfs_oozie
queueName=default
nameNode=hdfs://[your-cluster-nameNode]
startTime=2019-09-06T00:00Z
endTime=2019-10-06T00:00Z
jobTracker=[your-YARN-host]:8050
workflowPath=hdfs://[your-cluster-nameNode]/user/hdfs/hdfs_oozie
myCity=SanFrancisco
```

**注意:**最好在 nameNode 空间中使用集群的逻辑名称，以免在故障转移时出现名称节点切换时失去功能！

“startTime”和“endTime”字段分别定义了脚本的第一个实例运行到截止日期的时间。注意 Oozie 区分了“实际”和“名义”时间。当你设置每 15 分钟运行一次时，标称时间将正好是你的开始时间之后的每 15 分钟间隔——但是如果出现延迟，实际执行的*时间和*时间可能不同。Oozie UI 记录了 shell 操作的名义和实际执行时间。

1 *coordinator.xml* —同样，这是一个文件，它定义了协调器特定于作业的变量，并按照定义的时间间隔循环设置作业的执行。这里有一个例子:

```
<coordinator-app name="whatsmyCity" frequency="${coord:minutes(15)}" start="${startTime}" end="${endTime}" timezone ="GMT" >
<action>
      <workflow>
         <app-path>/user/hdfs/hdfs_oozie/workflow.xml</app-path>
      </workflow>
</action>
</coordinator-app>
```

您可以在 frequency 字段中设置您的时间间隔——在本例中，它被设置为每 15 分钟运行一次`{coord:minutes(15}`,但是您可以使用指南[在这里](https://oozie.apache.org/docs/3.1.3-incubating/CoordinatorFunctionalSpec.html#a4.4._Frequency_and_Time-Period_Representation)将其修改为您想要的任何粒度。注意，app-path 指向一个 *workflow.xml* 文件。虽然 *coordinator.xml* 文件包含重复运行您的工作的脚手架，但是 *workflow.xml* 文件包含应用程序本身的真正内容。

1 *workflow.xml* —该文件将为您的作业定义工作流和关键参数以及可执行文件。下面是我们的一个例子:

```
<workflow-app  name="my-python-wf">
    <start to="shell-node"/>
    <action name="shell-node">
        <shell >
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
                <property>
                    <name>mapred.job.queue.name</name>
                    <value>${queueName}</value>
                </property>
            </configuration>
            <exec>python_file.py</exec>
         <argument>${myCity}</argument>
       <file>${nameNode}/user/hdfs/hdfs_oozie/python_file.py</file>
        </shell>
        <ok to="end"/>
        <error to="fail"/>
    </action>
    <kill name="fail">
        <message>Shell action failed, error message[${wf:errorMessage(wf:lastErrorNode())}]</message>
    </kill>
    <end name="end"/>
</workflow-app>
```

注意，这里的“exec”字段指的是我们的(巧妙命名的)Python 文件 *python_file.py.* 这是您实际上想要每 15 分钟运行一次的脚本。“参数”字段从 *coordinator.properties* 文件传入我们的变量“myCity ”,该变量将作为系统参数传递给 Python 文件。

1 *python_file.py* —这是您希望重复执行的 python 脚本。记得在脚本文件的开头加上一个 shebang(！)指的是您的 Python 发行版或微型环境的位置。这里有一个例子，引用在 *workflow.xml* 文件中定义为“我的城市”的系统参数值:

```
#! /usr/bin/env pythonimport sysmy_city = sys.argv[1]
print("I live in {}".format(my_city))
```

这将每十五分钟向 stdout 发布一次定义好的语句(可能是史上最无聊的应用？)

# 方向

现在，您已经准备好了您的配料，请遵循以下说明:

1.  导航到集群上您最喜欢的节点，为您的 Oozie 项目创建一个专用目录，例如 */home/user/oozie_tests* 。
2.  切换到用户“hdfs”。你需要在这里与 HDFS 互动，这样 Oozie 才能访问这些文件。
3.  将所有四个文件放入新的本地目录 */home/user/oozie_tests*
4.  现在，您需要将一些文件推到一个特定的 HDFS 位置。**记得将文件推送到您在上面的 workflow.xml 文件中指定的 HDFS 位置！**(本例中称为*/用户/hdfs/hdfs_oozie* )。您可以使用以下命令来实现这一点:

```
hdfs dfs -put [your_file_name_here] /user/hdfs/hdfs_oozie/
```

对三个文件重复上述操作: *workflow.xml、coordinator.xml、*和 *python_file.py* 。

5.一旦这三个文件都在 HDFS，您就可以用下面的命令启动 Oozie 作业:

```
oozie job -oozie [oozie_host]:11000/oozie -config coordinator.properties -run
```

这应该会返回一个 Oozie 作业 ID。现在，您可以在 Oozie UI 中检查您的作业状态。

就是这样！如果你遇到任何问题或者任何步骤需要进一步澄清，请在评论中告诉我。协调愉快！

 [## 梅根·麦克拉蒂(@outsideline) * Instagram 照片和视频

### 650 个关注者，629 个关注者，566 个帖子——参见来自 Megan mccarty(@ outside line)的 Instagram 照片和视频

www.instagram.com](https://www.instagram.com/outsideline/)