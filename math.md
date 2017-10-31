# Calculus

## Taylor's formula

$$f(x)=f(x_0)+f'(x_0)\frac{x-x_0}{1!}+f''(x_0)\frac{(x-x_0)^2}{2!}+...+f^{(n)}(x_0)\frac{(x-x_0)^n}{n!}$$

[reference](https://www.zhihu.com/question/21149770): 简单讲就是泰勒展开式与f(x) 每一阶的导数值都相同



# linear algebra

矩阵线性变换：线性变换是基向量的在空间的转换，转换遵循两个原则：一个是原点固定，另外一个是保持网格平行并等距分布。

矩阵的两个基本计算是数乘和加法计算，矩阵的乘法是根据线性变换转化来的。

行列式(一般用det进行表示)是线性变换之后的面积变化的比例。求解线性方程组AX=V就是经过线性变换A后，v向量变化为V向量，所谓的逆矩阵就是将沿着线性变换的反方向变换为基向量，秩的作用是判断这个方程有没有解，其实秩变换指的就是变换后空间的维数。

```python
#numpy计算，不建议使用matrix类，建议使用array类
import numpy as np
a = np.matrix([[1,2,3],[3,4,5],[6,7,9]])
print a
print np.linalg.det(a)
#python求解线性方程组   https://ipreacher.github.io/2017/common-symbolic-calculations/
import numpy as np
A = np.mat('1,2;4,5')
b = np.mat('3,6').T
r = np.linalg.solve(A,b)
print r

```

点积：一个向量在另一个向量的投影与另一个向量的长度的乘积。对应的计算方法是对应元素相乘

## eigenvector

$$A x=\lambda x$$

[reference:3blue1brown](https://space.bilibili.com/88461692?from=search&seid=14640576376199499120#!/)







# Probability theory

