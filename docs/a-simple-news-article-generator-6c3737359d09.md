# 一个简单的新闻文章生成器

> 原文：<https://medium.datadriveninvestor.com/a-simple-news-article-generator-6c3737359d09?source=collection_archive---------1----------------------->

[![](img/ae7aa8b2ecbf33a4530432dafc9b5f1e.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/758c6a0983cfeda10769a3b3b888c7f4.png)

在过去的一篇文章中，我训练了一个神经网络模型来生成新闻标题:

[https://medium . com/@ Andreas stckl/creating-news-headlines-with-ai-2d 8 C5 bb 76241](https://medium.com/@andreasstckl/creating-news-headlines-with-ai-2d8c5bb76241)

这个模型是一个角色级别的模型，使用我收集的路透社新闻标题作为训练数据。作为字符级模型，系统为每个字符建立标题字符。你可以在[https://towards data science . com/character-level-language-model-1439 F5 DD 87 Fe](https://towardsdatascience.com/character-level-language-model-1439f5dd87fe)中找到关于这类模型的很好的描述

[](https://www.datadriveninvestor.com/2019/02/18/the-challenge-of-forex-trading-for-machine-learning/) [## 机器学习对外汇交易的挑战——数据驱动的投资者

### 机器学习是人工智能的一个分支，之前占据了很多头条。人们是…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/18/the-challenge-of-forex-trading-for-machine-learning/) 

在本文中，我想展示如何创建一个简单的单词级模型。它可以用来一个字一个字地构建新闻文本的一些段落。该系统接受奥地利新闻文本的训练，因此生成德语文本。

## 数据

我从奥地利在线报纸上收集新闻文章来训练神经网络:

*   ORF / [http://orf.at](http://orf.at)
*   http://tt.com
*   obersterreichische Nachrichten/[http://Nachrichten . at](http://nachrichten.at)
*   niedersterreichische Nachrichten/[http://noen . at](http://noen.at)
*   福拉尔贝格在线/ [http://vol.at](http://vol.at)
*   oster Reich/[http://oe24 . at](http://oe24.at)
*   萨尔茨堡 Nachrichten/[http://sn . at](http://sn.at)
*   库里耶/[http://库里耶](http://kurier)
*   http://diepresse.com
*   krone Zeitung/[http://krone . at](http://krone.at)
*   der Standard/[http://der Standard . at](http://derstandard.at)

新闻文本存储在一个文本文件中，并加载到一个变量中:

```
Mobilfunk-Diskonter stellt fast wöchentlich neue Tarife vor
Die Marketingstrategie von Spusu (Sprich und Surf) ist einfach: Der Mobilfunker versucht sich als der günstige Anbieter auf dem Markt zu positionieren. Dementsprechend stellt er fast wöchentlich neue Tarife vor.
Sechs neue Angebote
Nun hat Spusu gleich sechs neue Angebote an den Start gebracht. So bekommen Kunden etwa um 4,90 Euro pro Monat 3GB Daten, 100 Sprachminuten und 50 SMS. Für 5,90 Euro gibt es 10 GB Daten.
Mit seiner Strategie ...
```

我使用 NLTK 包中的标记器将文本分割成一个标记列表。大写字母被保留，标点符号被视为标记而不被过滤。

## 预处理

```
['Mobilfunk-Diskonter', 'stellt', 'fast', 'wöchentlich', 'neue', 'Tarife', 'vor', 'Die', 'Marketingstrategie', 'von', 'Spusu', '(', 'Sprich', 'und', 'Surf', ')', 'ist', 'einfach', ':', 'Der', 'Mobilfunker', 'versucht', 'sich', 'als', 'der', 'günstige', 'Anbieter', 'auf', 'dem', 'Markt', 'zu', 'positionieren', '.', 'Dementsprechend', 'stellt', 'er', 'fast', 'wöchentlich', 'neue', 'Tarife', 'vor', '.', 'Sechs', 'neue', 'Angebote', 'Nun', 'hat', 'Spusu', 'gleich', 'sechs', 'neue', 'Angebote', 'an', 'den', 'Start', 'gebracht', '.', 'So', 'bekommen', 'Kunden', 'etwa', 'um', '4,90', 'Euro', 'pro', 'Monat', '3GB', 'Daten', ',', '100', 'Sprachminuten', 'und', '50', 'SMS', '.', 'Für', '5,90', 'Euro', 'gibt', 'es', '10', 'GB', 'Daten', '.', 'Mit', 'seiner', 'Strategie', 'und', 'der', 'Präsenz', 'auf', 'Online-Vergleichsportalen', ',', 'wie', 'Tarife.at', ',', 'konnte', 'Spusu', 'rund', '200.000']
```

Keras 的记号赋予器([https://keras.io/](https://keras.io/))用于将这个记号列表转换成一个整数列表。词汇表的大小被限制为 10.000，因此只有 10.000 个最常见的单词被编码。这样做是为了节省内存和计算时间。

```
[599, 256, 143, 8781, 46, 4, 10, 8782, 26, 5648, 5, 27, 17, 347, 23, 3, 799, 20, 31, 3, 3309, 15, 21, 1154, 11, 1, 4428, 599, 34, 256, 143, 8781, 46, 1, 318, 143, 3461, 93, 39, 8782, 439, 318, 143, 3461, 37, 8, 782, 492, 1, 55, 435, 952, 126, 42, 84, 376, 1155, 728, 2, 583, 5, 521, 6046, 1, 16, 84, 99, 18, 790, 4158, 728, 1, 9, 104, 2651, 5, 3, 4714, 15, 2, 41, 2, 248, 8782, 119, 4715, 6, 9024, 419, 5, 24, 5939, 4371, 1, 7, 224, 39, 20, 6, 7]
```

该模型使用最后 5 个单词来预测下一个单词。因此，我通过将整个整数列表分割成长度为 6 的序列来准备训练数据。这给了我们总共 300 多万个用于训练的序列。

```
Total Sequences: 3170581
```

每个序列的前 5 个数字用作输入特征，最后一个数字用作目标标签。这给出了特征矩阵 X 和标签向量 y。

```
[[61 34 62 40 63]
 [34 62 40 63 35]
 [62 40 63 35  8]
 [40 63 35  8 36]
 [63 35  8 36 18]
 [35  8 36 18 10]
 [ 8 36 18 10 19]
 [36 18 10 19 13]
 [18 10 19 13 20]
 [10 19 13 20  3]]
[35  8 36 18 10 19 13 20  3 11]
```

## 培养

为了构建模型，我使用 Keras 的嵌入层、LSTM 层和密集层，并激活 softmax 来计算词汇的概率分布。关于这些话题的介绍可以在[https://medium . com/@ XiwangLi/NLP-from-zero-to-one for-class ification and machine-translation-part-one-23221 b8e 2e ef](https://medium.com/@XiwangLi/nlp-from-zero-to-one-for-classification-and-machine-translation-part-one-23221b8ee2ef)中找到

```
Layer (type)                 Output Shape              Param #   
=================================================================
embedding_4 (Embedding)      (None, 5, 300)            3000000   
_________________________________________________________________
lstm_4 (LSTM)                (None, 5, 150)            270600    
_________________________________________________________________
lstm_5 (LSTM)                (None, 75)                67800     
_________________________________________________________________
dense_4 (Dense)              (None, 10000)             760000    
=================================================================
Total params: 4,098,400
Trainable params: 4,098,400
Non-trainable params: 0
_________________________________________________________________
None
```

在拟合模型之前，我定义了一个生成器函数，它通过选择随机的特征和标签行来准备成批的训练数据。使用 Keras 辅助函数“to _ categorical”将标签转换为一键编码，并传递给模型的拟合函数。

该模型以“分类 _ 交叉熵”作为损失函数，以“Adam”作为优化器，经过 50 个时期的训练。

训练是在 AWS SageMaker(【https://aws.amazon.com/de/sagemaker/】T4)上用 jupyter 笔记本完成的，这是一项完全托管的服务，涵盖了机器学习工作流，以训练模型并进行预测。作为硬件，我使用的是“ml.p3.2xlarge”实例。该机采用 GPU 加速，使用 NVIDIA Tesla V100 GPU([https://www.nvidia.com/en-us/data-center/tesla-v100/)](https://www.nvidia.com/en-us/data-center/tesla-v100/))。

## 生成文本

用于生成新闻的函数将模型和种子文本作为输入，并生成一些新单词。如果种子文本比模型输入的长度短，则序列用零填充。新单词是根据模型的概率分布随机选择的。

生成文本的一些示例:

```
Stellt fast wöchentlich neue auf “ sagte den Spiel Sieg vor Austria am um im auf Leistung Die , dabei drei Der LASK Straße haben Salzburg im , zum das sind Salzburg sind . um Mählich wurde Mählich . wurden war sein sei eine Sonntag ist – , wieder im Truppe seiner 7 Euro muss letzten ein Die seinem die “ Salzburg In zum um Spiele haben bereits Spiele einen gegen vier hat sein der es an – . Ibertsberger muss WAC für drei hatte auch und war zum Der ) . spielen zu sei hatte Leistung In zum , wurden . den das
```

文本远离正确的甚至好的新闻文章。需要更多的训练、数据和更好的模型。我将在以后的文章中介绍这一点，迁移学习将是提高绩效的关键步骤。