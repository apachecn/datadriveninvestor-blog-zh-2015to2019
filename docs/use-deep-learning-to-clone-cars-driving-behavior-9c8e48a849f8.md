# 利用深度学习克隆汽车驾驶行为

> 原文：<https://medium.datadriveninvestor.com/use-deep-learning-to-clone-cars-driving-behavior-9c8e48a849f8?source=collection_archive---------16----------------------->

![](img/5892771ef29e1d01c477c16633e4eea8.png)

Autonomous Driving

# 目标

*   使用模拟器收集良好驾驶行为的数据。Udacity 提供了一个模拟器应用程序，我们可以在这个程序中驾驶汽车在赛道上行驶来收集数据。收集的数据包括从汽车的一组摄像头捕获的图像数据以及转向角度
*   在 Keras 中构建卷积神经网络，从图像中预测转向角度
*   使用训练和验证集训练和验证模型
*   测试模型在不离开道路的情况下绕轨道 1 成功行驶

# 模型架构

## 1.采用了适当的模型架构

我的模型由一个卷积神经网络组成，具有 3x3 的滤波器大小和 32 到 128 之间的深度(model.py 第 18-24 行)

该模型包括卷积神经网络(CNN)，我最初的方法是使用 [LeNet](http://yann.lecun.com/exdb/lenet/) ，但很难让汽车在街上行驶三个时期(该模型可以在这里找到)。在这之后，我决定尝试一下 [nVidia 自动驾驶汽车集团](https://devblogs.nvidia.com/parallelforall/deep-learning-self-driving-cars/)的车型，这辆车在仅仅三个训练时期后就行驶了完整的第一条赛道(这款车型可以在这里找到)。

## 2.试图减少模型中的过度拟合

我决定不通过应用正则化技术(如退出)来修改模型。相反，我决定保持低的训练周期:只有三个周期。除此之外，我还将样本数据分为训练数据和验证数据。使用 80%作为训练，20%作为验证。

## 3.模型参数调整

该模型使用了 Adam 优化器，因此学习率不是手动调整的( [model.py line 146](https://github.com/manisaiprasad/CarND-Behavioral-Cloning/blob/master/model.py#L146) )。

## 4.适当的培训数据

选择训练数据以保持车辆在道路上行驶。我使用了中央车道驾驶的组合，从道路的左侧和右侧恢复…

有关我如何创建训练数据的详细信息，请参见下一节。

# 培训策略

## 1.解决方案设计方法

衍生模型架构的总体策略

我的第一步是用三个纪元和 Udacity 提供的训练数据来尝试 LeNet](【http://yann.lecun.com/exdb/lenet/】)模型。在第一条赛道上，赛车直奔湖边。我需要做一些预处理。引入了一个[新的](https://github.com/manisaiprasad/CarND-Behavioral-Cloning/blob/master/model.py#L104) `Lambda`层，将输入图像归一化为零均值。这一步可以让赛车移动得更远一点，但它没有到达第一个弯道。又推出了一个`Cropping` [层](https://github.com/manisaiprasad/CarND-Behavioral-Cloning/blob/master/model.py#L105)，第一个转弯差不多了，但还不太。

第二步是使用一个更强大的模型: [nVidia 自主汽车集团](https://devblogs.nvidia.com/parallelforall/deep-learning-self-driving-cars/)唯一的修改是在末尾添加一个新层，以便根据需要有一个单独的输出。这一次赛车完成了它的第一条完整的赛道，但是在赛道上有一个地方它越过了虚线。需要更多的数据。通过添加以负角度翻转的相同图像来扩充数据([第 85–87 行](https://github.com/manisaiprasad/CarND-Behavioral-Cloning/blob/master/model.py#L85-L87))。除此之外，左侧和右侧摄像机图像引入了角度修正系数，以帮助汽车返回车道([第 50–63 行](https://github.com/manisaiprasad/CarND-Behavioral-Cloning/blob/master/model.py#L50-L63))。经过这个过程，汽车继续有同样的问题，同样的“虚线”。我需要更多的数据，但这是一个好的开始。

## 2.创建培训集和培训流程

为了获得更多数据，采集了以下轨迹:

*   第一首歌。
*   一条铁轨向前行驶。
*   一条轨道向后行驶。
*   三秒钟赛道向前行驶。

所有这些数据都用于训练具有三个时期的模型。数据被随机打乱。

训练结束后，赛车一直在第一[和第二](https://youtu.be/naBuIa3N734)赛道上行驶。

# 自动驾驶测试

这是在 1 号赛道成功骑行的视频

Track 1

Desktop Capture of Track 1 Test

这是在 2 号跑道成功骑行的视频

Track 2

# 存储库(GitHub)

项目的最终内容可以在我在 Github 的[个人存储库中找到。](https://github.com/manisaiprasad/CarND-Behavioral-Cloning)

*   `model.py`:读取数据集、创建 CNN 模型并对其进行训练的源代码。
*   `drive.py`:将训练好的模型反馈给模拟器的源代码。也用于保存模拟生成的帧。
*   `video.py`:将`drive.py`生成的帧转换成 MP4 视频的程序。
*   `model.h5`:用于赛道驾驶的最终训练模型
*   `video.mp4`:由`video.py`生成的轨道 1 模拟视频。
*   `video_second_track.mp4`由`video.py`生成的轨道 1 模拟视频。