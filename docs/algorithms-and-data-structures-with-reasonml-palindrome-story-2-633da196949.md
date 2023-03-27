# 带推理的算法和数据结构|回文|故事 2

> 原文：<https://medium.datadriveninvestor.com/algorithms-and-data-structures-with-reasonml-palindrome-story-2-633da196949?source=collection_archive---------15----------------------->

[![](img/201c27605d668622955f54c417c9a3ac.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/5773f4f6e829df0a482743840aef5f68.png)

Photo by [Daniele Levis Pelusi](https://unsplash.com/@yogidan2012?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好，这将是一个很短的。

所以，让我们从回文的定义开始:*一个单词、短语或序列，向后读和向前读一样，例如 madam 或 nurses run。*

[](https://www.datadriveninvestor.com/2019/03/22/the-seductive-business-logic-of-algorithms/) [## 算法诱人的商业逻辑|数据驱动的投资者

### 某些机器行为总是让我感到惊讶。我对他们从自己的成就中学习的能力感到惊讶…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/22/the-seductive-business-logic-of-algorithms/) 

基本上，我们需要两件事情来决定一个字符串是否是一个回文:
—字符串本身
—这个字符串的反向版本

请记住，我们的最后一个算法(故事 1)是“反转字符串”，我们可以使用它，这是一个可能的解决方案。

另一个解决方案是更有趣的方法:
像许多语言一样，在 ReasonML 中，字符串有索引。我们可以使用这些索引来获取一个字符，然后我们可以将它与字符串“另一边”的其他字符进行比较。

让我们创建一个测试文件来断言我们的算法:

创建一个名为 **"Palindrome.test.js"** 的新文件，代码如下:

```
**const** { isPalindrome, isPalindrome2 } = require("./Palindrome.bs");

***describe***("Palindromes", () => {

  ***test***("is palindrome fn: negative case", () => {
    const a = "abc";

    ***expect***(isPalindrome(a)).toBe(false);
  });

  ***test***("is palindrome fn: positive case", () => {
    const a = "abba";

    ***expect***(isPalindrome(a)).toBe(true);
  });

  ***test***("is palindrome fn: negative case", () => {
    const a = "abc";

    ***expect***(isPalindrome2(a)).toBe(false);
  });

  ***test***("is palindrome fn: positive case", () => {
    const a = "abba";

    ***expect***(isPalindrome2(a)).toBe(true);
  });

  ***test***("is palindrome fn: positive case", () => {
    const a = "12321";

    ***expect***(isPalindrome2(a)).toBe(true);
  });

  ***test***("is palindrome fn: positive case", () => {
    const a = "1221";

    ***expect***(isPalindrome2(a)).toBe(true);
  });
});
```

然后，创建另一个名为 **"Palindrome.re"** 的文件，并通过解决方案:

```
**let** isPalindrome = (s: string) => {
  s == StringReversal.reverseString(s);
};

**let rec** helper = (~it=0, s: string) =>
  if (it == String.length(s)) {
    true;
  } else {
    s.[it] == s.[String.length(s) - 1 - it] && helper(~it=it + 1, s);
  };

**let** isPalindrome2 = (s: string) => {
  helper(s);
};
```

请注意我们是如何遍历列表的，这对理解我们接下来的算法非常重要。

在函数“helper”上，我们有一个带标签的可选参数，名为“it”(也就是迭代器)。每次后续调用这个递归函数时，我们都用“1”来增加“它”，这样，在某些时候，它将成为我们离开“循环”的借口。