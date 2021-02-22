---
title: "Array learning"
date: 2021-02-07T11:23:33+08:00
Description: ""
Tags: [General]
Categories: [Home]
DisableComments: false
---
<!-- TOC -->

- [1. C++ Primer](#1-c-primer)
  - [1.1. 第1章 开始](#11-第1章-开始)
    - [1.1.1. 编写一个简单的C++程序](#111-编写一个简单的c程序)
      - [1.1.1.1. 编译、运行程序](#1111-编译运行程序)
    - [1.1.2. 节练习](#112-节练习)
    - [1.1.3. 初识输入输出](#113-初识输入输出)
    - [1.1.4. 注释简介](#114-注释简介)
    - [1.1.5. 控制流](#115-控制流)
      - [1.1.5.1. **while** 语句](#1151-while-语句)
      - [1.1.5.2. **for** 语句](#1152-for-语句)
      - [1.1.5.3. 读取不定量的输入数据](#1153-读取不定量的输入数据)
      - [1.1.5.4. **if** 语句](#1154-if-语句)
    - [1.1.6. 类简介](#116-类简介)
- [2. 数据结构](#2-数据结构)
  - [2.1. Arrays](#21-arrays)
    - [2.1.1. :pencil2: 补充说明 1](#211-pencil2-补充说明-1)
    - [2.1.2. :books: 数组操作](#212-books-数组操作)
    - [2.1.3. :books: Initializing arrays](#213-books-initializing-arrays)
    - [2.1.4. :pencil2: 补充说明 2](#214-pencil2-补充说明-2)
    - [2.1.5. :books: Multidimensional arrays](#215-books-multidimensional-arrays)
    - [2.1.6. 二维数组](#216-二维数组)
    - [2.1.7. :books: Arrays as parameters](#217-books-arrays-as-parameters)
    - [2.1.8. :books: Library arrays](#218-books-library-arrays)
- [3. STL---standard template library](#3-stl---standard-template-library)
  - [3.1. Vector](#31-vector)
    - [3.1.1. Initialize](#311-initialize)
    - [3.1.2. 迭代器(遍历器) Iterator](#312-迭代器遍历器-iterator)
    - [3.1.3. 基本操作](#313-基本操作)
- [4. 语法](#4-语法)
  - [4.1. Pointers](#41-pointers)
    - [4.1.1. :books: Address-of operator(&)](#411-books-address-of-operator)
    - [4.1.2. :books: Dereference operator(*)](#412-books-dereference-operator)
  - [4.2. Class](#42-class)
  - [- 类内不在限定符下声明的成员默认是private access.](#--类内不在限定符下声明的成员默认是private-access)
- [5. 算法](#5-算法)
  - [5.1. sort](#51-sort)
  - [5.2. Binary search](#52-binary-search)
    - [5.2.1. 常用场景](#521-常用场景)
    - [5.2.2. 框架](#522-框架)
      - [5.2.2.1. 寻找一个数](#5221-寻找一个数)
- [6. 刷题](#6-刷题)
  - [6.1. 数组](#61-数组)
    - [6.1.1. 寻找中心索引](#611-寻找中心索引)
    - [6.1.2. 搜索插入位置](#612-搜索插入位置)
    - [6.1.3. 合并区间](#613-合并区间)

<!-- /TOC -->
# 1. C++ Primer
## 1.1. 第1章 开始
### 1.1.1. 编写一个简单的C++程序
语句`statement`，声明`declaration`，初始化`initialize`
- 每个C++程序必须包含**main**函数，操作系统通过调用**main**来运行C++程序.
- 函数定义包括四部分：返回类型，函数名，形参列表，函数体.  
- `int`类型是一种内置类型，即语言自身定义的类型.  
- 类型不仅定义了数据元素的内容，还定义了这类数据上可以进行的运算.  

#### 1.1.1.1. 编译、运行程序  
程序编写后需要编译它，这一过程依赖于操作系统和编译器.  
- 编译器要求源码存储在一个或多个源文件中，源文件命名以(名字.后缀)组合. 
- 命令行运行编译器，命令如**例1.1.1.1**，Windows系统下，编译器生成可执行文件，命名为`prog1.exe`；UNIX系统下，编译器将可执行文件命名为`a.out`.
```cpp
/* 例1.1.1.1 */
$ CC prog1.cc   // CC是编译器名字，.cc是源文件后缀
```

- 在Windows下运行可执行性文件，可键入`$ .\prog1`，"."后跟反斜线指出该文件在当前目录中.  
- 在UNIX系统下，需要使用全文件名，包括文件扩展名，`$ ./a.out`.  
- 访问**main**的返回值，UNIX下可`$ echo $?`，Windows下可`$ echo %ERRORLEVEL%`，获得其返回值.  
- 常用编译器有GNU编译器和微软Visual Studio编译器，我们学习中选择GNU编译器.默认情况下，运行GNU编译器的命令是`g++`:`$ g++ -o prog1 prog1.cc`,`-o prog1`是编译器参数，指定了可执行文件的文件名，UNIX下生成无后缀的`prog1`，Windows下生成`prog1.exe`.  
- 根据GNU编译器的版本，可能需要指定`-std=c++0x`参数来打开对C++11的支持；此外，GNU编译器中使用`-Wall`选项，能对有问题的程序结构发出警告.  


### 1.1.2. 节练习  
GNU编译器默认命令为`g++`，所使用的文件命名约定为`name.cpp(c++,cxx...)`.  

### 1.1.3. 初识输入输出  
C++语言未定义任何输入输出(IO)语句，包含了一个全面的标准库来提供IO机制.所使用的`iostream`包含两个基础类型`istream`和`ostream`，分别表示输入流和输出流.  
- "流(`stream`)"是指，随时间的推移，字符是顺序生成或消耗的.  
- 标准库定义了4个IO对象，`istream`类型的`cin`对象；`ostream`类型的`cout`,`cerr`,`clog`对象.  
- `#include`指令和头文件的名字必须写在同一行中，通常情况下，`#include`指令必须出现在所有函数之外.  
- 表达式(`expression`)由一个或多个运算对象和运算符组成.  
- 输出运算符`<<`接受两个运算对象，左侧运算对象必须是一个`ostream`对象，右侧运算对象是要打印的值，实现将给定的值写到给定的`ostream`对象中，输出运算符返回其左侧运算对象作为其计算结果，由此，多个输出运算符链接，能将前一次计算结果(`ostream`对象)作为第二个运算符的左侧运算对象.  
- 字符串字面值常量(`string literal`)，是用双引号包围的字符序列.  
- `endl`是一个操纵符(`manipulator`)，结束当前行，并将与设备关联的缓冲区(`buffer`)中的内容刷到设备中；缓冲刷新操作能保证目前为止程序产生的输出都真正写入输出流中，而不仅仅顶留在内存中等待写入流.  
- 调试时，保持刷新流的输出，有利于程序崩溃时错误位置的推断.  
- 命名空间(`namespace`)帮助我们不免不经意的名字定义冲突，以及使用苦衷相同名字导致的冲突,标准库(**Standard Library**)中的名字都在命名空间`std`中.  
- 显式说明我们想使用来自命名空间`std`中的名字，可以通过作用域运算符`::`来实现.  
- 初始化(`initialize`)是指在创建一个变量(`variable`)的同时为它赋予一个值.  
- 输入运算符(`>>`)接受一个`istream`作为其左侧运算对象，接受一个对象作为其右侧运算对象，返回其左侧运算对象作为其计算结果，故同样可以链式计算.实现功能为：读入输入数据.  

### 1.1.4. 注释简介  
注释(`comments`)帮助人类读者理解程序，概述算法，确定变量用途，解释晦涩难懂的代码段.

### 1.1.5. 控制流
#### 1.1.5.1. **while** 语句
```cpp
while(condition)
    statement
```
- 语句块(`block`)是用花括号包围起来的零条或多条语句的序列.  
- 复合赋值运算符(`+=`)，将右侧运算对象加到左侧运算对象上，将结果保存到左侧运算对象中，其本质等价于一个加法结合一个赋值(`assignment`).  
- 前缀递增运算符(`++`)，`++val`等价于`val = val + 1`.  

#### 1.1.5.2. **for** 语句
在循环条件中检测变量，在循环体中递增变量的模式，衍生出`for 语句`.  

#### 1.1.5.3. 读取不定量的输入数据
```cpp
#include <iostream>
int main()
{
    int sum = 0, value = 0;
    // 读取数据直到遇到文件尾，计算所有读入数值的和
    while (std::cin >> value)
        sum += value;
    std::cout << "Sum is: " << sum << std::endl;
    return 0;
}
```
```
Windows下，输入文件结束符的方法是`Ctrl+Z`，然后按'Enter'；  
UNIX系统中，`Ctrl+D`
```

- 编译器检查中程序常见的形式(`form`)错误：语法错误(`syntax error`)、类型错误(`type error`)、声明错误(`declaration error`).  

#### 1.1.5.4. **if** 语句
- 相等运算符(`==`)，区别于赋值运算符(`=`)，在条件判断中注意别混淆.

### 1.1.6. 类简介
C++中通过类(`class`)来定义数据结构(`data structure`)，一个类定义一个类型以及相关的一组操作.C++的设计焦点就是能定义使用上像内置类型一样自然的类类型(`class type`).  

- 对于自己定义类的访问，可以通过头文件实现，习惯上，头文件根据其中定义类的名字来命名，以`.h`为后缀.另外需要注意，标准库头文件通常不带后缀，编译器一般不关心头文件名的形式.  
- 每一个类实际都定义了一个新的类型，其类型名就是类名，与内置类型一样，我们可以定义类类型的变量.

# 2. 数据结构
## 2.1. Arrays  
- 数组是一列相同类型元素的集合，内存连续.
- 数组内元素可通过同一标识符、不同索引访问.
- 数组同其它变量一样，使用前需要声明，索引从0开始.

```cpp
// 含5个int类型元素的foo数组
int foo [5]; 
```

- 集合：由一个或多个确定元素构成的整体，数据结构是在集合的基础上添加规则形成。1. 元素类型不一定相同；2. 元素没有顺序(取集合中的第三个元素，这一要求不成立).
- 列表：一种数据项构成的有限序列，具有顺序，长度可变(可进行增、删)，其主要表现形式有数组和列表，此外，栈和队列是两种特殊类型的列表.
- 数组：列表的实现形式之一，其与列表的区分在于<font color=red>**索引**</font>的概念，数组可通过索引标识元素在数组中的位置，但列表中不存在索引；再者，数组中元素在内存中连续存储，每个元素占用相同的内存大小，而列表中元素在内存中可能不相邻，如链表.

### 2.1.1. :pencil2: 补充说明 1
- 1.1 数组声明时方括号内的元素代表数组元素的个数，必须为常量表达，因为数组是静态存储块，在代码执行前的编译环节必须确定.    
- 1.2 [Emoji Cheat Sheet](https://www.webfx.com/tools/emoji-cheat-sheet/)

---

### 2.1.2. :books: 数组操作
- 读取元素：计算机会为数组在内存中申请一段<font color=red>**连续的空间**</font>，并记录索引为`0`处的内存地址，当访问索引为`m`处的元素时，计算机进行如下操作：  
  1. 找到数组索引`0`的内存地址(如`2008`)；
  2. 将内存地址加上目标索引值，作为目标元素的地址(`2008+m`)，这时便可找到目标元素.  

    该操作时间复杂度为$O(1)$.

- 查找元素：由于只保存了索引为`0`处的内存地址，查找元素时从数组开头逐步往后查找，直到寻得目标元素或搜索至数组末尾.该操作时间复杂度为$O(N)$.  

- 插入元素：1. 末尾插入 --> 计算机通过数组长度和位置计算得到待插入元素的内存地址，然后将其插入指定位置；2. 中间插入-->  需要为该元素腾位置，即将旧元素及其之后的元素整体后移一位，然后完成插入操作.<font color=red>**注意：**</font>频繁对数组元素进行插入操作很浪费时间，另一种数据结构(链表)可以有效解决此问题.

- 删除元素：同元素插入操作一般，数组元素删除后，会留下空缺位置，而数组元素在内存中是连续的，需要后面元素对该元素位置进行填补.该操作时间复杂度为$O(N)$.

### 2.1.3. :books: Initializing arrays
- 数组声明时初始化  

```cpp
// 花括号内的元素数目不大于声明数组的大小
int foo [5] = {16, 23, 36, 1203, 12071};

// 若初始化元素数目小于声明数组大小，剩余元素初始化为0
int bar [5] = {10, 20, 30}; // --> bar = {10, 20, 30, 0, 0};

// 初始化数组元素为 0
int baz [5] = {}; // --> baz = {0, 0, 0, 0, 0};

// 声明时不指定数组大小，由编译器由初始化数值数目来判断数组大小
int foo [] = {16, 23, 36, 1203, 12071}; // --> 数组foo大小为5

// 通用初始化方式
int foo[] {16, 23, 36, 1203, 12071};
```

### 2.1.4. :pencil2: 补充说明 2  
- 2.1 C++中，超过数组索引有效范围的操作是语法允许的，在访问超出范围的元素不会导致编译错误，但运行时会出现错误.允许该现象存在的原因在之后引入指针的章节会介绍.

---

### 2.1.5. :books: Multidimensional arrays
- 多维数组可视为"arrays of arrays"  

```cpp
// 声明一个二维数组，等同于3行5列的表格，内部元素具有统一 int 类型，同时，数组元素一样从 0 开始排序
int jimmy [3][5];
```

```cpp
// 使用定义常数声明数组，便于阅读和之后更改
#define WIDTH 5
#define HEIGH 3

int jimmy [HEIGH][WIDTH];
```

### 2.1.6. 二维数组
多维数组类似于表或矩阵的结构.对于二维数组，其本质还是一维数组，内部索引从`0`开始，其内部元素同样也是数组，故在定义二维数组时，计算机在内存中申请一段连续的空间，并记录第一个元素(也即第一行数组)的索引位置`A[0][0]`.  
![二维数组内存地址](https://raw.githubusercontent.com/hxie13/picMD/master/newTools/locationIndex.png.jpg?token=AJZDV2GET3ZU6S5GTX7L4A3AGO5ZC)  


### 2.1.7. :books: Arrays as parameters
- C++中不能将代表空间存储块的数组作为参数直接传递给函数，而是传递数组的地址，这样更快捷高效.

```cpp
/* 函数为接收数组参数，可以将参数声明为数组类型，但是不指定其真实大小
void procedure (int arg[]);
int myarray [40];
procedure (myarray); // 函数响应 */

// An example:
#include <iostream>
using namespace std;

void printArray (int arg[], int length)
{
    for(int n=0; n<length; ++n)
        cout << arg[n] << '';
    cout << '\n';
}

int main()
{
    int firstArray[] = {5, 10, 15};
    int secondArray[] = {2, 4, 6, 8, 10};
    printArray(firstArray, 3);
    printArray(secondArray, 5);
}
------------
/* OUTPUT
5 10 15
2 4 6 8 10
*/
------------
```  

- 同样，函数声明时，同样可以包含多维数组

~~~cpp
// 首维大小可以待定，但后面维的depth需要确定
void procedure (int myArray[][3][4]);
~~~

### 2.1.8. :books: Library arrays 
- C++提供标准容器这一数组类型，是一种类模板，在头文件\<array>中定义.允许复制(复制整个存储块单元).  

```cpp
#include <iostream>
#include <array>
using namespace std;

int main()
{
    array<int, 3> myArray {10, 20, 30};

    for(int i=0; i<myArray.size(); ++i)
        ++myArray[i];
    
    for(int elem: myArray)
        cout << elem << '\n';
}
```

# 3. STL---standard template library
## 3.1. Vector  
向量`vecotr`是一种对象实体，能容纳许多其他类型相同的元素，因此也被称为容器，属于标准模板库中的一种自定义数据类型，广义上被认为数组的增强版.  
- 使用前包含头文件`#include <vector>`
- 与数组相比其优点在于能根据需求随时自动调整大小，此外还提供许多方法对自身进行操作.  

### 3.1.1. Initialize
```cpp
vector<int> a;  // 声明一个int型向量 a
vector<int> b(10);  // 声明一个初始大小为10的向量 b
vector<int> c(10,1);    // 声明一个初始大小为10的向量 c，并初始化其元素值都为1
vector<int> d(c);   // 声明一个int型向量 d，并用向量c对其初始化
vector<int> g(c.begin(), c.begin()+3);  // 将c向量中从 0th 到 2th(共3个)元素作为向量g的初始值

/* 此外，还能使用数组来初始化向量 */
int n[] = {1, 2, 3, 4, 5};
vector<int> a(n,n+5);   // 将数组n的前5个元素作为向量a的初值
vector<int> a(&n[0], &n[4]);    // 等效于上一条语句
```

### 3.1.2. 迭代器(遍历器) Iterator
向量中，迭代器类型为`vector<type>::iterator`，迭代器不但可以表示元素位置，还能在容器中前后移动.
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main(){
    vector<int> a(10,0);

    for(int i =0; i < a.size(); i++>){
        cin >> a[i];
    }

    vector<int>::iterator t;
    for(t=a.begin(); t!=a.end(); t++){
        cout << *t << " ";
    }
}

```  

### 3.1.3. 基本操作  
```cpp
a.size();   // 获取向量中元素个数
a.empty();  // 判断向量是否为空
a.clear();  // 清空向量中的元素
a = b;  // 将向量b 复制到向量a中

a.insert(a.begin(), 1000);  // 将1000插入到向量起始位置
a.insert(a.begin(), 3, 1000);   //在a.begin()前增加3个1000

vector<int> a(5, 1);
vector<int> b(10);
b.insert(b.begin(), a.begin(), a.end());    // 将 a.begin(), a.end() 之间的全部元素插入到b.begin()前

b.erase(b.begin()); // 删除起始位置的元素
b.erase(b.begin(), b.begin()+3);    // 将起始起的四个元素删除.

b.swap(a);  // 将a向量和b向量进行交换

void push_back(const T& x); // 向向量尾部增加一个元素x
void pop_back();    // 删除向量中最后一个元素
```


---
# 4. 语法
## 4.1. Pointers
Variables是计算机内存中的位置，通过标识符(变量名)访问，程序允许不关心数据在内存中的物理地址，仅在引用变量时使用标识符.  
C++程序中，计算机内存类同相连的记忆单元，每个单元占据一个字节，任一单元可以通过其独特的地址进行定位.在变量声明时，存储其数值所需的内存在内存中分配了特定位置(其内存地址)，C++程序不主动决定变量存储内存的确切地址，而是由程序运行的操作系统决定.但在实际编程中，了解变量在运行时的内存地址是相当有用的.  

### 4.1.1. :books: Address-of operator(&)  
通过取地址运算符(&)能获取变量的地址，语法如：`foo = &myvar;`，此中，存储变量地址的变量(foo)就是C++中的指针.  

### 4.1.2. :books: Dereference operator(*)  
指针被称为"指向"其存储地址的变量，通过解引用运算符(*)能直接访问指针所指向的变量，`baz = *foo;`，baz等于指针foo所指向的数值.  

## 4.2. Class  
- 类内定义的成员函数被编译器自动视为内联函数，类内声明、类外定义的成员函数视为正常函数，在编译器优化时会产生区别.
- 类内不在限定符下声明的成员默认是private access.  
---

# 5. 算法

## 5.1. sort
- 对向量对象的排序，sort将`vector<int>`视为一个一维数组对象，整体进行比较和排序，默认从小到大排序，比较两个int向量时从第一个元素开始比较.

## 5.2. Binary search  
**`Although the basic idea of binary search is comparatiively straightward, the details can be surprisingly tricky.`**  

### 5.2.1. 常用场景  
- 寻找一个数  
- 寻找左测边界  
- 寻找右侧边界  

### 5.2.2. 框架  
```cpp
int binarySearch(int[] nums, int target){
    int left = 0, right = ...;

    while(...){
        int mid = (right + left) / 2;   // 防止溢出的技巧：mid = left + (right - left)/2;
        if (nums[mid] == target){
            ...
        }
        else if(nums[mid] < target){
            ...
        }
        else if(nums[mid] > target){
            ...
        }
    }
    return ...;
}
```  
二分查找不要出现`else`，而是用`else if`将所有情况说清楚，以此展现所有细节.  

#### 5.2.2.1. 寻找一个数
- 题目描述：搜索一个数，存在则返回其索引`index`，否则返回`-1`.

```cpp
int binarySearch(int[] nums, int target){
    int left = 0;
    int right = nums.length - 1;

    while(left<=right){
        int mid = left + (right - left) / 2;
        if (nums[mid] == target){
            return mid;
        }
        else if (nums[mid] > target){
            left = mid + 1;
        }
        else if (nums[mid] < target){
            right = mid -1;
        }
    }
    return -1;

}
```

# 6. 刷题  
## 6.1. 数组  
### 6.1.1. 寻找中心索引
题目描述：给定一个整数数组`nums`，请编写能返回数组**中心索引**的方法,若数组不存在中心索引，返回`-1`；若数组有多个中心索引，返回最靠近左边的一个.
- 数组**中心索引**其左侧所有元素相加的和等于右侧所有元素相加的和；
- 中心索引有可能出现在数组两端，在最左端时，索引`[0]`左侧视为**0**，右侧所有元素相加为**0**；出现在最右端同理.  

```cpp
/*
1. 从左往右寻找，返回第一个满足条件的索引，返回最靠左边一个索引的要求自动实现；
2. 先计算得到数组元素总和，以左边元素之和sumLeft等于右边元素之和sumRight为条件返回索引，否则返回-1；
3. 寻找条件中的等量关系，sumLeft + sumRight + nums[i] = sumAll，
   若满足条件，sumLeft = 0.5*(sumAll-nums[i])，判定条件得到简化.
*/

class Solution{
public:
    int pivotIndex(vector<int>& nums){
        int sumLeft = 0;
        int sumAll = 0;
        int len = nums.size();

// 发现一个有趣的现象，此处判断 'len == 1' or 'len == 0' 在leetcode上执行用时发生变化
// 可能是对测试用例中单元素向量进行了加速？
        if (len == 1){
            return 0;
        }

        for (auto element:nums){
            sumAll = sumAll + element;
        }

        int temp = 0;
        for (int i=0; i<=len-1; ++i){
            sumLeft = sumLeft + temp;
            
            if (sumLeft == (0.5*(sumAll-nums[i]))){
                return i;
            }

            temp = nums[i];
        }

        return -1;
    }
};
```

### 6.1.2. 搜索插入位置  
题目描述：给定一个**排序数组**和一个目标值`target`，从数组中找到目标值，并返回其索引，若目标值不存在数组中，返回它将被按顺序插入的位置索引(假设数组中无重复元素).  

- 二分查找相关

```cpp
/*
1. 套用二分查找的模板，更新左右端索引，寻找目标位置
2. 在二分查找基础上需要给定目标值在数组中的插入位置
*/

class Solution{
public:
    int searchInsert(vector<int> nums, int target){
        int len = nums.size();
        int idLeft = 0;
        int idRight = len - 1;
        
        if (len == 1){
            return (target<=nums[0]?0:1);
        }

        // 此处判定条件若为`!=`，会出现错误
        while(idLeft <= idRight){
            int idMid = idLeft + 0.5*(idRight - idLeft);

            if (target == nums[idMid]){
                return idMid;
            }
            else if(target > nums[idMid]){
                idLeft = idMid + 1;
            }
            else if(target < nums[idMid]){
                idRight = idMid - 1;
            }
        }

        return idLeft;
    }
};

```

### 6.1.3. 合并区间  
问题描述：以数组`intervals`表示若干个区间的集合，其中单个区间为 $intervals[i]=[start_i, end_i]$，要求合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需要恰好覆盖输入中的所有区间.  

```cpp
/*
1. 二维vector的初始化方式.
2. sort函数对二维vector的处理方式
*/

class Solution{
public:
    vector<vector<int> > merge(vector<vector<int> >& intervals){

    }
}
```
