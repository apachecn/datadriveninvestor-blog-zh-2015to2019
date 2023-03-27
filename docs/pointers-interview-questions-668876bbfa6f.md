# 指针:面试问题练习

> 原文：<https://medium.datadriveninvestor.com/pointers-interview-questions-668876bbfa6f?source=collection_archive---------0----------------------->

![](img/37e66b0e6474238efe21637abcfcf898.png)

## 理论主题:

1.  指针简介
2.  指针算法
3.  数组和指针
4.  字符和指针
5.  指针和函数
6.  双指针

## 问题:

**指针声明**

以下哪一项是指针的正确声明？

*   int x；
*   int &x;
*   int * x；
*   ptr x；

***答案:****int * x；*

**变量的地址**

下列哪一项给出了整型变量 a 的内存地址？

*   * a；
*   a；
*   &a; (ans)
*   地址(a)；

***答案:*** *&答*

***解释:*** *变量 a 是整数，而不是整数指针。所以我们用& a 来获取它的地址。*

**变量的地址**

下列哪一项给出了指针“a”指向的变量“b”的内存地址，即

```
int b = 10;
int *a = &b;
```

*   a
*   *a
*   &a
*   地址(a)

***答案:*** *答*

***解释:*** *a 是存储变量 b 地址的指针*

**指针输出**

这段代码会发生什么？

```
int a = 100, b = 200;
int *p = &a, *q = &b;
p = q;
```

*   b 被分配给 a
*   p 现在指向 b
*   a 被分配给 b
*   q 现在指向 a

***答案:*** *p 现在指向 b*

***解释:*** *a 和 b 是两个整型变量。p 存储 a 的地址，q 存储 b 的地址。通过执行 p = q，p 现在存储 b 的地址*

**输出**

```
int a = 7;
int b = 17;
int *c = &b;
*c = 7;
cout  << a << "  “ << b << endl;
```

*   7 17
*   17 7
*   7 7
*   17 17

***答案:*** *7 7*

***解释:*** *c 存储变量 b 的地址，然后将 c(属于 b)中存储的地址处的值更新为 7(即 b = 7)。*

**输出**

```
 int a = 50;
 int *ptr = &a;
 int *q = ptr;
 (*q)++;
 cout << a << endl;
```

*   50
*   51
*   错误
*   这些都没有

***答案:*** *51*

***解释:*** *ptr 指向 a. q 直接指向 ptr，通过 ptr 指向 a。* q = p 的值= a 的地址，所以，(*q)++在 a 的地址处递增值，所以 a 从 50 变成 51。*

**输出**

```
int *ptr = 0;
int a = 10;
*ptr = a;
 cout << *ptr << endl;
```

*   10
*   0
*   错误
*   这些都没有

***答案:*** *错误*

***说明:*** *打印时，*ptr 指向地址 a 的值为 10。地址 10 没有存储值。*

**输出**

```
int a = 7;
int b = 17;
int *c = &b; 
a = *c;
*c = *c + 1;
cout  << a << "  " << b << endl;
```

*   18 18
*   7 18
*   17 17
*   17 18

***答案:*** *17 18*

***解释:*** *c 指向 b. a 在 c 中存储的地址处有值，是 b 的(17)。存储在 c 中的地址值增加 1 (b = 17 + 1 = 18)。*

**指针输出**

```
float f = 10.5;
float p = 2.5;
float* ptr = &f;
(*ptr)++;
*ptr = p;
cout << *ptr << “ “ << f << “ “ << p;
```

*   2.5 10.5 2.5
*   2.5 11.5 2.5
*   2.5 2.5 2.5
*   11.5 11.5 2.5

***答案:*** *2.5 2.5 2.5*

***解释:*** *ptr 指向 f，f 通过 ptr 递增 1(现在 f = 11.5)。使用 ptr 时 f = p(现在 f = 2.5)。*

**指针输出**

```
int a = 7;
int *c = &a;
c = c + 1;
cout  << a << "  " << *c << endl;
```

