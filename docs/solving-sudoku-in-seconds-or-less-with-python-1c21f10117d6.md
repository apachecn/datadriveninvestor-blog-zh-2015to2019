# 在几秒钟内解决数独(或更少！)使用 Python

> 原文：<https://medium.datadriveninvestor.com/solving-sudoku-in-seconds-or-less-with-python-1c21f10117d6?source=collection_archive---------0----------------------->

[![](img/376ae34b1e8c527180eb516844cecb80.png)](http://www.track.datadriveninvestor.com/1B9E)

我和许多其他人一样，喜欢解谜。每天早上我都会做《纽约时报》的迷你填字游戏(大喊 NYT)，我在高中时玩过 1v1 俄罗斯方块，在我以前实验室工作的休息时间，我会玩数独游戏。也许我比大多数人更喜欢谜题，但这并不意味着你必须痴迷于它们才能用它们来制作一个好的编码项目！在这篇文章中，我将介绍如何使用逻辑和基本的 python 数据结构编写数独求解器。这个解谜 AI(像很多人工智能任务一样)不需要神经网络，所以我不会用锤子敲打这个螺丝钉。这篇文章中引用的代码可以在[https://github.com/aaronfrederick/SudokuSolver](https://github.com/aaronfrederick/SudokuSolver)找到。

There are 2 nines in the first column…

对于外行来说，数独的基本规则是，在 9x9 拼图中，一个 1-9 的数字不能在组成拼图的任何行、列或 3x3 方块中重复出现。有一些数字已经插入了拼图和一些空白。猜谜不是完成谜题的必要条件，因为不正确的猜测会使谜题无法解答。既然我们知道了我们需要知道的一切，让我们开始吧！

为了用 python 表示一个谜题，我将创建一个名为*容器*的列表列表，其中较大的列表将包含 9 个子列表(行)，子列表有 9 个条目(条目)。空格用 0 表示，填入的值用数字表示。

在数独游戏中，规则说明了如何解决难题，所以我们可以从那里开始第一次尝试求解器(* *预示警告:*将有不止一个)。我们将需要编写 3 个主要函数来检查哪些可能的值可以占据一个空方块:

1.  检查行中可能值的函数
2.  检查列中可能值的函数
3.  检查正方形可能值的函数

```
subtract_set = {1,2,3,4,5,6,7,8,9}def check_horizontal(i,j):
    return subtract_set - set(container[i])def check_vertical(i, j):
    ret_set = []
    for x in range(9):
        ret_set.append(container[x][j])
    return subtract_set - set(ret_set)def check_square(i, j):
    first = [0,1,2]
    second = [3,4,5]
    third = [6,7,8]
    find_square = [first, second, third]
    for l in find_square:
        if i in l:
            row = l
        if j in l:
            col = l
    return_set = []
    for x in row:
        for y in col:
            return_set.append(container[x][y])
    return subtract_set - set(return_set)
```

我刚刚展示的函数使用集合符号，其逻辑是我们可以通过从一组主数字 1-9 中减去当前占据该行的数字来获得一行中可能的值。用简单的英语来说，如果我们的行(由一个列表表示)包含数字 1、3、5、7、9，从 1-9 中减去这组数字，我们得到的可能值是 2、4、6 和 8。我们的函数返回那个集合，我们可以继续前进。

我们的 check_vertical 函数的操作非常类似，但是它不是检查行，而是检查每行的第 j 个元素，有效地模拟了一列。继续这个例子，如果我们的列包含 2、4 和 7，那么我们的函数将返回 1、3、5、6、8、9 的集合。

check_square 函数比前两个稍微复杂一点，但是基本的逻辑是，我们找到我们的空方块位于 9 个 3x3 方块中的哪一个，通过迭代它的索引来创建该 3x3 中的当前值的列表，并返回 1–9 减去该列表。

将这些函数一起包装在 get_poss_values 中，我们可以通过从上面的函数中取 3 个集合的交集来获得任何给定正方形的可能值列表:

```
def get_poss_vals(i, j):
    poss_vals = list(check_square(i, j) \
                    .intersection(check_horizontal(i, j)) \
                    .intersection(check_vertical(i, j)))
    return poss_valsdef explicit_solver(container):
    for i in range(9):
        for j in range(9):
            if container[i][j] == 0:
                poss_vals = get_poss_vals(i, j)
                if len(poss_vals) == 1:
                    container[i][j] = list(poss_vals)[0]
                    print_container(container)
    return container
```

上面的显式求解器函数遍历每个方块，如果它是空的(值为 0)，求解器会尝试填充它。如果基于我们之前描述的函数只有一个可能的值，就会发生这种情况。这种显式方法很好地解决了简单的难题，但是遗漏了一些重要的信息，使我们无法解决更困难的难题。

我们的显式求解器是一种非常天真的方法，但是忽略了从周围方块中获得的信息。例如，当我们检查一个可能值为 1、2 和 3 的正方形时，如果该行中的其他空白正方形只能是 1 或 2，那么通过排除过程，我们知道我们正在检查的正方形必须是 3。隐式求解函数通过组合一个正方形的可能值并将其与行、列和 3×3 正方形的其余部分的可能值进行比较来实现此逻辑。

下面，我已经包括了整个隐式求解函数。这是少量的代码，因为有三个不同的部分来包含上面提到的行、列和 3x3 正方形的逻辑。

```
def implicit_solver(i, j, container):
    if container[i][j] == 0:
        poss_vals = get_poss_vals(i, j)

        #check row
        row_poss = []
        for y in range(9):
            if y == j:
                continue
            if container[i][y] == 0:
                for val in get_poss_vals(i, y):
                    row_poss.append(val)
        if len(set(poss_vals)-set(row_poss)) == 1:
            container[i][j] = list(set(poss_vals)-set(row_poss))[0]
            print_container(container) #check column
        col_poss = []
        for x in range(9):
            if x == i:
                continue
            if container[x][j] == 0:
                for val in get_poss_vals(x, j):
                    col_poss.append(val)
        if len(set(poss_vals)-set(col_poss)) == 1:
            container[i][j] = list(set(poss_vals)-set(col_poss))[0]
            print_container(container) #check square
        first = [0, 1, 2]
        second = [3, 4, 5]
        third = [6, 7, 8]
        find_square = [first, second, third]
        for l in find_square:
            if i in l:
                row = l
            if j in l:
                col = l
        square_poss = []
        for x in row:
            for y in col:
                if container[x][y] == 0:
                    for val in get_poss_vals(x, y):
                        square_poss.append(val)
        if len(set(poss_vals)-set(square_poss)) == 1:
          container[i][j] = list(set(poss_vals)-set(square_poss))[0]
          print_container(container) return container
```

结合使用隐式求解器和显式求解器，我们可以在几秒钟内解决中等难度和高难度的难题(如果打印语句被注释掉，只需几分之一秒)！

有更多的方法来解决这个问题，但是通过遵守规则来坚持数独的精神仍然会导致一个非常快速的解决方案。我欢迎任何关于改进代码和加入更多解决方法的反馈，请在评论中联系我们！