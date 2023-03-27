# TensorFlow 内部构件。如何从源代码构建 TensorFlow 以供开发和使用

> 原文：<https://medium.datadriveninvestor.com/tensorflow-internals-how-to-build-tensorflow-from-source-for-development-and-usage-855792a312e0?source=collection_archive---------0----------------------->

![](img/d31caf5c9c6abc9ee67856f04daba6f7.png)

Photo by [Lewis Ngugi](https://unsplash.com/@ngeshlew?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我想告诉你一个很长的故事，关于我如何尝试在开发模式下构建 TensorFlow 并安装在一个系统上。我刚刚完成，并准备在未来几天深入研究代码。我粗略地看了一下代码，我惊讶于它是如此的井井有条。与 PyTorch codebase 相比，这是一种真正的阅读乐趣，虽然我是 py torch code base 的忠实粉丝。但是构建 TensorFlow 并不简单。你不可能从 TensorFlow [documentation](https://www.tensorflow.org/install/source) 就能准备好一切，对于那些苦苦挣扎的人，这里有相当粗鲁的回答。

也许这是我在 discuss.pytorch.org 的经历后的偏见，在那里你几乎可以得到所有问题的答案。尽管我提到脸书团队在回避 PyTorch 内部问题。

在我的旅途中，我遇到了一些在工作场所匆匆忙忙的人，他们非常需要建立 TensorFlow 和来自经验丰富的专业人士的零答案。但是我强烈建议仔细阅读 TensorFlow [文档](https://www.tensorflow.org/install/source)，注意细节。尤其是 GCC 版和 Bazel 版。

根据文档，Bazel 是一个真正的构建管道突破，但享受它的人可能是谷歌员工，他们在为内部使用做一些事情。它不是面向大众的产品。另一个魅力是 Google [Kythe](https://kythe.io/) 应该生成`compile_commands.json`来遍历代码。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

五天的快乐时光，我终于得到了我需要的一切。这个哲学介绍，因为我仍然处于震惊之中，我直接从我的灵魂里面自动输入。

**构建张量流的步骤**

下面的代码是为基于 Debian 的操作系统提供的。

1.  创建 conda 环境并激活它:

```
conda create -n tensorflow python=3.7
conda activate tensorflow
```

2.安装依赖项:

```
sudo apt install python-devconda install pip six numpy wheel setuptools mock 'future>=0.17.1pip install -U pip install -U keras_applications --no-deps
pip install -U keras_preprocessing --no-deps
```

3.克隆 git 仓库:

```
git clone https://github.com/tensorflow/tensorflow.git
```

4.如果你想要最新最好的，或者检查你所需要的，在[https://github.com/tensorflow/tensorflow/](https://github.com/tensorflow/tensorflow/)上检查你的操作系统最近的构建版本:

```
git checkout r2.0     # as an example checking out version 2.0
```

5.检查您的 GCC 版本。[文档](https://www.tensorflow.org/install/source)是关于您需要什么版本的参考。如果需要，更新您的 GCC[https://gcc.gnu.org/](https://gcc.gnu.org/)。我试用了最新的 9.2 版本，它正在编译 TensorFlow。

6.检查你的巴泽尔版本。关于 Bazel 的正确版本，请查阅[文档](https://www.tensorflow.org/install/source)。不要安装最新版本的 Bazel。构建张量流只需要特定的版本。你可以在这里下载 Bazel。

7.检查您的`libstdc++.so`版本。它应该有 GLIBCXX_3.4.26。您可以在您的系统中搜索`libstdc++.so.6`,然后检查文件中的每个版本:

```
strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBC
```

然后:

```
export LD_LIBRARY_PATH=/usr/local/lib64     # path to libstdc++.so.6
```

> 注意:如果你需要`compile_commands.json`遍历代码并使用你的 IDE 的智能感知，使用这个 repo:[https://github.com/vincent-picaud/Bazel_and_CompileCommands](https://github.com/vincent-picaud/Bazel_and_CompileCommands)。将资源库中的文件放入 TensorFlow 资源库文件夹的根目录，然后`./setup_compile_commands.sh`建筑本身就是`./create_compile_commands.sh //tensorflow/tools/pip_package:build_pip_package`。这还没有结束。在我的机器上，智能感知无法工作，所以我写了这个脚本来重命名`compile_commands.json`中的路径。根据您的情况修改 python 脚本:

```
import json
import os
json_file = open('compile_commands.json')
content = json.loads(json_file.read())
content[1]['file']
for line in content:
    if line['file'][:8] == 'external':
        line['file'] = '/var/lib/jenkins/workspace/tensoflow/third-party/' + line['file'][9:]
    elif line['file'][:10] == 'tensorflow':
        line['file'] = '/var/lib/jenkins/workspace/tensoflow/' + line['file']
    else:
        line['file'] = '/var/lib/jenkins/workspace/tensoflow/' + line['file']
        print(line['file'])
if not os.path.exists('ready_to_move_to_tensorflow'):
    os.mkdir('ready_to_move_to_tensorflow')
filename = os.path.join('ready_to_move_to_tensorflow', 'compile_commands.json')
json.dump(content, open(filename, 'w'))
```

> 主要问题是 JSON `file`属性没有完整的路径或者指向在构建过程中被删除的目录。

8.按照说明书就可以了:

```
./configurebazel build //tensorflow/tools/pip_package:build_pip_package
```

9.通过 pip 创建要安装的轮子:

```
./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

10.Pip 安装一个车轮文件:

```
pip install /tmp/tensorflow_pkg/tensorflow-**version**-**tags**.whl
```

指令 8、9 和 10 取自[https://www.tensorflow.org/install/source](https://www.tensorflow.org/install/source)。

> 注意:如果`import tensorflow`给出错误:
> 
> import error:/lib/x86 _ 64-Linux-GNU/libstdc++ . so . 6:找不到版本“CXXABI_1.3.11 ”(需要由/home/andreiliphd/anaconda 3/envs/tensor flow/lib/python 3.7/site-packages/tensor flow _ core/python/../libtensorflow_framework.so.2)
> 
> 我们的老朋友会帮忙的:
> 
> 将 LD _ LIBRARY _ PATH =/usr/local/lib 64 #路径导出到 libstdc++.so.6

可以考虑加到`~/.bashrc`里，避免每次需要的时候都要打字。