*   垃圾值 7
*   7 垃圾值
*   8 8
*   7 7

***答案:*** *7 垃圾 _ 值*

***解释:*** *c 存储 a 的地址(并指向 a 的值)。c 存储的地址加 1，所以现在它指向一个未知值。*

**输出**

假设变量“a”的内存地址是:400(一个整数需要 4 个字节)，输出会是什么

```
int a = 7;
int *c = &a;
c = c + 3;
cout  << c << endl;
```

***答案:*** *412*

***解释:*** *c 存储 a 的地址(并指向 a 的值)。c 存储的地址递增 3。因为 c 的类型是 int，所以字节的增量是 3 个整数地址，也就是 3*4 = 12 个字节。因此 400 + 12 = 412*

**输出**

假设整数占用 4 个字节，整数指针占用 8 个字节。

```
int a[5];
int *c;
cout << sizeof(a) << “ “ << sizeof(c);
```

*   8 8
*   5 8
*   20 8
*   20 4

***答案:*** *20 8*

***解释:*** *数组 a 的大小为 5，类型为 int(每 int 4 个字节)，所以总大小= 5*4 = 20。c 是一个整数指针，所以它的大小是 4(对于 32 位系统)或 8(对于 64 位系统)。*

**填充输出**

```
int a[] = {1, 2, 3, 4};
cout << *(a) << " " << *(a+1);
```

***答案:*** *1 2*

***解释:*** **a 指向数组 a = 1 的第一个值。*(a+1) = *(数组 a 的第二个值)= 2。*

**填充输出**

假设数组“a”第 0 个索引的地址是:200。

产量是多少-

```
int a[6] = {1, 2, 3};
cout << a << “ “ << &a;
```

*   错误
*   200 204
*   200 200
*   1 200
*   200 1

***答案:*** *200 200*

***解释:*** *a 是数组 a 的第一个值& a 是数组 a 的第一个值的地址，为 200。*

**填充输出**

假设数组“a”第 0 个索引的地址是:200。产量是多少-

```
int a[6] = {1, 2, 3};
cout << (a + 2);
```

***答案:*** *208*

***解释:*** *a 的类型是 int，所以每增加一个值，地址增加 4。a+2 是数组 a 的第三个值的地址。所以 200 (1) — 204 (2) — 208 (3)*

**输出**

假设数组“a”的第 0 个索引的地址是 200。

产量是多少-

```
int a[6] = {1, 2, 3};
int *b = a;
cout << b[2];
```

*   错误
*   3
*   1
*   200
*   212

***答案:*** *3*

***解释:*** *b 存储数组 a 第一个值的地址，b[2]会是数组 a 的第 0，1，2 个值，也就是 3。*

**输出**

假设数组“a”的第 0 个索引的地址是 200。

产量是多少-

```
int a[] = {1, 2, 3, 4, 5};
cout << *(a) << " " << *(a + 4);
```

*   错误
*   200 216
*   1 5
*   这些都没有

***答案:*** *1 5*

***解释:*** **a 给出数组 a 的第一个值(1)。*(a+4)给出数组 a (5)的第五个值。*

**输出**

```
int a[] = {1, 2, 3, 4};
int *p = a++;
cout << *p << endl;
```

*   1
*   2
*   垃圾价值
*   错误

***答案:*** *错误*

***解释:*** *整个数组的地址不能移位四个字节*

**指针输出**

```
char ch = 'a';
 char* ptr = &ch;
 ch++;
 cout << *ptr << endl;
```

*   a
*   b
*   97
*   98

***答案:b***

***解释:*** *小 a ascii 97。ptr 指向 ch。ch 递增，现在为 98 (b)。*

**输出**

假设数组“b”的第 0 个索引的地址是 200。产量是多少-

```
char b[] = "xyz";
char *c = &b[0];
cout << c << endl;
```

*   200
*   x
*   xyz
*   这些都没有

***答案:*** *xyz*

