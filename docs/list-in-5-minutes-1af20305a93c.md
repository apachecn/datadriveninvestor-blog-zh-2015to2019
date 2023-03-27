# 5 分钟后列出

> 原文：<https://medium.datadriveninvestor.com/list-in-5-minutes-1af20305a93c?source=collection_archive---------4----------------------->

![](img/49d56e0666f55b6e287b65fc5a285ffd.png)

Photo by [Josh Withers](https://unsplash.com/@joshwithers?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

```
Data Structure:A data structure is a collection of data elements (such as numbers or characters—or even other data structures) that is structured in some way, for example, by numbering the elements. The most basic data structure in Python is the "sequence".-> List is one of the Sequence Data structure-> Lists are collection of items (Strings, integers or even other lists)-> Lists are enclosed in [ ]-> Each item in the list has an assigned index value.-> Each item in a list is separated by a comm​-> Lists are mutable, which means they can be changed.
```

# 列表创建

```
emptyList **=** []\
lst **=** ['one', 'two', 'three', 'four'] *# list of strings* lst2 **=** [1, 2, 3, 4] *#list of integers* lst3 **=** [[1, 2], [3, 4]] *# list of lists\* lst4 **=** [1, 'ramu', 24, 1.24] *# list of different datatypes* print(lst4)[1, 'ramu', 24, 1.24]
```

# 列表长度

```
lst **=** ['one', 'two', 'three', 'four']
*#find length of a list* print(len(lst))4
```

# 列表追加

```
lst **=** ['one', 'two', 'three', 'four']
lst.append('five') *# append will add the item at the end* print(lst)['one', 'two', 'three', 'four', 'five']
```

# 列表插入

```
*#syntax: lst.insert(x, y)* lst **=** ['one', 'two', 'four']
lst.insert(2, "three") *# will add element y at location x* print(lst)['one', 'two', 'three', 'four']
```

# 列表删除

```
*#syntax: lst.remove(x)* lst **=** ['one', 'two', 'three', 'four', 'two']
lst.remove('two') *#it will remove first occurence of 'two' in a given list* print(lst)['one', 'three', 'four', 'two']
```

# 列表附加和扩展

```
lst **=** ['one', 'two', 'three', 'four']
lst2 **=** ['five', 'six']
*#append* lst.append(lst2)
print(lst)['one', 'two', 'three', 'four', ['five', 'six']] lst **=** ['one', 'two', 'three', 'four']
lst2 **=** ['five', 'six']
*#extend will join the list with list1* lst.extend(lst2)
print(lst)['one', 'two', 'three', 'four', 'five', 'six']
```

# 列表删除

```
*#del to remove item based on index position* lst **=** ['one', 'two', 'three', 'four', 'five']
**del** lst[1]
print(lst)
*#or we can use pop() method* a **=** lst.pop(1)
print(a)
print(lst)['one', 'three', 'four', 'five']
three
['one', 'four', 'five']lst **=** ['one', 'two', 'three', 'four']
*#remove an item from list* lst.remove('three')
print(lst)['one', 'two', 'four']
```

# 用 Python 列出相关的关键字

```
*#keyword 'in' is used to test if an item is in a list* lst **=** ['one', 'two', 'three', 'four']
**if** 'two' **in** lst:
  print('AI')
*#keyword 'not' can combined with 'in'* **if** 'six' **not** **in** lst:
  print('ML')AI
ML
```

# 反向列表

```
*#reverse is reverses the entire list* lst **=** ['one', 'two', 'three', 'four']
lst.reverse()
print(lst)['four', 'three', 'two', 'one']
```

# 列表排序

对列表排序最简单的方法是使用 sorted(list)函数。

它获取一个列表并返回一个新列表，其中的元素按排序顺序排列。

原始列表不变。

sorted()可选参数 reverse=True，例如 sorted(list，reverse=True)，使其向后排序。

```
*#create a list with numbers* numbers **=** [3, 1, 6, 2, 8]
sorted_lst **=** sorted(numbers)
print("Sorted list :", sorted_lst)
*#original list remain unchange* print("Original list: ", numbers)Sorted list : [1, 2, 3, 6, 8]
Original list:  [3, 1, 6, 2, 8]*#print a list in reverse sorted order* print("Reverse sorted list :", sorted(numbers, reverse**=True**))
*#orginal list remain unchanged* print("Original list :",  numbers)Reverse sorted list : [8, 6, 3, 2, 1]
Original list : [3, 1, 6, 2, 8]--------------------------------------------------------------------
lst **=** [1, 20, 5, 5, 4.2]
*#sort the list and stored in itself* lst.sort()
*# add element 'a' to the list to show an error* print("Sorted list: ", lst) Sorted list:  [1, 4.2, 5, 5, 20]
```

# 具有多个引用的列表

```
lst **=** [1, 2, 3, 4, 5]
abc **=** lst
abc.append(6)
*#print original list* print("Original list: ", lst)Original list:  [1, 2, 3, 4, 5, 6]
```

# 拆分字符串以创建列表

```
*#let's take a string* s **=** "one,two,three,four,five"
slst **=** s.split(',')
print(slst)['one', 'two', 'three', 'four', 'five']s **=** "This is AI Course"
split_lst **=** s.split() *# default split is white-character: space or tab* print(split_lst) ['This', 'is', 'AI', 'Course']
```

# 列表索引

列表中的每个项目都有一个从 0 开始的指定索引值。

访问列表中的元素称为索引。

```
lst **=** [1, 2, 3, 4]
print(lst[1]) *#print second element
#print last element using negative index* print(lst[**-**2])2
3
```

# 列表切片

访问部分数据段称为切片。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

要记住的关键点是:end 值表示不在所选切片中的第一个值。

```
numbers **=** [10, 20, 30, 40, 50,60,70,80]
*#print all numbers* print(numbers[:])
*#print from index 0 to index 3* print(numbers[0:4]) [10, 20, 30, 40, 50, 60, 70, 80]
[10, 20, 30, 40]--------------------------------------------------------------------
print (numbers)
*#print alternate elements in a list* print(numbers[::2])
*#print elemnts start from 0 through rest of the list* print(numbers[2::2])[10, 20, 30, 40, 50, 60, 70, 80]
[10, 30, 50, 70]
[30, 50, 70]
```

# 使用“+”扩展列表

```
lst1 **=** [1, 2, 3, 4]
lst2 **=** ['varma', 'naveen', 'murali', 'brahma']
new_lst **=** lst1 **+** lst2
print(new_lst)[1, 2, 3, 4, 'varma', 'naveen', 'murali', 'brahma']
```

# 列表计数

```
numbers **=** [1, 2, 3, 1, 3, 4, 2, 
*#frequency of 1 in a list* print(numbers.count(1))
*#frequency of 3 in a list* print(numbers.count(3))2
2
```

# 列表循环

```
*#loop through a list* lst **=** ['one', 'two', 'three', 'four']
**for** ele **in** lst:
   print(ele)one
two
three
four
```

# 列出理解

列表理解提供了一种创建列表的简洁方法。

常见的应用是创建新的列表，其中每个元素都是应用于另一个序列或可迭代的每个成员的一些操作的结果，或者创建满足特定条件的那些元素的子序列。

```
*# without list comprehension*squares **=** []
**for** i **in** range(10):
squares.append(i******2)   *#list append* print(squares) [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]*#using list comprehension*squares **=** [i******2 **for** i **in** range(10)]print(squares)[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]*#example*lst **=** [**-**10, **-**20, 10, 20, 50]*#create a new list with values doubled*new_lst **=** [i*****2 **for** i **in** lst]print(new_lst)*#filter the list to exclude negative numbers*new_lst **=** [i **for** i **in** lst **if** i **>=** 0]print(new_lst)*#create a list of tuples like (number, square_of_number)*new_lst **=** [(i, i******2) **for** i **in** range(10)]print(new_lst)[-20, -40, 20, 40, 100]
[10, 20, 50]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25), (6, 36), (7, 49), (8, 64), (9, 81)]
```

# 嵌套列表理解

```
*#let's suppose we have a matrix*​matrix **=** [[1, 2, 3, 4],[5, 6, 7, 8],[9, 10, 11, 12]]​*#transpose of a matrix without list comprehension*transposed **=** []**for** i **in** range(4): lst **=** [] **for** row **in** matrix: lst.append(row[i]) transposed.append(lst) print(transposed)​[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```