# Polymorphism
## 例子
C++中的多态是面向对象编程的一个重要特性，它允许程序在运行时决定调用哪个函数或方法。多态的实现依赖于类的继承和虚函数，主要包括以下几种形式：

1. **静态多态（编译时多态）**：
   - **函数重载**：同一个作用域内可以有多个同名但参数不同的函数。编译器根据函数的参数类型和数量来选择调用哪个函数。
   - **运算符重载**：可以重新定义运算符的行为，使其适应自定义的类。

2. **动态多态（运行时多态）**：
   - **虚函数**：通过基类指针或引用调用虚函数时，程序会在运行时确定实际调用的函数。为了实现动态多态，基类中的函数需要声明为`virtual`，但实际当中不一定要显示地写出来。
   - **纯虚函数和抽象类**：当一个类中包含一个或多个纯虚函数（`= 0`）时，该类称为抽象类，不能被实例化，只能作为基类使用。

下面是一个简单的示例来演示动态多态的使用：

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() { // 虚函数
        cout << "Base class show function" << endl;
    }
    virtual ~Base() {} // 虚析构函数
};

class Derived : public Base {
public:
    void show() override { // 重写基类的虚函数,override保证一定覆盖
        cout << "Derived class show function" << endl;
    }
};

int main() {
    Base* ptr; // 基类指针
    Derived obj; // 派生类对象
    ptr = &obj;

    ptr->show(); // 调用Derived类的show函数

    return 0;
}
```

在这个例子中，`show`函数在基类中被声明为虚函数，因此即使通过基类指针调用该函数，程序也会在运行时选择调用派生类的`show`函数，这就是动态多态的体现。

## 虚函数
在C++中，虚函数是面向对象编程中实现多态的一种机制。虚函数允许在派生类中重写（覆盖）基类中的函数行为。使用虚函数时，基于对象的实际类型，而不是对象的类型声明，来决定调用哪个函数，这种机制称为动态绑定或晚绑定。

### 虚函数的基本概念
- **虚函数：** 通过在基类中声明函数前加`virtual`关键字来定义。派生类可以重写这些函数来实现特定的功能。
- **多态：** 通过基类的指针或引用来调用虚函数，运行时根据对象的实际类型来决定调用哪个版本的函数，实现多态。

### 语法
在基类中，将函数声明为虚函数：
一个虚函数在派生类里也是隐式的虚函数，无需反复声明。C++11 提供了override关键字来说明派生类中的虚函数：如果使用override标记了某个函数，但是该函数没有覆盖已存在的虚函数则会报错。C++11新标准还提供了一种防止继承发生的方法，即在类名后面跟一个关键字final
```cpp
class Base {
public:
    virtual void show() {
        std::cout << "Base class show function called." << std::endl;
    }
    virtual ~Base() {  // 虚析构函数确保派生类对象的正确析构
        std::cout << "Base class destructor." << std::endl;
    }
};
```

在派生类中重写虚函数：

```cpp
class Derived : public Base {
public:
    void show() override {  // 使用override关键字是C++11标准的良好实践
        std::cout << "Derived class show function called." << std::endl;
    }
    ~Derived() {
        std::cout << "Derived class destructor." << std::endl;
    }
};
```

### 动态绑定
只有通过基类的指针或引用调用虚函数时，才会发生动态绑定。如果直接通过对象调用，就不会使用动态绑定。

```cpp
Base* b = new Derived();
b->show();  // 调用Derived类的show函数

Base b2;
b2.show();  // 调用Base类的show函数
```

### 虚析构函数
如果一个类被设计为基类并且具有虚函数，那么它的析构函数也应该是虚的。这确保了通过基类指针删除派生类对象时，可以调用正确的析构函数，从而避免资源泄漏。

### 纯虚函数和抽象类
在C++中，纯虚函数是一种特殊的虚函数，它在基类中没有实现，必须在派生类中实现。声明纯虚函数的类称为抽象类，不能实例化这样的类。

```cpp
class AbstractBase {
public:
    virtual void pureVirtualFunction() = 0;  // 纯虚函数
};

class ConcreteClass : public AbstractBase {
public:
    void pureVirtualFunction() override {
        std::cout << "Implemented pureVirtualFunction." << std::endl;
    }
};
```

使用虚函数和纯虚函数，C++程序员可以设计出灵活、可扩展的系统，这些系统能够处理不同类型的数据和行为，而不需要依赖于函数的静态绑定。这是实现高级抽象和设计模式的关键技术之一。