***解释:*** *c 存储数组 b 的起始地址(而不是它的值)。所以当 c 被打印时，整个数组也被打印。*

**输出**

假设数组“b”的第 0 个索引的地址是 200。产量是多少-

```
char b[] = "xyz";
char *c = &b[0];
c++;
cout << c << endl;
```

*   201
*   y
*   xyz
*   yz

***答案:*** *yz*

***解释:*** *c 存储数组 b 的起始地址(而不是它的值)。因为它是 char 类型的，所以 c 的地址增加了一个字节。因此，除了跳过的/第一个字符之外，数组的所有字符都被打印。*

**填充输出**

```
char s[]= "hello";
char *p = s;
cout << s[0] << " " << p[0];
```

***答案:*** *h h*

***解释:*** *p 指向数组 s 的起始值，p[0]调用从其地址跳过的 0 个字符处的值，该值是 s[0]的地址本身的值。*

**指针输出**

```
void changeSign(int *p){
  *p = (*p)  *  -1;
}int main(){
  int a = 10;
  changeSign(&a);
  cout << a << endl;
}
```

*   -10
*   10
*   错误
*   以上都不是

***答案:*** *-10*

***解释:*** *函数的 p 存储了 a 的地址.所以它指向 a 的实际值.当 p 指向的值为负时，a 也变为负，反之亦然。*

**填充输出**

```
void fun(int a[]) {
    cout << a[0] << " ";
}int main() {
    int a[] = {1, 2, 3, 4};
    fun(a + 1);
    cout << a[0];
}
```

***答案:*** *2 1*

***解释:*** *a +1 给出除数组第一个值以外的整个数组作为参数(2 3 4)。所以第 0 个值是 2。*

**输出**

```
void square(int *p){
 int a = 10;
 p = &a;
 *p = (*p) * (*p);
}int main(){
 int a = 10;
 square(&a);
 cout << a << endl;
}
```

*   100
*   10
*   错误
*   这些都没有

***答案:*** *10*

***解释:*** *p 指向 a 的实际值，因为 a 的地址是作为参数传递的。在函数内，p 现在指向函数内的局部 a。更新本地 a 不会更改主服务器中的 a。*

**输出**

```
int a = 10;
int *p = &a;
int **q = &p;
int b = 20;
*q = &b;
(*p)++;
cout << a << " " << b << endl;
```

*   10 21
*   11 20
*   11 21
*   10 20

***答案:*** *10 21*

***解释:*** *p 指向 a. q 直接指向 p，a 通过 p(双指针)。*q —存储在 p 中的值被更改为 b 的地址，而不是 a 的地址。(* p)++—p 指向的值(现在是 b 的)增加 1 (b 变成 21)。a 的值保持不变。*

**输出**

```
int a = 100;
int *p = &a;
int **q = &p;
int b = (**q)++ + 4;
cout << a << " " << b << endl;
```

*   100 104
*   101 104
*   101 105
*   100 105

***答案:*** *101 104*

***解释:*** *p 指向 a，q 直接指向 p，通过 p(双指针)指向 a。b 存储 a 到 p 到 q 加 4 的值，即 100 + 4 = 104。在该语句结束后，使用 post increment 运算符将存储在 b 中的值增加 1。*

**指针输出**

`int a = 100;
int *p = &a;
int **q = &p;
int b = (**q)++;
int *r = *q;
(*r)++;
cout << a << " " << b << endl;`

*   102 100
*   101 100
*   101 101
*   102 101

***答案:*** *102 100*

***解释:*** *p 指向 a. q 直接指向 p 并通过 p 指向 a . b 被赋予 a 到 q 的值(b = 100)a 到 q 的值被 post 递增(a = 101)。r 指向 p，p 处的值通过 r 后递增(a = 102)。*

**指针输出**

```
void increment(int **p){
  (**p)++;
}int main(){
 int num = 10;
 int *ptr = &num;
 increment(&ptr);
 cout << num << endl;
}
```

