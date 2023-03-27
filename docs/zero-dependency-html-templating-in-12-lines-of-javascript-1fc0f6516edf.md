# 12 行 Javascript 代码中的零依赖 HTML 模板。

> 原文：<https://medium.datadriveninvestor.com/zero-dependency-html-templating-in-12-lines-of-javascript-1fc0f6516edf?source=collection_archive---------9----------------------->

*这是我为之前一篇关于* [*编写定制摩卡记者的博文写的一段代码。*](https://medium.com/@aidobreen/how-to-build-a-custom-mocha-reporter-45b098d95ef6) *我想从模板生成 HTML 输出，但我不需要太多的功能或额外的依赖。事实证明，这并不困难。*

以编程方式生成或产生 HTML 并不是火箭科学。典型的方法是:

1.  构建一个你想要的 HTML 模板。
2.  确定模板中要更改的可变部分。
3.  编写您的代码来获取替换部件。
4.  使用模板引擎加载 HTML 并用替换部分替换变量。

外面有很多模板引擎。[小胡子](https://www.npmjs.com/package/mustache)是一个。[车把](http://tryhandlebarsjs.com/)、[圆点](http://olado.github.io/doT/index.html)和 [EJS](http://ejs.co/) 也起作用。它们基本上工作相同，但是它们都代表了我们不需要的额外依赖。我们在这里没有做任何复杂的事情，我宁愿保持这个包没有依赖性。所以我们自己建造它。

## 正则表达式

![](img/6b08f6954a3bb199e9dd5068b97b44e6.png)

Artists impression of a lake surrounded by red cabbage and carrots fields.

正则表达式(regex)是一个**奇妙的**、**强大的**和**复杂的**概念，我不会详细讨论。基本上，正则表达式允许您定义一个“表达式”，或模式，用于在文本主体中查找特定的序列。正则表达式的一个常见用途是查找子串，并替换它。Regex 还可以用来验证数据，确保数据符合某种结构(即电话号码仅包含数字，长度为 10 位数)

## 替换字符串。

正则表达式并不是 Javascript 独有的，即使在 JS 中，也有多种方法可以利用它们。在我们的例子中，我们将使用`string.replace()`方法。[(此处为完整文档)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

```
str.replace(regexp|substr, newSubstr|function)
```

我们将获取一个名为`template`的字符串，并查找每个出现在双波形括号中的单词，如下所示:`{{word}}`。然后，我们将用我们生成的值替换这个单词——在 Mocha reporter 的例子中，我们使用了我们测试的输出，但是它可以是任何值。

**例如**，假设我们已经计算了成功运行的测试的百分比:`run_percent`，并且在我们的模板中我们已经编写了`{{run_percent}}`。我们可以写: `template.replace(/{{run_precent}}/g, run_percent)`

> [正则表达式文字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Creating_a_regular_expression)被正斜杠包围。“g”表示[全局搜索。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/global)

## 替换多个字符串

但是我们可以做得更好。我们可以用下面的正则表达式找到任何被波浪线包围的单词

> `*.*`表示除换行符以外的任何字符。
> `***`表示与前一件事匹配 0 次或多次。
> `*?*`意为使前一件事‘不贪’——即。可能的最短匹配。

最后，我们不会仅仅用一个值来替换曲线中的每个单词。如果我们将一个函数作为第二个参数传递给`replace()`，我们可以聪明得多…

```
let newContent = template.replace(/{{.*?}}/g, function(match){
  **return** replacements[match]
})
```

这里，`Match`是正则表达式找到的单词。`replacements`是一个对象，它为我们的每个模板变量(曲线)提供了键，以及我们想要替换它们的值。这里有一个例子:

```
**// Example of replacements object**
{
      "{{lastrun_date}}": new Date(),
      "{{run_percent}}": run_percent,
      "{{run_numerator}}": sum,
      "{{run_denominator}}": total
}
```

用一个漂亮的小函数(在我们的 reporter 中称为`updateBillboard`)将文件读/写代码打包，我们在[中有了 12 行 Javascript](https://github.com/aido179/apb-mocha-reporter/blob/140e22119925142dd2d09bd22dd62764bbd46799/src/apbmochareporter.js#L91) 的模板引擎:

```
function updateBillboard(replacements){  
  content = fs.readFileSync(`template.html`, {encoding:'utf8'})
  let newContent = content.replace(/{{.*?}}/g, 
    function(match){
      return replacements[match]
    })
  let output= `/output.html`
  if (!fs.existsSync(output_dir)){
    fs.mkdirSync(output_dir);
  }
  fs.writeFileSync(output, newContent)
  return output
}
```

# 结论

显然，这不适合任何有复杂模板需求的东西。但是，在我看来，仅仅为了替换文件中的几个值而安装整个额外的包是多余的。

我叫艾丹·布林，在爱尔兰都柏林经营一家 T2 软件咨询公司。如果你喜欢这篇文章，可以考虑在[推特](https://twitter.com/aidanbreen)上关注我，或者注册我的[个人邮件列表](http://Ok, screw it. Let's give this a go and see what happens:  http://eepurl.com/dMEsHg)，不要一个月更新一次。