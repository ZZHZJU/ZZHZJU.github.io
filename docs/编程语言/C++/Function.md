# Function

在C++中，函数是执行特定任务的代码块。函数可以接收输入、处理数据，并返回结果。

## 基本结构

```cpp
返回类型 函数名(参数列表) {
    // 函数体
    // 执行一些操作
    return 返回值; // 如果返回类型为void，则不需要返回值
}
```

## 带默认参数的函数
默认参数必须放在最后
```cpp
#include <iostream>
using namespace std;

// 定义一个带默认参数的函数
int multiply(int a, int b = 2) {
    return a * b;
}

int main() {
    cout << multiply(5) << endl;   // 使用默认参数 b=2，输出: 10
    cout << multiply(5, 3) << endl; // 输出: 15
    return 0;
}
```
## 函数重载

C++允许函数重载，即同名但参数不同的函数：

```cpp
#include <iostream>
using namespace std;

// 定义两个重载的函数
int sum(int a, int b) {
    return a + b;
}

double sum(double a, double b) {
    return a + b;
}

int main() {
    cout << sum(5, 3) << endl;       // 调用 int 版本，输出: 8
    cout << sum(5.5, 3.3) << endl;   // 调用 double 版本，输出: 8.8
    return 0;
}
```
## 变长参数
### std::initializer_list
std::initializer_list 允许你传递一个参数列表，但所有参数必须是同一类型。示例如下：
``` cpp
#include <iostream>
#include <initializer_list>

using namespace std;

void printValues(const initializer_list<int>& values) {
    for (int value : values) {
        cout << value << " ";
    }
    cout << endl;
}

int main() {
    printValues({1, 2, 3, 4, 5});
    return 0;
}
```
### 使用变长参数模板（Variadic Templates）
变长参数模板允许你创建一个函数，可以接受任意数量的参数。
``` cpp
#include <iostream>

using namespace std;

// 基础模板函数
template<typename T>
void print(T value) {
    cout << value << " ";
}

// 递归模板函数，接受多个参数
template<typename T, typename... Args>
void print(T first, Args... rest) {
    cout << first << " ";
    print(rest...);
}

int main() {
    print(1, 2.5, "Hello", 'a', 42);
    return 0;
}
```