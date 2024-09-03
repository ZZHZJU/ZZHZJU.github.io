# Container
## Sequence Containers
### 概述
|Name       |Function|
|:----------:|:----------:|
|vector|可变大小的数组|
|deque|双端队列|
|list|双向链表|
|forward_list|单向链表|
|array|固定大小数组|
|string|字符串|

除了固定大小的数组，其它容器都提供高效、灵活的内存管理。没有特殊考虑一般情况选vector。容器的元素类型可以是另一种容器。

### Iterator
``` C++
auto begin = con.begin();
auto end = con.end();
while(begin != end)
{
    *begin = val;
    ++begin;
}
```
迭代器有多个版本：
* begin 正向迭代器
* rbegin 反向迭代器
* cbegin const迭代器
* crbegin const反向迭代器

## Generic Algorithm
泛型算法永远不会执行容器操作，它们只会运行于迭代器上，执行迭代器的操作
### 只读算法
``` C++
find(begin,end,val);
find_if(begin,end,predict);
// 返回第一个使谓词返回0的元素，没有则返回尾迭代器
accumulate(begin,end,0);
// The last parament determin the oringinal value
equal(begin1,end1,begin2);
// Assume that the second container is at least of the same length of the first one 
```
### 写容器的算法
``` C++
fill(begin,end,val);
// Like memset in C, but it is safer
fill_n(begin,size,value);
// make sure not visit the incorrect subscript
```
* 插入迭代器 back_inserter，可以向容器中插入元素
``` C++
copy(begin(a1),end(a1),a2);
// return iterator of the aimmed position
replace(begin,end,origin value,goal value);
replace_copy(begin,end,back_inserter(v),val1,val2)
// Compared with the above function, this one has a new parament determin where to contain the copy
```
### 重排元素的算法
``` C++
sort(begin,end);
//sort函数可以重载，增添predicate来指定
unique(begin,end);
// unique 会返回一个指向最后一个不重复元素后面的指针，所以还需要把后面的内容erase了才算彻底删除
```
### lambda 表达式
C++ 中的 lambda 表达式是匿名函数的一种，用于创建内联的、可以在函数内部使用的小函数。它们使代码更加简洁，特别是在需要短小的函数对象时。

#### 基本语法

```cpp
[capture](parameters) -> return_type {
    // function body
}
```

- **capture**：捕获列表，指定 lambda 函数如何捕获外部变量。可以使用 `[]` 表示不捕获，`[&]` 表示按引用捕获，`[=]` 表示按值捕获。
- **parameters**：参数列表，类似于普通函数的参数列表。如果没有参数，可以省略。
- **return_type**：返回类型，可以省略，由编译器自动推导。
- **function body**：函数体，lambda 表达式的具体实现。

#### 示例

##### 1. 基本用法

```cpp
#include <iostream>

int main() {
    // 无参数，无返回值
    auto printHello = []() {
        std::cout << "Hello, World!" << std::endl;
    };
    printHello();

    // 带参数，返回值为 int
    auto add = [](int a, int b) -> int {
        return a + b;
    };
    std::cout << add(2, 3) << std::endl;

    return 0;
}
```

##### 2. 捕获外部变量

```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // 按值捕获 x 和 y
    auto sum = [x, y]() {
        return x + y;
    };
    std::cout << "Sum: " << sum() << std::endl;

    // 按引用捕获 x
    auto increment = [&x]() {
        x++;
    };
    increment();
    std::cout << "Incremented x: " << x << std::endl;

    return 0;
}
```

##### 3. 捕获所有变量（按值或按引用）

```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // 捕获所有变量（按值）
    auto sum = [=]() {
        return x + y;
    };
    std::cout << "Sum: " << sum() << std::endl;

    // 捕获所有变量（按引用）
    auto printVars = [&]() {
        std::cout << "x: " << x << ", y: " << y << std::endl;
    };
    printVars();

    return 0;
}
```

#### 注意事项

- 如果 lambda 表达式需要修改捕获的变量，可以使用按引用捕获（`[&]`），否则使用按值捕获（`[=]`）可以确保外部变量不会被改变。
- 捕获列表可以同时使用按值和按引用捕获，例如 `[=, &x]` 表示按值捕获所有变量，但按引用捕获 `x`。

希望这些示例能帮你更好地理解和使用 C++ 中的 lambda 表达式！如果有其他问题或者需要更详细的解释，请告诉我。

## Associative Container
### Map & Set
|Name       |Function|
|:----------:|:----------:|
|按关键字有序保存元素|
|map|关联数组：保存关键字-值对|
|set|关键字即值，即只保存关键字的容器|
|multimap|关键字可重复出现的map|
|multiset|关键字可重复出现的set|
|无序集合|
|unordered_map|用哈希函数组织的map|
|unordered_set|用哈希函数组织的set|
|unordered_multiamp|哈希函数组织的map；关键字可重复出现|
unordered_multiset|哈希函数组织的set;关键字可以重复出现|

!!!note
    在实际编程中如果一个类型定义了“行为正常”的```<```运算符，则它可以用作关键字类型

### Pair
定义在头文件utility中
与其他标准库的类型不同，pair的数据成员是public的，所以可以直接
``` C++
p.first;
p.second;
```
### 关联容器迭代器
当解引用一个关联容器迭代器时，我们会得到一个类型为容器的value_type的值引用。
当使用一个迭代器遍历关联容器时，迭代器按关键字升序排列元素