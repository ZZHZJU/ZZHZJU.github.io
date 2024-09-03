# Exception
## try 语句块和异常处理
* throw 表达式
``` c++
if(item1.isbn()!=item2.isbn())
    throw runtime_error("Data must refer to same ISBN");
//runtime_error 是标准错误类型的一种，继承自 exception
cout << item1 + item2 << endl;
```
* try 语句模块
``` c++
while(cin >> item1 >> item2)
{
    try
    {
        //上面的throw 表达式
    }
    catch(runtime_error err)
    {
        cout << err.what()
             << "\nTry Again? Enter y or n" << endl;
        char c;
        cin >> c;
        if(!cin || c == 'n)
        {
        break;
        }
    }
}
```
## 调试帮助
* assert 预处理宏
``` C++
assert (expr); 
// 用于检查“不能发生的条件”
//宏是由预处理器管理，所以不需要声明命名空间
```
## 错误处理
C++ 的错误处理主要有两种方式：通过返回值处理错误和通过异常处理错误。

### 1. 返回值处理错误
这种方式在C语言中非常常见。函数通过返回一个特定的值来表示错误，调用者需要检查这个返回值并采取相应的措施。

```cpp
int divide(int a, int b) {
    if (b == 0) {
        return -1;  // 错误：除数为0
    }
    return a / b;
}

int main() {
    int result = divide(10, 0);
    if (result == -1) {
        std::cerr << "Error: Division by zero!" << std::endl;
    }
}
```

优点：
- 简单直接，特别是对于小型程序。

缺点：
- 容易忽略错误检查，导致潜在的bug。
- 难以处理复杂的错误信息。

### 2. 异常处理
C++ 提供了异常处理机制，可以捕获和处理运行时发生的异常。

```cpp
int divide(int a, int b) {
    if (b == 0) {
        throw std::runtime_error("Division by zero");
    }
    return a / b;
}

int main() {
    try {
        int result = divide(10, 0);
    } catch (const std::runtime_error& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }
}
```

优点：
- 代码更清晰，错误处理与主逻辑分离。
- 可以捕获并处理复杂的错误信息。

缺点：
- 异常处理有一定的性能开销。
- 过度使用异常可能导致代码复杂度增加。

## 自定义异常函数
类型excption仅仅定义了拷贝构造函数、拷贝赋值运算符、一个虚析构函数和一个名为what的虚成员。其中what函数返回一个const char* 类型的指针，并且确保不会发生任何异常。你当然在它的基础上继承出自己的异常类型。