*   10
*   11
*   错误
*   这些都没有

***答案:*** *11*

***解释:*** *ptr 指向小水。p 直接指向 ptr，通过 ptr 指向 num。num 处的值从 q 到 p 递增 1(num 变为 11)。*

**输出**

```
#include <iostream>
using namespace std;
int main()
{
  int arr[] = {4, 5, 6, 7};
  int *p = (arr + 1);
  cout << *arr + 9;
  return 0;
}
```

*   12
*   14
*   13
*   错误

***答案:*** *13*

***解释:*** *p 指向数组 arr 的起始索引地址加 4 个字节，为第 1 个索引。*arr 指向第一个索引 4，加上 9 得到 13。*

**输出**

```
#include <iostream>
using namespace std;
int main ()
{
  int numbers[5];
  int * p;
  p = numbers; 
  *p = 10;
  p = &numbers[2]; 
  *p = 20;
  p--; 
  *p = 30;
  p = numbers + 3;
  *p = 40;
  p = numbers;
  *(p+4) = 50;
  for (int n=0; n<5; n++) {
     cout << numbers[n] << ",";
  }
  return 0;
}
```

*   10,20,30,40,50,
*   50,40,30,20,10,
*   10,30,20,40,50,
*   这些都没有

***答案:*** 10，30，20，40，50，

***解释:*** *p 指向 numbers 数组的第一个值，更新为 10 (numbers[0] = 10)。p 现在指向 numbers 数组的第三个值，并将其更新为 20 (numbers [2] = 20)。p 减少 4 个字节，并更新为 30(数字[1])。p 现在指向 numbers 的第 4 个值，并将其更新为 40 (numbers[3] = 40)。p 现在指向 numbers 数组的第一个值，将其第五个值更新为 50。数字= 10 30 20 40 50*

**输出**

```
#include <iostream>
using namespace std;
int main()
{ 
  char *ptr; 
  char Str[] = "abcdefg";
  ptr = Str;
  ptr += 5;
  cout << ptr;
  return 0;
}
```

*   细粒
*   cdef
*   defg
*   加快收寄投递系统

***答案:*** *fg*

***解释:*** *ptr 指向整个字符串数组。ptr 现在指向字符串数组的第六个值。打印从第六个索引开始的所有字符。*

**字符&指针**

```
#include <iostream>
using namespace std;
int main()
{
  char arr[20];
  int i;
  for(i = 0; i < 10; i++) {
    *(arr + i) = 65 + i;
  }
  *(arr + i) = '\0';
  cout << arr;
  return 0;
}
```

*   ABCDEFGHIJ
*   AAAAAAAAAA
*   JJJJJJJJ
*   都没有提到

***答案:*** ABCDEFGHIJ

***解释:*** *对于第一次迭代，*(arr + 0)是 ascii(65 + 0)哪个是 A，以此类推……*

**输出**

```
#include<iostream>
using namespace std;
void swap (char *x, char *y) 
{
  char *t = x;
  x = y;
  y = t;
}int main()
{
   char *x = "geeksquiz";
   char *y = "geeksforgeeks";
   char *t;
   swap(x, y);
   cout<<x << " "<<y;
   t = x;
   x = y;
   y = t; 
   cout<<" "<<x<< " "<<y;
   return 0;
}
```

*   极客论坛极客论坛
*   极客 squiz 极客 forgeeks 极客 squiz 极客 forgeeks
*   极客论坛极客论坛极客论坛极客论坛
*   编译程序错误

***答案:***geeksquiz geeksforgeeks geeksforgeeks geeksquiz

***解释:*** *由于 swap 函数的参数不通过引用传递，所以调用 swap 函数时，其中的实际值保持不变。*

**输出**

```
#include <iostream>
using namespace std;
int main()
{
  float arr[5] = {12.5, 10.0, 13.5, 90.5, 0.5};
  float *ptr1 = &arr[0];
  float *ptr2 = ptr1 + 3;
  cout<<*ptr2<<" ";
  cout<< ptr2 - ptr1;
  return 0;
}
```

