# 数值算法

## 一元非线性方程的求解

### 二分法

缺陷：
1. 收敛较慢
2. 好的中间近似解可能被丢弃

### 不动点迭代

从几何上理解就是蛛网图，收敛条件是：
1. $g\in [a,b],g(x)\in [a,b]$对所有$x\in [a,b]$成立，那么g在$[a,b]$有一个不动点
2. $g'$存在，且存在$0<k<1$使得$|g'(x)|\leq k$对于$x\in [a,b]$成立

### Newton 迭代法

#### 原理

初始时我们从给定的f(x)和一个近似解$x_0$开始。

假设我们目前的近似解是$x_i$，我们画出f(x)在$x_i$处的切线l，将l与x轴的交点记为$x_{i+1}$，那么这就是一个更优近似解。根据导数的几何意义，有如下关系：$f'(x_i)=\frac{f(x_i)}{x_i-x_{i+1}}$，整理后得到如下递推关系$x_{i+1}=x_i-\frac{f(x_i)}{f'(x)}$。重复这个迭代过程，由于Newton迭代法的收敛是平方级别的，这意味着每次迭代后近似解精确数位会翻倍。

#### 代码示例

``` cpp
#include <iostream>
#include <cmath>
#include <functional>

using namespace std;

// 函数：newt
// 参数：
// x：初始根的猜测值，返回时存储最终的根
// eps：精度要求
// f：待求解方程的原函数
// df：原函数的导函数
// 返回值：
// 返回迭代次数，如果失败则返回-1
// 使用C++的std::function代替函数指针
int newt(double* x, double eps, function<double(double)> f, function<double(double)> df)
{
    int k, inter;
    double y, dy, d, p, x0, x1;
    inter = 500; // 最大迭代次数为500
    k = 0;
    x0 = *x;
    y = f(x0);
    dy = df(x0);
    d = eps + 1.0;

    while (d >= eps && k != inter)
    {
        if (fabs(dy) < 1e-15) // 小于这个临界值就可以认为是等于0了
        {
            cout << "dy == 0 !" << endl;
            return -1;
        }
        x1 = x0 - y / dy;
        y = f(x1);
        dy = df(x1);
        d = fabs(x1 - x0); // 新的近似根相比于旧的的变化幅度，是度量精度的主要依据
        p = fabs(y); // 新的根对应的函数值到零点的距离，也就是残差，是度量精度的次要依据
        if (p > d) // 避免在根变化很小但函数值还未足够接近零的情况下过早停止迭代
            d = p;
        x0 = x1;
        k = k + 1;
    }

    *x = x0;
    return k;
}
```

## 插值

### 概念

插值是一种通过已知的、离散的数据点推算一定范围内的新数据点的方法。插值法常用于函数拟合中。

### Lagrange 插值

#### 原理

由于要构造一个函数f(x)过所有已知点。首先设第$i$个点在$x$轴上的投影为$P'_i(x_i,0)$。考虑构造$n$个函数$f_1(x),f_2(x),...f_n(x)$，使得对于第$i$个函数$f_i(x)$，其图像过$\begin{cases}
    P'_j(x_j,0),(j\neq i)\\P_i(x_i,y_i)
\end{cases}$，则$f(x)=\Sigma_{i=1}^nf_i(x)$。对于每一个$f_i(x)$，显然已经知道它$n-1$个零点的值，根据因式分解的原理，函数可以用一个乘积表示，设$f_i(x)=a\cdot \Pi_{j\neq i}(x-x_j)$，将剩下那一个点代入可得$a=\frac{y_i}{\Pi_{j\neq i}(x_i-x_j)}$，所以$f_i(x)=y_i\cdot \Pi_{j\neq i}\frac{x-x_j}{x_i-x_j}$，求和得到Lagrange插值公式$f(x)=\Sigma_{i=1}^ny_i\cdot \Pi_{j\neq i}\frac{x-x_j}{x_i-x_j}$

#### 代码实现
朴素的实现代码时间复杂度是$O(N^2)$，但如果横坐标是连续整数，可以靠一定技巧做到$O(N)$时间复杂度

### Newton 插值法
#### 原理
Newton插值法是基于高阶差分来插值的方法，优点是支持$O(N)$插入新数据。令$f(x)=\Sigma_{j=0}^na_jn_j(x)$，其中$n_j(x)=\Pi_{i=0}^{j-1}(x-x_i)$称为Newton基

递归定义k阶向前差商(forward divided differences):$[x_i,x_{i+1}\dots,x_{i+k}=\frac{[x_{i+1},x_{i+2},\dots,x_{i+k}]-[x_i,x_{i+1}\dots,x_{i+k-1}]}{x_{i+k}-x_i}]$，向前差商的记号也可以带上一个f

其实所谓的Newton插值法就是用差商去重写Lagrange插值公式，写成$f(x)=\Sigma_{j=0}^n[y_0,\dots y_j]n_j(x)$，若样本是等距的（即$x_i=x_0+ih,i=1,\dots n$），上式可以简化为$f(x)=\Sigma_{j=0}^n\binom{s}{j}j!h^j[y_0,\dots y_j]$
#### 代码实现
朴素的实现代码时间复杂度还是$O（N^2$

### Hermite 插值
### 三次样条插值

## 数值积分
### 概念
不借助牛顿莱布尼茨定理，高效准确地求出一个定积分的近似值
### 

## 高斯消元
### 原理
高斯消元法是求解线性方程组的经典算法，还可以用于行列式的计算，矩阵求逆等。高斯消元法的原理很简单，线性代数一入门就学了，老老实实计算就行了
### 代码实现
下面这段代码其实是优化过的，相比朴素的实现增加了一个选择最大主元的过程以减小误差
``` cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// 使用浮点数类型
typedef double dtype;

void gaussianElimination(vector<vector<dtype>>& A, vector<dtype>& b) {
    int n = A.size();

    // 消元过程
    for (int i = 0; i < n; i++) {
        // 寻找第 i 列的主元
        int maxRow = i;
        for (int k = i + 1; k < n; k++) {
            if (fabs(A[k][i]) > fabs(A[maxRow][i])) {
                maxRow = k;
            }
        }

        // 交换当前行和主元行
        swap(A[i], A[maxRow]);
        swap(b[i], b[maxRow]);

        // 消去当前列以下的元素
        for (int k = i + 1; k < n; k++) {
            dtype factor = A[k][i] / A[i][i];
            for (int j = i; j < n; j++) {
                A[k][j] -= factor * A[i][j];
            }
            b[k] -= factor * b[i];
        }
    }

    // 回代过程
    vector<dtype> x(n);
    for (int i = n - 1; i >= 0; i--) {
        x[i] = b[i] / A[i][i];
        for (int j = i - 1; j >= 0; j--) {
            b[j] -= A[j][i] * x[i];
        }
    }

    // 输出解向量
    cout << "Solution: ";
    for (int i = 0; i < n; i++) {
        cout << x[i] << " ";
    }
    cout << endl;
}

int main() {
    int n;
    cout << "Enter the number of variables: ";
    cin >> n;

    vector<vector<dtype>> A(n, vector<dtype>(n));
    vector<dtype> b(n);

    cout << "Enter the coefficient matrix A:" << endl;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> A[i][j];
        }
    }

    cout << "Enter the constant vector b:" << endl;
    for (int i = 0; i < n; i++) {
        cin >> b[i];
    }

    gaussianElimination(A, b);

    return 0;
}
```