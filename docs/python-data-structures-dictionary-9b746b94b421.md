# Python 数据结构-字典

> 原文：<https://medium.datadriveninvestor.com/python-data-structures-dictionary-9b746b94b421?source=collection_archive---------3----------------------->

*先决条件:任何编程语言的基础知识*

*我们将在这里探讨数据结构字典及其常见操作。*

朱庇特笔记本上的[字典](https://github.com/arshren/Data-Structures/blob/master/Python%20Data%20Structure%20-%20Dictionary.ipynb)

字典是键/值对的无序集合，其中**键在字典中应该是唯一的**。

字典是由关键字索引的，它们是可变的和动态的，它们可以增长和收缩。键和值可以是任何数据类型，如字符串或数字。

*现在，我们将一步一步地定义字典，在字典中添加元素，更新字典中的元素，从字典中删除元素和检索字典中的元素，遍历字典*

***所有输出为粗体斜体***

# **定义字典**

它是用一对空括号{}定义的。

```
Contact_info = {}
```

键值对由逗号分隔，冒号(:)将键与其值分隔开。

在下面的例子中，Name 是键,' Jane Dow '是与之关联的值

```
Contact_info = {'Name':'Jane Dow', 
                'Address':'1800 SW'
               }
Contact_info***{'Address': '1800 SW', 'Name': 'Jane Dow'}***
```

# **向字典添加元素**

要添加元素，我们需要指定键和值。这里的关键是“移动”，值是一个数字 1234567

```
Contact_info["Mobile"] = 1234567
Contact_info***{'Address': '1800 SW', 'Mobile': 1234567, 'Name': 'Jane Dow'}***
```

向字典添加元素的另一种方法是使用 **Update** ()方法。update()-用指定的键值对更新字典

```
Contact_info.update({"email":"[abc@domain.com](mailto:abc@domain.com)"})
Contact_info***{'Address': '1800 SW',
 'Mobile': 9999999,
 'Name': 'Jane Dow',
 'email': 'abc@domain.com'}***
```

我们还可以将字典作为参数传递给 update()方法。比如我们有字典 data_1，我们将它的内容添加到 Contact_info 字典中

```
data_1={'City':'New York', 'Zip':51234}
Contact_info.update(data_1)
Contact_info***{'Address': '1800 SW',
 'City': 'New York',
 'Mobile': 9999999,
 'Name': 'Jane Dow',
 'Zip': 51234,
 'email': 'abc@domain.com'}***
```

# **更新字典中现有关键字的值**

指定密钥并提供新值

```
Contact_info["Mobile"] = 9999999
Contact_info***{'Address': '1800 SW', 'Mobile': 9999999, 'Name': 'Jane Dow'}***
```

# 检索字典的内容

我们可以通过指定字典的键来检索字典的值，如下所示

```
print(Contact_info['Name'])
print(Contact_info['email'])***Jane Dow
abc@domain.com***
```

我们还可以使用 **get** ()方法，通过将 key 作为参数传递来访问键值。

```
Contact_info.get('Address')***'1800 SW'***
```

用于访问字典中的所有键

```
print(Contact_info.keys())***dict_keys(['Name', 'Address', 'Mobile', 'email', 'City', 'Zip'])***
```

用于访问字典中的所有值

```
print(Contact_info.values())***dict_values(['Jane Dow', '1800 SW', 9999999, 'abc@domain.com', 'New York', 51234])***
```

# 删除词典中的条目

要删除字典中的条目，我们可以使用 **del**

```
del Contact_info[“email”]
Contact_info***{'Address': '1800 SW',
 'City': 'New York',
 'Mobile': 9999999,
 'Name': 'Jane Dow',
 'Zip': 51234}***
```

如果您想清除整个字典的内容，则使用**清除**()如下所示

```
State_capital ={'Arkansas':'Little Rock', 'Wisconsin':'Madison', 'California':'Sacramento', 'Iowa':'Des Moines'}
State_capital***{'Arkansas': 'Little Rock',
 'California': 'Sacramento',
 'Iowa': 'Des Moines',
 'Wisconsin': 'Madison'}***State_capital.clear()
State_capital***{}***
```

我们还可以使用 **pop()** 通过将项目的键作为参数传递来删除特定的项目。

在下面的例子中，我们使用 pop()从字典中删除“Iowa”项

```
State_capital ={'Arkansas':'Little Rock', 'Wisconsin':'Madison', 'California':'Sacramento', 'Iowa':'Des Moines'}
State_capital.pop("Iowa")
State_capital***{'Arkansas': 'Little Rock',
'Wisconsin': 'Madison',
'California': 'Sacramento'
 }***
```

我们还可以使用 **popitem** ()方法移除最后一个键值对。它返回从字典中删除的键值

```
State_capital.popitem()***('California', 'Sacramento')***State_capital***{'Arkansas': 'Little Rock', 'Wisconsin': 'Madison'}***
```

# 遍历字典

有不同的方法来迭代一个字典。最简单的方法是使用 for 循环

```
for i in Contact_info:
 print(Contact_info[i])***Jane Dow
1800 SW
9999999
New York
51234***
```

接下来我们将使用字典理解，它就像是一条语句中 for 循环的快捷方式

```
state_capital={
    'New York': 'Albany',
    'New Jersey': 'Trenton',
    'Arkansas':'Little Rock',
    'Wisconsin':'Madison',
    'Illinois':'Springfield',
    'Iowa':'Des Moines',
    'California':'Sacramanto'
    }dict_capital = {key:value for (key,value) in state_capital.items()}
print(dict_capital)***{'New York': 'Albany', 'New Jersey': 'Trenton', 'Arkansas': 'Little Rock', 'Wisconsin': 'Madison', 'Illinois': 'Springfield', 'Iowa': 'Des Moines', 'California': 'Sacramento'}***
```

**条件搜索**

同样，我们可以使用一个简单的 for 循环和其中的 if 语句来搜索特定的条件，如下所示，我们正在搜索“Iowa”的大写字母

```
search_state ='Iowa'
for state in state_capital:
    if search_state == state:
        print(state_capital[state])***Des Moines***
```

现在使用字典理解的条件搜索。这里我们要显示一个州的所有县。我们搜索“阿肯色州”,然后显示值

```
counties_in_state={
    'New York': 'Albany',
    'New Jersey': 'Trenton',
    'Arkansas':'Little Rock, Bentonville, Rogers, Fayetteville',
    'Wisconsin':'Madison, Milwaukee',
    'Illinois':'Springfield, chicago',
    'Iowa':'Des Moines',
    'California':'Sacromanto, San Francisco, Los Angeles'
    }
counties = {value for (key,value) in counties_in_state.items() if key == 'Arkansas'}
print(counties)***{'Little Rock, Bentonville, Rogers, Fayetteville'}***
```

# 字典操作快速参考

[**clear()**](https://www.w3schools.com/python/ref_dictionary_clear.asp) :从字典中删除所有元素

[**get()**](https://www.w3schools.com/python/ref_dictionary_get.asp) :返回指定键的值

[**items()**](https://www.w3schools.com/python/ref_dictionary_items.asp) :返回字典中每个键值对的元组列表

[**values()**](https://www.w3schools.com/python/ref_dictionary_values.asp) :返回字典中所有值的列表

[**【副本()】**](https://www.w3schools.com/python/ref_dictionary_copy.asp) :返回字典的浅副本

[**【update()**](https://www.w3schools.com/python/ref_dictionary_update.asp):用指定的键值对更新字典

[**pop()**](https://www.w3schools.com/python/ref_dictionary_pop.asp)**:**删除指定键的元素

[**【pop item()**](https://www.w3schools.com/python/ref_dictionary_popitem.asp)**:**删除最后一个键值对

[](https://www.w3schools.com/python/ref_dictionary_setdefault.asp)**:返回指定键的值。如果密钥不存在:插入具有指定值的密钥**

***给我留言，让我知道如何让我的帖子更好***