# Overload
C++中的运算符重载允许你为自定义类型定义或修改运算符的行为。通过运算符重载，你可以让自定义类型（例如类）使用标准运算符（如 `+`, `-`, `*`, `/`）进行操作，使得这些操作对于对象是直观和自然的。

重载的运算符是具有特殊名字的函数：它们的名字由关键字operator和其后要定义的运算符号公共组成，重载运算符应尽量与内置类型保持一致。

### 运算符重载的基本语法

运算符重载是通过定义一个特殊的成员函数或全局函数来实现的。这里是一些常见运算符重载的示例：

#### 1. 成员函数重载

对于大多数运算符，重载的实现可以作为类的成员函数。例如，对于加法运算符 `+`，你可以这样定义：

```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imag;
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // 运算符重载的成员函数
    Complex operator + (const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    void print() const {
        std::cout << real << " + " << imag << "i" << std::endl;
    }
};

int main() {
    Complex c1(1.5, 2.5);
    Complex c2(3.0, 4.0);
    Complex c3 = c1 + c2;  // 使用重载的 + 运算符
    c3.print();            // 输出: 4.5 + 6.5i
    return 0;
}
```

#### 2. 全局函数重载

有些运算符需要定义为全局函数，例如 `<<` 或 `>>` 运算符：

```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imag;
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // 友元函数声明
    friend std::ostream& operator << (std::ostream& out, const Complex& c);
};

// 友元函数定义
std::ostream& operator << (std::ostream& out, const Complex& c) {
    out << c.real << " + " << c.imag << "i";
    return out;
}

int main() {
    Complex c1(1.5, 2.5);
    std::cout << c1 << std::endl;  // 使用重载的 << 运算符
    return 0;
}
```

### 注意事项

1. **对称性**: 有些运算符（如 `==`, `<`, `>`）通常是对称的，你可能需要考虑到这一点。
2. **效率**: 运算符重载应该高效，不应引入不必要的开销。
3. **清晰性**: 运算符的行为应该与其直观的意义相符，以避免困惑。

运算符重载是一种强大的特性，但也要谨慎使用，以保持代码的可读性和一致性。

!!!warning
    一个例外是，++ 和 -- 既可以作为前缀，也可以作为后缀；这如何区分呢？由于其他的单目运算符都是前缀，因此 C++ 规定 Foo::operator++() 和 operator++(Foo) 用来处理前缀的 ++，而后缀的 x++ 会调用 x.operator++(0) 或者 operator++(x, 0)，即作为后缀时，编译器通过让一个额外的参数 0 参与重载解析。