*   90.5 3
*   90.5 12
*   10.0 12
*   不明确的

***答案:*** 90.5 3

***解释:*** *ptr1 指向 arr 的第一个值(12.5)。ptr2 指向 arr 的第四个值(90.5)。所以，*ptr2 是 90.5，如果 ptr1 是 x，ptr2 就是 x + 3。减去这些得到 3。*

**输出**

```
#include<iostream>
using namespace std;
int main() {
  char st[] = "ABCD";
  for(int i = 0; st[i] != ‘\0’; i++) {
     cout << st[i] << *(st)+i << *(i+st) << i[st];
  }
  return 0;
}
```

*   AAAABBBBCCCCDDDD
*   AcceleratedBusinessCollectionandDelivery（美国邮局采用的）加快收寄投递系统
*   A65AAB66BBC67CCD68DD
*   编译错误

***答案:*** A65AAB66BBC67CCD68DD

***解释:*** *第一次迭代:A<<*(ST[0])+0 = A+0(cast to 65)<<ST[0]= A<<ST = A 的第 0 个索引值…..以此类推……*

**输出**

```
#include <iostream>
using namespace std;
void Q(int z)
{
  z += z;
  cout<<z << " ";
}void P(int *y) 
{
  int x = *y + 2;
  Q(x);
  *y = x - 1; 
  cout<<x << " ";
}int main()
{
  int x = 5;
  P(&x);
  cout<<x;
  return 0;
}
```

*   7 6 14
*   14 7 5
*   14 7 6
*   14 6 5

***答案:*** 14 7 6

***解释:****P()中的 y 指向 main 中 x 的实际值。P()中的局部 x 的值为(5 + 2 = 7)。本地 x (7)的副本被传递给 Q()并输出 7+7 = 14。x 的实际值通过 y 更新到局部 x:x-1 = 7–1 = 6。局部 x (7)打印在 P()的末尾。x (6)的实际值在 main 中输出。*

**输出**

```
#include<iostream>
using namespace std;
int main()
{
  int ***r, **q, *p, i=8;
  p = &i;
  (*p)++;
  q = &p;
  (**q)++;
  r = &q;
  cout<<*p << " " <<**q << " "<<***r;
  return 0;
}
```

*   8 8 8
*   10 10 10
*   9 10 11
*   9 10 10

***答案:*** *10 10 10*

***解释:*** *p 指向 I . i++的值通过 p (i = 9)。q 直接指向 p，通过 p 指向 I . i++(I = 10)通过 q. r 直接指向 q，p 通过 q，I 通过 p 通过 q. i，I，I 打印出来，就是 10，10，10。*

**输出**

```
int f(int x, int *py, int **ppz) {
    int y, z;
    **ppz += 1;
    z = **ppz;
    *py += 2;
    y = *py;
    x += 3;
    return x + y + z;
}int main() {
    int c, *b, **a;
    c = 4;
    b = &c;
    a = &b;
    cout << f(c, b, a);
    return 0;
}
```

*   21
*   18
*   19
*   24

***答案:*** *19*

***解释:*** *b 指向 c. a 直接指向 b 并通过 b 指向 c . c，b，a 的副本传递给函数(同样的规则也适用于参数变量)。x 的值通过**ppz (x = 4)递增 1。z 现在店铺**ppz = 4。使用*py (x = 6)将 x 的值增加 2。= *py = 6。x 增加 3 (x = 9)。x + y + x = 4 + 6 + 9 = 19。*

# 链接:

[](https://drive.google.com/file/d/1Ht1oyCWNVSroPS1sEJROBSxyuYyOrMCC/view?usp=sharing) [## pointers_notes.pdf

### 编辑描述

drive.google.com](https://drive.google.com/file/d/1Ht1oyCWNVSroPS1sEJROBSxyuYyOrMCC/view?usp=sharing)