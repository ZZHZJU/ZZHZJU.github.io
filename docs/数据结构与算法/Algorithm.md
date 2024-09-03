# 常见算法
!!!abstract
    算法是一种很宽泛的东西，感觉结合实际问题去理解比较好
## BackTracking
这是一种很基础的算法，本质上是走不通就回头，在DFS和BFS常用。基本思路是遍历所有的可能情况，在验证过程中要注意合理地剪枝(pruning)。
## Divide and Conquer
分治法基本思想是将一个问题分解为若干个较小的子问题，然后递归解决这些问题，最后把这些子问题的解合并得到原问题的解。
### 一些最基本的例子：
都是fds里面学过的：
* 最大子序列和
* 树的遍历
* 归并排序和快速排序
## Dynamic Programming
## Introduction
动态规划（Dynamic Programming, DP）常用于解决具有重叠子问题和最优子结构性质的问题。动态规划通过将问题分解为更小的子问题，逐步构建解决方案，避免了重复计算子问题的结果，从而提高了算法的效率。简而言之就是消耗空间存储已计算出的结果，避免重复运算从而节约时间。
## Examples
### Longest Common Substring(LCS)

## Greedy
每个阶段都选当前最优，从而希望得到全局最优，易于实现，但是未必能得到想要的结果，一个经典的例题是排课表。
## NP Completeness
根据问题的难度，由不同的定义划分，问题可以分为：
P问题(polynomial time)，NP问题(nondeterministic polynomial time)，NPC问题(NP completence)，NPH问题(NP hard)。除此以外还有不可计算问题(undecidable)
### P
多项式时间内可解决的问题
### NP
多项式时间内可以验证的问题
### NPC
NP完全是NP中最难的决定性问题