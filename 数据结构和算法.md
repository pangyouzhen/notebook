# 数据结构与算法的作用
[数据结构与算法的作用](https://www.zhihu.com/question/29587605)

# 绪论

## 数据结构和数据存储结构

数据结构

- 集合：无
- 线性：一对一
- 树：一对多
- 图：多对多

数据存储结构

- 顺序
- 链式
- 索引
- 散列

## 时间复杂度

常用的时间复杂度
$$
O(1)<O(log_2{n})<O(n)<O(nlog_2{n})<O(n^2)<O(n^3)<O(2^n)
$$


# 线性表

# 栈与队列

## 栈(LIFO)

问题:

- ​	n个元素进栈，一共有多少中出栈顺序，并用python实现
- ​

## 队列(FIFO)

# 二叉树(Binary tree)及其应用

## 定义及性质

### 定义

- 完全二叉树：

- Huffman树：

- 堆：堆可以视为一棵树的数组对象。所以二叉堆(binary heap) 实为完全二叉树或者是近似完全二叉树，当父节点的键值总是大于或者等于子节点的键值时为最大堆，反之为最小堆。

- 二叉查找树(Binary Search tree,BST): 左节点均小于根节点，右节点大于根节点，每个左右子树均为二叉查找树。问题：如何利用python构建BST？

  ```python
  class Node:
      def __init__(self, val):
          self.l_child = None
          self.r_child = None
          self.data = val

  def binary_insert(root, node):
      if root is None:
          root = node
      else:
          if root.data > node.data:
              if root.l_child is None:
                  root.l_child = node
              else:
                  binary_insert(root.l_child, node)
          else:
              if root.r_child is None:
                  root.r_child = node
              else:
                  binary_insert(root.r_child, node)

  def in_order_print(root):
      if not root:
          return
      in_order_print(root.l_child)
      print root.data
      in_order_print(root.r_child)

  def pre_order_print(root):
      if not root:
          return        
      print root.data
      pre_order_print(root.l_child)
      pre_order_print(root.r_child)
      
  r = Node(3)
  binary_insert(r, Node(7))
  binary_insert(r, Node(1))
  binary_insert(r, Node(5))
  ```

### 性质：  

- 一颗二叉树第i层(i>= 0 )上最多有2^i 个结点
- 如果二叉树中度为0的结点数有n个，那么度为2的结点数为n-1个

## 存储结构

- 顺序存储结构
- 链式存储结构

## 遍历

- 先序遍历：根左右
- 中序遍历：左根右
- 后序遍历：左右根
- （这里不必刻意的记忆遍历的方法，记住左右，然后前序，中序，后序主要不同在于根的不同，根的位置依次插入）

## 线索二叉树

## Huffman编码

Trie 树



# 树与森林

# 图

## Why



## What

- 连通分量：在无向图中，尽可能的从集合中收集顶点和边，使它们构成一个极大的连通子图，这个子图就被称为无向图的一个连通分量
- 最小生成树：连通加权无向图中的权值最小的树。
- 回路：第一个顶点和最后一个顶点相同的路径是回路
- 简单路径：序列中顶点不重复出现的是简单路径

## 存储结构

- 邻接矩阵
- 邻接表

## 遍历

- 深度优先遍历(DFS)
- 广度优先遍历

## 图的最小生成树

- Prim算法
- Kruskal算法

## 最短路径

- Dijkstra算法
- Floyd算法

## 有向无环图

- 拓扑结构，[拓扑排序](http://www.cnblogs.com/lavezhang/archive/2012/05/14/2499017.html)：拓扑排序的作用：例如linux的包依赖问题，经过拓扑排序以后，前一个node跟后一个node要不是没有关系就是一定相关，不存在环路的问题。
- 关键路径

# 查找

# 排序

快速排序，归并排序都是是分治法的一种实现(Python Algorithms_Magus Lie Hetland)
快速排序是以第一个元素为基准，小于该元素的放在左边，大于该元素的放在右边，然后对两边递归排序
归并排序是将序列长度为n的元素分为左右两列，然后分别排序，最后再进行合并。

```python
## quick sort
def partition(seq):
    pi, seq = seq[0], seq[1:]
    low = [x for x in seq if x <= pi]
    high = [x for x in seq if x > pi]
    return low, pi, high


def quicksort(seq):
    if len(seq) <= 1: return seq
    low, pi, high = partition(seq)
    return quicksort(low) + [pi] + quicksort(high)
  
 ## mergesort
def mergesort(seq):
    mid = len(seq) // 2
    print seq
    left, right = seq[:mid], seq[mid:]
    if len(left) > 1: left = mergesort(left)
    if len(right) > 1: right = mergesort(right)
    res = []
    while left and right:
        if left[-1] >= right[-1]:
            res.append(left.pop())
        else:
            res.append(right.pop())
    res.reverse()
    return (left or right) + res
```

