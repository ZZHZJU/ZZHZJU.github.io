# Random Number
C的随机数是伪随机数，而且不方便调整范围、精度、分布等参数，C++提供了提供了更好的随机数库,在 C++ 中，可以使用标准库中的 <random> 头文件来生成随机数。
## 示例
``` C++
#include <iostream>
#include <random>

int main() {
    // 1. 创建随机数引擎（Mersenne Twister 引擎）
    std::random_device rd; // 用于生成种子
    std::mt19937 gen(rd());

    // 2. 定义分布范围
    std::uniform_int_distribution<> distrib_int(1, 100);   // 生成1到100之间的整数
    std::uniform_real_distribution<> distrib_real(0.0, 1.0); // 生成0到1之间的浮点数

    // 3. 生成随机数
    int random_int = distrib_int(gen);
    double random_real = distrib_real(gen);

    std::cout << "随机整数: " << random_int << std::endl;
    std::cout << "随机浮点数: " << random_real << std::endl;

    return 0;
}
```