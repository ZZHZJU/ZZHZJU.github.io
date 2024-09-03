# Template
C++模板是C++编程语言中的一种强大工具，允许你编写与类型无关的代码。模板分为两种主要类型：函数模板和类模板。

编写泛型代码的两个重要原则：
* 模版中的函数参数是const引用：保证函数可以用于不能拷贝的类型
* 函数体中的条件判断仅使用 < 比较：降低函数对处理类型的要求，只需要支持<，不一定要支持>

## 1. 函数模板

函数模板允许你创建一个函数模板，这个模板可以处理多种数据类型。其基本形式如下：

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```

使用时，你可以传递不同类型的参数：

```cpp
int main() {
    cout << max(10, 5) << endl;        // int 类型
    cout << max(10.5, 5.5) << endl;    // double 类型
    return 0;
}
```

## 2. 类模板

类模板允许你创建一个类模板，该模板可以处理不同的数据类型。基本形式如下：

```cpp
template <typename T>
class Stack {
private:
    std::vector<T> elements;
public:
    void push(const T& element) {
        elements.push_back(element);
    }
    T pop() {
        if (elements.empty()) throw std::out_of_range("Stack<>::pop(): empty stack");
        T elem = elements.back();
        elements.pop_back();
        return elem;
    }
    bool empty() const {
        return elements.empty();
    }
};
```

使用时，你可以指定模板参数：

```cpp
int main() {
    Stack<int> intStack;
    intStack.push(1);
    intStack.push(2);
    cout << intStack.pop() << endl;

    Stack<std::string> stringStack;
    stringStack.push("hello");
    stringStack.push("world");
    cout << stringStack.pop() << endl;

    return 0;
}
```

### 3. 模板的特化

有时你可能需要对模板的特定类型进行特化，以便提供专门的实现。例如，特化`Stack`类模板以处理`bool`类型：

```cpp
template <>
class Stack<bool> {
private:
    std::vector<bool> elements;
public:
    void push(bool element) {
        elements.push_back(element);
    }
    bool pop() {
        if (elements.empty()) throw std::out_of_range("Stack<bool>::pop(): empty stack");
        bool elem = elements.back();
        elements.pop_back();
        return elem;
    }
    bool empty() const {
        return elements.empty();
    }
};
```