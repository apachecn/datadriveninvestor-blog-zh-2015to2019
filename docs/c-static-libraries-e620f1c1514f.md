# C 静态库和你的厨房有什么共同之处

> 原文：<https://medium.datadriveninvestor.com/c-static-libraries-e620f1c1514f?source=collection_archive---------3----------------------->

![](img/f1d97832062d3ee5794fa6c24def3571.png)

让我们深入一小段 C 源代码:

```
#include <stdio.h>int main(void)
{
    printf("Hello, World\n");
    return (0);
}
```

在顶部，我们包含了标准的输入输出头<stdio.h>，其中声明了 printf 函数。</stdio.h>

# 什么是头文件，什么是库

**头文件**，比如 stdio.h，包含了要在源文件之间共享的函数声明和宏定义。它们告诉编译器如何调用一些功能，**，而不知道这些功能是如何工作的**。

**库**是实现**实际功能的地方**，因为它们包含函数定义。库有两种类型:

*   静态(我们将在这篇博文中讨论静态库)
*   动态(稍后讨论)

库本质上是函数、变量和符号的集合。

# C 静态库和你的厨房有什么共同之处

想象一下，你的家人每周都喜欢吃鸡肉、肉千层面和南瓜派。他们很挑食，你每周都用同样的方法做，因为你知道食谱很管用。

现在你想方便快捷地访问你的食谱，所以你把它们放在一起，甚至索引它们。

静态库就像您在厨房中使用的菜谱，因为您可以以一种易于访问、索引和可重用的方式保存一组函数。

**使用静态库的理由:**

*   随着程序的增长，使用库使得管理代码变得更加容易。
*   您不必不断重写您经常使用的相同函数。
*   它们在可重用性以及与其他程序员的协作方面非常出色。
*   如果您的目标文件位于库中并已建立索引，则需要搜索和打开的文件更少，访问速度更快。

# 静态库是如何工作的

回忆[编译的四个步骤](https://medium.com/datadriveninvestor/compilation-process-db17c3b58e62)。

1.  预处理:删除注释并处理#指令
2.  编译:预处理代码被转换成汇编代码
3.  汇编:代码被转换成机器代码(零和一)，也称为目标代码
4.  链接:生成可执行文件

在步骤 4 中，链接试图解析引用的符号，并定位在哪个目标文件中定义了这些符号。**程序中的目标代码被复制到可执行文件中。**

如果我们有一个包含目标文件和定义符号索引的静态库(相对于不同磁盘上的目标文件)，链接过程会更快。我们的程序也更具可移植性，因为我们不必依赖系统上的特定库。

# 如何创建静态库

1.  **用你的函数原型创建一个头文件，并将该头文件包含在你的 C 源文件中。**

```
#ifndef WENDYBLOGTECH_H
#define WENDYBLOGTECH_Hint _putchar(char c);
int _isalpha(int c);
int _abs(int n);
int _strlen(char *s);
void _puts(char *s);
char *_strcpy(char *dest, char *src);
char *_strcat(char *dest, char *src);
char *_strncat(char *dest, char *src, int n);
int _strcmp(char *s1, char *s2);
char *_memcpy(char *dest, char *src, unsigned int n);
char *_strstr(char *haystack, char *needle);#endif
```

2.**使用 gcc** `**-c**` **标志编译您的 C 源文件，不进行链接。**

```
gcc -Wall -pedantic -Werror -Wextra -c *.c
```

-c 标志编译 C 源文件，但不链接。您现在将看到包含以下内容的文件。o 您的目录中的扩展名。

```
0-strcat.o
1-memcpy.o
1-strncat.o
2-strlen.o
2-strncpy.o
3-puts.o
3-strcmp.o
4-isalpha.o
5-strstr.o
6-abs.o
_putchar.o
```

3.**用** `**ar**` **工具创建一个静态库(存档)。**

```
ar -rc <libraryname.a> *.oexample: ar -rc libwendyblogtech.a *.o
```

`-r`标志创建一个新的档案，然后将对象添加到档案中。`-c`标志禁止输出我们正在创建一个新的归档。

4.**使用带有** `**-t**` **标志的** `**ar**` **工具显示存档内容列表。**

```
ar -t <libraryname.a>example: ar -t libwendyblogtech.a
```

5.**使用** `**ranlib**` **生成归档内容的索引。**

```
ranlib <libraryname.a>example: ranlib libwendyblogtech.a
```

6.**使用** `**nm**` **列出目标文件中的符号。**

```
$ nm libwendyblogtech.a

0-strcat.o:
0000000000000000 T _strcat

1-memcpy.o:
0000000000000000 T _memcpy

1-strncat.o:
0000000000000000 T _strncat

2-strlen.o:
0000000000000000 T _strlen

2-strncpy.o:
0000000000000000 T _strncpy

3-puts.o:
                 U _putchar
0000000000000000 T _puts

3-strcmp.o:
0000000000000000 T _strcmp

4-isalpha.o:
0000000000000000 T _isalpha

5-strstr.o:
0000000000000000 T _strstr

6-abs.o:
0000000000000000 T _abs

_putchar.o:
0000000000000000 T _putchar
                 U write
```

# 如何使用静态库

现在我们有了静态库，让我们在编写一个使用库中的 _puts 函数的程序后调用这个库。

注意，在顶部，我们将文件名放在引号中，而不是方括号中，因为 wendyblogtech.h 是我们自己的头文件，而不是系统头文件。

```
#include "wendyblogtech.h"int main(void)
{
    _puts("\"That's how you create a static libary.\"");
    return (0);
}
```

**调用库:**

```
Example of invoking libwendyblogtech.a:gcc quote.c -L. -lwendyblogtech -o quote
```

`-L`在目录中查找库文件，因为它后面有一个句点，所以它将在当前目录中查找。
`-l`链接库文件并自动添加 lib 前缀和。这就是为什么我们不输入整个 libwendyblogtech

**现在我们运行我们的可执行程序** `**./quote**` **并查看输出:**

```
"That's how you create a static library."
```

现在你知道了…静态库就像你在厨房里使用的食谱，因为你可以用一种容易访问、索引和可重用的方式保存一组函数。