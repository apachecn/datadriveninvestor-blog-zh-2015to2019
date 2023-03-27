# 检索给定对象的填充字段

> 原文：<https://medium.datadriveninvestor.com/retrieve-populated-fields-of-an-sobject-990ac5c0ca39?source=collection_archive---------4----------------------->

![](img/fd555c03caccc07a3dfbe880124becd2.png)

伙计们，如果你是 Salesforce 开发人员，特别是如果你从事产品开发，我们一定会编写可重用的通用代码，但我们会在某个时候陷入困境。由于我属于一个产品开发团队，我也卡住了，但是在解决它的冒险中，我发现了一些很酷的方法。我来和大家分享一下。不是什么高级代码什么的，只是 Salesforce 给出的简单方法，大概你已经知道了。别担心，我不会用大段大段和数百行代码来烦你。我会尽我最大的努力让这篇文章足够简单、明快和清晰。大概等你喝完 ***咖啡*** 的时候就能看完了！

所以我遇到的问题是，我必须对给定的 sObject 实例中的字段进行一些处理。我需要 sObject 实例中使用的字段的 API 名称。它可以是填充了任意数量字段的任何自定义或标准 salesforce 对象。我不能硬编码字段，也不能只获取特定对象中的每个字段，那么该怎么办呢？我在 Apex 文档中滚动 sObject 类，在这里，我发现了一个很酷的方法，叫做["***getpopulatedfieldssamap()"***](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_sobject.htm)***。***

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

这是基本的实现…

```
//Pass an instance of any standard or custom objects.
public static List<String> getPopulatedFieldApiNames(sObject sObjectInstance){//Basically this returns a map of field api name as string and value as object for the given sObject instance
Map<String,Object> apiNameObjectMap =      sObjectInstance.getPopulatedFieldsAsMap();return new List<String>(apiNameObjectMap.keySet());}
```

以下是一些使用案例和注意事项:

*   获取 sObject 实例中使用的字段来进行访问检查，比如当您想要插入或更新给定的 sObject 时。当然，也有一些警告。不建议照原样使用上述方法的返回列表。假设从上述方法返回的字符串数组中有' ***Id*** '字段，并且您正在对其进行更新访问检查，并相应地抛出异常，不可避免地，您将最终处理自己的异常。此外，如果实例包含关系字段，如从子查询中提取的子记录，以及父对象的字段，那么就会变得棘手
*   一次对一组预定义的字段进行一些验证。使用"[***【contains key(fieldToCheck)***](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_map.htm)***"****检查要验证的字段是否存在于映射中，并运行您的验证(当然，您可以使用验证规则，也可以在触发器中进行验证。但是触发器相对昂贵。如果你想在插入或更新字段之前验证它，那么这个方法就派上用场了)*

嗯，我同意，这个方法非常简单，但是意义重大。我不是说照原样使用上面的代码片段，而是让您自己决定如何使用它。Apex sObject 类有很酷的有用的方法，请检查一下。最后，感谢您的时间和耐心。 ***希望你没有厌烦*** 。