# Interitance
在C++中，继承是一种面向对象编程中的重要特性，它允许一个类（称为子类或派生类）从另一个类（称为基类或父类）获取属性和方法。继承使代码的复用性和扩展性得到了提升，同时也支持了多态性和动态绑定等特性。

### 基本概念
- **基类（Base Class）：** 提供成员变量和方法的类，其他类可以继承它。
- **派生类（Derived Class）：** 从基类继承的类，它继承了基类的成员变量和方法，但也可以有自己的独特成员。
  
### 继承的语法
在C++中，继承是通过使用一个冒号(`:`)和访问控制符（`public`, `protected`, `private`）来实现的。

```cpp
class Base {
public:
    int baseVar;
    void baseMethod() {
        // 基类的方法
    }
};

class Derived : public Base {  // Derived从Base公有继承
public:
    int derivedVar;
    void derivedMethod() {
        // 派生类的方法
    }
};
```

### 继承类型
- **公有继承（Public Inheritance）：** 基类的`public`成员在派生类中仍然是`public`的，`protected`成员在派生类中仍然为`protected`，`private`成员则无法被直接访问。
  
- **保护继承（Protected Inheritance）：** 基类的`public`和`protected`成员在派生类中都变为`protected`，`private`成员仍然无法被直接访问。

- **私有继承（Private Inheritance）：** 基类的`public`和`protected`成员在派生类中都变为`private`，`private`成员无法被直接访问。

### 访问控制
访问控制决定了派生类对象是否可以访问基类中的成员。根据继承类型，基类的成员在派生类中的访问级别会有所不同：

| 继承类型    | 基类的`public`成员 | 基类的`protected`成员 | 基类的`private`成员 |
|-------------|-------------------|-----------------------|---------------------|
| `public`    | `public`           | `protected`           | 不可访问             |
| `protected` | `protected`        | `protected`           | 不可访问             |
| `private`   | `private`          | `private`             | 不可访问             |

### 多继承
C++支持多继承，即一个类可以从多个基类继承：

```cpp
class Derived : public Base1, public Base2 {
    // Derived类继承了Base1和Base2的成员
};
```

但多继承可能引发**菱形继承问题**，这是因为多个基类可能会有同名的成员，导致在派生类中产生二义性。为解决这一问题，C++提供了虚函数。

### 构造函数与析构函数
派生类的构造函数会首先调用基类的构造函数，而析构函数的调用顺序则与构造函数相反。

```cpp
class Derived : public Base {
public:
    Derived() : Base() { // 调用基类的构造函数
        // 派生类的构造函数
    }
    ~Derived() {
        // 派生类的析构函数
    }
};
```

### 继承的优点
- **代码复用：** 子类可以直接使用父类的方法和属性，减少重复代码。
- **扩展性：** 子类可以在继承的基础上添加新的方法和属性。
- **多态性：** 通过基类指针或引用调用子类的方法，实现多态性。

通过继承，C++可以很好地组织代码，简化开发过程，同时也支持创建更为复杂和功能丰富的应用程序。