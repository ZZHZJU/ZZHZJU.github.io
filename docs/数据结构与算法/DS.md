# 高级数据结构
## Tree
对于一颗普通的二叉树，对其节点的操作代价为$O(\log n)$，但是在最坏的情况下，二叉树会退化为一个链表，这是我们最不希望看到的，所以我们需要一些手段去控制树的高度。
### AVL Tree
* 一颗空的二叉树是一个AVL树
* 如果一个二叉树是一个AVL树，则其左右孩子树$T_l$和$T_r$，也都应该是AVL树，且有$|h(T_l)-h(T_r)\leq 1|$。这里我们引入一个平衡因子(Balance Factor,BF)的概念，定义$BF(T_p)=h(T_l)-h(T_r)$。不难证明(由线性递推求出通项)AVL Tree的高度为$O(\log n)$。
* 如何维护一颗AVL Tree呢？需要用到左旋和右旋。一共分为四种情况：
  * 左子树高度比右子树大2：
    * 左子树的左子树比其右子树高：RR
    * 左子树的右子树比其左子树高：LR
  * 反过来是完全对称的
### Splay Tree
* Splay Tree 的核心思想是把目标点旋转到根部，达到任意M次连续的操作时间复杂度为$O(m\log n)$
### Red Black Tree
### B+ Tree
## Heap
### Leftist Heap
### Skew Heap
### Binomial Heap