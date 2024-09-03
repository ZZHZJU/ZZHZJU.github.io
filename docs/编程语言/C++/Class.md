# Class
## 类的定义
类是用户定义的数据类型，它由数据成员（变量）和成员函数（方法）组成。在C++中class和struct都可以用于定义类，区别是class默认是私有的，而struct默认是公开的。

每个类定义了唯一类类型，类是按名称等价，而不是按内容。
## 对象的创建
类定义完成后，可以创建类的对象。对象是类的实例，通过对象可以访问类中的数据成员和成员函数。
## 构造函数和析构函数
构造函数是用于初始化对象的特殊函数，构造函数的名称必须与类的名称相同，并且它没有返回类型（甚至没有void）；析构函数则用于清理对象在销毁前的资源，在类名前加一个取反运算符```~```。

构造函数可以有很多个（重载即可），在C++11 标准中，如果我们在定义了构造函数的情况下需要默认行为，那么可以通过在参数列表后写上 = default 来要求编译器生成默认构造函数
## 类的访问控制
C++ 提供了三种访问控制修饰符：public、private 和 protected。
* public: 公共成员可以在类的外部访问。
* private: 私有成员只能在类的内部访问。
* protected: 受保护成员可以在类的内部以及派生类中访问。
## 类的this指针
任何对类成员的直接访问都被看做作this的隐式引用，this是一个总是指向“这个对象”的**常量指针**，任何自定义名为this的参数或者变量都是非法的。注意默认状态下this是指向类类型非常量版本的常量指针，因此不能在一个常量对象上调用普通成员函数
## 友元
在C++中友元是一种特殊的机制，允许一个类或函数访问另一个类的私有和保护成员。通常，类的私有和保护成员只能被该类的成员函数或从该类派生的子类访问。然而，通过使用友元，你可以指定其他类或函数可以直接访问这些成员。友元关系不存在传递性，重载函数需要单独声明友元
## 示例
```cpp
#include <iostream>
using namespace std;

// 定义一个简单的类
class Box {
private:
    double length;   // 长度 - 私有成员
    double breadth;  // 宽度 - 私有成员
    double height;   // 高度 - 私有成员

public:
    // 构造函数
    Box(double l, double b, double h) : length(l), breadth(b), height(h) {
        cout << "Box 被创建" << endl;
    }

    // 重载的默认构造函数
    Box() = default;

    // 计算体积的公共成员函数
    double Volume() const {
        return length * breadth * height;
    }

    // 设置长度的公共成员函数
    void setLength(double l) {
        length = l;
    }

    // 友元函数声明
    friend void printBoxDetails(const Box &box);

    // 析构函数
    ~Box() {
        cout << "Box 被销毁" << endl;
    }
};

// 友元函数的定义
void printBoxDetails(const Box &box) {
    // 友元函数可以访问私有成员
    cout << "Box 的长度: " << box.length << endl;
    cout << "Box 的宽度: " << box.breadth << endl;
    cout << "Box 的高度: " << box.height << endl;
}

int main() {
    // 创建Box的对象
    Box box1(10.0, 5.0, 4.0);  // 使用参数化构造函数

    // 调用公共成员函数
    cout << "Box1 的体积: " << box1.Volume() << endl;

    // 使用友元函数访问私有成员
    printBoxDetails(box1);

    // 创建另一个Box对象
    Box box2;
    box2.setLength(7.0);
    cout << "Box2 的体积: " << box2.Volume() << endl;

    return 0;
}
```