# C++ 标准库学习

[整理主要来源：OIwiki](https://oi-wiki.org/lang/csl/)

[TOC]

## 标准库简介

### C++标准

>C++ 自 1985 年诞生以来，一共由国际标准化组织（ISO）发布了 5 个正式的 C++ 标准，依次为 C++98、C++03、C++11（亦称 C++0x）、C++14（亦称 C++1y）、C++17（亦称 C++1z）、C++20（亦称 C++2a）。C++ 标准草案在 open-std 网站上，最新的标准 C++23（亦称 C++2b）仍在制定中。此外还有一些补充标准，例如 C++ TR1。

>每一个版本的 C++ 标准不仅规定了 C++ 的*语法、语言特性*，还**规定了一套 C++ 内置库的实现规范**，这个库便是 **C++ 标准库**。C++ 标准库中包含大量常用代码的实现，如输入输出、基本数据结构、内存管理、多线程支持等。掌握 C++ 标准库是编写更现代的 C++ 代码必要的一步。C++ 标准库的详细文档在 [cppreference](https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5) 网站上，文档对标准库中的类型函数的用法、效率、注意事项等都有介绍，请善用。

### 标准模板库（STL）

**标准模板库（Standard Template Library）**，是 C++ 标准库的一部分，里面包含了一些模板化的通用的数据结构和算法
由于其模板化的特点，它能够兼容自定义的数据类型，避免大量的造轮子（Reinventing_the_wheel）工作

STL的六大件包括容器、算法、迭代器、仿函数、适配器和空间配置器，其中几乎所有代码均使用了模板类和模板函数的概念[^1]

### Boost库

乃除了标准库外，另一个久副盛名的**开源 C++ 工具库**，其代码具有可移植、高质量、高性能、高可靠性等特点。
其模块数量非常之大，功能全面，并且拥有完备的跨平台支持，因此被看作 C++ 的准标准库。
C++ 标准中的不少特性也都来自于 Boost，如智能指针、元编程、日期和时间等

## STL容器

>在C++ 中容器被定义为：**在数据存储上，有一种对象类型，它可以持有其它对象或指向其它对像的指针，这种对象类型就叫做容器。** 很简单，容器就是**保存其它对象的对象**，当然这是一个朴素的理解，这种“对象”还包含了一系列处理“其它对象”的方法，因为这些方法在程序的设计上会经常被用到，所以容器也体现了一个好处， 就是“容器类是一种**对特定代码重用问题的良好的解决方案**”。
容器还有另一个特点是容器可以自行扩展。在解决问题时我们常常不知道我们需要存储多少个对象，也就是说我们不知道应该创建多大的内存空间来保存我们的对象。 显然，数组在这一方面也力不从心。容器的优势就在这里，它不需要你预先告诉它你要存储多少对象，只要你创建一个容器对象，并合理的调用它所提供的方法，所 有的处理细节将由容器来自身完成。它可以为你申请内存或释放内存，并且用最优的算法来执行您的命令。
容器是随着面向对象语言的诞生而提出的，容器类在面向对象语言中特别重要，甚至它被认为是早期面向对象语言的基础。在现在几乎所有的面向对象的语言中也都伴随着一个容器集，在C++ 中，就是标准模板库（STL）。
和其它语言不一样，C++ 中处理容器是采用基于模板的方式。标准C++ 库中的容器提供了多种数据结构，这些数据结构可以与标准算法一起很好的工作，这为我们的软件开发提供了良好的支持！

>kimiAI：在C++中，容器（Container）是标准模板库（Standard Template Library，STL）的一部分，它**提供了一种灵活的方式来存储数据集合**。容器**可以容纳各种类型的数据，并且提供了多种操作来管理这些数据**。

### STL简介

#### 分类

[分类](./pictures/container1.png)

##### 序列式容器（顺序容器）

- **向量(vector)** 后端可高效增加元素的顺序表。
- **数组(array)** C++11，定长的顺序表，C 风格数组的简单包装。
- **双端队列(deque)** 双端都可高效增加元素的顺序表。
- **列表(list)** 可以沿双向遍历的链表。
- **单向列表(forward_list)** 只能沿一个方向遍历的链表。

##### 关联式容器

- **集合(set)** 用以有序地存储 **互异** 元素的容器。其实现是由节点组成的红黑树，每个节点都包含着一个元素，节点之间以某种比较元素大小的谓词进行排列。
- **多重集合(multiset)** 用以有序地存储元素的容器。允许存在相等的元素。
- **映射(map)** 由 `{键，值}` 对组成的集合，以某种比较键大小关系的谓词进行排列。
- **多重映射(multimap)** 由 `{键，值}` 对组成的多重集合，亦即允许键有相等情况的映射。

##### 无序（关联式）容器

- **无序（多重）集合(unordered_set/unordered_multiset)** C++11，与 `set`/`multiset` 的区别在于元素无序，只关心「元素是否存在」，使用哈希实现。
- **无序（多重）映射(unordered_map/unordered_multimap)** C++11，与 `map`/`multimap` 的区别在于键 (key) 无序，只关心 "键与值的对应关系"，使用哈希实现。

##### 容器适配器

容器适配器其实**并不是容器**。它们不具有容器的某些特点（如：有迭代器、有 clear() 函数……）
>「适配器是使一种事物的行为类似于另外一种事物行为的一种机制」，适配器对容器进行包装，使其表现出另外一种行为。

- **栈(stack)** 后进先出 (LIFO) 的容器，默认是对双端队列（deque）的包装。
- **队列(queue)** 先进先出 (FIFO) 的容器，默认是对双端队列（deque）的包装。
- **优先队列(priority_queue)** 元素的次序是**由作用于所存储的值对上的某种谓词决定的**的一种队列，默认是对向量（vector）的包装。

#### 共同点

##### 容器声明

都是 `containerName<typeName,...> name` 的形式，但模板参数（`<>` 内的参数）的个数、形式会根据具体容器而变。

本质原因：STL 就是「标准模板库」，所以容器都是模板类。

**泛型编程是一种编程范式，旨在编写可以适用于多种数据类型的通用代码。**通过泛型编程，我们可以编写一次代码，然后将其应用于不同的数据类型，从而避免重复编写相似的代码
编写与类型无关的通用代码，是代码复用的一种手段。**模板是泛型编程的基础**。
面向对象编程（OOP）和泛型编程都能处理在编写程序时不知类型的情况，不同之处在于：OOP能处理类型在程序运行之前都未知的情况：而在泛型编程中，在编译时就能获知类型了

##### 迭代器

在 STL 中，迭代器（`Iterator`）用来**访问和检查** STL 容器中元素的对象，它的行为模式和*指针*类似，但是它封装了一些有效性检查，并且提供了统一的访问格式。类似的概念在其他很多高级语言中都存在，如 Python 的 `__iter__` 函数，C# 的 `IEnumerator`。

###### 基础使用

其实迭代器本身可以看作一个数据指针。迭代器主要支持两个运算符：自增 `++` 和解引用（单目 `*` 运算符）
其中自增用来**移动迭代器**，解引用可以**获取或修改它指向的元素**。
指向某个 STL 容器 `container` 中元素的迭代器的类型一般为 `container::iterator`

迭代器可以用来遍历容器，例如，下面两个 for 循环的效果是一样的：

~~~C++
vector<int> data(10);

for (int i = 0; i < data.size(); i++)
  cout << data[i] << endl;  // 使用下标访问元素

for (vector<int>::iterator iter = data.begin(); iter != data.end(); iter++)
  cout << *iter << endl;  // 使用迭代器访问元素
// 在C++11后可以使用 auto iter = data.begin() 来简化上述代码
~~~

auto之于算法竞赛
大部分选手都喜欢使用 auto 来代替繁琐的迭代器声明。NOI 系列比赛（包括 CSP J/S）在评测时将使用 C++14，这个版本已经支持了 auto 关键字。

###### 分类

迭代器根据其支持的操作依次分为以下几类：

- **InputIterator（输入迭代器）**：只要求支持拷贝、自增和解引访问。
- **OutputIterator（输出迭代器）**：只要求支持拷贝、自增和解引赋值。
- **ForwardIterator（向前迭代器）**：同时满足 InputIterator 和 OutputIterator 的要求。
- **BidirectionalIterator（双向迭代器）**：在 ForwardIterator 的基础上支持自减（即反向访问）。
- **RandomAccessIterator（随机访问迭代器）**：在 BidirectionalIterator 的基础上支持加减运算和比较运算（即随机访问）。
- **ContiguousIterator（连续迭代器）**：在 RandomAccessIterator 的基础上要求对可解引用的迭代器 `a + n` 满足 `(a + n)` 与 `(std::address_of(*a) + n)` 等价（即连续存储，其中 a 为连续迭代器、n 为整型值）。

（ContiguousIterator 于 C++17 中正式引入。）
（「输入」指的是「可以从迭代器中获取输入」，而「输出」指的是「可以输出到迭代器」。
「输入」和「输出」的施动者是程序的其它部分，而不是迭代器自身。）
（指针满足随机访问迭代器的所有要求，可以当作随机访问迭代器使用。）

迭代器并不互斥——一个「类别」的迭代器是可以包含另一个「类别」的迭代器的。例如，在要求使用向前迭代器的地方，同样可以使用双向迭代器。

###### 相关函数

很多 STL 函数 都使用迭代器作为参数。

- 可以使用 `std::advance(it, n)` 将迭代器 `it` 向后移动 `n` 步；若 `n` 为负数，则对应向前移动。迭代器必须满足双向迭代器，否则行为未定义。
- 可以使用 `std::next(it)` 获得向前迭代器 `it` 的后继（此时迭代器 `it` 不变），`std::next(it, n)` 获得向前迭代器 `it` 的第 `n` 个后继。（C++11）
- 可以使用 `std::prev(it)` 获得双向迭代器 `it` 的前驱（此时迭代器 `it` 不变），`std::prev(it, n)` 获得双向迭代器 `it` 的第 `n` 个前驱。（C++11）

STL 容器 一般支持从一端或两端开始的访问，以及对 const 修饰符 的支持。
例如容器的 `begin()` 函数可以获得指向容器第一个元素的迭代器，`rbegin()` 函数可以获得指向容器最后一个元素的反向迭代器，`cbegin()` 函数可以获得指向容器第一个元素的 const 迭代器，`end()` 函数可以获得指向容器尾端（「尾端」并不是最后一个元素，可以看作是最后一个元素的后继；「尾端」的前驱是容器里的最后一个元素，其本身不指向任何一个元素）的迭代器。

##### 共有函数

- `=`：有赋值运算符以及复制构造函数。
- `begin()`：返回指向开头元素的迭代器。
- `end()`：返回指向末尾的下一个元素的迭代器。end() 不指向某个元素，但它是末尾元素的后继。
- `size()`：返回容器内的元素个数。
- `max_size()`：返回容器**理论上**能存储的最大元素个数。依容器类型和所存储变量的类型而变。
- `empty()`：返回容器是否为空。
- `swap()`：交换两个容器。
- `clear()`：清空容器。
- `==`/`!=`/`<`/`>`/`<=`/`>\=`：按 字典序 比较两个容器的大小。（比较元素大小时 map 的每个元素相当于 set<pair<key, value> >，无序容器不支持 </>/<=/>=。）

### 序列式容器（即顺序容器）

#### vector

`std::vector` 是 STL 提供的 内存连续的、可变长度 的数组（亦称列表）数据结构。能够提供线性复杂度的插入和删除，以及常数复杂度的随机访问。

##### 为何使用vector（OIwiki）

作为 OIer，对程序效率的追求远比对工程级别的稳定性要高得多，而 vector 由于其对内存的动态处理，**时间效率在部分情况下低于静态数组**，并且在 OJ 服务器不一定开全优化的情况下更加糟糕。所以在正常存储数据的时候，通常不选择 vector。下面给出几个 vector 优秀的特性，**在需要用到这些特性的情况下，vector 能给我们带来很大的帮助**。

###### vector 可以动态分配内存

很多时候我们**不能提前开好那么大的空间**（eg：预处理 1~n 中所有数的约数）。尽管我们能知道数据总量在空间允许的级别，但是单份数据还可能非常大，这种时候我们就**需要 vector 来把内存占用量控制在合适的范围内**。vector 还支持**动态扩容**，在内存非常紧张的时候这个特性就能派上用场了。

###### vector 重写了比较运算符及赋值运算符

vector **重载了六个比较运算符**，以**字典序**实现，这使得我们可以**方便地判断两个容器是否相等**（*复杂度与容器大小成线性关系*）。例如可以利用 `vector<char>` 实现字符串比较（当然，还是用 `std::string` 会更快更方便）。另外 vector 也重载了赋值运算符，使得数组拷贝更加方便。

###### vector 便利的初始化

由于 `vector` 重载了 `=` 运算符，所以我们**可以方便地初始化**。此外从 C++11 起 vector 还支持 **列表初始化**，例如 `vector<int> data {1, 2, 3};`

##### vector 之使用方法

以下为常用用法，详细内容 [请参见 C++ 文档](https://zh.cppreference.com/w/cpp/container/vector)。

###### 构造函数

用例参见如下代码：

~~~C++
using namespace std;

// 1. 创建空vector; 常数复杂度
vector<int> v0;
// 1+. 这句代码可以使得向vector中插入前3个元素时，保证常数时间复杂度
v0.reserve(3);
// 2. 创建一个初始空间为3的vector，其元素的默认值是0; 线性复杂度
vector<int> v1(3);
// 3. 创建一个初始空间为3的vector，其元素的默认值是2; 线性复杂度
vector<int> v2(3, 2);
// 4. 创建一个初始空间为3的vector，其元素的默认值是1，
// 并且使用v2的空间配置器; 线性复杂度
vector<int> v3(3, 1, v2.get_allocator());
// 5. 创建一个v2的拷贝vector v4， 其内容元素和v2一样; 线性复杂度
vector<int> v4(v2);
// 6. 创建一个v4的拷贝vector v5，其内容是{v4[1], v4[2]}; 线性复杂度
vector<int> v5(v4.begin() + 1, v4.begin() + 3);
// 7. 移动v2到新创建的vector v6，不发生拷贝; 常数复杂度; 需要 C++11
vector<int> v6(std::move(v2));  // 或者 v6 = std::move(v2);
~~~

~~~C++
// 以下是测试代码，有兴趣的同学可以自己编译运行一下本代码。
cout << "v1 = ";
copy(v1.begin(), v1.end(), ostream_iterator<int>(cout, " "));
cout << endl;
cout << "v2 = ";
copy(v2.begin(), v2.end(), ostream_iterator<int>(cout, " "));
cout << endl;
cout << "v3 = ";
copy(v3.begin(), v3.end(), ostream_iterator<int>(cout, " "));
cout << endl;
cout << "v4 = ";
copy(v4.begin(), v4.end(), ostream_iterator<int>(cout, " "));
cout << endl;
cout << "v5 = ";
copy(v5.begin(), v5.end(), ostream_iterator<int>(cout, " "));
cout << endl;
cout << "v6 = ";
copy(v6.begin(), v6.end(), ostream_iterator<int>(cout, " "));
cout << endl;
~~~

>Kimi: 在C++中，`ostream_iterator` 是一个模板类，用于提供对输出流的迭代访问。`ostream_iterator<int>` 表示一个专门用于输出 `int` 类型数据的迭代器，它将数据输出到 `cout`（标准输出流）。
构造函数 `ostream_iterator<int>(cout, " ")` 表示创建了一个 `int` 类型的输出流迭代器，它将输出的每个整数后面跟一个空格。这里的 `" "` 是一个分隔符，用于在输出多个整数时分隔它们。
例如，如果你有一个整数数组或容器，你可以使用这个迭代器来输出它们：

```cpp
#include <iostream>
#include <iterator>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::ostream_iterator<int> out_it( std::cout, " " );
    std::copy( vec.begin(), vec.end(), out_it );
    return 0;
}
```

>这段代码会输出：`1 2 3 4 5`，每个数字后面都有一个空格。

###### 元素访问

有如下方法
方法|解释
---|---
`at()`          |v.at(pos) 返回容器中下标为 `pos` 的引用。如果数组越界抛出 `std::out_of_range` 类型的异常。
`operator[]`    |`v[pos]` 返回容器中下标为 `pos` 的引用。不执行越界检查。
`front()`       |`v.front()` 返回首元素的引用。
`back()`        |`v.back()` 返回末尾元素的引用。
`data()`        |`v.data()` 返回指向数组第一个元素的指针。

###### vector 迭代器

vector 提供了如下几种 迭代器：

迭代器|解释
---|---
`begin()`/`cbegin()`    |返回指向首元素的迭代器，其中 `*begin = front`。
`end()`/`cend()`        |返回指向数组尾端占位符的迭代器，注意是没有元素的。
`rbegin()`/`crbegin()`  |返回指向逆向数组的首元素的逆向迭代器，可以理解为正向容器的末元素。
`rend()`/`crend()`      |返回指向逆向数组末元素后一位置的迭代器，对应容器首的前一个位置，没有元素。

上述的迭代器中，含有字符 `c` 的为只读迭代器，你不能通过只读迭代器去修改 vector 中的元素的值。如果一个 vector 本身就是只读的，那么它的一般迭代器和只读迭代器完全等价。只读迭代器自 C++11 开始支持。

###### 长度和容量

vector 有以下几个与容器长度和容量相关的函数。注意，vector 的**长度（size）**指**有效元素数量**，而**容量（capacity）**指其**实际分配的内存长度**，相关细节请参见后文的实现细节介绍。

**长度相关：**
函数|解释
---|---
`empty()`       |返回一个 bool 值，即 `v.begin() == v.end()`，true 为空，false 为非空。
`size()`        |返回容器长度（元素数量），即 `std::distance(v.begin(), v.end())`。
`resize()`      |改变 vector 的长度，多退少补。补充元素可以由参数指定。
`max_size()`    |返回容器的最大可能长度。

**容量相关：**
函数|解释
---|---
`reserve()`       |使得 vector 预留一定的内存空间，避免不必要的内存拷贝。
`capacity()`      |返回容器的容量，即不发生拷贝的情况下容器的长度上限。
`shrink_to_fit()` |使得 vector 的容量与长度一致，多退但不会少。

##### 元素增删及修改

操作|含义
---|---
clear()`        |清除所有元素
`insert()`      |支持在某个迭代器位置插入元素、可以插入多个。复杂度与 `pos` 距离末尾长度成线性而非常数的
`erase()`       |删除某个迭代器或者区间的元素，返回最后被删除的迭代器。复杂度与 `insert` 一致。
`push_back()`   |在末尾插入一个元素，均摊复杂度为 常数，最坏为线性复杂度。
`pop_back()`    |删除末尾元素，常数复杂度。
`swap()`        |与另一个容器进行交换，此操作是 常数复杂度 而非线性的。

##### vector 的实现细节

vector 的**底层仍是定长数组**，它能够实现动态扩容的原因是**增加了避免数量溢出**的操作。
首先需要指明的是 vector 中元素的**数量（长度）n** 与它已**分配内存最多能包含元素的数量（容量）N** 是不一致的，vector 会分开存储这两个量。
当向 vector 中添加元素时，如发现 **n>N**，那么容器会分配一个**尺寸为 2N 的**数组，然后将旧数据从原本的位置**拷贝到新的数组中**，再将原来的内存**释放**。尽管这个操作的渐进复杂度是 O(n)，但是可以证明其**均摊复杂度为 O(1)**。
而在末尾删除元素和访问元素则都仍然是 O(1) 的开销。 因此，只要对 vector 的尺寸估计得当并善用 `resize()` 和 `reserve()`，就能使得 vector 的效率与定长数组不会有太大差距。

##### `vector<bool>`

标准库特别提供了对 bool 的 vector **特化**，每个「bool」只占 1 bit，且支持动态增长。但是其 `operator[]` 的返回值的类型不是 `bool&` 而是 `vector<bool>::reference`。因此，使用 `vector<bool>` 使需谨慎，可以考虑使用 `deque<bool>` 或 `vector<char>` 替代。而如果你需要节省空间，请直接使用 `bitset`（见之后）。

#### array(C++11)

`std::array` 是 STL 提供的 **内存连续的、固定长度** 的数组数据结构。其本质是对原生数组的直接封装。

##### 为何用array

array 实际上是 **STL 对数组的封装**。它相比 vector **牺牲了动态扩容的特性**，但是换来了**与原生数组几乎一致的性能**（在开满优化的前提下）。因此能够使用原生数组的地方几乎都可以直接把定长数组都换成 array，而动态分配的数组可以替换为 vector

##### 成员函数

###### 隐藏定义的成员函数

函数|作用
---|---
`operator=`|以来自另一 array 的每个元素重写 array 的对应元素

###### 元素访问

函数|作用
---|---
`at`            |访问指定的元素，同时进行越界检查
`operator[]`    |访问指定的元素，不进行越界检查
`front`         |访问第一个元素
`back`          |访问最后一个元素
`data`          |返回指向内存中数组第一个元素的指针

>`at` 若遇 `pos >= size()` 的情况会抛出 `std::out_of_range`。

###### 容量

函数|作用
---|---
`empty`     |检查容器是否为空
`size`      |返回容纳的元素数
`max_size`  |返回可容纳的最大元素数

##### 操作

函数|作用
---|---
`fill`|以指定值填充容器
`swap`|交换内容

**注意，交换两个 array 是 $\Theta(\text{size})$ 的，而非与常规 STL 容器一样为 $O(1)$。**

##### 非成员函数

函数|作用
---|---
`operator==` 等 |按照字典序比较 array 中的值
`std::get`      |访问 array 的一个元素
`std::swap`     |特化的 `std::swap` 算法

下面是一个 array 的使用示例：

~~~C++
// 1. 创建空array，长度为3; 常数复杂度
std::array<int, 3> v0;
// 2. 用指定常数创建array; 常数复杂度
std::array<int, 3> v1{1, 2, 3};

v0.fill(1);  // 填充数组

// 访问数组
for (int i = 0; i != arr.size(); ++i) cout << arr[i] << " ";
~~~

#### deque

`std::deque` 是 STL 提供的 **双端队列** 数据结构。能够提供线性复杂度的插入和删除，以及常数复杂度的随机访问。

##### deque的使用方法

以下介绍常用用法，详细内容 [请参见 C++](https://zh.cppreference.com/w/cpp/container/deque) 文档。deque 的迭代器函数与 vector 相同，因此不作详细介绍。

###### 构造函数

~~~C++
using namespace std;
// 1. 定义一个int类型的空双端队列 v0
deque<int> v0;
// 2. 定义一个int类型的双端队列 v1，并设置初始大小为10; 线性复杂度
deque<int> v1(10);
// 3. 定义一个int类型的双端队列 v2，并初始化为10个1; 线性复杂度
deque<int> v2(10, 1);
// 4. 复制已有的双端队列 v1; 线性复杂度
deque<int> v3(v1);
// 5. 创建一个v2的拷贝deque v4，其内容是v4[0]至v4[2]; 线性复杂度
deque<int> v4(v2.begin(), v2.begin() + 3);
// 6. 移动v2到新创建的deque v5，不发生拷贝; 常数复杂度; 需要 C++11
deque<int> v5(std::move(v2));
~~~

###### deque之元素访问

与 vector 一致，但无法访问底层内存。其高效的元素访问速度可参考实现细节部分。

函数|作用
---|---
`at()`        |返回容器中指定位置元素的引用，执行越界检查，常数复杂度。
`operator[]`  |返回容器中指定位置元素的引用。不执行越界检查，常数复杂度。
`front()`     |返回首元素的引用。
`back()`      |返回末尾元素的引用。

###### deque之迭代器

与 `vector` 一致。

###### deque之元素增删及修改

与 vector 一致，并额外有向队列头部增加元素的函数。

函数|用法
---|---
`clear()`       |清除所有元素
`insert()`      |支持在某个迭代器位置插入元素、可以插入多个。复杂度与 `pos` 与两端距离较小者成线性。
`erase()`       |删除某个迭代器或者区间的元素，返回最后被删除的迭代器。复杂度与 `insert` 一致。
`push_front()`  |在头部插入一个元素，常数复杂度。
`pop_front()`   |删除头部元素，常数复杂度。
`push_back()`   |在末尾插入一个元素，常数复杂度。
`pop_back()`    |删除末尾元素，常数复杂度。
`swap()`        |与另一个容器进行交换，此操作是 常数复杂度 而非线性的。

##### deque 的实现细节

deque 通常的底层实现是**多个不连续的缓冲区**，而缓冲区中的内存是连续的。而每个缓冲区还会**记录首指针和尾指针**，用来标记**有效数据的区间**。当一个缓冲区填满之后便会在之前或者之后分配新的缓冲区来存储更多的数据。更详细的说明可以参考 [STL 源码剖析——deque 的实现原理和使用方法详解](https://blog.csdn.net/baidu_28312631/article/details/48000123)

#### list

`std::list` 是 `STL` 提供的 **双向链表** 数据结构。能够提供线性复杂度的随机访问，以及常数复杂度的插入和删除。

##### list 之使用方法

`list` 的使用方法与 `deque` 基本相同，但是增删操作和访问的复杂度不同。详细内容 [请参见 C++ 文档](https://zh.cppreference.com/w/cpp/container/list)
list 的迭代器、长度、元素增删及修改相关的函数与 deque 相同，因此不作详细介绍。

###### list 之元素访问

由于 list 的实现是链表，因此它不提供随机访问的接口。若需要访问中间元素，则需要使用迭代器。

- `front()` 返回首元素的引用。
- `back()` 返回末尾元素的引用。

###### list 之操作

list 类型还提供了一些针对其特性实现的 STL 算法函数。由于这些算法需要 随机访问迭代器（RandomAccessIterator），因此 list 提供了特别的实现以便于使用。
这些算法有

函数|作用（kimiAI）
---|---
`splice()`  |`splice()` 用于将一个 list 中的元素或者一段元素移动到另一个 list 中。它有多个重载版本，但最常见的用法是将一个列表的节点移动到另一个列表中指定的位置。
`remove()`  |`remove()` 用于移除列表中所有与给定值相等的元素。
`sort()`    |`sort()` 用于对列表中的元素进行排序。
`unique()`  |`unique()` 用于移除列表中连续重复的元素。
`merge()`   |`merge()` 用于合并两个已排序的列表。

#### forward_list (C++11)

`std::forward_list` 是 STL 提供的 单向链表 数据结构，相比于 `std::list` 减小了空间开销。

##### forward_list 的使用方法

forward_list 的使用方法与 list 几乎一致，但是迭代器只有单向的，因此其具体用法不作详细介绍。详细内容 [请参见 C++ 文档](https://zh.cppreference.com/w/cpp/container/forward_list)

### 关联式容器

#### set

`set` 是关联容器，含有**键值类型对象的已排序集**，搜索、移除和插入拥有对数复杂度。
`set` 内部通常采用 **红黑树** 实现。**平衡二叉树** 的特性使得 `set` 非常适合处理需要同时兼顾查找、插入与删除的情况。
和数学中的集合相似，`set` 中不会出现值相同的元素。
如果需要有相同元素的集合，需要使用 `multiset`。`multiset` 的使用方法与 `set` 的使用方法基本相同。

##### set之插入与删除工作

函数|作用
---|---
`insert(x)`         |当容器中没有等价元素的时候，将元素 `x` 插入到 `set` 中。
`erase(x)`          |删除值为 `x` 的 所有 元素，返回删除元素的个数。
`erase(pos)`        |删除迭代器为 `pos` 的元素，要求迭代器必须合法。
`erase(first,last)` |删除迭代器在 `[first,last)` 范围内的所有元素。
`clear()`           |清空 `set`。

`insert` 函数的返回值类型为 `pair<iterator, bool>`，其中 `iterator` 是一个指向所插入元素（或者是指向等于所插入值的原本就在容器中的元素）的迭代器，而 `bool` 则代表元素是否插入成功，由于 `set` 中的元素具有唯一性质，所以如果在 `set` 中已有等值元素，则插入会失败，返回 `false`，否则插入成功，返回 `true`；
`map` 中的 `insert` 也是如此。

##### 迭代器

迭代器|意义
---|---
`begin()/cbegin()`  |返回**指向首元素**的迭代器，其中 `*begin = front`。
`end()/cend()`      |返回指向**数组尾端占位符**的迭代器，注意是没有元素的。
`rbegin()/crbegin()`|返回指向**逆向数组的首元素**的逆向迭代器，可以理解为**正向容器的末元素**。
`rend()/crend()`    |返回指向**逆向数组末元素后一位置**的迭代器，对应**容器首的前一个位置**，没有元素。

以上列出的迭代器中，含有字符 `c` 的为只读迭代器，你不能通过只读迭代器去修改 set 中的元素的值。
如果一个 set 本身就是只读的，那么它的一般迭代器和只读迭代器完全等价。
只读迭代器自 C++11 开始支持。

##### 查找操作

函数|意义
---|---
`count(x)`        |返回 set 内键为 `x` 的元素**数量**。
`find(x)`         |在 set 内存在**键为 `x` 的元素**时会返回该元素的**迭代器**，否则返回 `end()`。
`lower_bound(x)`  |返回指向**首个不小于给定键**的元素的迭代器。如果不存在这样的元素，返回 `end()`。
`upper_bound(x)`  |返回指向**首个大于给定键**的元素的迭代器。如果不存在这样的元素，返回 `end()`。
`empty()`         |返回容器是否为**空**。
`size()`          |返回容器内**元素个数**。

注意,set是键值对象的**已排序**集,故所谓"首个"即为最小

>`lower_bound` 和 `upper_bound` 的时间复杂度
>
>set 自带的 `lower_bound` 和 `upper_bound` 的时间复杂度为 $O(\log n)$。
但使用 `algorithm` 库中的 `lower_bound` 和 `upper_bound` 函数对 `set` 中的元素进行查询，时间复杂度为 $O(n)$。

>`nth_element` 的时间复杂度
>
>set 没有提供自带的 `nth_element`。使用 `algorithm` 库中的 `nth_element` 查找第 `k` 大的元素时间复杂度为 $O(n)$。
如果需要实现平衡二叉树所具备的 $O(\log n)$ 查找第 `k` 大元素的功能，需要自己手写平衡二叉树或权值线段树，或者选择使用 `pb_ds` 库中的平衡二叉树。


##### 使用案例

###### `set`在贪心中的使用

在贪心算法中经常会需要出现类似 **找出并删除最小的大于等于某个值的元素**。这种操作能轻松地通过 set 来完成。

~~~C++
// 现存可用的元素
set<int> available;
// 需要大于等于的值
int x;

// 查找最小的大于等于x的元素
set<int>::iterator it = available.lower_bound(x); //"点"成员函数运算符
if (it == available.end()) {
  // 不存在这样的元素，则进行相应操作……
} else {
  // 找到了这样的元素，将其从现存可用元素中移除
  available.erase(it);
  // 进行相应操作……
}
~~~

#### map

map 是**有序键值对容器**，它的**元素的键是唯一的**。搜索、移除和插入操作拥有对数复杂度。map 通常实现为 **红黑树**。

设想如下场景：现在需要**存储一些键值对**，例如存储学生姓名对应的分数：`Tom 0`，`Bob 100`，`Alan 100`。
但是由于**数组下标只能为非负整数**，所以无法用姓名作为下标来存储，这个时候最简单的办法就是使用 STL 中的 map。

map 重载了 `operator[]`，可以用任意定义了 `operator <` 的类型作为下标（在 map 中叫做 `key`，也就是索引）：

~~~C++
map<Key, T> yourMap; \\Key 是键的类型，T 是值的类型
~~~

其实例:

~~~C++
map<string, int> mp;
~~~

map 中不会存在键相同的元素，`multimap` 中允许多个元素拥有同一键。`multimap` 的使用方法与 map 的使用方法基本相同。
正是因为 multimap 允许多个元素拥有同一键的特点，multimap 并没有提供给出**键访问其对应值**的方法。

##### map的插入与删除操作

- 可以**直接通过下标**访问来进行查询或插入操作。例如 `mp["Alan"]=100`。
- 通过向 map 中插入一个类型为 `pair<Key, T>` 的值可以达到插入元素的目的，例如 `mp.insert(pair<string,int>("Alan",100));`；
- `erase(key)` 函数会**删除**键为 `key` 的 **所有** 元素。返回值为**删除元素的数量**。
- `erase(pos)`: **删除**迭代器为 `pos` 的元素，要求迭代器必须合法。
- `erase(first,last)`: **删除**迭代器在 `[first,last)` 范围内的所有元素。
- `clear()` 函数会**清空**整个容器。

>在利用下标访问 map 中的某个元素时，如果 map 中不存在相应键的元素，会**自动在 map 中插入一个新元素**，并将其值设置为默认值
（对于整数，值为零；对于有默认构造函数的类型，会调用默认构造函数进行初始化）。
>
>当下标访问操作过于频繁时，容器中会出现大量无意义元素，影响 map 的效率。因此一般情况下推荐使用 `find()` 函数来寻找特定键的元素。

##### 查询操作

函数|作用
---|---
`count(x)`        | 返回容器内键为 `x` 的元素数量。复杂度为 $O(\log(size)+ans)$（关于容器大小对数复杂度，加上匹配个数）。
`find(x)`         | 若容器内存在键为 `x` 的元素，会返回该元素的迭代器；否则返回 `end()`。
`lower_bound(x)`  | 返回指向首个不小于给定键的元素的迭代器。
`upper_bound(x)`  | 返回指向首个大于给定键的元素的迭代器。若容器内所有元素均小于或等于给定键，返回 `end()`。
`empty()`         | 返回容器是否为空。
`size()`          | 返回容器内元素个数。

##### 使用样例

###### map用于储存复杂状态

在搜索中，我们有时需要存储一些**较为复杂的状态**（如*坐标*，*无法离散化的数值*，*字符串*等）以及**与之有关的答案**（如到达此状态的最小步数）。`map` 可以用来实现此功能。其中的键是状态，而值是与之相关的答案。
下面的示例展示了如何使用 map 存储以 `string` 表示的状态。

~~~C++
// 存储状态与对应的答案
map<string, int> record;

// 新搜索到的状态与对应答案
string status;
int ans;
// 查找对应的状态是否出现过
map<string, int>::iterator it = record.find(status);
if (it == record.end()) {
  // 尚未搜索过该状态，将其加入状态记录中
  record[status] = ans;
  // 进行相应操作……
} else {
  // 已经搜索过该状态，进行相应操作……
}
~~~

#### 遍历容器

利用迭代器来遍历关联式容器的所有元素

~~~C++
set<int> s;
typedef set<int>::iterator si;
for (si it = s.begin(); it != s.end(); it++) cout << *it << endl;
~~~

注意:对 `map` 的迭代器解引用后，得到的是类型为 `pair<Key, T>` 的键值对

C++11 中，使用**范围 for 循环**会让代码简洁很多

~~~C++
set<int> s;
for (auto x : s) cout << x << endl;
~~~

对于任意关联式容器，使用迭代器遍历容器的时间复杂度均为 $O(n)$。

#### 自定义比较方式

set 在默认情况下的比较函数为 `<`（如果是**非内置类型**需要 重载 < 运算符）。然而在某些特殊情况下，我们希望能**自定义 set 内部的比较方式**。

这时候可以通过**传入自定义比较器**来解决问题。
具体来说，我们需要定义一个类，并在这个类中 **重载 ()** 运算符。
例如，我们想要维护一个存储整数，且较大值靠前的 set，可以这样实现：

~~~C++
struct cmp {
  bool operator()(int a, int b) { return a > b; }
};

set<int, cmp> s;
~~~

对于其他关联式容器，可以用类似的方式实现自定义比较

### 无序关联式容器

#### 概述

自 C++11 标准起，四种基于 **哈希** 实现的无序关联式容器正式纳入了 C++ 的标准模板库中，分别是：`unordered_set`，`unordered_multiset`，`unordered_map`，`unordered_multimap`。

>无序关联式容器属于 C++ 的 TR1 扩展

它们与相应的关联式容器**在功能，函数等方面有诸多共同点**，而最大的不同点则体现在普通的关联式容器一般采用**红黑树**实现，内部元素**按特定顺序进行排序**；而这几种无序关联式容器则采用**哈希方式**存储元素，内部元素**不以任何特定顺序进行排序**，所以访问无序关联式容器中的元素时，访问顺序也没有任何保证。

采用哈希存储的特点**使得无序关联式容器 在平均情况下 大多数操作**（包括查找，插入，删除）都能在**常数时间复杂度**内完成，相较于关联式容器与容器大小成对数的时间复杂度更加优秀。

无序关联式容器与相应的关联式容器在用途和操作中有很多共同点，这里不再介绍无序关联式容器的各种操作

#### 制造哈希冲突

上文中提到了，在最坏情况下，对**无序关联式容器进行一些操作的时间复杂度会与容器大小成线性关系**。

在**哈希函数确定**的情况下，可以构造出数据使得容器内产生大量哈希冲突，导致复杂度达到上界。
在标准库实现里，每个元素的**散列值**是**将值对一个质数取模**得到的，更具体地说，是 **这个列表** 中的质数（g++ 6 及以前版本的编译器，这个质数一般是 $126271$，g++ 7 及之后版本的编译器，这个质数一般是 $107897$）。
因此可以通过向容器中**插入这些模数的倍数**来达到制造大量哈希冲突的目的。

#### 自定义哈希函数

可以有效避免构造数据产生的大量哈希冲突

需要定义一个结构体，并在结构体中重载 () 运算符，像这样

~~~C++
struct my_hash {
  size_t operator()(int x) const { return x; }
};
~~~

为了确保哈希函数不会被迅速破解（例如 Codeforces 中对使用无序关联式容器的提交进行 hack），可以试着在哈希函数中**加入一些随机化函数**（如时间）来增加破解的难度。

例如，在 [这篇博客](https://codeforces.com/blog/entry/62393) 中给出了如下哈希函数：

~~~C++
struct my_hash {
  static uint64_t splitmix64(uint64_t x) {
    x += 0x9e3779b97f4a7c15;
    x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9;
    x = (x ^ (x >> 27)) * 0x94d049bb133111eb;
    return x ^ (x >> 31);
  }

  size_t operator()(uint64_t x) const {
    static const uint64_t FIXED_RANDOM =
        chrono::steady_clock::now().time_since_epoch().count();
    return splitmix64(x + FIXED_RANDOM);
  }

  // 针对 std::pair<int, int> 作为主键类型的哈希函数
  size_t operator()(pair<uint64_t, uint64_t> x) const {
    static const uint64_t FIXED_RANDOM =
        chrono::steady_clock::now().time_since_epoch().count();
    return splitmix64(x.first + FIXED_RANDOM) ^
           (splitmix64(x.second + FIXED_RANDOM) >> 1);
  }
};
~~~

写完自定义的哈希函数后，就可以通过 `unordered_map<int, int, my_hash> my_map;` 或者 `unordered_map<pair<int, int>, int, my_hash> my_pair_map;` 的定义方式将自定义的哈希函数传入容器了。

### 容器适配器

#### 栈

**STL 栈**(`std::stack`) 是一种**后进先出** (Last In, First Out) 的容器适配器，**仅支持查询或删除最后一个加入的元素（栈顶元素）**，不支持随机访问，且为了保证数据的**严格有序性**，不支持迭代器。

##### stack之头文件

~~~C++
#include <stack>
~~~

##### stack之定义

~~~C++
std::stack<TypeName> s;     // 使用默认底层容器 deque，数据类型为 TypeName
std::stack<TypeName, Container> s;  // 使用 Container 作为底层容器
std::stack<TypeName> s2(s1);        // 将 s1 复制一份用于构造 s2
~~~

##### stack之成员函数

函数|意义
---|---
`top()`     |**访问**栈顶元素（如果栈为空，此处会出错）
`push(x)`   |向栈中**插入**元素 x
`pop()`     |**删除**栈顶元素
`size()`    |查询容器中的**元素数量**
`empty()`   |询问容器**是否为空**

以上成员函数均为常数复杂度

##### stack之简单示例

~~~C++
std::stack<int> s1;
s1.push(2);
s1.push(1);
std::stack<int> s2(s1);
s1.pop();
std::cout << s1.size() << " " << s2.size() << std::endl;  // 1 2
std::cout << s1.top() << " " << s2.top() << std::endl;    // 2 1
s1.pop();
std::cout << s1.empty() << " " << s2.empty() << std::endl;  // 1 0
~~~

#### 队列

**STL 队列**(`std::queue`) 是一种**先进先出** (First In, First Out) 的容器适配器，仅支持**查询或删除第一个加入的元素（队首元素）**，不支持随机访问，且为了保证数据的**严格有序性**，不支持迭代器。

##### queue之头文件

~~~C++
#include <queue>
~~~

##### queue之定义

~~~C++
std::queue<TypeName> q;   // 使用默认底层容器 deque，数据类型为 TypeName
std::queue<TypeName, Container> q;  // 使用 Container 作为底层容器
std::queue<TypeName> q2(q1);  // 将 s1 复制一份用于构造 q2
~~~

##### queue之成员函数

函数|意义
---|---
`front()` |**访问**队首元素（如果队列为空，此处会出错）
`push(x)` |向队列中**插入**元素 `x`
`pop()`   |**删除**队首元素
`size()`  |查询容器中的**元素数量**
`empty()` |询问容器**是否为空**

以上成员函数均为常数复杂度

##### 简单示例

~~~C++
std::queue<int> q1;
q1.push(2);
q1.push(1);
std::queue<int> q2(q1);
q1.pop();
std::cout << q1.size() << " " << q2.size() << std::endl;    // 1 2
std::cout << q1.front() << " " << q2.front() << std::endl;  // 1 2
q1.pop();
std::cout << q1.empty() << " " << q2.empty() << std::endl;  // 1 0
~~~

#### 优先队列

**优先队列** `std::priority_queue` 是一种 **堆**，一般为 **二叉堆**。

##### 优先队列之头文件

~~~C++
#include <queue>
~~~

##### 优先队列之定义

~~~C++
std::priority_queue<TypeName> q;             // 数据类型为 TypeName
std::priority_queue<TypeName, Container> q;  // 使用 Container 作为底层容器
std::priority_queue<TypeName, Container, Compare> q;
// 使用 Container 作为底层容器，使用 Compare 作为比较类型

// 默认使用底层容器 vector
// 比较类型 less<TypeName>（此时为它的 top() 返回为最大值）
// 若希望 top() 返回最小值，可令比较类型为 greater<TypeName>
// 注意：不可跳过 Container 直接传入 Compare

// 从 C++11 开始，如果使用 lambda 函数自定义 Compare
// 则需要将其作为构造函数的参数代入，如：
auto cmp = [](const std::pair<int, int> &l, const std::pair<int, int> &r) {
  return l.second < r.second;
};
std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int> >,
                    decltype(cmp)>
    pq(cmp);
~~~

##### 成员函数

以下所有函数均为**常数复杂度**
函数|作用
---|---
`top()`     |**访问堆顶**元素（此时优先队列不能为空）
`empty()`   |询问容器**是否为空**
`size()`    |查询容器中的**元素数量**

以下所有函数均为**对数复杂度**
函数|作用
---|---
`push(x)` |插入元素，并**对底层容器排序**
`pop()`   |**删除堆顶**元素（此时优先队列不能为空）

##### 简单示例

~~~C++
std::priority_queue<int> q1;
std::priority_queue<int, std::vector<int> > q2;
// C++11 后空格可省略
std::priority_queue<int, std::deque<int>, std::greater<int> > q3;
// q3 为小根堆
for (int i = 1; i <= 5; i++) q1.push(i);
// q1 中元素 :  [1, 2, 3, 4, 5]
std::cout << q1.top() << std::endl;
// 输出结果 : 5
q1.pop();
// 堆中元素 : [1, 2, 3, 4]
std::cout << q1.size() << std::endl;
// 输出结果 ：4
for (int i = 1; i <= 5; i++) q3.push(i);
// q3 中元素 :  [1, 2, 3, 4, 5]
std::cout << q3.top() << std::endl;
// 输出结果 : 1
~~~

## STL算法

STL 提供了大约 100 个**实现算法的模版函数**，基本都包含在 `<algorithm>` 之中，还有一部分包含在 `<numeric>` 和 `<functional>`。完备的函数列表请 [参见参考手册](https://zh.cppreference.com/w/cpp/algorithm)，排序相关的可以参考 [排序内容的对应页面(OIwiki)](https://oi-wiki.org/basic/stl-sort/)。

算法|作用
---|---
`find`                |**顺序查找**。`find(v.begin(), v.end(), value)`，其中 `value` 为需要查找的值。
`reverse`             |**翻转数组、字符串**。`reverse(v.begin(), v.end())` 或 `reverse(a + begin, a + end)`。
`unique`              |**去除容器中相邻的重复元素**。`unique(ForwardIterator first, ForwardIterator last)`，返回值为指向 **去重后 容器结尾的迭代器**，**原容器大小不变**。与 sort 结合使用可以实现完整容器去重。
`random_shuffle`[^3]  |**随机地打乱**数组。`random_shuffle(v.begin(), v.end())` 或 `random_shuffle(v + begin, v + end)`。
`sort`                |**排序**。`sort(v.begin(), v.end(), cmp)` 或 `sort(a + begin, a + end, cmp)`，其中 `end` 是**排序的数组最后一个元素的后一位**，`cmp` 为**自定义的比较函数**。
`stable_sort`         |**稳定排序**，用法同 sort()。
`nth_element`         |按指定范围进行**分类**，即找出序列中**第 n 大的元素**，使其左边均为小于它的数，右边均为大于它的数。`nth_element(v.begin(), v.begin() + mid, v.end(), cmp)` 或 `nth_element(a + begin, a + begin + mid, a + end, cmp)`。
`binary_search`       |**二分查找**。`binary_search(v.begin(), v.end(), value)`，其中 `value` 为需要查找的值。
`merge`               |将两个（已排序的）序列 **有序合并** 到第三个序列的 插入迭代器 上。`merge(v1.begin(), v1.end(), v2.begin(), v2.end() ,back_inserter(v3))`。
`inplace_merge`       |将两个（已按小于运算符**排序的**）：`[first,middle)`, `[middle,last)` 范围 原地合并为一个**有序序列**。inplace_merge(v.begin(), v.begin() + middle, v.end())`。
`lower_bound`         |在一个**有序序列中进行二分查找**，返回指向第一个 **大于等于 x** 的元素的位置的迭代器。如果不存在这样的元素，则返回尾迭代器。`lower_bound(v.begin(),v.end(),x)`。
`upper_bound`[^4]     |在一个**有序序列中进行二分查找**，返回指向第一个 **大于 x** 的元素的位置的迭代器。如果不存在这样的元素，则返回尾迭代器。`upper_bound(v.begin(),v.end(),x)`。
`next_permutation`    |将当前排列更改为 **全排列中的下一个排列**。如果当前排列已经是 全排列中的最后一个排列（元素完全从大到小排列），函数返回 `false` 并将排列更改为 全排列中的第一个排列（元素完全从小到大排列）；否则，函数返回 `true`。`next_permutation(v.begin(), v.end())` 或 `next_permutation(v + begin, v + end)`。
`prev_permutation`    |将当前排列更改为 全排列中的上一个排列。用法同 `next_permutation`。
`partial_sum`         |求**前缀和**。设源容器为 `x`，目标容器为 `y`，则令 `y[i]=x[0]+x[1]+\dots+x[i]`。`partial_sum(src.begin(), src.end(), back_inserter(dst))`。


[^3]: random_shuffle 自 C++14 起被弃用，C++17 起被移除。
在 C++11 以及更新的标准中，您可以使用 shuffle 函数代替原来的 random_shuffle。使用方法为 shuffle(v.begin(), v.end(), rng)（最后一个参数传入的是使用的随机数生成器，一般情况使用以真随机数生成器 random_device 播种的梅森旋转伪随机数生成器 mt19937）。
  `// #include <random>`
  `std::mt19937 rng(std::random_device{}());`
  `std::shuffle(v.begin(), v.end(), rng);`
[^4]: `lower_bound` 和 `upper_bound` 的时间复杂度
在一般的数组里，这两个函数的时间复杂度均为 O(\log n)，但在 set 等关联式容器中，直接调用 lower_bound(s.begin(),s.end(),val) 的时间复杂度是 O(n) 的。
set 等关联式容器中已经封装了 lower_bound 等函数（像 s.lower_bound(val) 这样），这样调用的时间复杂度是 O(\log n) 的。

### 算法使用案例

实现全排列

***

[^1]: [链接](https://blog.csdn.net/baidu_35536188/article/details/122881541)
[^2]: 
