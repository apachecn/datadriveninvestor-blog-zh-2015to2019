# 假人的 NumPy

> 原文：<https://medium.datadriveninvestor.com/numpy-for-dummies-3dbd5f946731?source=collection_archive---------8----------------------->

在 Python 中，我们有“列表”。

![](img/54d8ef61997ac19504824be291ce1845.png)

in case you need a reminder

NumPy 数组就像“列表”——但更好，因为它(1)更快，(2)更方便，(3)占用更少的内存。它是 Python 中科学计算的核心库 ( [Edureka](https://www.youtube.com/watch?v=8JfDAm9y_7s) )。

> NumPy 的主要对象是同构多维数组。它是一个元素表(通常是数字)，所有的元素都是相同的类型，由一组正整数(【SciPy.org】)索引。

在本文中，我们将介绍 10 种常见的操作，但首先要介绍 NumPy:

![](img/5843007eb775302dce5b7169caea3d66.png)

1.  **。array()**

![](img/a8e36e2fabf1dbb6f72a2b262b51c824.png)

创建数组有不同的方法，但这是最简单的方法。您可以创建一个或多个维度数组。

![](img/5b72db9a7a6e1d6729cdd93a66cab794.png)

**2。。arange()**

![](img/0577f06ec835172972da199f5e1e0b2d.png)![](img/be6c744ff0ddde5b24fa7ef1dcce711a.png)

**3。。linspace()**

![](img/b7c8f9cc7ca4895cbf70385b33cc50c4.png)![](img/1d0b6c9e0dc18c8e123ec898801f86e1.png)

**4。。reshape()**

![](img/9897980ffb24538acd1efd040ffacaff.png)![](img/a9cc6adbe1e69866866f0450d30b9772.png)![](img/5478484d3df5ea0b613334641dbc0763.png)

你可以看到，在这个例子中，0 轴上有**三个**元素(从 0，4，8 开始)，1 轴上有**四个**元素(从 0，1，2，3 开始)。

**5。。总和(轴=1)**

![](img/69eddd17682162e492ee79b033e3aea6.png)![](img/1bad9763e823a367e9eeddd61468747c.png)![](img/5478484d3df5ea0b613334641dbc0763.png)

在前面的例子中，“hey”在轴 0 中有 3 个元素，在轴 1 中有 4 个元素。看看每个轴的和是怎么算出来的。

![](img/539d3f4fd77c779acc3924b5aa5d9533.png)

对于轴 0，第一个元素是 12，因为 0 + 4 + 8 = 12。

对于轴 1，第一个元素是 6，因为 0 + 1 + 2 + 3 = 6。

重复剩下的部分。

6。。var()

![](img/33c2c3036042ee94074c4d842c8a985b.png)![](img/ff512004254af16a6967b01122907f0e.png)

7。。std()

![](img/ea88996b505751500be078b80f00ee8f.png)![](img/5f7c4959fa35a31205d8a499fbeb5cdb.png)

8。. random.shuffle()

![](img/45df60548e40ddf7cc0e0c7d47201aa8.png)![](img/4cb61b710f88fd7ba2c35bb7b865ded8.png)

比较第一个数组和被打乱后的 E。

9。slice()

![](img/b7ea37302d1537a8fe563b4589dce088.png)![](img/1a155465945e98bcd707616a34eb744b.png)

您可以使用 slice 函数或直接应用 slice 语法。

10。。拉威尔()

![](img/ce6cfba73e0863cbc2e1ec2c8d8e7282.png)![](img/ae0de79f2f5e92b3f3441576646cc832.png)

在上面的示例中，您可以看到阵列完全变平。

还有更多函数和 NumPy 教程，但希望这些帮助你入门！

**资源:**

[视频] [Python NumPy 教程| Edureka](https://www.youtube.com/watch?v=8JfDAm9y_7s)

【视频】 [Python: NumPy |数值型 Python 数组教程](https://www.youtube.com/watch?v=8Mpc9ukltVA)

【文章】[索引(SciPy.org)](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html)