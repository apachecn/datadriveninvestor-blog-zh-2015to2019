# 揭开子串搜索算法的神秘面纱— Rabin-Karp

> 原文：<https://medium.datadriveninvestor.com/demystifying-substring-search-algorithms-rabin-karp-60937db6c1d9?source=collection_archive---------3----------------------->

[![](img/08589f1e293e1549bae10862bec36747.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/b4f7d2c5b6b165ac8aeded8bdf989bc8.png)

Photo by [McDobbie Hu](https://unsplash.com/@hjx518756?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 问题是

子串搜索问题给定一个类似“罗伊”的字符串，看它是否存在于另一个字符串中，类似“金罗伊气”。强力方法是检查字符串中每个可能的子序列。例如，这将是

```
"Jin"
"in "
"n R"
" Ro"
"Roy" <= found!
```

该算法的复杂度是 O(nm ),其中 n 是我们正在搜索的字符串的长度，m 是我们正在寻找的字符串的长度。

[](https://www.datadriveninvestor.com/2019/03/22/the-seductive-business-logic-of-algorithms/) [## 算法诱人的商业逻辑——数据驱动的投资者

### 某些机器行为总是让我感到惊讶。我对他们从自己的成就中学习的能力感到惊讶…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/22/the-seductive-business-logic-of-algorithms/) 

# 使用哈希

解决这个问题的一个有趣的方法是使用哈希。让我们散列正在搜索的子字符串，只是为了好玩。让我们假设一个 hash 函数 hash()可以做到这一点

```
hash("Roy") => Returns 135
```

让我们对找到的所有子字符串运行 hash()。

```
hash("Jin") => 211
hash"in ") => 132
hash("n R") => 321
hash(" Ro") => 813
hash("Roy") => 135 => found!
```

现在你可能在想我们为什么要这么做。这看起来毫无意义。它所做的只是减慢我们的速度，因为计算散列所花的时间比简单地检查一个子串是否匹配我们正在寻找的字符串所花的时间要长。这是真的— *除非*你知道该用什么散列函数。

# 引入滚动哈希

为了克服散列的缓慢，有了滚动散列的想法。把这个散列想象成一个散列，你可以在 O(1)时间内从字符串的前面弹出并推到后面。为了让我所说的更清楚，下面是一个 rollinghash 的样子:

```
a = rollinghash('a')  // O(1) because a is length 1
  a.hash = 312  // this is the hash for the string "a"
  a.append('b')  // O(1) because we're adding one letter
  a.hash == 121  // this is the hash for the string "ab"
  a.pop()  // O(1) because we're removing one letter
  a.hash == 712  // this is the hash for the string "b"
```

如何追加和弹出一个字母 O(1)？rollinghash 有许多不同的实现，但几乎总是简单地在 hash 中添加一个数字。下面是一个示例实现的输出:

*   字符串" a" => 97
*   字符串" ab" => 97001
*   字符串" b" => 98

如果你熟悉 python，你可以[看看](https://github.com/wontonst/py-rollinghash/blob/1394a6b5b5e007ee12862e9737b536416c6b8a25/rollinghash/rollinghash.py#L86)这个滚动散列的实现，并尝试一下！你可以在这里阅读文档。

```
pip install rollinghash
```

# 把所有的放在一起

现在我们可以在 O(1)时间内添加序列中的下一个字母，我们可以简单地使用一个滑动窗口，这是我们获取每个子串的散列的一种奇特方式，但这次不同的是，添加下一个字母需要 O(1 ),删除前一个字母需要 O(1)。在名为 source 的字符串中查找名为 target 的字符串的算法如下所示:

```
function RabinKarp(source, target)
    hpattern := hash(target);
    hs = rollinghash(source[0:len(target)])
    for i from 0 to len(target) - len(target):
        if hs.hash == htpattern:
            return i
        hs.pop()
        hs.append(source[i])
    return not found
```