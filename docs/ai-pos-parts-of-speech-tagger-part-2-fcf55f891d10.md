# Ai POS-(词性)tagger #PART-2

> 原文：<https://medium.datadriveninvestor.com/ai-pos-parts-of-speech-tagger-part-2-fcf55f891d10?source=collection_archive---------7----------------------->

![](img/7645013ecd7da6ceef1f0c4bc3630633.png)

我肯定你对 Ai 的兴奋把你带到了这里！如果你是词性标注的新手，请确保你首先遵循我的第一部分，这是我不久前写的。本文更多的是对那里所做工作的增强。如果你真的有一些前期的部分，那么这部分对你来说就是小菜一碟了:)

这里，我们将使用条件随机场来构建我们的词性标注器

让我们先了解什么是 crf…

看到这里，[第一部分](https://medium.com/@i_am_manish/ai-pos-parts-of-speech-tagger-part-1-a3d6bd77ce5e)，你可能已经意识到我们需要一种更合适的方法来做词性标注。

离散分类器预测单个样本的标签而不考虑“相邻”样本，而 CRF 可以考虑上下文；例如，线性链 CRF 预测输入样本序列的标签序列。

更简单地说， *it* 是一个标准模型，用于预测与输入序列相对应的最可能的标签序列。和[隐马尔可夫模型一样。](https://medium.com/@kangeugine/hidden-markov-model-7681c22f5b9)

基本上，通用报告格式的工作流程是这样的，如果给我们:

1.  *一些特征提取器*
2.  *与特征相关的权重-权重是可学习的参数*
3.  *以前的标签*

*预测* ***当前标签。***

让我们开始…

在第 1 部分的前面，我们使用了[宾夕法尼亚树库](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)语料库。为了比较，我们在这里做同样的事情。

请注意，在之前的教程中，我们没有使用任何历史特征。我们之前的分类器对之前的决策一无所知。

最初，如果 crf 库不存在，安装它。你可以像 pip install sk learn–CRF suite 一样简单地安装它，或者在 [colab](https://colab.research.google.com/) / [kaggle](https://www.kaggle.com/) 中继续安装！pip 安装 sklearn-crfsuite(注意感叹号)。

首先，我们需要加载数据，

```
import nltk tagged_sentences = nltk.corpus.treebank.tagged_sents()
```

我们将继续进行与前面相同的特征提取。

```
def features(sentence, index):
 ##sentence:[w1, w2, ...],index: the index of the word   
  return {         'word': sentence[index],  
       'is_first': index == 0,     
    'is_last': index == len(sentence) - 1,   
      'is_capitalized': sentence[index][0].upper() ==sentence[index[0],   
      'is_all_caps': sentence[index].upper() == sentence[index],         'is_all_lower': sentence[index].lower() == sentence[index],         'prefix-1': sentence[index][0],      
   'prefix-2': sentence[index][:2],    
     'prefix-3': sentence[index][:3],       
  'suffix-1': sentence[index][-1],       
  'suffix-2': sentence[index][-2:],  
       'suffix-3': sentence[index][-3:],         
'prev_word': '' if index == 0 else sentence[index - 1],         'next_word': '' if index == len(sentence) - 1 else sentence[index + 1],         
'has_hyphen': '-' in sentence[index],        
'is_numeric': sentence[index].isdigit(),         
'capitals_inside': sentence[index][1:].lower() != sentence[index][1:]     }
```

现在，和以前一样，我们需要分割数据集进行训练和测试。我们预留了. 75*len(tagged_sentences)之前的标记句进行训练和休息测试。

```
part=int(.75 * len(tagged_sentences)) training_sentences = tagged_sentences[:part] test_sentences = tagged_sentences[part:] def transform_to_dataset(tagged_sentences):  
X, y = [], []     
 for tagged in tagged_sentences:       
  for index in range(len(tagged)):    X.append(features(untag(tagged), index))              y.append(tagged[index][1])      
 return X, yX_train, y_train = transform_to_dataset(training_sentences) X_test, y_test = transform_to_dataset(test_sentences)
```

让我们通过打印来检查，

```
print(len(X_train))      print(len(X_test))          print(X_train[0]) print(y_train[0])
```

**['NNP '，' NNP '，'，'，' CD '，' NNS '，'，'，' MD '，' VB '，' DT '，' NN '，' IN '，' DT '，' JJ '，' NN '，' NNP '，' CD '，'，'】**

在这里，您可能已经注意到数据集中的每一行都是一个序列，而不是一个单词。我们的 crf 学习序列。

现在，我们导入之前安装的 crf 包，并在上面安装我们的数据。

```
from sklearn_crfsuite import CRF  model = CRF() model.fit(X_train, y_train)
```

测试我们的模型来预测

```
sentence = ['I', 'am', 'Bob','!'] def pos_tag(sentence):     sentence_features = [features(sentence, index) for index in range(len(sentence))]     return list(zip(sentence, model.predict([sentence_features])[0]))
```

在打印 *print(pos_tag(sentence))* 时，输出为

# [('我'，' PRP ')，(' am '，' VBP ')，('鲍勃'，' NNP ')，('！', '.')]

为了检验我们的模型有多精确，我们会这样做

```
from sklearn_crfsuite import metrics y_pred = model.predict(X_test) print(metrics.flat_accuracy_score(y_test, y_pred)
```

哪个输出: **0.960**

请记住，这个准确率高于我们之前的决策树分类器，后者为 **90%。**但是在这里，我们通过使用一种更有效的方法来学习句子及其字符之间的关系，获得了 96%的高准确率。

而且，我们可以摆弄它的参数，做微调等。进一步提高精度和性能。

如果你想知道如何用 keras(lstm/GRUs)做词性标注，请阅读[第三部分](https://medium.com/@i_am_manish/ai-pos-parts-of-speech-tagger-part-3-c94b116a93e3)

**有用链接:**

[https://nlp.stanford.edu/software/tagger.shtml](https://nlp.stanford.edu/software/tagger.shtml)

[https://medium . freecodecamp . org/an-introduction-to-part-of-speech-tagging-and-the-hidden-Markov-model-953d 45338 f24](https://medium.freecodecamp.org/an-introduction-to-part-of-speech-tagging-and-the-hidden-markov-model-953d45338f24)

[https://www.nltk.org/book/ch05.html](https://www.nltk.org/book/ch05.html)

[https://becoming human . ai/词性标注教程深度学习库-d7f93fa05537](https://becominghuman.ai/part-of-speech-tagging-tutorial-with-the-keras-deep-learning-library-d7f93fa05537)

*原载于 2018 年 11 月 3 日*[*blog.lipishala.com*](https://blog.lipishala.com/2018/11/03/ai-pos-parts_of_speech-tagger-part-2/)*。*