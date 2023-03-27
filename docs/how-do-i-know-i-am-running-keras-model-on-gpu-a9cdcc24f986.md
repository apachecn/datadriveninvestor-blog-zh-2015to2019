# 我怎么知道我在 gpu 上运行的是 Keras 模型？

> 原文：<https://medium.datadriveninvestor.com/how-do-i-know-i-am-running-keras-model-on-gpu-a9cdcc24f986?source=collection_archive---------0----------------------->

## ✍Tips 和 Python 中的技巧

![](img/bdde413df3d06c49690fb3078eb30bb8.png)

Photo by [Dave Gandy](http://skuawk.com/) under the [Public Domain Dedication License](https://creativecommons.org/licenses/publicdomain/)

可以在 GPU 上运行 keras 模型。有几件事你必须先检查一下。

1.  你的系统有 GPU (Nvidia。由于 AMD 还不工作)
2.  您已经安装了 tensorflow 的 GPU 版本

要在 anaconda 上安装 tensoflow-gpu:

conda 安装-c anaconda tensorflow-gpu

3.你已经安装了 CUDA [安装说明](https://www.tensorflow.org/install/install_linux)

要在 anaconda 上安装 conda:

conda install-c anaconda cuda toolkit

验证 tensorflow 是否与 GPU 一起运行[检查 GPU 是否工作](https://stackoverflow.com/questions/38009682/how-to-tell-if-tensorflow-is-using-gpu-acceleration-from-inside-python-shell)

`sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))`

运筹学

`from tensorflow.python.client import device_lib`

`print(device_lib.list_local_devices())`

输出将是这样的:

```
[
  name: "/cpu:0"device_type: "CPU",
  name: "/gpu:0"device_type: "GPU"
]
```

所有这些完成后，您的模型将在 GPU 上运行:

要检查 keras(>=2.1.1)是否正在使用 GPU:

```
from keras import backend as K
K.tensorflow_backend._get_available_gpus()
```

例如，如果您在一台拥有 56 个核心 cpu 和一个 gpu 的机器上工作，则需要在导入 keras 后添加以下块。

```
import kerasconfig = tf.ConfigProto( device_count = {'GPU': 1 , 'CPU': 56} ) 
sess = tf.Session(config=config) 
keras.backend.set_session(sess)
```

当然，这种用法强制了我的机器的最大限制。您可以降低 cpu 和 gpu 消耗值。

更多讨论见:[https://stack overflow . com/questions/45662253/can-I-run-keras-model-on-GPU](https://stackoverflow.com/questions/45662253/can-i-run-keras-model-on-gpu)

这里有一个视频，展示了如何获得 TensorFlow 和 Keras 的 GPU 支持。

**请查看我最近发表的文章:**

## 📈Python For Finance 系列

1.  [识别异常值](https://medium.com/python-in-plain-english/identifying-outliers-part-one-c0a31d9faefa)
2.  [识别异常值—第二部分](https://medium.com/better-programming/identifying-outliers-part-two-4c00b2523362)
3.  [识别异常值—第三部分](https://medium.com/swlh/identifying-outliers-part-three-257b09f5940b)
4.  [程式化的事实](https://towardsdatascience.com/data-whispering-eebb77a422da)
5.  [特征工程&特征选择](https://medium.com/@kegui/feature-engineering-feature-selection-8c1d57af18d2)
6.  [数据转换](https://towardsdatascience.com/data-transformation-e7b3b4268151)
7.  [微小差异特征](https://medium.com/swlh/fractionally-differentiated-features-9c1947ed2b55)
8.  [数据标签](https://towardsdatascience.com/the-triple-barrier-method-251268419dcd)
9.  [元标签和堆叠](https://towardsdatascience.com/meta-labeling-and-stacking-f17a7f9804ec)

点击这里订阅英特尔[。](https://ddintel.datadriveninvestor.com/)

在这里加入我们的网络:[https://datadriveninvestor.com/collaborate](https://datadriveninvestor.com/collaborate)