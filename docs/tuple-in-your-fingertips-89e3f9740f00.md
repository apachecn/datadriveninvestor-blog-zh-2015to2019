# 触手可及的元组！！

> 原文：<https://medium.datadriveninvestor.com/tuple-in-your-fingertips-89e3f9740f00?source=collection_archive---------7----------------------->

![](img/c127670702f3b3f669dd9f9efe465094.png)

Photo by [Christophe Ferron](https://unsplash.com/@christopheferron?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

->元组类似于列表

*   >两者的区别在于，一旦元组被赋值，我们就不能改变它的元素，而在列表中，元素是可以改变的

[](https://www.datadriveninvestor.com/2019/03/25/a-programmers-guide-to-creating-an-eclectic-bookshelf/) [## 创建折衷书架的程序员指南|数据驱动的投资者

### 每个开发者都应该有一个书架。他的内阁中可能的文本集合是无数的，但不是每一个集合…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/25/a-programmers-guide-to-creating-an-eclectic-bookshelf/) 

# 元组创建

```
*#empty tuple*t **=** ()*#tuple having integers*t **=** (1, 2, 3)
print(t)*#tuple with mixed datatypes* t **=** (1, 'raju', 28, 'abc')
print(t)*#nested tuple* t **=** (1, (2, 3, 4), [1, 'raju', 28, 'abc'])
print(t)(1, 2, 3)
(1, 'raju', 28, 'abc')
(1, (2, 3, 4), [1, 'raju', 28, 'abc'])*#only parenthesis is not enough*t **=** ('satish')type(t)str*#need a comma at the end*t **=** ('satish',)type(t)tuple*#parenthesis is optional*t **=** "satish",print(type(t))print(t)<class 'tuple'>
('satish',)
```

# 访问元组中的元素

```
t **=** ('satish', 'murali', 'naveen', 'srinu', 'brahma')print(t[1])murali*#negative index*print(t[**-**1]) *#print last element in a tuple*brahma*#nested tuple*t **=** ('ABC', ('satish', 'naveen', 'srinu'))​print(t[1]) ('satish', 'naveen', 'srinu')print(t[1][2])srinu *#Slicing*t **=** (1, 2, 3, 4, 5, 6)print(t[1:4])*#print elements from starting to 2nd last elements*print(t[:**-**2])*#print elements from starting to end*print(t[:]) (2, 3, 4)
(1, 2, 3, 4)
(1, 2, 3, 4, 5, 6)
```

# 更改元组

#与列表不同，元组是不可变的

#这意味着元组的元素一旦被赋值就不能被改变。但是，如果元素本身是一个可变的数据类型，比如 list，那么它的嵌套项是可以改变的。

*#创建元组*

```
t **=** (1, 2, 3, 4, [5, 6, 7])t[2] **=** 'x' *#will get TypeError*---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-9f4cbf6ee0de> in <module>()
 **2** t = (1, 2, 3, 4, [5, 6, 7])
 **3** 
----> 4 t[2] = 'x' #will get TypeErrorTypeError: 'tuple' object does not support item assignmentt[4][1] **=** 'satish'print(t)(1, 2, 3, 4, [5, 'satish', 7])
```

*#串联元组*

```
t **=** (1, 2, 3) **+** (4, 5, 6)print(t)(1, 2, 3, 4, 5, 6)
```

*#使用*操作符将元组中的元素重复给定的次数。*

```
t **=** (('satish', ) ***** 4)print(t)('satish', 'satish', 'satish', 'satish')
```

# 元组删除

# 我们不能改变元组中的元素。

```
*# That also means we cannot delete or remove items from a tuple.**#delete entire tuple using del keyword*t **=** (1, 2, 3, 4, 5, 6)*#delete entire tuple***del** t
```

# 元组索引

```
t **=** (1, 2, 3, 1, 3, 3, 4, 1)​print(t.index(3)) *#return index of the first element is equal to 3**#print index of the 1*2
```

# 元组成员资格

```
*#test if an item exists in a tuple or not, using the keyword in.*t **=** (1, 2, 3, 4, 5, 6)print(1 **in** t)Trueprint(7 **in** t)False
```

# 内置函数

# 元组长度

# t **=** (1，2，3，4，5，6)

```
print(len(t))6
```

# 元组排序

t **=** (4，5，1，2，3)

```
new_t **=** sorted(t)print(new_t) *#Take elements in the tuple and return a new sorted list**#(does not sort the tuple itself).*[1, 2, 3, 4, 5]*#get the largest element in a tuple*t **=** (2, 5, 1, 6, 9)print(max(t))9*#get the smallest element in a tuple*print(min(t))1:*#get sum of elments in the tuple*print(sum(t))23
```