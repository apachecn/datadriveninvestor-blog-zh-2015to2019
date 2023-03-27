# 将 PyTorch 模型部署到生产环境中

> 原文：<https://medium.datadriveninvestor.com/deploy-your-pytorch-model-to-production-f69460192217?source=collection_archive---------0----------------------->

继上一篇关于[用 PyTorch 和 Google Colab 训练 Choripan 分类器](https://medium.com/@nicolas.metallo/train-a-choripan-classifier-with-fast-ai-v1-in-google-colab-6e438817656a)的文章之后，我们现在将讨论如果您想要将您最近训练的模型部署为 API，您可以做哪些步骤。关于如何用 Fast.ai 做到这一点的讨论目前正在进行中，并且很可能会持续到 PyTorch 发布正式的 1.0 版本。您可以在 Fast.ai 论坛、PyTorch 文档/论坛及其各自的 GitHub 资源库中找到更多信息。

# 保存和加载模型

建议您看一下 [PyTorch 文档](https://pytorch.org/tutorials/beginner/saving_loading_models.html)，因为这是一个很好的起点，但是简而言之，有两种方法可以序列化和恢复模型。一种是只加载权重，另一种是加载整个模型(和权重)。您将需要首先创建一个模型来定义它的架构，否则您将得到一个只有权重值的`OrderedDict`。这两个选项都适用于推断和/或从先前的检查点恢复模型的训练。

## 1.使用`torch.save()`和`torch.load()`

这个保存/加载过程使用最直观的语法，涉及的代码最少。以这种方式保存模型将使用 Python 的 [pickle](https://docs.python.org/3/library/pickle.html) 模块保存整个模块。这种方法的缺点是序列化数据被绑定到特定的类和保存模型时使用的确切目录结构。之所以这样，是因为 pickle 本身并不保存模型类。相反，它保存了包含该类的文件的路径，该路径在加载时使用。因此，当在其他项目中使用或重构后，您的代码可能会以各种方式中断。

**保存模型**

```
torch.save(learner.model, PATH)
```

有时`pickle`不能序列化一些模型创建函数(例如`resnext_50_32x4d`，在 Fastai 的以前版本中可以找到)，所以你需要使用`dill`来代替。解决方法如下。

```
import dill as dill
torch.save(learner.model, PATH, pickle_module=dill)
```

你可以在这篇[文章](%5Bhttps://medium.com/@jwnx/multiprocessing-serialization-in-python-with-pickle-9844f6fa1812%209%5D(https://medium.com/@jwnx/multiprocessing-serialization-in-python-with-pickle-9844f6fa1812))中读到更多关于`pickle`的局限性。一个常见的 PyTorch 惯例是使用`.pt`或`.pth`文件扩展名保存模型。

**负载模型**

```
# Model class must be defined somewhere
model = torch.load(PATH)
model.eval()
```

## 2.使用`state_dict`

在 PyTorch 中，`torch.nn.Module`模型的可学习参数(如权重和偏差)包含在模型的*参数*(通过`model.parameters()`访问)中。一个 *state_dict* 只是一个 Python 字典对象，它将每个层映射到它的参数张量。请注意，只有具有可学习参数的层(卷积层、线性层等。)在模型的 *state_dict* 中有条目。

我们需要以保存权重时最初定义和创建模型的相同方式重新初始化我们的模型，确保用于创建模型的变量、类和函数可用，无论是通过模块导入还是直接在同一个脚本/文件中。使用这种方法的一个潜在优势是，如果参数相同，您可以使用更新的脚本来加载旧模型，这也是官方文档推荐的[方法。你还应该记住的一点是，`state_dict`接受一个字典对象，而不是一个保存对象的路径，所以你不能使用`model.load_state_dict(PATH)`加载。](https://pytorch.org/docs/master/notes/serialization.html)

**保存模型**

```
torch.save(model.state_dict(), PATH)
```

**负荷模型**

```
model = TheModelClass(*args, **kwargs) # Model class must be defined somewhere
model.load_state_dict(torch.load(PATH))
model.eval() # run if you only want to use it for inference
```

您在加载后运行`model.eval()`，因为您通常有`BatchNorm`和`Dropout`层，默认情况下它们在构建时处于训练模式。如果你想恢复你的模型训练，你不需要呼叫`model.eval()`。

由于我们已经用 Fastai 完成了我们的训练，我们可以调用`[Learner.save](https://docs.fast.ai/basic_train.html#Learner.save)`和`[Learner.load](https://docs.fast.ai/basic_train.html#Learner.load)`来保存和加载模型(更多信息在[文档](https://docs.fast.ai/basic_train.html#Saving-and-loading-models))。这是在后台运行`state_dict()`，所以只有模型参数将被保存，而不是架构。这意味着您将需要运行 create_cnn 方法来从给定的体系结构(与您之前用来训练您的模型的体系结构相同，例如 *models.resnet34* )中获得一个预训练模型，该模型具有适合您的数据的自定义头。从`path` / `model_dir`目录保存和加载模型，并自动为两个操作添加`.pth`扩展名。

# 使用烧瓶进行简单部署

在我们使用 Google Colab 中的免费 GPU 训练了我们的分类器之后，我们就可以在自己的终端进行推理了。我们可以在本地或云中完成，有许多不同的选项(AWS、Paperspace、Google Cloud 等)可供我们选择。因为我还有一些免费的 Amazon AWS 信用，所以我将使用 Amazon AMI，它带有几个已经安装在 t2.medium 实例上的 ML 库。这里有一些在你的终端上运行 Docker 镜像的简单说明(当我们不做 GPU 训练时应该差不多)。

## 准备运行的 Docker 图像

Jupyter Docker 书库是一种很好的方式，可以让笔记本立即进入最新的图书馆。这些是现成的 Docker 映像，包含 Jupyter 应用程序和交互式计算工具。在[官方文档](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-datascience-notebook)中了解更多信息。我们将使用[这个存储库](https://github.com/jupyter/docker-stacks)中的 **Jupyter 笔记本数据科学堆栈**。

一旦你安装了[Docker，打开终端，`cd`进入你的工作目录，然后运行](https://docs.docker.com/install/)

```
$ docker run --rm -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work jupyter/datascience-notebook:e5c5a7d3e52d
```

这将创建一个服务器，您可以登录到该服务器并连接到 Jupyter 笔记本。您可以直接从那里运行一些命令，也可以通过获取`container id`，在终端中键入`docker ps`，然后运行来运行 bash 或 Docker 容器中的任何命令

```
$ docker exec -it {container-id} /bin/bash
```

## 安装 PyTorch & [Fastai](https://github.com/fastai/fastai)

根据您的机器配置，您可能希望在 GPU 或 CPU 上运行推理。在我们的例子中，我们将在 CPU 上运行所有的东西，所以您需要运行以下命令来安装最新的 [PyTorch](https://pytorch.org/) 。

```
pip install torch_nightly -f [https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html](https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html) 
```

现在你可以用`pip install fastai`安装 Fastai 了

## 创建一个烧瓶应用程序

通过运行以下命令安装烧瓶库

```
pip install -U flask
```

我们将创建一个名为`flask_app`的文件夹和两个新的 python 文件`server.py`，其中包含加载模型权重和运行推理服务器的代码，以及设置一些基本参数的`settings.py`，以便在将来为我们提供更多的灵活性。下面是一个关于`flask_app/settings.py`的例子。然后我们将用`from settings import *`将它导入到`server.py`中。

```
# add your custom labels
labels = ['Not Choripan', 'Choripan']
​
# set your data directory
data_dir = 'data'
​
# set the URL where you can download your model weights
MODEL_URL = 'https://s3.amazonaws.com/nicolas-dataset/stage1.pth' # example weights
​
# set some deployment settings
PORT = 8080
```

我们现在可以通过`flask_app/server.py`。第一部分将导入库和设置。

```
# flask_app/server.py
​
# import libraries
print('importing libraries...')
from flask import Flask, request, jsonify
import logging
import random
import time
​
from PIL import Image
import requests, os
from io import BytesIO
​
# import fastai stuff
from fastai import *
from fastai.vision import *
import fastai
​
# import settings
from settings import * # import 
​
print('done!\nsetting up the directories and the model structure...')
```

为了运行我们的单一图像推断预测，我们首先需要创建一个新模型，该模型遵循我们训练它时使用的相同文件夹结构。这就是为什么我们要基于之前在`settings.py`中设置的标签创建一个新的空目录。

```
# set dir structure
def make_dirs(labels, data_dir):
    root_dir = os.getcwd()
    make_dirs = ['train', 'valid', 'test']
    for n in make_dirs:
        name = os.path.join(root_dir, data_dir, n)
        for each in labels:
            os.makedirs(os.path.join(name, each), exist_ok=True)
​
make_dirs(labels=labels, data_dir=data_dir) # comes from settings.py
path = Path(data_dir)
```

一旦定义了`path`，我们将创建一个新的`learn`模型，并为 [Choripan 分类器](https://medium.com/@nicolas.metallo/train-a-choripan-classifier-with-fast-ai-v1-in-google-colab-6e438817656a)下载预先训练好的权重。

```
# download model weights if not already saved
path_to_model = os.path.join(data_dir, 'models', 'model.pth')
if not os.path.exists(path_to_model):
    print('done!\nmodel weights were not found, downloading them...')
    os.makedirs(os.path.join(data_dir, 'models'), exist_ok=True)
    filename = Path(path_to_model)
    r = requests.get(MODEL_URL)
    filename.write_bytes(r.content)
​
print('done!\nloading up the saved model weights...')
​
fastai.defaults.device = torch.device('cpu') # run inference on cpu
empty_data = ImageDataBunch.single_from_classes(
    path, labels, tfms=get_transforms(), size=224).normalize(imagenet_stats)
learn = create_cnn(empty_data, models.resnet34)
learn = learn.load('model')
```

网上已经有很多很棒的教程[非常详细，所以我不会解释太多 Flask 是如何工作的。我创建了一个`predict`函数，它将您收到的 URL 作为输入，通过`learn.predict(img)`运行它以获得预测的类，然后返回一个`json`。](http://flask.pocoo.org/)

```
print('done!\nlaunching the server...')
​
# set flask params
​
app = Flask(__name__)
​
@app.route("/")
def hello():
    return "Image classification example\n"
​
@app.route('/predict', methods=['GET'])
def predict():
​
    url = request.args['url']
    app.logger.info("Classifying image %s" % (url),)

    response = requests.get(url)
    img = open_image(BytesIO(response.content))
​
    t = time.time() # get execution time
​
    pred_class, pred_idx, outputs = learn.predict(img)
​
    dt = time.time() - t
    app.logger.info("Execution time: %0.02f seconds" % (dt))
    app.logger.info("Image %s classified as %s" % (url, pred_class))
​
    return jsonify(pred_class)
​
if __name__ == '__main__':
​
    app.run(host="0.0.0.0", debug=True, port=PORT)
​
```

一旦我们完成了这些，我们就可以到终端，cd 到`flask_app`目录，然后运行`python server.py`。我们应该看到这样的东西。

```
* Serving Flask app "server" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on [http://0.0.0.0:8080/](http://0.0.0.0:8080/) (Press CTRL+C to quit)
 * Restarting with stat
importing libraries...
done!
setting up the directories and the model structure...
done!
loading up the saved model weights...
done!
launching the server...
 * Debugger is active!
 * Debugger PIN: 261-786-850
```

**就是这样！**现在我们可以从终端运行这样的命令(我正在运行一个 AWS 实例)。让我们以这张图片为例。

![](img/c11c9af8e440f59472d1ebfccaf977b1.png)

```
$ curl [http://ec2-100-24-34-242.compute-1.amazonaws.com:8080/predict?url=https://media.minutouno.com/adjuntos/150/imagenes/028/853/0028853430.jpg](http://ec2-100-24-34-242.compute-1.amazonaws.com:8080/predict?url=https://media.minutouno.com/adjuntos/150/imagenes/028/853/0028853430.jpg)
"Choripan"
```

这是从服务器端看起来的样子

```
[2018-11-13 16:49:32,245] INFO in server: Classifying image [https://media.minutouno.com/adjuntos/150/imagenes/028/853/0028853430.jpg](https://media.minutouno.com/adjuntos/150/imagenes/028/853/0028853430.jpg)
[2018-11-13 16:49:33,836] INFO in server: Execution time: 1.35 seconds
[2018-11-13 16:49:33,858] INFO in server: Image [https://media.minutouno.com/adjuntos/150/imagenes/028/853/0028853430.jpg](https://media.minutouno.com/adjuntos/150/imagenes/028/853/0028853430.jpg) classified as Choripan
```

**还不错！**您现在有了自己的“chori pan/Not chori pan”API。如果您想进入下一个级别，请查看 Flask 文档中的[本教程](http://flask.pocoo.org/docs/1.0/tutorial/deploy/)以部署到生产环境，和/或[本教程](http://containertutorials.com/docker-compose/flask-simple-app.html)如果您想对 Flask 应用程序进行 docker 化(您也可以使用 [docker-compose](http://containertutorials.com/docker-compose/flask-compose.html) )。

# 部署到生产的其他方式

# 1.使用[裁剪器](http://clipper.ai)的图像分类示例

在 GitHub 的[剪贴教程](%20https://github.com/ucbrise/clipper-tutorials)中有一个很棒的`ipynb`，你可以跟随它学习所有东西是如何工作的。他们提供一个 Docker 图像，或者你可以运行他们的 Amazon AMI。遗憾的是，这仅适用于 PyTorch 0.4.0，当您的模型已经使用 PyTorch 和 Fastai 的最新预览版进行了训练时，要转换到这一版本会非常困难。不过，与示例预训练模型一起使用效果很好。

## 创建 clipper 连接

要启动 Clipper，您必须首先用您想要使用的`ContainerManager`类型创建一个`[ClipperConnection](http://docs.clipper.ai/en/develop/#clipper-connection)`对象。在这种情况下，您将使用`DockerContainerManager`。

```
from clipper_admin import ClipperConnection, DockerContainerManager
clipper_conn = ClipperConnection(DockerContainerManager())
```

## 起动削波器

现在您已经有了一个`ClipperConnection`对象，您可以启动一个裁剪器集群。

以下命令将启动 3 个 Docker 容器:

1.  查询前端:查询前端容器监听传入的预测请求，并将它们调度和路由到已部署的模型。
2.  管理前端:管理前端容器管理和更新集群的内部配置状态，比如跟踪部署了哪些模型，注册了哪些应用程序端点。
3.  Redis 实例:Redis 用于持久存储 Clipper 的内部配置状态。默认情况下，Redis 在端口 6380 上启动，而不是在标准的 Redis 默认端口 6379 上启动，以避免与任何已经运行的 Redis 实例发生冲突。

```
clipper_conn.start_clipper()
clipper_addr = clipper_conn.get_query_addr()
```

快船已经开始看集装箱了。

```
!docker ps --filter label=ai.clipper.container.label
```

## 创建应用程序

```
app_name = "squeezenet-classsifier"
default_output = "default"
​
clipper_conn.register_application(
    name=app_name,
    input_type="bytes",
    default_output=default_output,
    slo_micros=10000000)
```

当您列出向 Clipper 注册的应用程序时，您应该会看到新注册的`squeezenet-classifier`应用程序出现。

```
clipper_conn.get_all_apps()
```

## 加载预训练 PyTorch 模型示例

```
from torchvision import models, transforms
model = models.squeezenet1_1(pretrained=True)
```

PyTorch 模型不能只是腌制和装载。相反，必须使用 PyTorch 的本机序列化 API 保存它们。因此，您不能使用通用 Python 模型部署器将模型部署到 Clipper。相反，您将使用 Clipper PyTorch 部署器来部署它。当容器启动时，Docker 容器将从序列化的模型检查点加载并重建模型。

## 预处理

```
# First we define the preproccessing on the images:
normalize = transforms.Normalize(
   mean=[0.485, 0.456, 0.406],
   std=[0.229, 0.224, 0.225]
)
preprocess = transforms.Compose([
   transforms.Scale(256),
   transforms.CenterCrop(224),
   transforms.ToTensor(),
   normalize
])
​
# Then we download the labels:
labels = {int(key):value for (key, value)
          in requests.get('https://s3.amazonaws.com/outcome-blog/imagenet/labels.json').json().items()}
```

## 定义预测函数并添加指标

```
import clipper_admin.metrics as metrics
​
def predict_torch_model(model, imgs):
    import io
    import PIL.Image
    import torch
    import clipper_admin.metrics as metrics

    metrics.add_metric("batch_size", 'Gauge', 'Batch size passed to PyTorch predict function.')
    metrics.report_metric('batch_size', len(imgs)) # TODO: Fill in the batch size

    # We first prepare a batch from `imgs`
    img_tensors = []
    for img in imgs:
        img_tensor = preprocess(PIL.Image.open(io.BytesIO(img)))
        img_tensor.unsqueeze_(0)
        img_tensors.append(img_tensor)
    img_batch = torch.cat(img_tensors)

    # We perform a forward pass
    with torch.no_grad():
        model_output = model(img_batch)

    # Parse Result
    img_labels = [labels[out.data.numpy().argmax()] for out in model_output]

    return img_labels
```

Clipper 必须从互联网上下载此 Docker 图像，因此这可能需要一分钟的时间

```
from clipper_admin.deployers import pytorch as pytorch_deployer
pytorch_deployer.deploy_pytorch_model(
    clipper_conn,
    name="pytorch-model",
    version=1, 
    input_type="bytes", 
    func=predict_torch_model, # predict function wrapper
    pytorch_model=model, # pass model to function
)
```

现在将生成的`pytorch-model`链接到我们之前创建的应用程序`squeezenet-classsifier`。

```
clipper_conn.link_model_to_app(app_name="squeezenet-classsifier", model_name="pytorch-model")
```

**就是这样！**

## 如何用请求查询 API

```
import requests
import json
import base64
​
clipper_addr = 'localhost:1337'
​
for img in ['img1.jpg', 'img2.jpg', 'img3.jpg']: # example with local images
  req_json = json.dumps({
          "input":
          base64.b64encode(open(img, "rb").read()).decode() # bytes to unicode
      })
​
  response = requests.post(
           "http://%s/%s/predict" % (clipper_addr, 'squeezenet-classsifier'),
           headers={"Content-type": "application/json"},
           data=req_json)

  print(response.json())
```

## 停止削波器

如果您遇到问题，并且想要完全停止 Clipper，您可以通过调用`[ClipperConnection.stop_all()](http://docs.clipper.ai/en/latest/#clipper_admin.ClipperConnection.stop_all)`来完成。

```
clipper_conn.stop_all()
```

当您最后一次列出所有 Docker 容器时，您应该看到所有的 Clipper 容器都已经停止。

```
!docker ps --filter label=ai.clipper.container.label
```

# 2.使用来自 Zeit 的 Now

论坛中讨论的另一个选择是使用来自 [Zeit](https://zeit.co/) 的 [Now](https://zeit.co/now) 服务。你可以按照 Fast.ai 文档中的[这个指南](https://course-v3.fast.ai/deployment_zeit.html)。我已经试过了，但没有得到准确的结果(可能是因为标准化)。似乎很有希望。

您只需要运行这些命令一次。第一个安装 Now 的 CLI(命令行界面)。

```
sudo apt install npm # if not already installed
sudo npm install -g now
```

接下来下载一个 **starter pack** 用于基于 Fast.ai 第二课的模型部署。

```
wget [https://github.com/fastai/course-v3/raw/master/docs/production/zeit.tgz](https://github.com/fastai/course-v3/raw/master/docs/production/zeit.tgz)
tar xf zeit.tgz
cd zeit
```

## 上传您的训练模型文件

将你训练好的模型文件(例如`stage-2.pth`)上传到 Google Drive 或 Dropbox 等云服务。复制文件的下载链接。**注意:**下载链接是直接开始文件下载的链接，通常不同于向您展示下载文件的共享链接(如果需要，使用[https://rawdownload.now.sh/](https://rawdownload.now.sh/))

## 为您的模型定制应用程序

1.  打开`app`目录中的文件`server.py`，用上面复制的 url 更新`model_file_url`变量
2.  在同一个文件中，用您期望从模型中得到的类更新行`classes = ['black', 'grizzly', 'teddys']`

## 部署

在终端上，确保您在`zeit`目录中，然后键入:

```
now
```

第一次运行时，它会提示您输入电子邮件地址并为您创建 Now 帐户。创建帐户后，再次运行它以部署项目。

每次使用`now`进行部署时，它都会为应用程序创建一个唯一的**部署 URL** 。它的格式为`xxx.now.sh`，在您部署应用程序时显示。

# 3.使用`Torch Script`和`PyTorch C++ API`

这些是 PyTorch 官方 1.0 版本的一些最新变化。你可以按照文档中的[这篇](https://pytorch.org/tutorials/advanced/cpp_export.html)文章中的说明，或者查看 Udacity 的 PyTorch 课程的[深度学习介绍的最后一章，在那里他们会一步一步地完成这个过程。这只是主要步骤的概述。](https://classroom.udacity.com/courses/ud188)

```
import torch
import torchvision
​
# An instance of your model.
model = torchvision.models.resnet18()
​
# An example input you would normally provide to your model's forward() method.
example = torch.rand(1, 3, 224, 224)
​
# Use torch.jit.trace to generate a torch.jit.ScriptModule via tracing.
traced_script_module = torch.jit.trace(model, example)
​
# Save the model
traced_script_module.save("model-resnet18-jit.pt")
```

## 构建一个最小的 C++应用程序

*   按照[这些步骤](https://pytorch.org/tutorials/advanced/cpp_export.html)建立`example-app.cpp`和`CMakeLists.txt`。
*   安装 [Anaconda](https://www.anaconda.com/download/) 并让 CMAKE 在你的机器上运行。你可以通过他们的[二进制文件](https://cmake.org/download/)来安装它，或者，如果你运行的是 MacOS，输入`brew install cmake`(安装`homebrew`到[这些](https://brew.sh/)指令)。如果你对 CMAKE 有什么问题，记得直接从[这里](https://developer.apple.com/download/more/)下载 X-Code 命令行工具作为`.dmg`(我这里是 MacOS 10.14)。
*   从[这里](https://caffe2.ai/docs/getting-started.html?platform=mac)安装咖啡 2 并运行`conda install pytorch-nightly-cpu -c pytorch`
*   [构建应用](https://pytorch.org/tutorials/advanced/cpp_export.html)

## PyTorch、Libtorch、C++和 NodeJS

看[http://blog . Christian perone . com/2018/10/py torch-1-0-tracing-JIT-and-lib torch-c-API-to-integrate-py torch-into-nodejs/](http://blog.christianperone.com/2018/10/pytorch-1-0-tracing-jit-and-libtorch-c-api-to-integrate-pytorch-into-nodejs/)

# 结论

我尽力总结了一些可用的选项来部署您最近训练的 PyTorch 模型。希望这是有用的，并期待阅读您的评论。