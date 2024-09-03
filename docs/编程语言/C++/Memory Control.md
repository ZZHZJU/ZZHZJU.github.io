# Memory Control
## Memory Distribution
new 表达式是 唯一的用来创建动态生命周期对象的方式（因为 malloc 只是开辟内存，并不创建对象。如果 p 在 new 的时候创建的是数组，则应该用 delete[] p; (array delete expression) 的形式回收，否则是未定义行为。
## nullptr
这是 C++11 引入的一个关键字，用来表示空指针。
为了类型安全，C++ 不允许 void* 隐式转换到其他指针类型。因此，如果我们将 NULL 定义为 (void*) 0，那么 int * p = NULL; 会引发编译错误。但是这种情况下函数重载可能会发生问题。
``` c++
void f(int *);
void f(int);

#define NULL 0
f(NULL);   // ==> f(0) , so f(int) is called
```
为了避免这种问题，C++引入了nullptr，然后为了兼容值为 0 的整型字面量仍然是空指针常量。
## Smart Pointer
在C++中，智能指针是一种用于管理动态分配内存的工具，它们可以自动释放内存，帮助避免内存泄漏和悬空指针等问题。C++标准库提供了几种智能指针，主要包括以下几种：

1. **`std::unique_ptr`**：
   - **特点**：独占式智能指针，确保同一时间只有一个`unique_ptr`拥有所指向的对象。
   - **使用**：通过`std::move`可以转移`unique_ptr`的所有权。
   - **示例**：
     ```cpp
     #include <memory>
     
     int main() {
         std::unique_ptr<int> ptr1 = std::make_unique<int>(10);
         std::unique_ptr<int> ptr2 = std::move(ptr1); // 转移所有权
         // ptr1 现在为空
     }
     ```

2. **`std::shared_ptr`**：
   - **特点**：共享式智能指针，允许多个`shared_ptr`实例共享同一个对象。引用计数机制用于跟踪多少个`shared_ptr`指向相同的对象，当最后一个`shared_ptr`被销毁时，对象也被销毁。
   - **使用**：不需要手动管理引用计数。
   - **示例**：
     ```cpp
     #include <memory>
     
     int main() {
         std::shared_ptr<int> ptr1 = std::make_shared<int>(20);
         std::shared_ptr<int> ptr2 = ptr1; // 共享所有权
         // 引用计数为2
     }
     ```

3. **`std::weak_ptr`**：
   - **特点**：弱引用智能指针，通常与`shared_ptr`一起使用，以防止循环引用造成内存泄漏。它不改变引用计数。
   - **使用**：可以通过`lock()`方法获取一个`shared_ptr`实例。
   - **示例**：
     ```cpp
     #include <memory>
     
     int main() {
         std::shared_ptr<int> sharedPtr = std::make_shared<int>(30);
         std::weak_ptr<int> weakPtr = sharedPtr; // 不增加引用计数
         
         if (auto lockedPtr = weakPtr.lock()) {
             // 使用 lockedPtr
         }
     }
     ```