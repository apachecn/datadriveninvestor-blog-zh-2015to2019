# Python 数据科学入门教程:NLTK

> 原文：<https://medium.datadriveninvestor.com/python-data-science-getting-started-tutorial-nltk-2d8842fedfdd?source=collection_archive---------1----------------------->

[![](img/13e997374d917bc91ad46ba4dea0f0dd.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/f51653b7f8232440a7b2fc085139a6ba.png)

Photo by [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 使用 NLTK 分析单词和句子

欢迎学习自然语言处理系列教程，使用 Python 的自然语言工具包 NLTK 模块。

NLTK 模块是一个巨大的工具包，旨在帮助您使用整个自然语言处理(NLP)方法。NLTK 将为你提供一切，从拆分段落到句子，拆分单词，识别词性，突出主题，甚至帮助你的机器理解文本的内容。在这个系列中，我们将讨论观点挖掘或情感分析领域。

当我们学习如何使用 NLTK 进行情感分析时，我们将学习以下内容:

*   分词—将文本正文拆分成句子和单词。
*   词性标注
*   机器学习和朴素贝叶斯分类器
*   如何将 Scikit Learn (sklearn)与 NLTK 一起使用
*   用数据集训练分类器
*   使用 Twitter 进行实时流情感分析。
*   …以及更多。

要开始，您需要 NLTK 模块，以及 Python。

> [DDI 编辑推荐—用于数据科学和机器学习的 Python 训练营](http://go.datadriveninvestor.com/pybootcamp/matf)

如果你还没有 Python，去`python.org`下载最新版本的 Python(如果你在 Windows 上的话)。如果你在 Mac 或者 Linux 上，你应该可以运行`apt-get install python3`。

接下来，你需要 NLTK 3。安装 NLTK 模块最简单的方法是使用`pip`。

对于所有用户，这是通过打开`cmd.exe`、bash 或您使用的任何 shell 并键入以下命令来完成的:

```
pip install nltk
```

接下来，我们需要为 NLTK 安装一些组件。以任何常用方式打开 python，然后键入:

```
Import nltk
Nltk.download()
```

为所有软件包选择全部下载，然后单击下载。这将会给你所有的断字器，拦截器，其他算法和所有的语料库。如果空间是个问题，您可以选择手动下载所有内容。NLTK 模块将占用大约 7MB，整个`nltk_data`目录将占用大约`nltk_data`，包括您的`nltk_data`、解析器和语料库。

如果您运行的是带有 VPS 的无头版本，您可以通过运行 Python 并执行以下操作来安装所有内容:

```
Import nltk
Nltk.download()
d (for download)
All (for download everything)
```

这将为您下载所有内容。

现在你已经有了你需要的所有东西，让我们键入一些简单的单词:

*   语料库—文本的主体，单数。语料库是它的复数。例子:`A collection of medical journals`。
*   词汇——词汇及其意义。比如:英语词典。不过考虑到每个领域都有不同的词库。比如对于金融投资者来说，`Bull`这个词的第一个含义就是对市场有信心的人。与“普通英语词汇”相比，这个词的第一个意思是动物。所以，金融投资人，医生，孩子，机械师等。都有专门的词汇。
*   令牌—每个“实体”都是基于规则的分割的一部分。例如，当一个句子被“拆分”成单词时，每个单词就是一个标签。如果你把一个段落分成几个句子，每个句子也可以是一个标记。

这些是进入自然语言处理(NLP)领域时最常听到的词，但我们将及时涵盖更多的词。因此，让我们展示一个如何用 NLTK 模块将一些东西分割成标记的例子。

```
From nltk.tokenize import sent_tokenize, word_tokenizeEXAMPLE_TEXT = "Hello Mr. Smith, how are you doing today? The weather is great, and Python is awesome. The sky is pinkish-blue. You shouldn't eat cardboard."Print(sent_tokenize(EXAMPLE_TEXT))
```

一开始你可能会觉得按词或按句分词是一件相当琐碎的事情。对于很多句子来说，可能是。第一步可能是执行一个简单的`.split('. ')`，或者通过一个句点，然后是一个空格分割。然后可能你会介绍一些正则表达式，用句号，空格，然后大写字母来划分。问题是类似`Mr. Smith`的东西，还有很多其他的东西会给你带来麻烦。按单词分段也是一个挑战，尤其是在考虑缩写时，比如`we`和`we're`。NLTK 用这个看似简单却非常复杂的操作为你节省了大量的时间。

上面的代码会输出句子，分成一个句子列表，可以用`for`循环来遍历。

```
[ 'Hello Mr. Smith, how are you doing today?', 'The weather is great, and Python is awesome.', 'The sky is pinkish-blue.', "You shouldn't eat cardboard." ]
```

所以我们在这里创建标签，它们都是句子。这次让我们把单词一个单词一个单词地分开。

```
Print (word_tokenize(EXAMPLE_TEXT))[ 'Hello' , 'Mr.' , 'Smith' , ',' , 'how' , 'are' , 'you ' , 'doing ' , 'today ' , '?' , 'The' , 'weather' , 'is' , 'great' , ',' , 'and' , 'Python' , 'is' , 'awesome ' , '.' , 'The' , 'sky' , 'is' , 'pinkish-blue' , '.' , 'You' , 'should' , "n't" , 'eat' , 'cardboard' , '.' ]
```

这里有几点需要注意。首先，请注意标点被视为一个单独的标签。另外，注意单词`shouldn't`分成了`should`和`n't`。最后要注意的是，`pinkish-blue`确实被当成了“一个字”，就是这样。酷！

现在，看看这些分词后面的单词，我们必须开始思考我们的下一步可能是什么。我们开始思考如何通过观察这些词来获得意思。我们可以思考如何给很多词赋予价值，但也看到一些词基本上没有价值。这是一种我们也能处理的“停用词”形式。这是我们将在下一个教程中讨论的内容。

# 二。NLTK 和停止字

自然语言处理的思想是执行某种形式的分析或处理。机器至少可以在一定程度上理解文本的含义、表示或暗示。

这显然是一个巨大的挑战，但有任何人都可以遵循的步骤。但是，主要思想是计算机不直接理解单词。令人震惊的是，人类不会。在人类中，记忆在大脑中被分解成电信号，其形式是发出模式的神经组。关于大脑还有很多未知的东西，但是我们越是把人脑分解成基本元素，就会发现基本元素。好吧，原来电脑储存信息的方式非常相似！如果我们想模仿人类阅读和理解文本的方式，我们需要一种尽可能接近的方式。一般来说，计算机都是用数字来表示一切，但我们经常在编程中看到直接使用二进制信号(`True`或`False`，可以直接转换成 1 或 0，直接来自于一个电信号的存在`(True, 1)`或不存在`(False, 0)`)。要做到这一点，我们需要一种将单词转换成数字或信号模式的方法。将数据转换成计算机可以理解的东西称为“预处理”预处理的主要形式之一是过滤掉无用的数据。在自然语言处理中，无用的词(数据)称为停用词。

我们可以立即意识到有些词比其他词更有意义。我们也可以看到有些词是没用的，是填充词。比如我们在英语中用它们来填句子，所以没有这种奇怪的声音。一个最常见的、非官方的、无用的例子是`umm`这个词。人们常用`umm`来填充，多于其他词。这个词毫无意义，除非我们要找的是一个可能缺乏自信，迷茫，或者不怎么自信的人。我们都这样做，有...哦...很多时候，你可以在视频里听到我说`umm`或者`uhh`。对于大多数分析来说，这些词是没有用的。

我们不希望这些单词占用我们的数据库空间或占用宝贵的处理时间。所以，我们把这些话叫做“无用的话”，因为它们是无用的，我们要对待它们。“停字”的另一个版本可以写得更多:我们停在的字。

例如，如果您发现经常用于讽刺的词语，您可能想立即停止。讽刺性的单词或短语会因同义词库和语料库而异。暂时，我们会将停用词视为不包含任何含义的词，我们将删除它们。

你可以通过存储一个你认为是停用词的单词列表很容易地做到这一点。NLTK 使用一堆他们认为是停用词的单词来帮助您入门，您可以通过 NLTK 语料库访问它:

```
From nltk.corpus import stopwords
```

以下是清单:

```
>>> set (stopwords. words ( 'english' ))
 { 'ourselves' , 'hers' , 'between' , 'yourself' , 'but' , 'again ' , 'there ' , 'about ' , 'once ' , 'during ' , ' out ' , 'very ' , ' Having' , 'with' , 'they' , 'own' , 'an' , 'be' , 'some' , 'for' , 'do' , 'its' , 'yours ' , 'such' , 'into' , 'of' , 'most' , 'itself' , 'other' , 'off' , 'is' , 's' , 'am' , 'or' , 'who ' , 'as' , 'from ' , ' Him' , 'each' , 'the' , 'themselves' , 'until' , 'below' , 'are' , 'we' , 'these ' , 'your ' , 'his' , 'through' , 'don' , 'nor' , 'me' , 'were' , 'her' , 'more' , 'himself ' , 'this' , 'down' , 'should' , 'our' , 'their ' , 'while ' , ' Above' , 'both' , 'up' , 'to' , 'ours' , 'had' , 'she' , 'all' , 'no' , 'when' , 'at' , 'any' , 'before' , 'them' , 'same' , 'and' , 'been' , 'have' , 'in' , 'will' , 'on' , 'does ' , 'yourselves ' , 'then ' , 'that ' , ' Because' , 'what' , 'over' , 'why' , 'so' , 'can' , 'did ' , 'not' , ' now' , 'under' , 'he' , 'you' , 'herself' , 'has' , 'just' , 'where' , 'too' , 'only' , 'myself ' , 'which' , 'those ' , 'i' , 'after' , 'few ' , 'whom'  , 't' , 'being' , 'if' , 'theirs' , 'my' , 'against ' , 'a' , 'by ' , 'doing ' , 'it ' , 'how' , 'further ' , ' Was' , 'here' , 'than' }
```

下面是如何使用`stop_words`集合从文本中删除停用词:

```
From nltk.corpus import stopwords
From nltk.tokenize import word_tokenizeExample_sent = "This is a sample sentence, showing off the stop words filtration."Stop_words = set(stopwords.words( 'english' ))Word_tokens = word_tokenize(example_sent)Filtered_sentence = [w for w in word_tokens if not w in stop_words]Filtered_sentence = []For w in word_tokens:
   If w not in stop_words:
      Filtered_sentence.append(w)Print(word_tokens)
Print(filtered_sentence)
```

我们的输出是:

```
['This', 'is', 'a', 'sample', 'sentence', ',', 'showing', 'off', 'the', 'stop', 'words', 'filtration', ' .']
['This', 'sample', 'sentence', ',', 'showing', 'stop', 'words', 'filtration', '.']
```

多亏了我们的数据库。数据预处理的另一种形式是“词干提取”，这是我们接下来要讨论的。

# 三。NLTK 茎提取

词干的概念是一种标准化的方法。除了时态，这个词的许多变体都有相同的意思。

我们提取词干的原因是为了缩短搜索的时间并使句子规范化。

考虑:

```
I was taking a ride in the car.
I was riding in the car.
```

这两句话的意思是一样的。`in the car`(在车上)也是一样。`I`(我)也是一样。在这两种情况下，`ing`都明确表达了过去式，那么在试图弄清楚这种过去式活动的意义的情况下，真的有必要区分`riding`和`taking a ride`吗？

不，不是。

这只是一个小例子，但是想象一下英语中每一个可以放在每一个可能的时态上，并在单词上加词缀的单词。每个版本都有一个单独的字典条目，这将是非常多余和低效的，特别是因为一旦我们转换为数字，“值”将是相同的。

最流行的瓷器提取算法之一是 Porter，它存在于 1979 年。

首先，我们必须爬行并定义我们的茎:

```
From nltk.stem import PorterStemmer
From nltk.tokenize import sent_tokenize, word_tokenizePs = PorterStemmer()
```

现在让我们选择一些词干相似的单词，例如:

```
Example_words = [ "python" , "pythoner" , "pythoning" , "pythoned" , "pythonly" ]
```

下面，我们可以这样做来轻松提取茎:

```
For w in example_words:
   Print (ps.stem(w))
```

我们的产出:

```
Python
Python
Python
Python
Pythonli
```

现在让我们试着从一个典型的句子中提取词干，而不是一些单词:

```
New_text = "It is important to by very pythonly while you are pythoning with python. All pythoners have pythoned poorly at least once."
Words = word_tokenize(new_text)For w in words :
   Print(ps.stem(w))
```

我们现在的结果是:

```
It
Is
Import
To
By
Veri
Pythonli
While
You
Are
Python
With
Python
.
All
Python
Have
Python
Poorli
At
Least
Onc
.
```

接下来，我们将讨论 NLTK 模块的一些更高级的内容，词性标注，其中我们可以使用 NLTK 模块来识别句子中每个单词的词性。

# 四。NLTK 词性标注

NLTK 模块的一个更强大的方面是它可以用于词性标注。它的意思是将句子中的词标记为名词、形容词、动词等。更令人印象深刻的是，它还可以用时态和其他来标记。这是标签、它们的含义和一些例子的列表:

```
POS tag list: CC coordinating conjunction
 CD cardinal digit
 DT determiner
 EX existential there ( like : "there is" ... think of it like "there exists" )
 FW foreign word
 IN preposition/subordinating conjunction
 JJ adjective 'big'
 JJR adjective, comparative 'bigger'
 JJS adjective, superlative 'biggest'
 LS list marker 1 )
 MD modal could, will
 NN noun, singular 'desk'
 NNS noun plural 'desks'
 NNP proper noun, singular 'Harrison'
 NNPS proper noun, plural 'Americans'
 PDT predeterminer 'all the kids'
 POS possessive ending parent 's
 PRP personal pronoun I, he, she
 PRP$ possessive pronoun my, his, hers
 RB adverb very, silently,
 RBR adverb, comparative better
 RBS adverb, superlative best
 RP particle give up
 TO to go 'to' the store.
 UH interjection errrrrrrrm
 VB verb, base form take
 VBD verb, past tense took
 VBG verb, gerund/present participle taking
 VBN verb, past participle taken
 VBP verb, sing. present, non- 3 d take
 VBZ verb, 3 rd person sing. present takes
 WDT wh-determiner which
 WP wh-pronoun who, what
 WP$ possessive wh-pronoun whose
 WRB wh-abverb where , when
```

我们如何使用这个？我们在处理的时候，不得不解释一个新的句子标记，叫做`PunktSentenceTokenizer`。这个标记可以实现无监督的机器学习，所以你可以在你使用的任何文本上进行训练。首先，让我们获得一些我们计划使用的导入:

```
Import nltk
From nltk.corpus import state_union
From nltk.tokenize import PunktSentenceTokenizer
```

现在让我们创建训练和测试数据:

```
Train_text = state_union.raw( "2005-GWBush.txt" )
Sample_text = state_union.raw( "2006-GWBush.txt" )
```

一个是 2005 年以来的国情咨文演讲，一个是 2006 年以来的小布什总统的演讲。

接下来，我们可以按如下方式训练 Punkt 标记:

```
Custom_sent_tokenizer = PunktSentenceTokenizer(train_text)
```

在那之后，我们实际上可以把这个词分开来用:

```
Tokenized = custom_sent_tokenizer.tokenize(sample_text)
```

现在，我们可以通过创建一个函数来完成词性标注脚本，该函数将遍历并标记每个句子的词性，如下所示:

```
Def process_content () :
   Try :
      For i in tokenized[: 5 ]:
         Words = nltk.word_tokenize(i)
         Tagged = nltk.pos_tag(words)
         Print(tagged) Except Exception as e:
        Print(str(e)) Process_content()
```

输出应该是一个元组列表，元组中的第一个元素是一个单词，第二个元素是一个词性标签。它应该看起来像:

```
[('PRESIDENT', 'NNP'), ('GEORGE', 'NNP'), ('W.', 'NNP'), ('BUSH', 'NNP'), ( "'S" , 'POS '), ('ADDRESS', 'NNP'), ('BEFORE', 'NNP'), ('A', 'NNP'), ('JOINT', 'NNP'), ('SESSION', 'NNP '), ('OF', 'NNP'), ('THE', 'NNP'), ('CONGRESS', 'NNP'), ('ON', 'NNP'), ('THE', 'NNP '), ('STATE', 'NNP'), ('OF', 'NNP'), ('THE', 'NNP'), ('UNION', 'NNP'), ('January', 'NNP '), (' 31 ', 'CD'), (',', ','), (' 2006 ', 'CD'), ('THE', 'DT'), ('PRESIDENT', 'NNP '), (':', ':'), ('Thank', 'NNP'), ('you', 'PRP'), ('all', 'DT'), ('.', '. ')] [('Mr.', 'NNP'), ('Speaker', 'NNP'), (',', ','), ('Vice', 'NNP'), ('President', 'NNP'), ('Cheney', 'NNP'), (',', ','), ('members', 'NNS'), ('of', 'IN'), ('Congress', 'NNP'), (',', ','), ('members', 'NNS'), ('of', 'IN'), ('the', 'DT'), ('Supreme', 'NNP'), ('Court', 'NNP'), ('and', 'CC'), ('diplomatic', 'JJ'), ('corps', 'NNS'), (',', ','), ('distinguished', 'VBD'), ('guests', 'NNS'), (',', ','), ('and', 'CC'), ('fellow', 'JJ'), ('citizens', 'NNS'), (':', ':'), ('Today', 'NN'), ('our', 'PRP  $'), ('nation', 'NN'), ('lost', 'VBD'), ('a', 'DT'), ('beloved', 'VBN'), (',', ' ,'), ('graceful', 'JJ'), (',', ','), ('courageous', 'JJ'), ('woman', 'NN'), ('who', ' WP'), ('called', 'VBN'), ('America', 'NNP'), ('to', 'TO'), ('its', 'PRP$'), ('founding', 'NN'), ('ideals', 'NNS'), ('and', 'CC'), ('carried', 'VBD'), ('on', 'IN'), ('a', 'DT'), ('noble', 'JJ'), ('dream', 'NN'), ('.', '.')] [('Tonight', 'NNP'), ('we' , 'PRP'), ('are', 'VBP'), ('comforted', 'VBN'), ('by', 'IN'), ('the', 'DT'), ('hope' , 'NN'), ('of', 'IN'), ('a', 'DT'), ('glad', 'NN'), ('reunion', 'NN'), ('with' , 'IN'), ('the', 'DT'), ('husband', 'NN'), ('who', 'WP'), ('was', 'VBD'), ('taken' , 'VBN'), ('so', 'RB'), ('long', 'RB'), ('ago', 'RB'), (',', ','), ('and' , 'CC'), ('we', 'PRP'), ('are', 'VBP'), ('grateful', 'JJ'), ('for', 'IN'), ('the' , 'DT'), ('good', 'NN'), ('life', 'NN'), ('of', 'IN'), ('Coretta', 'NNP'), ('Scott' , 'NNP'), ('King', 'NNP'), ('.', '.')] [('(', 'NN'), ('Applause', 'NNP'), ('. ', '.'), (')', ':')] [('Pres  Ident', 'NNP'), ('George', 'NNP'), ('W.', 'NNP'), ('Bush', 'NNP'), ('reacts', 'VBZ'), ( 'to', 'TO'), ('applause', 'VB'), ('during', 'IN'), ('his', 'PRP$'), ('State', 'NNP'), ('of', 'IN'), ('the', 'DT'), ('Union', 'NNP'), ('Address', 'NNP'), ('at', 'IN'), ('the', 'DT'), ('Capitol', 'NNP'), (',', ','), ('Tuesday', 'NNP'), (',', ','), ('Jan', 'NNP'), ('.', '.')]
```

当我们到了这里，我们可以开始得到的意义，但仍有一些工作要做。我们将讨论的下一个主题是组块，我们按照单词的部分，将单词分成有意义的组。

# 动词 （verb 的缩写）NLTK 块

既然知道了词性，就可以关注所谓的块，就是把单词分成有意义的块。阻塞的主要目标之一是对所谓的“名词短语”进行分组。这些短语包含一个或多个名词，可以是描述性词语、动词或副词。这个想法是把名词和与之相关的单词结合起来。

为了分块，我们把词性标签和正则表达式结合起来。主要来自正则表达式，我们想利用这些东西:

```
+ = match 1 or more
? = match 0 or 1 repetitions.
* = match 0 or MORE repetitions   
. = Any character except a new line
```

如果你需要正则表达式的帮助，请参阅上面链接的教程。最后要注意的是，单词 tag 是用`<`和`>`来表示的。我们也可以在标签中放置一个正则表达式来表达“所有名词”(`<N.*>`)。

```
Import nltk
From nltk.corpus import state_union
From nltk.tokenize import PunktSentenceTokenizerTrain_text = state_union.raw( "2005-GWBush.txt" )
Sample_text = state_union.raw( "2006-GWBush.txt" )Custom_sent_tokenizer = PunktSentenceTokenizer(train_text)Tokenized = custom_sent_tokenizer.tokenize(sample_text)Def process_content () :
    Try :
        For i in tokenized:
            Words = nltk.word_tokenize(i)
            Tagged = nltk.pos_tag(words)
            chunkGram = r"""Chunk: {<RB.?>*<VB.?>*<NNP>+<NN>?}"""
            chunkParser = nltk.RegexpParser(chunkGram)
            Chunked = chunkParser.parse(tagged)
            Chunked.draw()         Except Exception as e:
        Print(str(e)) Process_content()
```

![](img/cb60befdc498fa79c75f085f2c26fe09.png)

这里的主线是:

```
chunkGram = r"""Chunk: {<RB.?>*<VB.?>*<NNP>+<NN>?}"""
```

将这条线分开:

`<RB.?>*`:零个或多个任意时态的副词，后跟:

`<VB.?>*`:任意时态的零个或多个动词，后跟:

`<NNP>+`:一个或多个合理的名词，后接:

零个或一个名词单数。

尝试有趣的组合，将不同的实例分组，直到你感到熟悉为止。

视频中没有涉及，但也有一个合理的任务，实际访问一个特定的块。这很少被提及，但是取决于你正在做什么，这可能是重要的一步。假设您打印出该块，您将看到以下输出:

```
( S ( Chunk PRESIDENT/NNP GEORGE/NNP W./NNP BUSH/NNP) 'S/POS ( Chunk ADDRESS/NNP BEFORE/NNP A/NNP JOINT/NNP SESSION/NNP OF/NNP THE/NNP CONGRESS/NNP ON/ NNP THE/NNP STATE/NNP OF/NNP THE/NNP UNION/NNP January/NNP) 31 /CD , /, 2006 /CD THE/DT ( Chunk PRESIDENT/NNP ) :/ : ( Chunk Thank/NNP) you/PRP All/DT ./.)
```

酷，这有助于我们可视化，但如果我们想通过我们的程序访问这些数据呢？所以这里发生的是我们的“阻塞”变量是一个 NLTK 树。每个“块”和“非块”都是树的“子树”。我们可以用类似`chunked.subtrees`的东西来指代它们。然后我们可以像这样遍历这些子树:

```
For subtree in chunked.subtrees():
        Print (subtree)
```

接下来，我们可能只关心得到这些块，而忽略其余的。我们可以在`chunked.subtrees()`调用中使用`filter`参数。

```
For subtree in chunked.subtrees(filter= lambda t: t.label() == 'Chunk' ):
        Print(subtree)
```

现在我们执行过滤来显示标签为“Block”的子树。请记住，这不是 NLTK block 属性中的“block”…这是一个字面上的“block”，因为这是我们给它的标签:`chunkGram = r"""Chunk: {<RB.?>*<VB.?>*<NNP>+<NN>?}"""`。

如果我们写类似于`chunkGram = r"""Pythons: {<RB.?>*<VB.?>*<NNP>+<NN>?}"""`的东西，那么我们可以传递`"Pythons."`标签来过滤。结果应该是这样的:

```
- ( Chunk PRESIDENT / NNP GEORGE / NNP W . / NNP BUSH / NNP ) ( Chunk ADDRESS / NNP BEFORE / NNP A / NNP JOINT / NNP SESSION / NNP OF / NNP THE / NNP CONGRESS / NNP ON / NNP THE / NNP STATE / NNP OF / NNP THE / NNP UNION / NNP January / NNP ) ( Chunk PRESIDENT / NNP ) ( Chunk Thank / NNP )
```

完整的代码是:

```
Import nltk
From nltk.corpus import state_union
From nltk.tokenize import PunktSentenceTokenizerTrain_text = state_union.raw( "2005-GWBush.txt" )
Sample_text = state_union.raw( "2006-GWBush.txt" )Custom_sent_tokenizer = PunktSentenceTokenizer(train_text)Tokenized = custom_sent_tokenizer.tokenize(sample_text)Def process_content () :
    Try :
        For i in tokenized:
            Words = nltk.word_tokenize(i)
            Tagged = nltk.pos_tag(words)
            chunkGram = r"""Chunk: {<RB.?>*<VB.?>*<NNP>+<NN>?}"""
            chunkParser = nltk.RegexpParser(chunkGram)
            Chunked = chunkParser.parse(tagged) Print(chunked)
            For subtree in chunked.subtrees(filter= lambda t: t.label() == 'Chunk' ):
                Print(subtree) Chunked.draw() Except Exception as e:
        Print(str(e))Process_content()
```

# 不及物动词 NLTK 增加了一个缺口(Chinking)

你可能会发现，经过大量的分块，你的分块中有一些你不想要的单词，但是你不知道如何通过分块来摆脱它们。你可能会发现增加一个缺口就是你的解决方案。

添加一个缺口类似于一个块，基本上是一种从块中移除块的方法。你从木块上移开的木块就是你的缺口。

代码很像，你只需要用`}{`来编码缺口，后面的块，而不是`{}`块。

```
Import nltk
From nltk.corpus import state_union
From nltk.tokenize import PunktSentenceTokenizerTrain_text = state_union.raw( "2005-GWBush.txt" )
Sample_text = state_union.raw( "2006-GWBush.txt" )Custom_sent_tokenizer = PunktSentenceTokenizer(train_text)Tokenized = custom_sent_tokenizer.tokenize(sample_text)Def process_content () :
    Try :
        For i in tokenized[ 5 :]:
            Words = nltk.word_tokenize(i)
            Tagged = nltk.pos_tag(words) chunkGram = r"""Chunk: {<.*>+} }<VB.?|IN|DT|TO>+{""" chunkParser = nltk.RegexpParser(chunkGram)
            Chunked = chunkParser.parse(tagged) Chunked.draw() Except Exception as e:
        Print(str(e))Process_content()
```

![](img/3f78dd28866161f5509b305d938d14a2.png)

现在，主要的区别是:

```
}<VB.?| IN |DT| TO >+{
```

这意味着我们要从空白中删除一个或多个动词、介词、限定词或`to`词。

既然我们已经了解了如何执行一些自定义分区和添加间隙，那么让我们讨论 NLTK 附带的块形式，它被称为命名实体识别。

# 七。NLTK 命名实体识别

自然语言处理中最重要的分块形式之一叫做“命名实体识别”这个想法是让机器立即拉出“实体”，如人、地点、事物、位置、货币等。

这可能是一个挑战，但是 NLTK 是为我们构建的。NLTK 的命名实体识别有两个主要选项:识别所有命名实体，或者将命名实体识别为它们各自的类型，比如人、地点、位置等。

这是一个例子:

```
Import nltk
From nltk.corpus import state_union
From nltk.tokenize import PunktSentenceTokenizerTrain_text = state_union.raw( "2005-GWBush.txt" )
Sample_text = state_union.raw( "2006-GWBush.txt" )Custom_sent_tokenizer = PunktSentenceTokenizer(train_text)Tokenized = custom_sent_tokenizer.tokenize(sample_text)Def process_content () :
    Try :
        For i in tokenized[ 5 :]:
            Words = nltk.word_tokenize(i)
            Tagged = nltk.pos_tag(words)
            namedEnt = nltk.ne_chunk(tagged, binary= True )
            namedEnt.draw()
    Except Exception as e:
        Print(str(e)) Process_content()
```

你马上就能看到一些东西。当`binary`为假时，它也选取同样的东西，但是把术语`White House`分解成`White`和`House`好像它们是不同的，我们可以在选项`binary = True`中看到，命名实体标识说`White House`是同一个命名实体的一部分，这是正确的。

根据你的目标，可以使用`binary`选项。如果你的`binary`是`false`，这里是你能得到的，命名实体的类型:

```
NE Type and Examples
ORGANIZATION - Georgia -Pacific Corp . , WHO
PERSON - Eddy Bonte, President Obama
LOCATION - Murray River, Mount Everest
DATE - June, 2008 - 06 - 29
TIME - two fifty am, 1 : 30 p . m .
MONEY - 175 million Canadian Dollars, GBP 10.40
PERCENT - twenty pct, 18.75 %
FACILITY - Washington Monument, Stonehenge
GPE - South East Asia, Midlothian
```

无论哪种方式，你可能会发现你需要做更多的工作来得到它的权利，但这个功能是非常强大的。

在下一个教程中，我们将讨论类似于词干提取的东西，称为“词汇化”。

# 八。NLTK 形态恢复

一种与词干提取非常相似的操作被称为形态学恢复。两者的主要区别在于，正如你之前看到的，词干化能力经常创造不存在的单词，而单词形式是实际的单词。

所以，你的词干，也就是你最后用的词，不是你能在字典里查到的，而是你能找到一个词形。

有时你会得到非常相似的单词，但有时你会得到完全不同的单词。让我们看一些例子。

```
From nltk.stem import WordNetLemmatizerLemmatizer = WordNetLemmatizer() Print(lemmatizer.lemmatize( "cats" ))
 Print(lemmatizer.lemmatize( "cacti" ))
 Print(lemmatizer.lemmatize( "geese" ))
 Print(lemmatizer.lemmatize( "rocks" ))
 Print(lemmatizer.lemmatize( "python" ))
 Print(lemmatizer.lemmatize( "better" , pos= "a" ))
 Print(lemmatizer.lemmatize( "best" , pos= "a" ))
 Print(lemmatizer.lemmatize( "run" ))
 Print(lemmatizer.lemmatize( "run" , 'v' ))
```

这里有一些我们使用的单词形式的例子。唯一需要注意的是`lemmatize`接受词性参数`pos`。如果未提供，默认为“名词”。这意味着它将试图找到最接近的名词，这可能会给你带来麻烦。如果用形态学复原，请记住！

在下一篇教程中，我们将深入模块附带的 NTLK 语料库，查看所有优秀的文档，它们就在那里等着我们。

# 九。NLTK 语料库

在教程的这一部分，我想花一点时间深入研究我们下载的所有语料库！NLTK 语料库是自然语言数据的集合，绝对值得一看。

NLTK 语料库中的几乎所有文件都遵循相同的规则，通过使用 NLTK 模块来访问它们，但它们并没有什么神奇之处。这些文件大部分是纯文本文件，有些是 XML 文件，有些是其他格式的文件，但是可以手动访问或者在模块和 Python 中访问。我们来谈谈手动查看它们。

根据您的安装，您的`nltk_data`目录可能隐藏在多个位置。要找到它在哪里，请转到您的 Python 目录，NLTK 模块就在那里。如果你不知道在哪里，请使用下面的代码:

```
Import nltk
Print (nltk. __file__ )
```

运行它，输出将是 NLTK 模块`__init__.py`的位置。`data.py`到 NLTK 目录并寻找`data.py`文件。

代码的重要部分是:

```
If sys.platform.startswith( 'win' ):
    # Common locations on Windows:
    Path += [
       Str( r'C:\nltk_data' ), str( r'D:\nltk_data' ), str( r'E:\nltk_data' ),
        Os.path.join(sys.prefix, str( 'nltk_data' )),
        Os.path.join(sys.prefix, str( 'lib' ), str( 'nltk_data' )),
        Os.path.join(os.environ.get(str( 'APPDATA' ), str( 'C:\\' )), str( 'nltk_data' ))
     ]
Else :
    # Common locations on UNIX & OS X:
    Path += [
        Str( '/usr/share/nltk_data' ),
        Str( '/usr/local/share/nltk_data' ),
        Str( '/usr/lib/nltk_data' ),
        Str( '/usr/local/lib/nltk_data' )
    ]
```

在那里，您可以看到`nltk_data`的各种可能的目录。如果你在 Windows 上，它可能在你的`appdata`中，在一个本地目录中。要做到这一点，你需要打开你的文件浏览器，到顶部，键入`%appdata%`。

接下来点击`roaming`并找到`nltk_data`目录。在那里，您将找到您的语料库文件。完整的路径如下所示:

```
C: \Users \swayam.mittal\AppData \Roaming \nltk _data \corpora
```

这里有所有可用的语料库，包括书籍、聊天、电影评论等等。

我们现在将讨论如何通过 NLTK 访问这些文档。如您所见，这些主要是文本文档，因此您可以使用普通 Python 代码打开和阅读文档。也就是说，NLTK 模块有一些很好的方法来处理语料库，所以您可能会发现使用它们的方法很实用。这里有一个我们如何打开古腾堡圣经并阅读前几行的例子:

```
From nltk.tokenize import sent_tokenize, PunktSentenceTokenizer
From nltk.corpus import gutenberg# sample text
Sample = gutenberg.raw( "bible-kjv.txt" )Tok = sent_tokenize(sample)For x in range( 5 ):
    Print(tok[x])
```

更高级的数据集之一是`wordnet`。Wordnet 是单词、定义、用法示例、同义词、反义词等的集合。接下来我们将深入使用 wordnet。

# X.NLTK 和 Wordnet

WordNet 是普林斯顿大学创建的英语词汇数据库，是 NLTK 语料库的一部分。

您可以结合使用 WordNet 和 NLTK 模块来查找单词含义、同义词、反义词等等。下面介绍几个例子。

首先，您需要导入`wordnet`:

```
From nltk.corpus import wordnet
```

然后我们计划用`program`这个词来寻找同义词:

```
Syns = wordnet.synsets( "program" )
```

同义词的一个例子:

```
Print (syns[ 0 ].name())# plan.n.01
```

就这个词:

```
Print(syns[ 0 ] .lemmas ()[ 0 ] .name ())# plan
```

第一个同义词的定义:

```
Print(syns[ 0 ].definition())# a series of steps to be carried out or goals to be accomplished
```

单词用法的例子:

```
Print(syns[ 0 ].examples())# [ 'they drew up a six-step plan', 'they discussed plans for a new bond issue']
```

接下来，我们如何识别一个词的同义词和反义词？这些形式是同义的，然后你可以用`.antonyms`找到形式的反义词。所以我们可以填充一些列表，比如:

```
Synonyms = []
Antonyms = []For syn in wordnet.synsets( "good" ):
    For l in syn.lemmas():
        Synonyms.append(l.name())
        If l.antonyms():
            Antonyms.append(l.antonyms()[ 0 ].name()) Print( set (synonyms))
 Print( set (antonyms)) '' ' {' beneficial ', ' just ', ' upright ', ' thoroughly ', ' in _force ', ' well ', ' skilful ', ' skillful ', ' sound ', ' unspoiled ', ' expert ', ' Proficient ', ' in _effect ', ' honorable ', ' adept ', ' secure ', ' commodity ', ' estimable ', ' soundly ', ' right ', ' respectable ', ' good ', ' serious ', ' ripe ', ' salutary ', ' dear ', ' practiced ', ' goodness ', ' safe ', ' effective ', ' unspoilt ', ' dependable ', ' undecomposed ', ' honest ', ' full ', ' near ', ' trade_good '} {' evil ', ' evilness ', ' bad ', ' badness ', ' ill '} ' ''
```

正如你所看到的，我们的同义词不仅仅是反义词，因为我们只查找第一种形式的反义词，但是你可以很容易地通过对单词`bad`执行完全相同的过程来平衡这一点。

接下来，我们可以很容易地使用 WordNet 来比较两个单词及其时态的相似性，并结合 Wu 和 Palmer 方法进行语义关联。

让我们比较一下名词`ship`和`boat`:

```
W1 = wordnet.synset( 'ship.n.01' )
W2 = wordnet.synset( 'boat.n.01' )
print (w1.wup_similarity(w2))# 0.9090909090909091W1 = wordnet.synset( 'ship.n.01' )
W2 = wordnet.synset( 'car.n.01' )
print (w1.wup_similarity(w2))# 0.6956521739130435W1 = wordnet.synset( 'ship.n.01' )
W2 = wordnet.synset( 'cat.n.01' )
print (w1.wup_similarity(w2))# 0.38095238095238093
```

接下来，我们将讨论一些问题，并开始讨论文本分类的话题。

# XI。NLTK 文本分类

现在我们已经熟悉了 NLTK，让我们尝试处理文本分类。文本分类的目标可以非常广泛。也许我们试图将文本归类为政治或军事。也许我们试着按作者性别分类。一个相当流行的文本分类任务是识别文本主体是垃圾邮件还是非垃圾邮件，例如电子邮件过滤器。在我们的例子中，我们将尝试创建一个情感分析算法。

为此，我们首先尝试使用一个属于 NLTK 语料库的电影评论数据库。从那里，我们将尝试使用词汇作为“特征”，这是“积极”或“消极”电影评论的一部分。NLTK 语料库`movie_reviews`数据集有注释，它们被标记为正面或负面。这意味着我们可以训练和测试这些数据。首先，让我们对数据进行预处理。

```
Import nltk
import random
from nltk.corpus import movie_reviewsDocuments = [(list(movie_reviews.words(fileid)), category)
             For category in movie_reviews.categories()
              for fileid in movie_reviews.fileids(category)]Random.shuffle(documents)Print(documents[ 1 ])All_words = []
For w in movie_reviews.words():
    All_words.append(w.lower())All_words = nltk.FreqDist(all_words)
Print(all_words.most_common( 15 ))
Print(all_words[ "stupid" ])
```

运行此脚本可能需要一些时间，因为电影评论数据集有点大。我们来介绍一下这里发生的事情。

导入我们想要的数据集后，您将看到:

```
Documents = [( list (movie_reviews. words (fileid)), category)
              for category in movie_reviews.categories()
              for fileid in movie_reviews.fileids(category)]
```

基本上用简单的英语把上面的代码翻译成:在每个类别中(我们有 forward 和 exclusive)，选择所有的文件 ID(每个评论都有自己的 ID)，然后把文件 ID 的`word_tokenized`版本(单词列表)后面跟着一个肯定或否定的标签存储在一个大列表中。

接下来，我们使用`random`来打乱我们的文件。这是因为我们要训练和测试。如果我们将它们按顺序排列，我们可能会训练所有的负面评论，以及一些正面评论，然后在所有正面评论上进行测试。我们不希望这样，所以我们弄乱了数据。

然后，为了让你看到你正在使用的数据，我们打印出`documents[1]`这是一个大列表，其中第一个元素是单词列表，第二个元素是`pos`或`neg`标签。

接下来，我们要收集我们找到的所有单词，这样我们就可以有一个巨大的典型单词列表。从这里，我们可以执行频率分布，然后找到最常见的单词。如你所见，最流行的“单词”实际上是标点、`the`、`a`等。，但是很快我们就会得到有效的词汇。我们将存储成千上万个最流行的单词，所以这应该不成问题。

```
Print(all_words. most_common( 15 ) )
```

上面给出了 15 个最常用的单词。您也可以按照以下步骤找出一个单词出现的次数:

```
Print  (all_words[ "stupid" ])
```

接下来，我们开始将我们的单词存储为正面或负面电影评论的特征。

# 十二。使用 NLTK 将单词转换成特征

在本教程中，我们基于以前的视频，编辑了一个正面和负面评论中单词的特征列表，以查看正面或负面评论中特定类型单词的趋势。

最初，我们的代码:

```
Import nltk
Import random 
from nltk.corpus import movie_reviewsDocuments = [(list(movie_reviews. words (fileid)), category)
              for category in movie_reviews.categories()
              for fileid in movie_reviews.fileids(category)]Random .shuffle(documents)All_words = []For w in movie_reviews. words ():
    All_words.append(w. lower ())All_words = nltk.FreqDist(all_words)Word_features = list(all_words. keys ())[: 3000 ]
```

几乎和之前一样，只是现在有了一个新的变量`word_features`包含了前 3000 个最常用的单词。接下来，我们将构建一个简单的函数，在我们的正面和负面文档中查找前 3000 个单词，将它们的存在标记为是或否:

```
Def  find_features  (document) :
    Words = set(document)
    Features = {}
    For w in word_features:
        Features[w] = (w in words) Return features
```

下面，我们可以打印出特性集:

```
Print(( find_features(movie_reviews. words( 'neg/cv000_29416.txt' ) ) ) ) )
```

然后，我们可以通过执行以下操作来保存特征布尔值及其相应的正或负类别，从而为我们的所有文档执行此操作:

```
Featuresets = [(find_features(rev), category) for (rev, category) in documents]
```

太棒了，现在我们有了特性和标签，下一步是什么？通常，下一步是继续和训练算法，然后测试它。所以让我们继续这样做，从下一个教程中的朴素贝叶斯分类器开始！

# 十三。NLTK 朴素贝叶斯分类器

是时候选择一个算法，把我们的数据分成训练集和测试集，然后开始了！我们首先使用的算法是朴素贝叶斯分类器。这是一个非常流行的文本分类算法，所以我们只能先尝试一下。然而，在我们可以训练和测试我们的算法之前，我们需要首先将数据分成训练集和测试集。

你可以训练和测试相同的数据集，但这会给你一些严重的偏差，所以你不应该训练和测试完全相同的数据。正因如此，既然我们打乱了数据集，我们就先用 1900 条有正面和负面评论的乱序评论作为训练集。然后我们可以在最后 100 个上测试，看看我们有多准确。

这被称为监督机器学习，因为我们正在向机器呈现数据，并告诉它“这个数据是正的”或“这个数据是负的。”然后，在训练完成后，我们向机器展示一些新数据，并询问计算机基于我们之前所教的内容，我们对新数据的看法。

我们可以通过以下方式分割数据:

```
# set that we'll train our classifier with 
training_ set = featuresets[: 1900 ]# set that we'll test against. 
testing_ set = featuresets[ 1900 :]
```

下面，我们可以定义和训练我们的分类器:

```
Classifier = nltk .NaiveBayesClassifier  .train (training_set)
```

首先，我们简单地调用朴素贝叶斯分类器，并在一行`.train()`中使用它进行训练。

很简单，现在已经训练好了。接下来，我们可以测试它:

```
Print ( "Classifier accuracy percent:" ,(nltk.classify.accuracy(classifier, testing_set)) *100 )
```

嘿，你得到答案了。如果你错过了，我们可以“测试”数据的原因是我们仍然有正确的答案。因此，在测试中，我们将数据呈现给计算机，但不提供正确的答案。如果它正确地猜测了我们所知道的，那么计算机就是正确的。考虑到我们所做的破坏，你和我的准确性可能不同，但你应该看到平均 60–75%的准确性。

接下来，我们可以进一步了解正面或负面评论中最有价值的词语:

```
classifier the .Show _most_informative_features ( 15 )
```

这因人而异，但您应该会看到这样的内容:

```
Most Informative Features
Insulting = True neg : pos = 10.6 : 1.0 
ludicrous = True neg : pos = 10.1 : 1.0 
winslet = True pos : neg = 9.0 : 1.0 
detract = True pos : neg = 8.4 : 1.0 
breathtaking = True pos : neg = 8.1 : 1.0 
Silverstone = True neg : pos = 7.6 : 1.0 
excruciatingly = True neg : pos = 7.6 : 1.0 
warns =True pos : neg = 7.0 : 1.0 
tracy = True pos : neg = 7.0 : 1.0 
insipid = True neg : pos = 7.0 : 1.0 
freddie = True neg : pos = 7.0 : 1.0 
damon = True pos : neg = 5.9 : 1.0 
debate = True pos : neg = 5.9 : 1.0 
ordered = True pos : neg = 5.8 : 1.0 
lang = True pos : neg = 5.7: 1.0
```

这告诉你的是，每个单词都是从负面到正面出现的，反之亦然。所以这里我们可以看到，负面评论中的`insulting`字出现的次数是正面评论的 10.6 倍。`Ludicrous`现在是 10.1。

现在让我们假设你对你的结果完全满意，你想继续，也许用这个分类器来预测正在发生的事情。训练分类器并在需要使用分类器时重新训练它是非常不切实际的。因此，您可以使用`pickle`模块来保存分类器。我们接下来会做。

# 十四。用 NLTK 保存分类器

训练分类器和机器学习算法可能需要很长时间，尤其是在较大的数据集上训练时。我们的其实很小。你能想象每次想开始使用分类器都要训练分类器吗？太恐怖了！相反，我们可以使用`pickle`模块并序列化我们的分类器对象，这样我们所要做的就是简单地加载文件。

那么我们该怎么办呢？第一步是保存对象。为此，你首先需要在脚本顶部导入`pickle`，然后在用分类器进行`.train()`训练之后，你可以调用下面几行:

```
Save_classifier = open ( "naivebayes.pickle" , "wb" )
Pickle. dump (classifier, save_classifier)
Save_classifier. close ()
```

这将打开一个`pickle`文件，并准备写入一些字节数据。然后我们使用`pickle.dump()`来转储数据。`pickle.dump()`第一个论点是你写了什么，第二个论点是你写在哪里。

之后，我们按照要求关闭了文件，这意味着我们现在在脚本的目录中有了一个`pickle`序列化对象！

接下来，我们如何开始使用这个分类器？`.pickle`文件是序列化的对象，我们现在要做的就是把它们读入内存，这和读取任何其他普通文件一样简单。这边走:

```
Classifier_f = open ( "naivebayes.pickle" , "rb" )
Classifier = pickle. load (classifier_f)
Classifier_f. close ()
```

这里我们执行了一个非常相似的过程。我们打开文件来读取字节。然后我们使用`pickle.load()`加载文件并将数据保存到分类器变量中。然后我们关闭文件，就这样。我们现在有了和以前一样的分类器对象！

现在我们可以使用这个对象，每当我们想用它进行分类时，我们不再需要训练我们的分类器。

虽然这一切都很好，但我们可能不会满意我们获得的 60–75%的准确性。其他量词呢？其实分类器有很多，但是我们需要 scikit-learn (sklearn)模块。幸运的是，NLTK 员工认识到了将 sklearn 模块并入 NLTK 的价值，他们为我们构建了一个小 API。这是我们将在下一个教程中做的。

# 十五。NLTK 和 Sklearn

现在我们已经看到了使用分类器是多么容易，现在我们想尝试更多！Python 的最佳模块是 Scikit-learn (sklearn)模块。

如果你想了解更多关于 Scikit-learn 模块的知识，我有一些关于 Scikit-Learn 机器学习的教程。

幸运的是，对我们来说，NLTK 背后的人重视将 sklearn 模块合并到 NLTK 分类器方法中的价值。就这样，他们创造了各种`SklearnClassifier`API。要使用它，您只需要像这样导入它:

```
From nltk.classify.scikitlearn import SklearnClassifier
```

从现在开始，您可以使用任何`sklearn`分类器。例如，让我们介绍朴素贝叶斯算法的更多变体:

```
From sklearn.naive_bayes import MultinomialNB , BernoulliNB
```

之后你如何使用它们？因此，这很简单。

```
MNB_classifier = SklearnClassifier(MultinomialNB())
MNB_classifier .train (training_set)
Print( " MultinomialNB accuracy percent:" ,nltk .classify  .accuracy (MNB_classifier, testing_set))BNB_classifier = SklearnClassifier(BernoulliNB())
BNB_classifier .train (training_set)
Print( "BernoulliNB accuracy percent:" ,nltk .classify  .accuracy (BNB_classifier, testing_set))
```

就这么简单。让我们介绍更多的东西:

```
From sklearn.linear_model import LogisticRegression,SGDClassifier
 from sklearn.svm import SVC, LinearSVC, NuSVC
```

现在，我们所有的分类器应该看起来像这样:

```
Print( "Original Naive Bayes Algo accuracy percent:" , (nltk .classify  .accuracy (classifier, testing_set))* 100 )
classifier the .Show _most_informative_features ( 15 )MNB_classifier = SklearnClassifier(MultinomialNB())
MNB_classifier .train (training_set)
Print( "MNB_classifier accuracy percent:" , (nltk .classify  .accuracy (MNB_classifier, testing_set))* 100 )BernoulliNB_classifier = SklearnClassifier(BernoulliNB())
BernoulliNB_classifier .train (training_set)
Print( "BernoulliNB_classifier accuracy percent:" , (nltk .classify  .accuracy (BernoulliNB_classifier, testing_set))* 100 )LogisticRegression_classifier = SklearnClassifier(LogisticRegression())
LogisticRegression_classifier .train (training_set)
Print( "LogisticRegression_classifier accuracy percent:" , (nltk .classify  .accuracy (LogisticRegression_classifier, testing_set))* 100 )SGDClassifier_classifier = SklearnClassifier(SGDClassifier())
SGDClassifier_classifier .train (training_set)
Print( "SGDClassifier_classifier accuracy percent:" , (nltk .classify  .accuracy (SGDClassifier_classifier, testing_set))* 100 )SVC_classifier = SklearnClassifier(SVC())
SVC_classifier .train (training_set)
Print( "SVC_classifier accuracy percent:" , (nltk .classify  .accuracy (SVC_classifier, testing_set))* 100 )LinearSVC_classifier = SklearnClassifier(LinearSVC())
LinearSVC_classifier .train (training_set)
Print( "LinearSVC_classifier accuracy percent:" , (nltk .classify  .accuracy (LinearSVC_classifier, testing_set))* 100 )NuSVC_classifier = SklearnClassifier(NuSVC())
NuSVC_classifier .train (training_set)
Print( "NuSVC_classifier accuracy percent:" , (nltk .classify  .accuracy (NuSVC_classifier, testing_set))* 100 )
```

运行它的结果应该如下所示:

```
Original Naive Bayes Algo accuracy percent: 63.0 
Most Informative Features
Thematic = True pos : neg = 9.1 : 1.0 
secondly = True pos : neg = 8.5 : 1.0 
narrates = True pos : neg = 7.8 : 1.0 
rounded = True pos : neg = 7.1 : 1.0 
supreme = True pos : neg = 7.1 : 1.0 
Layered = True pos : neg = 7.1 : 1.0 
crappy = True Neg : pos = 6.9 : 1.0 
uplifting = True pos : neg = 6.2 : 1.0 
ugh = True neg : pos = 5.3 : 1.0 
mamet = True pos : neg = 5.1 : 1.0 
gaining = True pos : neg = 5.1 : 1.0 
wanda = True Neg : pos = 4.9 : 1.0 
onset = True neg : pos = 4.9 :1.0 
fantastic = True pos : neg = 4.5 : 1.0 
kentucky = True pos : neg = 4.4 : 1.0 
MNB_classifier accuracy percent: 66.0 
BernoulliNB_classifier accuracy percent: 72.0 
LogisticRegression_classifier accuracy percent: 64.0 
SGDClassifier_classifier accuracy percent: 61.0 
SVC_classifier accuracy percent: 45.0 
LinearSVC_classifier accuracy percent: 68.0 
NuSVC_classifier accuracy percent: 59.0
```

因此，我们可以看到 SVC 错误比正确的更常见，所以我们可能应该丢弃它。但是呢？接下来，我们可以尝试同时使用所有这些算法。一个算法的算法！为此，我们可以创建另一个分类器，并根据其他算法的结果生成分类器的结果。这有点像投票系统，所以我们只需要奇数个算法。这是我们将在下一个教程中讨论的内容。

# 十六。使用 NLTK 组合算法

现在我们知道如何使用一堆算法分类器，就像糖果岛上的一个孩子，告诉他们只能选择一个，我们可能会发现很难只选择一个分类器。好消息是你不必如此！组合分类器算法是一种常用的技术，它是通过创建投票系统来实现的。每个算法有一票，票数最多的被选中。

为此，我们希望我们的新分类器像典型的 NLTK 分类器一样工作，并拥有所有的方法。很简单，使用面向对象编程，我们可以确保从 NLTK 分类器类继承。为此，我们将导入它:

```
From nltk.classify import ClassifierI
from statistics import mode
```

我们还导入`mode`(多数)，因为这将是我们选择最大计数的方式。

现在让我们构建我们的分类器类:

```
Class  VoteClassifier  (ClassifierI) : 
    def  __init__  (self, *classifiers) : 
        self._classifiers = classifiers
```

我们称我们的类为`VoteClassifier`，我们继承 NLTK `ClassifierI`。接下来，我们将分类器列表分配给我们的类`self._classifiers`。

接下来，我们将继续创建我们自己的分类方法。我们打算把它叫做`.classify`，这样我们以后就可以把它叫做`.classify`，就像传统的 NLTK 分类器一样。

```
Def  classify  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v)
        Return mode(votes)
```

很简单，我们在这里做的是遍历我们的分类器对象列表。然后，对于每一个，我们要求它基于特征分类。分类被认为是投票。遍历完成后，我们返回`mode(votes)`，这只是返回投票的模式。

这是我们真正需要的，但我认为另一个参数，信心是有用的。既然有了投票算法，我们也可以统计支持票和反对票的数量，称之为“信心”比如 3/5 票的信心比 5/5 票弱。因此，我们可以从字面上返回投票比例作为信心的衡量标准。这是我们的信心方法:

```
Def  confidence  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v) Choice_votes = votes.count(mode(votes))
        Conf = choice_votes / len(votes)
        Return conf
```

现在让我们把事情放在一起:

```
Import nltk
Import random
From nltk.corpus import movie_reviews
From nltk.classify.scikitlearn import SklearnClassifier
Import pickleFrom sklearn.naive_bayes import MultinomialNB, BernoulliNB
From sklearn.linear_model import LogisticRegression, SGDClassifier
From sklearn.svm import SVC, LinearSVC, NuSVCFrom nltk.classify import ClassifierI
From statistics import mode Class VoteClassifier(ClassifierI):
Def __init__(self, *classifiers): 
self._classifiers = classifiersDef classify(self, features): 
votes = [] 
for c in self._classifiers: 
v = c.classify(features) 
votes.append(v) 
return mode(votes)Def confidence(self, features): 
votes = [] 
for c in self._classifiers: 
v = c.classify(features) 
votes.append(v)Choice_votes = votes.count(mode(votes)) 
conf = choice_votes / len(votes) 
return confDocuments = [(list(movie_reviews.words(fileid)), category)
For category in movie_reviews.categories() 
for fileid in movie_reviews.fileids(category)]Random.shuffle(documents)All_words = []For w in movie_reviews.words():
 All_words.append(w.lower())All _words = nltk.FreqDist(all_ words)Word _features = list(all_ words.keys())[:3000]Def find_features(document):
Words = set(document) 
features = {} 
for w in word_features: 
features[w] = (w in words) Return features#print((find_features(movie_reviews.words('neg/cv000_29416.txt')))))Featuresets = [(find_features(rev), category) for (rev, category) in documents]Training_set = featuresets[:1900]
Testing_set = featuresets[1900:]#classifier = nltk.NaiveBayesClassifier.train(training_set)Classifier_f = open("naivebayes.pickle","rb")
Classifier = pickle.load(classifier_f)
Classifier_f.close() Print("Original Naive Bayes Algo accuracy percent:", (nltk.classify.accuracy(classifier, testing_set))*100)
classifier.show _most_ informative_features (15)MNB_classifier = SklearnClassifier(MultinomialNB())
MNB _classifier.train(training_ set)
Print("MNB _classifier accuracy percent:", (nltk.classify.accuracy(MNB_ classifier, testing_set))*100)BernoulliNB_classifier = SklearnClassifier(BernoulliNB())
BernoulliNB _classifier.train(training_ set)
Print("BernoulliNB _classifier accuracy percent:", (nltk.classify.accuracy(BernoulliNB_ classifier, testing_set))*100)LogisticRegression_classifier = SklearnClassifier(LogisticRegression())
LogisticRegression _classifier.train(training_ set)
Print("LogisticRegression _classifier accuracy percent:", (nltk.classify.accuracy(LogisticRegression_ classifier, testing_set))*100)SGDClassifier_classifier = SklearnClassifier(SGDClassifier())
SGDClassifier _classifier.train(training_ set)
Print("SGDClassifier _classifier accuracy percent:", (nltk.classify.accuracy(SGDClassifier_ classifier, testing_set))*100)##SVC_classifier = SklearnClassifier(SVC()) 
##SVC_classifier.train(training_set) 
##print("SVC_classifier accuracy percent:", (nltk.classify.accuracy(SVC_classifier, testing_set))*100)LinearSVC_classifier = SklearnClassifier(LinearSVC())
LinearSVC _classifier.train(training_ set)
Print("LinearSVC _classifier accuracy percent:", (nltk.classify.accuracy(LinearSVC_ classifier, testing_set))*100)NuSVC_classifier = SklearnClassifier(NuSVC())
NuSVC _classifier.train(training_ set)
Print("NuSVC _classifier accuracy percent:", (nltk.classify.accuracy(NuSVC_ classifier, testing_set))*100) Voted_classifier = VoteClassifier(classifier,
NuSVC_classifier, 
LinearSVC_classifier, 
SGDClassifier_classifier, 
MNB_classifier, 
BernoulliNB_classifier, 
LogisticRegression_classifier)Print("voted _classifier accuracy percent:", (nltk.classify.accuracy(voted_ classifier, testing_set))*100)Print("Classification:", voted _classifier.classify(testing_ set[ 0 ][ 0 ]), "Confidence %:",voted _classifier.confidence(testing_ set[ 0 ][ 0 ])*100)
Print("Classification:", voted _classifier.classify(testing_ set[ 1 ][ 0 ]), "Confidence %:",voted _classifier.confidence(testing_ set[ 1 ][ 0 ])*100)
Print("Classification:", voted _classifier.classify(testing_ set[ 2 ][ 0 ]), "Confidence %:",voted _classifier.confidence(testing_ set[ 2 ][ 0 ])*100)
Print("Classification:", voted _classifier.classify(testing_ set[ 3 ][ 0 ]), "Confidence %:",voted _classifier.confidence(testing_ set[ 3 ][ 0 ])*100)
Print("Classification:", voted _classifier.classify(testing_ set[ 4 ][ 0 ]), "Confidence %:",voted _classifier.confidence(testing_ set[ 4 ][ 0 ])*100)
Print("Classification:", voted _classifier.classify(testing_ set[ 5 ][ 0 ]), "Confidence %:",voted _classifier.confidence(testing_ set[ 5 ][ 0 ])*100)
```

所以在最后，我们运行了一些文本分类器的例子。我们所有的产出:

```
Original Naive Bayes Algo accuracy percent: 66.0
Most Informative Features
                Thematic = True pos : neg = 9.1 : 1.0 
                secondly = True pos : neg = 8.5 : 1.0 
                narrates = True pos : neg = 7.8 : 1.0 
                 layered = True pos : neg = 7.1 : 1.0 
                 rounded = True pos : neg = 7.1 : 1.0 
                 Supreme = True pos : neg = 7.1 : 1.0 
                  crappy = True neg: pos = 6.9 : 1.0 
               uplifting = True pos : neg = 6.2 : 1.0 
                     ugh = True neg : pos = 5.3 : 1.0 
                 gaining = True pos : neg = 5.1 : 1.0 
                   mamet = True pos : neg = 5.1 : 1.0 
                   wanda = True neg : pos = 4.9 : 1.0 
                   onset = True neg : pos = 4.9 :1.0 
               fantastic = True pos : neg = 4.5 : 1.0 
                   milos = True pos : neg = 4.4 : 1.0 
MNB_classifier accuracy percent: 67.0 
BernoulliNB_classifier accuracy percent: 67.0 
LogisticRegression_classifier accuracy percent: 68.0 
SGDClassifier_classifier accuracy percent: 57.99999999999999 
LinearSVC_classifier accuracy percent: 67.0 
NuSVC_classifier accuracy percent: 65.0 
voted_classifier accuracy percent: 65.0 
Classification:  neg Confidence %:100.0 
Classification: pos Confidence %: 57.14285714285714 
Classification:  neg Confidence %: 57.14285714285714 
Classification:  neg Confidence %: 57.14285714285714 
Classification: pos Confidence %: 57.14285714285714 
Classification: pos Confidence %: 85.71428571428571
```

# 十七。使用 NLTK 调查偏倚

在本教程中，我们将讨论一些问题。主要问题是我们有一个相当偏颇的算法。您可以通过注释掉文档的混乱来测试它，然后用前 1900 条进行训练，留下最后 100 条(全部是正面的)注释。测试一下你会发现你的准确率很差。

而是可以用前 100 的数据来测试，都是负数，用 1900 的训练。在这里你会发现准确率很高。这是一个不好的迹象。这可能意味着很多事情，我们有很多选项来解决它。

换句话说，我们正在考虑的项目建议我们继续并使用不同的数据集，因此我们将这样做。最后我们会发现，这个新的数据集还是有一些偏差的，就是它更多的选择了负面的东西。原因是负面评论的负面倾向于正面多于正面。这可以通过一些简单的加权来实现，但也可能很复杂。可能又是一天的教程吧。现在我们要获取一个新的数据集，我们将在下一个教程中讨论。

# 十八。使用 NLTK 改进用于情感分析的训练数据

所以现在是在新数据集上训练的时候了。我们的目标是分析 Twitter 的情绪，所以我们希望数据集中的每个正面和负面陈述都简短。恰好我有 5300+的正面和 5300+的负面影评，这是一个短得多的数据集。我们应该能够从更大的训练集中获得更多的准确性，并更好地适应 Twitter 的推文。

我在这里托管了这两个文件，下载一个短评就能找到。将这些文件保存为`positive.txt`和`negative.txt`。

现在我们可以像以前一样建立新的数据集。需要改变什么？

我们需要一种新的方法来创建我们的“文档”变量，然后我们需要一种新的方法来创建`all_words`变量。真的没问题，我是这样做的:

```
Short_pos = open ( "short_reviews/positive.txt" , "r" ). read ()
Short_neg = open ( "short_reviews/negative.txt" , "r" ). read ()Documents = []For r in short_pos. split ( '\n' ):
    Documents.append( (r, "pos" ) )For r in short_neg. split ( '\n' ):
    Documents.append( (r, "neg" ) ) All_words = []Short_pos_words = word_tokenize(short_pos)
Short_neg_words = word_tokenize(short_neg)For w in short_pos_words:
    All_words.append(w. lower ())For w in short_neg_words:
    All_words.append(w. lower ())All_words = nltk.FreqDist(all_words)
```

接下来，我们还需要调整我们的特征查找功能，主要基于文档中的单词，因为我们的新样本没有漂亮的`.words()`特征。我继续补充了最常用的词:

```
Word_features = list(all_words.keys())[: 5000 ]Def  find_features  (document) :
    Words = word_tokenize(document)
    Features = {}
    For w in word_features:
        Features[w] = (w in words) Return featuresFeaturesets = [(find_features(rev), category) for (rev, category) in documents]
Random.shuffle(featuresets)
```

除此之外，其余都一样。这是一个完整的脚本，以防你我遗漏了什么:

这个过程需要一段时间。你可能想做点别的。我花了大约 30-40 分钟让它全部运行起来，我在 i7 3930k 上运行了它。在撰写本文时(2015 年)，一个通用处理器可能需要几个小时。但这是一次性的过程。

```
Import nltk
import random
from nltk.corpus import movie_reviews
from nltk.classify.scikitlearn import SklearnClassifier
import pickleFrom sklearn.naive_bayes import MultinomialNB , BernoulliNB
from sklearn.linear_model import LogisticRegression, SGDClassifier
from sklearn.svm import SVC, LinearSVC, NuSVCFrom nltk.classify import ClassifierI
from statistics import modeFrom nltk.tokenize import word_tokenize Class  VoteClassifier  (ClassifierI) : 
    def  __init__  (self, *classifiers) :
        Self._classifiers = classifiers Def  classify  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v)
        Return mode(votes) Def  confidence  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v) Choice_votes = votes.count(mode(votes))
        Conf = choice_votes / len(votes)
        Return confShort_pos = open( "short_reviews/positive.txt" , "r" ).read()
Short_neg = open( "short_reviews/negative.txt" , "r" ).read()Documents = []For r in short_pos.split( '\n' ):
    Documents.append( (r, "pos" ) )For r in short_neg.split( '\n' ):
    Documents.append( (r, "neg" ) ) All_words = []Short_pos_words = word_tokenize(short_pos)
Short_neg_words = word_tokenize(short_neg)For w in short_pos_words:
    All_words.append(w.lower())For w in short_neg_words:
    All_words.append(w.lower())All_words = nltk.FreqDist(all_words)Word_features = list(all_words.keys())[: 5000 ]Def  find_features  (document) :
    Words = word_tokenize(document)
    Features = {}
    For w in word_features:
        Features[w] = (w in words) Return features#print((find_features(movie_reviews.words('neg/cv000_29416.txt')))))Featuresets = [(find_features(rev), category) for (rev, category) in documents]Random.shuffle(featuresets)# positive data example: 
training_set = featuresets[: 10000 ]
Testing_set = featuresets[ 10000 :]## 
### negative data example: 
##training_set = featuresets[100:] 
##testing_set = featuresets[:100] Classifier = nltk.NaiveBayesClassifier.train(training_set)
Print( "Original Naive Bayes Algo accuracy percent:" , (nltk.classify.accuracy(classifier, testing_set))* 100 )
Classifier.show_most_informative_features( 15 )MNB_classifier = SklearnClassifier(MultinomialNB())
MNB_classifier.train(training_set)
Print( "MNB_classifier accuracy percent:" , (nltk.classify.accuracy(MNB_classifier, testing_set))* 100 )BernoulliNB_classifier = SklearnClassifier(BernoulliNB())
BernoulliNB_classifier.train(training_set)
Print( "BernoulliNB_classifier accuracy percent:" , (nltk.classify.accuracy(BernoulliNB_classifier, testing_set))* 100 )LogisticRegression_classifier = SklearnClassifier(LogisticRegression())
LogisticRegression_classifier.train(training_set)
Print( "LogisticRegression_classifier accuracy percent:" , (nltk.classify.accuracy(LogisticRegression_classifier, testing_set))* 100 )SGDClassifier_classifier = SklearnClassifier(SGDClassifier())
SGDClassifier_classifier.train(training_set)
Print( "SGDClassifier_classifier accuracy percent:" , (nltk.classify.accuracy(SGDClassifier_classifier, testing_set))* 100 )##SVC_classifier = SklearnClassifier(SVC()) 
##SVC_classifier.train(training_set) 
##print("SVC_classifier accuracy percent:", (nltk.classify.accuracy(SVC_classifier, testing_set))*100)LinearSVC_classifier = SklearnClassifier(LinearSVC())
LinearSVC_classifier.train(training_set)
Print( "LinearSVC_classifier accuracy percent:" , (nltk.classify.accuracy(LinearSVC_classifier, testing_set))* 100 )NuSVC_classifier = SklearnClassifier(NuSVC())
NuSVC_classifier.train(training_set)
Print( "NuSVC_classifier accuracy percent:" , (nltk.classify.accuracy(NuSVC_classifier, testing_set))* 100 ) Voted_classifier = VoteClassifier(
                                  NuSVC_classifier,
                                  LinearSVC_classifier,
                                  MNB_classifier,
                                  BernoulliNB_classifier,
                                  LogisticRegression_classifier)Print( "voted_classifier accuracy percent:" , (nltk.classify.accuracy(voted_classifier, testing_set))* 100 )
```

输出:

```
Original Naive Bayes Algo accuracy percent: 66.26506024096386 
Most Informative Features
              Refreshing = True pos : neg = 13.6 : 1.0 
                captures = True pos : neg = 11.3 : 1.0 
                  stupid = True neg : pos = 10.7 : 1.0 
                  tender = True pos : neg = 9.6 : 1.0 
              meandering = True neg : pos = 9.1 : 1.0 
                      Tv = True neg : pos = 8.6 : 1.0 
                 low-key = TruePos : neg = 8.3 : 1.0 
              thoughtful = True pos : neg = 8.1 : 1.0 
                   banal = True neg : pos = 7.7 : 1.0 
              amateurish = True neg : pos = 7.7 : 1.0 
                terrific = True pos : neg = 7.6 : 1.0 
                  record = True Pos : neg = 7.6 : 1.0 
             captivating = True pos : neg = 7.6 :1.0 
                portrait = True pos : neg = 7.4 : 1.0 
                 culture = True pos : neg = 7.3 : 1.0 
MNB_classifier accuracy percent: 65.8132530120482 
BernoulliNB_classifier accuracy percent: 66.71686746987952 
LogisticRegression_classifier accuracy percent: 67.16867469879519 
SGDClassifier_classifier accuracy percent: 65.8132530120482 
LinearSVC_classifier accuracy percent: 66.71686746987952 
NuSVC_classifier accuracy percent: 60.09036144578314 
voted_classifier accuracy percent: 65.66265060240963
```

是的，我打赌你花了一段时间，所以在下一个教程中我们将谈论`pickle`的一切！

# 十九。使用 NLTK 创建情感分析模块

有了这个新的数据集和新的分类器，我们可以继续前进。您可能已经注意到，这个新数据集需要更长的时间来训练，因为它是一个更大的集合。我已经向你展示了，通过`pickel`序列化或序列化训练好的分类器，我们实际上可以节省很多时间。这些分类器只是对象。

我已经向您展示了如何使用它`pickel`来实现它，所以我鼓励您亲自尝试一下。如果你需要帮助，我会粘贴完整的代码...但是要小心，自己动手！

这个过程需要一段时间。你可能想做点别的。我花了大约 30-40 分钟让它全部运行起来，我在 i7 3930k 上运行了它。在撰写本文时(2015 年)，一个通用处理器可能需要几个小时。但这是一次性的过程。

```
Import nltk
 import random
 #from nltk.corpus import movie_reviews 
from nltk.classify.scikitlearn import SklearnClassifier
 import pickle
 from sklearn.naive_bayes import MultinomialNB , BernoulliNB
 from sklearn.linear_model import LogisticRegression, SGDClassifier
 from sklearn.svm import SVC, LinearSVC, NuSVC
 from nltk. Classify import ClassifierI
 from statistics import mode
 from nltk.tokenize import Word_tokenizeClass  VoteClassifier  (ClassifierI) : 
    def  __init__  (self, *classifiers) :
        Self._classifiers = classifiers Def  classify  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v)
        Return mode(votes) Def  confidence  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v) Choice_votes = votes.count(mode(votes))
        Conf = choice_votes / len(votes)
        Return confShort_pos = open( "short_reviews/positive.txt" , "r" ).read()
Short_neg = open( "short_reviews/negative.txt" , "r" ).read()# move this up here
All_words = []
Documents = [] # j is adject, r is adverb, and v is verb 
#allowed_word_types = ["J","R","V"] 
allowed_word_types = [ "J" ]For p in short_pos.split( '\n' ):
    Documents.append( (p, "pos" ) )
    Words = word_tokenize(p)
    Pos = nltk.pos_tag(words)
    For w in pos:
         if w[ 1 ][ 0 ] in allowed_word_types:
            All_words.append(w[ 0 ].lower()) For p in short_neg.split( '\n' ):
    Documents.append( (p, "neg" ) )
    Words = word_tokenize(p)
    Pos = nltk.pos_tag(words)
    For w in pos:
         if w[ 1 ][ 0 ] in allowed_word_types:
            All_words.append(w[ 0 ].lower()) Save_documents 
= open( "pickled_algos/documents.pickle" , "wb" )
Pickle.dump(documents, save_documents)
Save_documents.close() All_words = nltk.FreqDist(all_words) Word_features = list(all_words.keys())[: 5000 ] Save_word_features = open( "pickled_algos/word_features5k.pickle" , "wb" )
Pickle.dump(word_features, save_word_features)
Save_word_features.close() Def  find_features  (document) :
    Words = word_tokenize(document)
    Features = {}
    For w in word_features:
        Features[w] = (w in words) Return featuresFeaturesets = [(find_features(rev), category) for (rev, category) in documents]Random.shuffle(featuresets)
Print(len(featuresets))Testing_set = featuresets[ 10000 :]
Training_set = featuresets[: 10000 ] Classifier = nltk.NaiveBayesClassifier.train(training_set)
Print( "Original Naive Bayes Algo accuracy percent:" , (nltk.classify.accuracy(classifier, testing_set))* 100 )
Classifier.show_most_informative_features( 15 )############### 
save_classifier = open( "pickled_algos/originalnaivebayes5k.pickle" , "wb" )
Pickle.dump(classifier, save_classifier)
Save_classifier.close()MNB_classifier = SklearnClassifier(MultinomialNB())
MNB_classifier.train(training_set)
Print( "MNB_classifier accuracy percent:" , (nltk.classify.accuracy(MNB_classifier, testing_set))* 100 )Save_classifier = open( "pickled_algos/MNB_classifier5k.pickle" , "wb" )
Pickle.dump(MNB_classifier, save_classifier)
Save_classifier.close()BernoulliNB_classifier = SklearnClassifier(BernoulliNB())
BernoulliNB_classifier.train(training_set)
Print( "BernoulliNB_classifier accuracy percent:" , (nltk.classify.accuracy(BernoulliNB_classifier, testing_set))* 100 )Save_classifier = open( "pickled_algos/BernoulliNB_classifier5k.pickle" , "wb" )
Pickle.dump(BernoulliNB_classifier, save_classifier)
Save_classifier.close()LogisticRegression_classifier = SklearnClassifier(LogisticRegression())
LogisticRegression_classifier.train(training_set)
Print( "LogisticRegression_classifier accuracy percent:" , (nltk.classify.accuracy(LogisticRegression_classifier, testing_set))* 100 )Save_classifier = open( "pickled_algos/LogisticRegression_classifier5k.pickle" , "wb" )
Pickle.dump(LogisticRegression_classifier, save_classifier)
Save_classifier.close() LinearSVC_classifier = SklearnClassifier(LinearSVC())
LinearSVC_classifier.train(training_set)
Print( "LinearSVC_classifier accuracy percent:" , (nltk.classify.accuracy(LinearSVC_classifier, testing_set))* 100 )Save_classifier = open( "pickled_algos/LinearSVC_classifier5k.pickle" , "wb" )
Pickle.dump(LinearSVC_classifier, save_classifier)
Save_classifier.close() ##NuSVC_classifier = SklearnClassifier(NuSVC()) 
##NuSVC_classifier.train(training_set) 
##print("NuSVC_classifier accuracy percent:", (nltk.classify.accuracy(NuSVC_classifier, testing_set))*100) SGDC_classifier = SklearnClassifier(SGDClassifier())
SGDC_classifier.train(training_set)
Print( "SGDClassifier accuracy percent:" ,nltk.classify.accuracy(SGDC_classifier, testing_set)* 100 )Save_classifier = open( "pickled_algos/SGDC_classifier5k.pickle" , "wb" )
Pickle.dump(SGDC_classifier, save_classifier)
Save_classifier.close()
```

现在你只需要运行一次。如果您愿意，您可以随时运行它，但是现在您已经准备好创建一个情感分析模块了。这就是我们所说的`sentiment_mod.py`文件:

```
#File: sentiment_mod.pyImport nltk
 import random
 #from nltk.corpus import movie_reviews 
from nltk.classify.scikitlearn import SklearnClassifier
 import pickle
 from sklearn.naive_bayes import MultinomialNB , BernoulliNB
 from sklearn.linear_model import LogisticRegression, SGDClassifier
 from sklearn.svm import SVC, LinearSVC, NuSVC
 from nltk. Classify import ClassifierI
 from statistics import mode
 from nltk.tokenize import Word_tokenizeClass  VoteClassifier  (ClassifierI) : 
    def  __init__  (self, *classifiers) :
        Self._classifiers = classifiers Def  classify  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v)
        Return mode(votes) Def  confidence  (self, features) :
        Votes = []
        For c in self._classifiers:
            v = c.classify(features)
            Votes.append(v) Choice_votes = votes.count(mode(votes))
        Conf = choice_votes / len(votes)
        Return conf Documents_f = open( "pickled_algos/documents.pickle" , "rb" )
Documents = pickle.load(documents_f)
Documents_f.close() Word_features5k_f = open( "pickled_algos/word_features5k.pickle" , "rb" )
Word_features = pickle.load(word_features5k_f)
Word_features5k_f.close() Def  find_features  (document) :
    Words = word_tokenize(document)
    Features = {}
    For w in word_features:
        Features[w] = (w in words) Return features Featuresets_f 
= open( "pickled_algos/featuresets.pickle" , "rb" )
Featuresets = pickle.load(featuresets_f)
Featuresets_f.close()Random.shuffle(featuresets)
Print(len(featuresets))Testing_set = featuresets[ 10000 :]
Training_set = featuresets[: 10000 ] Open_file 
= open( "pickled_algos/originalnaivebayes5k.pickle" , "rb" )
Classifier = pickle.load(open_file)
Open_file.close()Open_file 
= open( "pickled_algos/MNB_classifier5k.pickle" , "rb" )
MNB_classifier = pickle.load(open_file)
Open_file.close() Open_file 
= open( "pickled_algos/BernoulliNB_classifier5k.pickle" , "rb" )
BernoulliNB_classifier = pickle.load(open_file)
Open_file.close()Open_file 
= open( "pickled_algos/LogisticRegression_classifier5k.pickle" , "rb" )
LogisticRegression_classifier = pickle.load(open_file)
Open_file.close()Open_file 
= open( "pickled_algos/LinearSVC_classifier5k.pickle" , "rb" )
LinearSVC_classifier = pickle.load(open_file)
Open_file.close()Open_file 
= open( "pickled_algos/SGDC_classifier5k.pickle" , "rb" )
SGDC_classifier = pickle.load(open_file)
Open_file.close() Voted_classifier = VoteClassifier(
                                  Classifier,
                                  LinearSVC_classifier,
                                  MNB_classifier,
                                  BernoulliNB_classifier,
                                  LogisticRegression_classifier) Def  sentiment  (text) :
    Feats = find_features(text)
    Return voted_classifier.classify(feats),voted_classifier.confidence(feats)
```

所以在这里，除了最后的功能，没有什么新的，很简单。这个功能是从这里与我们交互的关键。这个函数，我们称之为“情感”，接受一个参数，文本。这里，我们使用我们创建的`find_features`函数来分解这些特性。我们现在要做的就是用我们的投票分类器返回分类，返回分类的置信度。

有了这个，我们现在可以使用这个文件，以及情感功能，作为一个模块。以下是使用此模块的示例脚本:

```
Import sentiment_mod as sPrint(s.sentiment( "This movie was awesome! The acting was great, plot was wonderful, and there were pythons...so yea!" ))
Print(s.sentiment( "This movie was utter junk. There were absolutely 0 pythons. I don't see what the point was at all. Horrible movie, 0/10" ))
```

不出所料，`python`对电影的评价显然是好的，没有一部`python`电影是垃圾。两人都有百分百的信心。

我花了大约 5 秒钟导入模块，因为我们保存了分类器，如果不保存可能需要 30 分钟。感谢`pickle`你的时间，根据你的处理器会有很大的差异。如果你继续下去，我会说你可能也想看`joblib`。

现在我们有了这个伟大的模块，它很容易工作，我们能做什么？我建议大家去 Twitter 做实时情绪分析！

# XX。NLTK 推特情感分析

现在我们有了情感分析模块，我们可以将它应用于任何文本，但最好是短文本，比如 Twitter！为此，我们将把本教程与 Twitter 流 API 教程结合起来。

本教程的初始代码是:

```
From tweepy import Stream
 from tweepy import OAuthHandler
 from tweepy.streaming import StreamListener #consumer key, consumer secret, access token, access secret. 
ckey= "fsdfasdfsafsffa" 
csecret= "asdfsadfsadfsadf" 
atoken= "asdf-aassdfs" 
asecret= "asdfsadfsdafsdafs"Class  listener  (StreamListener) : Def  on_data  (self, data) :
        Print(data)
        Return ( True ) Def  on_error  (self, status) : 
        print statusAuth = OAuthHandler(ckey, csecret)
Auth.set_access_token(atoken, asecret)twitterStream = Stream(auth, listener())
twitterStream.filter(track=[ "car" ])
```

这足以打印包含单词的流媒体直播 tweet 的所有数据。我们可以使用`json`模块`json.loads(data)`加载数据变量，然后可以引用具体的`tweet`:

```
Tweet = all_data[ "text" ]
```

因为我们有一条 tweet，所以我们可以很容易地将它传递给我们的`sentiment_mod`模块。

```
From tweepy import Stream
 from tweepy import OAuthHandler
 from tweepy.streaming import StreamListener
 import json
 import sentiment_mod as s#consumer key, consumer secret, access token, access secret. 
ckey= "asdfsafsafsaf" 
csecret= " 
asdfasdfsadfsa " atoken= "asdfsadfsafsaf-asdfsaf" 
asecret= "asdfsadfsadfsadfsadfsad"From twitterapistuff import *Class  listener  (StreamListener) : Def  on_data  (self, data) : All_data = json.loads(data) Tweet = all_data[ "text" ]
        Sentiment_value, confidence = s.sentiment(tweet)
        Print(tweet, sentiment_value, confidence) If confidence* 100 >= 80 :
            Output = open( "twitter-out.txt" , "a" )
            Output.write(sentiment_value)
            Output.write( '\n' )
            Output.close() Return  True Def  on_error  (self, status) :
        Print(status)Auth = OAuthHandler(ckey, csecret)
Auth.set_access_token(atoken, asecret)twitterStream = Stream(auth, listener())
twitterStream.filter(track=[ "happy" ])
```

除此之外，我们还将结果保存到输出文件`twitter-out.txt`。

接下来，图表不完整的数据分析是什么？让我们结合另一个教程，从 Twitter API 上的情绪分析中绘制一个实时流图。

# 二十一。使用 NLTK 绘制 Twitter 实时情感分析

现在我们已经从 Twitter 流 API 中获得了实时数据，为什么没有显示情绪趋势的活动图？为此，我们将本教程与 matplotlib 绘图教程相结合。

如果你想了解更多关于代码是如何工作的，请看这篇教程。否则:

```
Import matplotlib.pyplot as plt
 import matplotlib.animation as animation
 from matplotlib import style
 import timeStyle.use( "ggplot" )Fig = plt.figure()
Ax1 = fig.add_subplot( 1 , 1 , 1 )Def  animate  (i) : 
    pullData = open( "twitter-out.txt" , "r" ).read()
    Lines = pullData.split( '\n' ) Xar = []
    Yar = [] x = 0 
    y = 0 For l in lines[- 200 :]:
        x += 1 
        if  "pos"  in l:
            y += 1 
        elif  "neg"  in l:
            y -= 1 Xar.append(x)
        Yar.append(y) Ax1.clear()
    Ax1.plot(xar,yar)
Ani = animation.FuncAnimation(fig, animate, interval= 1000 )
Plt.show()
```

# 二十二。斯坦福 NER 标记和命名实体识别

斯坦福 NER 标记为 NLTK 的命名实体识别(NER)分类器提供了一种替代方案。这个标记在很大程度上被视为命名实体识别的标准，但是因为它使用高级统计学习算法，所以它的计算开销比 NLTK 提供的选项更大。

斯坦福 NER 标记的一大优势是我们有几种不同的模型来提取命名实体。我们可以使用以下任何一种方法:

*   识别位置、人员和组织的三种模型
*   用于识别位置、人员、组织和其他实体的四种模型
*   七种类型的模型，标识位置、人员、组织、时间、金钱、百分比和日期

为了继续，我们需要下载模型和`jar`文件，因为 NER 分类器是用 Java 编写的。这些可以从斯坦福自然语言处理小组免费获得。NTLK 为了方便我们，NLTK 提供了斯坦福标记器的包装器，所以我们可以用最好的语言(当然是 Python)来使用！

`StanfordNERTagger`传递给该类的参数包括:

*   分类模型的路径(使用以下三种类型的模型)
*   `jar`斯坦福标记文件的路径
*   训练数据编码(默认为 ASCII)

下面是我们如何使用三种类型的模型来设置标记句子:

```
# -*- coding: utf-8 -*-From nltk.tag import StanfordNERTagger
 from nltk.tokenize import word_tokenizeSt = StanfordNERTagger( '/usr/share/stanford-ner/classifiers/english.all.3class.distsim.crf.ser.gz' ,
                        '/usr/share/stanford-ner/stanford-ner.jar' ,
                       Encoding= 'utf-8' )Text = 'While in France, Christine Lagarde discussed short-term stimulus efforts in a recent interview with the Wall Street Journal.'Tokenized_text = word_tokenize(text)
Classified_text = st.tag(tokenized_text)Print(classified_text)
```

一旦我们遵循分词并对句子进行分类，我们将看到标记产生以下元组列表:

```
[('While', 'O'), ('in', 'O'), ('France', 'LOCATION'), (',', 'O'), ('Christine', 'PERSON') , ('Lagarde', 'PERSON'), ('discussed', 'O'), ('short-term', 'O'), ('stimulus', 'O'), ('efforts', 'O '), ('in', 'O'), ('a', 'O'), ('recent', 'O'), ('interview', 'O'), ('with', 'O '), ('the', 'O'), ('Wall', 'ORGANIZATION'), ('Street', 'ORGANIZATION'), ('Journal', 'ORGANIZATION'), ('.', 'O ')]
```

太好了！每个标签使用`PERSON`、`LOCATION`、`ORGANIZATION`或`O`标签(使用我们的三种型号)。`O`仅表示其他未命名的实体。

这个列表现在可以用来测试带注释的数据，我们将在下一个教程中介绍。

# 二十三。检验 NLTK 和斯坦福 NER 标记的准确性

我们知道如何使用两种不同的 NER 分类器！但是我们应该选择哪一个，NLTK 还是斯坦福？让我们做一些测试来找出答案。

我们首先需要一些标记的参考数据来测试我们的 NER 分类器。获取这些数据的一种方法是找到大量文章，并将每个标签标记为命名实体(例如，人、组织、位置)或其他非命名实体。然后，我们可以用我们知道的正确标签来测试我们单独的 NER 分类器。

遗憾的是，这非常耗时！好消息是，有一个手动注释的数据集，可以免费获得，包含超过 16，000 个英语句子。还有德语、西班牙语、法语、意大利语、荷兰语、波兰语、葡萄牙语和俄语的数据集！

这是数据集中的一个带注释的句子:

```
Founding O 
member O 
Kojima I -PER
Minoru I -PER
Played O 
guitar O 
on O 
Good I -MISC
Day I -MISC
, O 
and O 
Wardanceis the I -misc
Cover O 
of O 
A O 
Song O 
by O 
UK the I -LOC
Post O 
punk O 
industrial O 
band O 
Killing I -ORG
Joke I -ORG
. O
```

让我们读取、分割和操作数据，使其成为更好的测试格式。

```
Import nltk
from nltk.tag import StanfordNERTagger
from nltk.metrics.scores import accuracyRaw_annotations = open( "/usr/share/wikigold.conll.txt" ).read()
Split_annotations = raw_annotations.split()# Amend class annotations to reflect Stanford's NERTagger 
for n,i in enumerate(split_annotations):
     if i == "I-PER" :
        Split_annotations[n] = "PERSON" 
    if i == "I-ORG" :
        Split_annotations[n] = "ORGANIZATION" 
    if i == "I-LOC" :
        Split_annotations[n] = "LOCATION"# Group NE data into tuples 
def  group  (lst, n) : 
  for i in range( 0 , len(lst), n):
    Val = lst[i:i+n]
    If len(val) == n:
       yield tuple(val)Reference_annotations = list(group(split_annotations, 2 ))
```

好的，看起来不错！然而，我们还需要将这些数据的“干净”形式粘贴到我们的 NER 分类器中。让我们开始吧。

```
Pure_tokens = split_annotations[::2]
```

它读入数据，按空白分割，然后以 2 为增量获取所有内容的子集(从第 0 个元素开始)。这将产生一个类似于下面(较小的)示例的数据集:

```
['Founding', 'member', 'Kojima', 'Minoru', 'played', 'guitar', 'on', 'Good', 'Day', ',', 'and', 'Wardanceis', ' Cover', 'of', 'a', 'song', 'by', 'UK', 'post', 'punk', 'industrial', 'band', 'Killing', 'Joke', '.' ]
```

让我们继续测试 NLTK 分类器:

```
Tagged_words = nltk.pos_tag(pure_tokens)
nltk_unformatted_prediction = nltk.ne_chunk(tagged_words)
```

由于 NLTK NER 分类器生成树(包括 POS 标签)，我们需要做一些额外的数据操作来获得测试的正确形式。

```
#Convert prediction to multiline string and then to list (includes pos tags)
Multiline_string = nltk.chunk.tree2conllstr(nltk_unformatted_prediction)
Listed_pos_and_ne = multiline_string.split()# Delete pos tags and rename
Del listed_pos_and_ne[ 1 :: 3 ]
Listed_ne = listed_pos_and_ne# Amend class  annotations  for  consistency  with  reference_annotations
 for n,i in enumerate(listed_ne):
     if i == "B-PERSON" :
        Listed_ne[n] = "PERSON" 
    if i == "I-PERSON" :
        Listed_ne[n] = "PERSON"     
    if i == "B-ORGANIZATION" :
        Listed_ne[n] = "ORGANIZATION" 
    if i == "I-ORGANIZATION" :
        Listed_ne[n] = "ORGANIZATION" 
    if i == "B-LOCATION" :
        Listed_ne[n] = "LOCATION" 
    if i == "I-LOCATION" :
        Listed_ne[n] = "LOCATION" 
    if i == "B-GPE" :
        Listed_ne[n] = "LOCATION" 
    if i == "I-GPE" :
        Listed_ne[n] = "LOCATION"# Group prediction into tuples
Nltk_formatted_prediction = list(group(listed_ne, 2 ))
```

现在我们可以测试 NLTK 的准确性。

```
Nltk_accuracy = accuracy(reference_annotations, nltk_formatted_prediction) print(nltk_accuracy)
```

哇，准确率`.8971`！

现在让我们测试斯坦福分类器。因为这个分类器以元组的形式生成输出，所以测试不需要更多的数据操作。

```
St = StanfordNERTagger( '/usr/share/stanford-ner/classifiers/english.all.3class.distsim.crf.ser.gz' ,
                        '/usr/share/stanford-ner/stanford-ner.jar' ,
                       Encoding= 'utf-8' )                  
Stanford_prediction = st.tag(pure_tokens)
Stanford_accuracy = accuracy(reference_annotations, stanford_prediction)
Print (stanford_accuracy)
```

`.9223`准确率！更好！

如果你想画这个，这里有一些额外的代码。如果您想进一步了解这是如何工作的，请查看 matplotlib 系列:

```
Import numpy as np
Import matplotlib.pyplot as plt
from matplotlib import styleStyle.use( 'fivethirtyeight' )N = 1 
ind = np.arange(N) # the x locations for the groups 
width = 0.35  # the width of the barsFig, ax = plt.subplots()Stanford_percentage = stanford_accuracy * 100 
rects1 = ax.bar(ind, stanford_percentage, width, color= 'r' )Nltk_percentage = nltk_accuracy * 100 
rects2 = ax.bar(ind+width, nltk_percentage, width, color= 'y' )# add some text for labels, title and axes ticks 
ax.set_xlabel( 'Classifier' )
Ax.set_ylabel( 'Accuracy (by percentage)' )
Ax.set_title( 'Accuracy by NER Classifier' )
Ax.set_xticks(ind+width)
Ax.set_xticklabels( ( '' ) )Ax.legend( (rects1[ 0 ], rects2[ 0 ]), ( 'Stanford' , 'NLTK' ), bbox_to_anchor=( 1.05 , 1 ), loc= 2 , borderaxespad= 0\. )Def  autolabel  (rects) : 
    # attach some text labels 
    for rect in rects:
        Height = rect.get_height()
        Ax.text(rect.get_x()+rect.get_width()/ 2\. , 1.02 *height, '%10.2f' % float(height),
                Ha= 'center' , va= 'bottom' )Autolabel(rects1)
Autolabel(rects2)Plt.show()
```

![](img/05a7ff6e1356ae0874adb88a33f8ffe6.png)

# 二十四。测试 NLTK 和斯坦福 NER 标记的速度

我们已经测试了我们的 NER 分类器的准确性，但是在决定使用哪个分类器时，还有更多的问题需要考虑。我们来测试一下速度！

我们知道我们在比较同样的东西，我们将在同一篇文章中测试它。在 NBC 新闻中使用这一集:

```
House Speaker John Boehner became animated Tuesday over  the proposed Keystone Pipeline, castigating the Obama administration for  not having the project.Republican House Speaker John Boehner says there's "nothing complex about the Keystone Pipeline,"  and  that  it 's time  to build it ."Complex? You think the Keystone Pipeline is complex?!" Boehner responded to a questioner. "It's been under study for five years! We build pipelines in America every day. Do you realize that are 200,000 miles of pipelines in the United States? "At The Speaker Wentworth ON : "And at The only reason at The President is's Involved in at The Keystone Pipeline IS Because IT Crosses AN International's boundary the Listen, WE CAN Build IT There's Nothing Complex the About at The Keystone Pipeline - IT's Time to Build IT..."Of Said Boehner at The President is NO excuse HAD AT the this Point to  not give at The Pipeline at The Go-Ahead the After  at The State Department Report Released A ON catalog on Friday Indicating, at The Project Impact Would have have A minimal ON  at The Environment.Republicans have long pushed for construction of  the project, which enjoys some measure of Democratic support as well. The GOP is  considering conditioning an extension of  the debt limit on approval of  the project by Obama.The White House, though, has said that  it has no timetable for a final decision on  the project.
```

首先，我们执行导入，并通过阅读和分词来处理文章。

```
# -*- coding: utf-8 -*-Import nltk
 import os
 Import numpy as np
Import matplotlib.pyplot as plt
 from matplotlib import style
 from nltk import pos_tag
 from nltk.tag import StanfordNERTagger
 from nltk.tokenize import word_tokenizeStyle.use( 'fivethirtyeight' )# Process text 
def  process_text  (txt_file) : 
    raw_text = open( "/usr/share/news_article.txt" ).read()
    Token_text = word_tokenize(raw_text)
    Return token_text
```

太好了！现在让我们写一些函数来分解我们的分类任务。因为 NLTK NEG 分类器需要一个 POS 标记，所以我们将在 NLTK 函数中添加一个 POS 标记。

```
# Stanford NER tagger 
def  stanford_tagger  (token_text) : 
    st = StanfordNERTagger( '/usr/share/stanford-ner/classifiers/english.all.3class.distsim.crf.ser.gz' ,
                             '/usr/share/stanford-ner /stanford-ner.jar' ,
                            Encoding= 'utf-8' )   
    Ne_tagged = st.tag(token_text)
    Return (ne_tagged)# NLTK POS and NER 
taggers def  nltk_tagger  (token_text) :
    Tagged_words = nltk.pos_tag(token_text)
    Ne_tagged = nltk.ne_chunk(tagged_words)
    Return (ne_tagged)
```

每个分类器都需要阅读文章并对命名实体进行分类，因此我们将这些函数包装在一个更大的函数中，以使计时更容易。

```
Def  stanford_main  () :
    Print(stanford_tagger(process_text(txt_file)))Def  nltk_main  () : 
    print(nltk_tagger(process_text(txt_file)))
```

当我们调用我们的程序时，我们调用这些函数。我们将`os.times()`在函数调用中包装我们的`stanford_main()` sum `nltk_main()`函数，取第四个索引，即运行时间。然后我们将绘制我们的结果。

```
If __name__ == '__main__' :
    Stanford_t0 = os .times()[ 4 ]
    Stanford_main()
    Stanford_t1 = os .times()[ 4 ]
    Stanford_total_time = stanford_t1 - stanford_t0 Nltk_t0 = os .times()[ 4 ]
    Nltk_main()
    Nltk_t1 = os .times()[ 4 ]
    Nltk_total_time = nltk_t1 - nltk_t0 Time_plot(stanford_total_time, nltk_total_time)
```

对于我们的绘图，我们使用`time_plot()`功能:

```
Def  time_plot  (stanford_total_time, nltk_total_time) : 
    N = 1 
    ind = np.arange(N) # the x locations for the groups 
    width = 0.35  # the width of the bars
    Stanford_total_time = stanford_total_time
    Nltk_total_time = nltk_total_time   
    Fig, ax = plt.subplots()    
    Rects1 = ax.bar(ind, stanford_total_time, width, color= 'r' )    
    Rects2 = ax.bar(ind+width, nltk_total_time, width, color= 'y' ) # Add text for labels, title and axes ticks 
    ax.set_xlabel( 'Classifier' )
    Ax.set_ylabel( 'Time (in seconds)' )
    Ax.set_title( 'Speed ​​by NER Classifier' )
    Ax.set_xticks(ind+width)
    Ax.set_xticklabels( ( '' ) )   
    Ax.legend( (rects1[ 0 ], rects2[ 0 ]), ( 'Stanford' , 'NLTK' ), bbox_to_anchor=( 1.05 , 1 ), loc= 2 , borderaxespad= 0\. ) Def  autolabel  (rects) : 
        # attach some text labels 
        for rect in rects:
            Height = rect.get_height()
            Ax.text(rect.get_x()+rect.get_width()/ 2\. , 1.02 *height, '%10.2f' % float(height),
                    Ha= 'center' , va= 'bottom' ) Autolabel(rects1)
    Autolabel(rects2)    
    Plt.show()
```

哇，NLTK 快如闪电！好像斯坦福更准，但是 NLTK 更快。在平衡我们的偏好精度和所需的计算资源时，这是需要了解的重要信息。

但是等等，还有一个问题。我们的输出很难看！这是斯坦福大学的一个小样本:

```
[( 'House' , 'ORGANIZATION' ), ( 'Speaker' , 'O' ), ( 'John' , 'PERSON' ), ( 'Boehner' , 'PERSON' ), ( 'became' , 'O' ) , ( 'animated' , 'O' ), ( 'Tuesday' , 'O' ), ( 'over' , 'O' ), ( 'the' , 'O' ), ( 'proposed' , 'O' ) ,( 'Keystone' , 'ORGANIZATION' ), ('Pipeline' , 'ORGANIZATION' ), ( ',' , 'O' ), ( 'castigating' , 'O' ), ( 'the' , 'O' ), ( 'Obama' , 'PERSON' ), ( 'administration' , 'O' ), ( 'for' , 'O' ), ( 'not' , 'O' ), ( 'having' , 'O' ), ( 'approved' , 'O' ),( 'the' , 'O' ), ( 'project' ,'O' ), ( 'yet' , 'O' ), ( '.' , 'O' )
```

和 NLTK:

```
( S  ( ORGANIZATION House/NNP) Speaker/NNP ( PERSON John/NNP Boehner/NNP) became/VBD animated/VBN Tuesday/NNP over/IN the/DT proposed/VBN ( PERSON Keystone/NNP Pipeline/NNP) , /, Castigating/VBG the/DT ( ORGANIZATION Obama/NNP) administration/NN for/IN not/RB having/VBG approved/VBN the/DT project/NN yet/RB ./.
```

让我们在下一个教程中把它们变成可读的形式。

![](img/5a8c62a0d4f9a99c72193ff4a45b76ef.png)

# 二十五。使用生物标签创建一个可读的命名实体列表

现在我们已经完成了测试，让我们把命名实体转换成一个好的可读格式。

同样，我们将使用来自 NBC 新闻的相同新闻:

```
House Speaker John Boehner became animated Tuesday over  the proposed Keystone Pipeline, castigating the Obama administration for  not having the project.Republican House Speaker John Boehner says there's "nothing complex about the Keystone Pipeline,"  and  that  it 's time  to build it ."Complex? You think the Keystone Pipeline is complex?!" Boehner responded to a questioner. "It's been under study for five years! We build pipelines in America every day. Do you realize that are 200,000 miles of pipelines in the United States? "At The Speaker Wentworth ON : "And at The only reason at The President is's Involved in at The Keystone Pipeline IS Because IT Crosses AN International's boundary the Listen, WE CAN Build IT There's Nothing Complex the About at The Keystone Pipeline - IT's Time to Build IT..."Of Said Boehner at The President is NO excuse HAD AT the this Point to  not give at The Pipeline at The Go-Ahead the After  at The State Department Report Released A ON catalog on Friday Indicating, at The Project Impact Would have have A minimal ON  at The Environment.Republicans have long pushed for construction of  the project, which enjoys some measure of Democratic support as well. The GOP is  considering conditioning an extension of  the debt limit on approval of  the project by Obama.The White House, though, has said that  it has no timetable for a final decision on  the project.
```

我们的 NTLK 输出已经是一棵树了(只是最后一步)，所以我们来看看我们的斯坦福输出。我们将标记 BIO，B 代表命名实体的开始，I 代表内部，O 代表其他。比如我们的句子是 yes `Barack Obama went to Greece today`，就要标记为`Barack-B Obama-I went-O to-O Greece-B today-O`。为此，我们将编写一系列条件来检查当前和以前的`O`标签的标签。

```
# -*- coding: utf-8 -*-Import nltk
 import os
 Import numpy as np
Import matplotlib.pyplot as plt
 from matplotlib import style
 from nltk import pos_tag
 from nltk.tag import StanfordNERTagger
 from nltk.tokenize import word_tokenize
 from nltk.chunk import conlltags2tree
 from nltk.tree import TreeStyle.use( 'fivethirtyeight' )# Process text 
def  process_text  (txt_file) : 
    raw_text = open( "/usr/share/news_article.txt" ).read()
    Token_text = word_tokenize(raw_text)
    Return token_text# Stanford NER tagger 
def  stanford_tagger  (token_text) : 
    st = StanfordNERTagger( '/usr/share/stanford-ner/classifiers/english.all.3class.distsim.crf.ser.gz' ,
                             '/usr/share/stanford-ner /stanford-ner.jar' ,
                            Encoding= 'utf-8' )   
    Ne_tagged = st.tag(token_text)
    Return (ne_tagged)# NLTK POS and NER 
taggers def  nltk_tagger  (token_text) :
    Tagged_words = nltk.pos_tag(token_text)
    Ne_tagged = nltk.ne_chunk(tagged_words)
    Return (ne_tagged)# Tag tokens with standard NLP BIO tags 
def  bio_tagger  (ne_tagged) :
        Bio_tagged = []
        Prev_tag = "O" 
        for token, tag in ne_tagged:
             if tag == "O" : #O
                Bio_tagged.append((token, tag))
                Prev_tag = tag
                Continue 
            if tag != "O"  and prev_tag == "O" : # Begin NE 
                bio_tagged.append((token, "B-" +tag))
                Prev_tag = tag
            Elif prev_tag != "O"  and prev_tag == tag: # Inside NE 
                bio_tagged.append((token, "I-" +tag))
                Prev_tag = tag
            Elif prev_tag != "O"  and prev_tag != tag: # Adjacent NE 
                bio_tagged.append((token, "B-" +tag))
                Prev_tag = tag
        Return bio_tagged
```

现在我们将生物标记的标签写到树中，因此它们与 NLTK 输出的格式相同。

```
# Create tree 
def  stanford_tree  (bio_tagged) :
    Tokens, ne_tags = zip(*bio_tagged)
    Pos_tags = [pos for token, pos in pos_tag(tokens)] Conlltags = [(token, pos, ne) for token, pos, ne in zip(tokens, pos_tags, ne_tags)]
    Ne_tree = conlltags2tree(conlltags)
    Return ne_tree
```

遍历并解析出所有命名实体:

```
# Parse named entities from tree 
def  structure_ne  (ne_tree) :
    Ne = []
    For subtree in ne_tree:
         if type(subtree) == Tree: # If subtree is a noun chunk, ie NE != "O"
            Ne_label = subtree.label()
            Ne_string = " " .join([token for token, pos in subtree.leaves()])
            Ne.append((ne_string, ne_label))
    Return ne
```

在我们的调用中，我们将所有附加函数放在一起。

```
Def  stanford_main  () :
    Print(structure_ne(stanford_tree(bio_tagger(stanford_tagger(process_text(txt_file)))))))Def  nltk_main  () : 
    print(structure_ne(nltk_tagger(process_text(txt_file))))
```

然后调用这些函数:

```
If __name__ == '__main__' :
    Stanford_main()
    Nltk_main()
```

这是斯坦福大学的一个漂亮的输出:

```
[('House', 'ORGANIZATION'), ('John Boehner', 'PERSON'), ('Keystone Pipeline', 'ORGANIZATION'), ('Obama', 'PERSON'), ('Republican House', ' ORGANIZATION'), ('John Boehner', 'PERSON'), ('Keystone Pipeline', 'ORGANIZATION'), ('Keystone Pipeline', 'ORGANIZATION'), ('Boehner', 'PERSON'), ('America ', 'LOCATION'), ('United States', 'LOCATION'), ('Keystone Pipeline', 'ORGANIZATION'), ('Keystone Pipeline', 'ORGANIZATION'), ('Boehner', 'PERSON'), ('State Department', 'ORGANIZATION'), ('Republicans', 'MISC'), ('Democratic', 'MISC'), ('GOP', 'MISC'), ('Obama', 'PERSON'), ('White House', 'LOCATION')]
```

来自 NLTK:

```
[('House', 'ORGANIZATION'), ('John Boehner', 'PERSON'), ('Keystone Pipeline', 'PERSON'), ('Obama', 'ORGANIZATION'), ('Republican', 'ORGANIZATION '), ('House', 'ORGANIZATION'), ('John Boehner', 'PERSON'), ('Keystone Pipeline', 'ORGANIZATION'), ('Keystone Pipeline', 'ORGANIZATION'), ('Boehner' , 'PERSON'), ('America', 'GPE'), ('United States', 'GPE'), ('Keystone Pipeline', 'ORGANIZATION'), ('Listen', 'PERSON'), (' Keystone', 'ORGANIZATION'), ('Boehner', 'PERSON'), ('State Department', 'ORGANIZATION'), ('Democratic', 'ORGANIZATION'), ('GOP', 'ORGANIZATION'), ('Obama', 'PERSON'), ('White House', 'FACILITY')]
```

## 努力工作。上帝保佑。

## 来自 DDI 的相关故事:

[](https://www.datadriveninvestor.com/2019/01/23/deep-learning-explained-in-7-steps/) [## 用 7 个步骤解释深度学习——数据驱动的投资者

### 自动驾驶汽车、Alexa、医学成像——在深度学习的帮助下，我们周围的小工具变得超级智能…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/deep-learning-explained-in-7-steps/) [](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) [## 成为数据科学家所需的 8 项技能——数据驱动型投资者

### 数字吓不倒你？没有什么比一张漂亮的 excel 表更令人满意的了？你会说几种语言…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) 

编辑披露:编辑有时会发布有用资源的链接。如果你发现它们有用并购买，我们会赚很多钱。不，我不是说要把我的薯条做大。我说的是超大披萨上的意大利香肠。感谢您一直以来的支持，我们将继续为 p̶e̶p̶p̶e̶r̶o̶n̶i̶出版而努力。