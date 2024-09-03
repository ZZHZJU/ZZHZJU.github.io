# Copy
## 1. 拷贝构造函数（Copy Constructor）

### 定义
拷贝构造函数是用于初始化一个新对象为现有对象的拷贝。其函数签名为：

```cpp
ClassName(const ClassName &other);
```

其中，`ClassName`是类名，`other`是需要拷贝的对象的引用。

### 用途
- 创建对象时通过另一个对象进行初始化。
- 通常在以下情况下被调用：
  - 使用拷贝初始化（`ClassName obj2 = obj1;`）
  - 通过对象传递到函数（按值传递）
  - 从函数返回对象（按值返回）

### 示例
```cpp
class MyClass {
public:
    int data;
    
    // 默认构造函数
    MyClass(int value) : data(value) {}

    // 拷贝构造函数
    MyClass(const MyClass &other) : data(other.data) {
        std::cout << "Copy constructor called" << std::endl;
    }
};
```

## 2. 拷贝赋值操作符（Copy Assignment Operator）

### 定义
拷贝赋值操作符用于将一个对象的值赋给另一个已经存在的对象。其函数签名为：

```cpp
ClassName& operator=(const ClassName &other);
```

其中，`ClassName`是类名，`other`是需要拷贝的对象的引用。

### 用途
- 赋值已有对象（`obj1 = obj2;`）
- 确保自我赋值时正确处理资源释放

### 示例
```cpp
class MyClass {
public:
    int data;
    
    // 默认构造函数
    MyClass(int value) : data(value) {}

    // 拷贝赋值操作符
    MyClass& operator=(const MyClass &other) {
        if (this == &other) {
            return *this; // 处理自我赋值
        }
        data = other.data;
        return *this;
    }
};
```

## 3. 拷贝语义（Copy Semantics）

### 浅拷贝（Shallow Copy）
浅拷贝只复制对象的非动态资源（例如基本数据类型），它会拷贝对象中数据的直接副本，而不会处理动态分配的内存。这可能导致多个对象共享相同的资源，如果一个对象修改了资源，其他对象也会受到影响。

### 深拷贝（Deep Copy）
深拷贝会复制对象中所有资源，包括动态分配的内存。每个对象都有自己独立的资源副本，不会相互影响。深拷贝通常需要实现自定义的拷贝构造函数和拷贝赋值操作符。

### 示例
```cpp
#include <iostream>

class MyClass {
public:
    int* data;

    // 构造函数
    MyClass(int value) {
        data = new int(value);
    }

    // 拷贝构造函数（深拷贝）
    MyClass(const MyClass &other) {
        data = new int(*other.data);
    }

    // 拷贝赋值操作符（深拷贝）
    MyClass& operator=(const MyClass &other) {
        if (this == &other) {
            return *this;
        }
        delete data; // 释放旧资源
        data = new int(*other.data);
        return *this;
    }

    // 析构函数
    ~MyClass() {
        delete data;
    }

    void print() const {
        std::cout << *data << std::endl;
    }
};

int main() {
    MyClass obj1(10);
    MyClass obj2 = obj1; // 调用拷贝构造函数
    MyClass obj3(20);
    obj3 = obj1; // 调用拷贝赋值操作符

    obj1.print(); // 输出 10
    obj2.print(); // 输出 10
    obj3.print(); // 输出 10

    return 0;
}
```

## 4. 自我赋值检查

在拷贝赋值操作符中，通常会检查自我赋值（`if (this == &other)`），这是为了避免释放自身资源后再分配新资源，导致程序出错。确保在执行资源分配之前，旧的资源已经被适当释放。

## 移动构造函数（Move Constructor）

**定义：** 移动构造函数用于将一个对象的资源（如动态分配的内存）从一个对象转移到另一个对象。它通常用于在对象初始化时避免不必要的复制操作，从而提高效率。

**语法：**
```cpp
ClassName(ClassName&& other) noexcept;
```

**示例：**
```cpp
class MyClass {
public:
    MyClass() : data(new int[10]) {}
    
    // 移动构造函数
    MyClass(MyClass&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }
    
    ~MyClass() {
        delete[] data;
    }
    
private:
    int* data;
};
```
在这个例子中，`MyClass` 类的移动构造函数将 `other` 对象的 `data` 指针转移到新对象中，并将 `other` 的 `data` 指针设为 `nullptr`，以防止在 `other` 对象的析构函数中删除同样的内存。

## 移动赋值运算符（Move Assignment Operator）

**定义：** 移动赋值运算符用于将一个对象的资源转移到当前对象中。与移动构造函数类似，它也用于避免不必要的复制操作，并释放当前对象持有的资源。

**语法：**
```cpp
ClassName& operator=(ClassName&& other) noexcept;
// noexcept 表示不会抛出异常
```

**示例：**
```cpp
class MyClass {
public:
    MyClass() : data(new int[10]) {}
    
    // 移动赋值运算符
    MyClass& operator=(MyClass&& other) noexcept {
        if (this != &other) { // 自赋值检查
            delete[] data; // 释放当前对象的资源
            data = other.data; // 转移资源
            other.data = nullptr; // 使其他对象失效
        }
        return *this;
    }
    
    ~MyClass() {
        delete[] data;
    }
    
private:
    int* data;
};
```
在这个例子中，`MyClass` 类的移动赋值运算符首先检查是否为自赋值，然后释放当前对象的资源，最后将 `other` 对象的 `data` 指针转移到当前对象中，并将 `other` 的 `data` 指针设为 `nullptr`。

## 移动语义的优势

1. **性能优化：** 移动构造和移动赋值避免了不必要的深拷贝操作，减少了资源的分配和释放次数，通常比复制操作更高效。
2. **资源管理：** 移动操作使得资源管理更加明确，减少了可能出现的内存泄漏和重复释放问题。

### 注意事项

- **资源管理：** 移动操作应该确保资源的正确转移，并处理自赋值的情况。
- **异常安全：** 移动构造函数和移动赋值运算符应尽可能地提供强异常保证（例如使用 `noexcept`），以保证在发生异常时资源的正确管理。