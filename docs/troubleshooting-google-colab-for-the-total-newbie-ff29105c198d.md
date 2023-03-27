# 为所有新手排除 Google Colab 故障

> 原文：<https://medium.datadriveninvestor.com/troubleshooting-google-colab-for-the-total-newbie-ff29105c198d?source=collection_archive---------2----------------------->

[![](img/798bae060eb43bcc3a0110b7945ae80b.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/1f273e2ece2eed8c4a99be980fa9bcc3.png)

第一次在 Google Colab 中工作非常棒，非常简单，但是也有一些小挑战！我想我应该记录下我所面临的一些问题，以便像我一样的其他新手可以节省一点时间来启动和运行。

如果你对 Jupyter 笔记本有所了解的话，你可以使用 Google Colab，但是有一些小的区别可以让你在自由的 GPU 上自由飞翔和坐在电脑前用头撞墙…

![](img/10547738b38f913b5bb96f7ae486b4dc.png)

Photo by [Gabriel Matula](https://unsplash.com/@gmat07?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对于任何还不知道的人来说，谷歌已经做了有史以来最酷的事情，它提供了基于支持免费 GPU 的 Jupyter 笔记本的免费云服务！这不仅是一个提高你的编码技能的伟大工具，而且它还允许任何人使用流行的库来开发深度学习应用程序，如 **PyTorch** 、 **TensorFlow** 、 **Keras、**和 **OpenCV。**

Colab 提供 GPU，而且完全免费。说真的！

当然，这是有限度的。它支持 **Python 2.7** 和 **3.6** ，但还不支持 **R** 或 **Scala** 。你的会话和大小是有限制的，但是如果你有创造力并且不介意偶尔重新上传你的文件，你肯定可以绕过它…

你可以在 Colab 中创建笔记本，上传笔记本，存储笔记本，共享笔记本，安装你的 Google Drive 并使用你存储在那里的所有东西，导入你最喜欢的目录，上传你的个人 Jupyter 笔记本，直接从 GitHub 上传笔记本，上传 Kaggle 文件，下载你的笔记本，以及做你想做的任何事情。太牛逼了。

我在这里省略了许多“入门”基础知识，只关注一点快速故障排除。有一些很棒的文章是关于如何从头开始的。如果你是 Colab 的新手，我强烈推荐你去看看！([这个](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)可能是我最喜欢的！)

我开始使用 Colab 是作为 Udacity 的脸书 AI PyTorch 奖学金挑战的一部分，所以我的经历肯定是 PyTorch 重，但下面是我迄今为止学到的:

*****更新！(01/29)*** Colab 现在支持原生 PyTorch！！！你不需要运行下面的 torch 代码来导入 Torch，但是我把它保留下来，以防有人有任何问题！**

-如果您想使用 PyTorch，您肯定需要导入 PyTorch！这是一个很好的起点。在任何其他火炬进口之前，你会想跑

```
# [http://pytorch.org/](http://pytorch.org/)
from os.path import exists
from wheel.pep425tags import get_abbr_impl, get_impl_ver, get_abi_tag
platform = '{}{}-{}'.format(get_abbr_impl(), get_impl_ver(), get_abi_tag())
cuda_output = !ldconfig -p|grep cudart.so|sed -e 's/.*\.\([0-9]*\)\.\([0-9]*\)$/cu\1\2/'
accelerator = cuda_output[0] if exists('/dev/nvidia0') else 'cpu'!pip install -q [http://download.pytorch.org/whl/{accelerator}/torch-0.4.1-{platform}-linux_x86_64.whl](http://download.pytorch.org/whl/{accelerator}/torch-0.4.1-{platform}-linux_x86_64.whl) torchvision
import torch
```

然后你就可以继续进口了！

-不能用 import 语句简单地导入您想要的其他内容？尝试 pip 安装！

```
!pip install -q keras
import keras
```

或者:

```
!pip3 install torch torchvision
```

并且:

```
!apt-get install
```

也有用！

-想要安装您的 Google Drive 吗？使用:

```
from google.colab import drive
drive.mount('/content/gdrive')
```

然后你会看到一个链接，点击它，允许访问，复制弹出的代码，粘贴到框中，点击回车，你就可以开始了！如果你没有在左边的边框中看到你的驱动器，只需点击“刷新”,它就会显示出来。

(运行单元，单击链接，复制页面上的代码，将其粘贴到框中，按 enter 键，当您成功安装驱动器时，您会看到这一点):

![](img/9d470e7fbf2d3bd3f746f89ba09861c6.png)

-如果您更愿意下载共享的 zip 文件链接，您可以使用:

```
!wget 
!unzip 
```

例如:

```
!wget -cq [https://s3.amazonaws.com/content.udacity-data.com/courses/nd188/flower_data.zip](https://s3.amazonaws.com/content.udacity-data.com/courses/nd188/flower_data.zip)
!unzip -qq flower_data.zip
```

这将在几秒钟内为您提供 Udacity 的花卉数据集！

如果你上传的是小文件，你可以用一些简单的代码直接上传。然而，如果你愿意，如果你不想运行一些简单的代码来获取一个本地文件，你也可以只去屏幕的左侧，并点击“上传文件”。

![](img/ed0f59cac5a1243e793f8e0116f0900a.png)

谷歌 Colab 在几乎每个层面上都非常容易使用，尤其是如果你对 Jupyter 笔记本非常熟悉的话。然而，抓取一些大文件并让几个特定的目录工作确实让我犯了一两分钟的错误。

-我发现枕头可能有点问题，但你可以通过跑步来解决

```
import PIL
print(PIL.PILLOW_VERSION)
```

如果你得到低于 5.3 的任何东西，进入“运行时”下拉菜单，重启运行时，并再次运行单元。你应该可以走了！

想用 GPU？就像进入“运行时”下拉菜单，选择“更改运行时类型”，在硬件加速器下拉菜单中选择 GPU 一样简单！

![](img/494f862d8bc8e6688a843556388b20fe.png)

然后我喜欢跑步

```
# check if GPU is available
train_on_gpu = torch.cuda.is_available()if not train_on_gpu:
    print('Bummer!  Training on CPU ...')
else:
    print('You are good to go!  Training on GPU ...')
```

只是为了确保它的工作。

这应该足够让你在 GPU 上运行一个大文件了！请让我知道，如果你遇到任何其他的新手问题，我也许可以帮助你。如果可以的话，我很乐意帮助你！

![](img/51194fb089e13ca52b026338c8c3643a.png)

Photo by [Sarah Cervantes](https://unsplash.com/@scaitlin82?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)