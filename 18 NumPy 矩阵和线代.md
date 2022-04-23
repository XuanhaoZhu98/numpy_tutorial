# 18 NumPy 矩阵和线代

## Matrix矩阵库

NumPy 提供了一个 矩阵库模块`numpy.matlib`，该模块中的函数返回的是一个 matrix 对象，而非 ndarray 对象。矩阵由 m 行 n 列（m*n）元素排列而成，矩阵中的元素可以是数字、符号或数学公式等。

### 1) matlib.empty()

matlib.empty() 返回一个空矩阵，所以它的创建速度非常快。语法格式为：

```
numpy.matlib.empty(shape, dtype, order)
```

该函数的参数说明如下：

- shape：以元组的形式指定矩阵的形状。
- dtype：表示矩阵的数据类型。
- order：有两种选择，C（行序优先） 或者 F（列序优先）。

示例如下：

```python
import numpy.matlib
import numpy as np
#矩阵中会填充无意义的随机值
print(np.matlib.empty((2,2)))
```

输出结果：

```
[[1.19239296e-311 4.67296746e-307]
 [1.69121096e-306 7.56598449e-307]]
```

### 2) numpy.matlib.zeros()

numpy.matlib.zeros() 创建一个以 0 填充的矩阵，示例如下：

```python
import numpy.matlib
import numpy as np
print(np.matlib.zeros((2,2))) 
```

输出结果：

```
[[0. 0.]
 [0. 0.]]
```

### 3) numpy.matlib.ones()

numpy.matlib.ones() 创建一个以 1 填充的矩阵。

```python
import numpy.matlib
import numpy as np
print(np.matlib.ones((2,2)))
```

输出结果：

```
[[1. 1.]
 [1. 1.]]
```

### 4) numpy.matlib.eye()

numpy.matlib.eye() 返回一个对角线元素为 1，而其他元素为 0 的矩阵 。

```
numpy.matlib.eye(n,M,k, dtype)
```

- n：返回矩阵的行数；
- M：返回矩阵的列数，默认为 n；
- k：对角线的索引；
- dtype：矩阵中元素数据类型。

示例如下：

```python
import numpy.matlib
import numpy as np
print (np.matlib.eye(n =  3, M =  4, k =  0, dtype =  float))
```

输出结果：

```
[[1. 0. 0. 0.]
[0. 1. 0. 0.]
[0. 0. 1. 0.]]
```

### 5) numpy.matlib.identity()

该函数返回一个给定大小的单位矩阵，矩阵的对角线元素为 1，而其他元素均为 0。

单位矩阵是个方阵，从左上角到右下角的对角线（称为主对角线）上的元素均为 1，除此以外全都为 0。

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204231130681.png)

```python
import numpy.matlib 
import numpy as np 
# 大小为 5，类型位浮点型
print (np.matlib.identity(5, dtype =  float))
```

输出结果：

```
[[1. 0. 0. 0. 0.]
 [0. 1. 0. 0. 0.]
 [0. 0. 1. 0. 0.]
 [0. 0. 0. 1. 0.]
 [0. 0. 0. 0. 1.]]
```

### 6) numpy.matlib.rand()

numpy.matlib.rand() 创建一个以随机数填充，并给定维度的矩阵。示例如下：

```python
import numpy.matlib
import numpy as np
print (np.matlib.rand(3,3))
```

示例如下：

```
[[0.27732985 0.96723737 0.86159908]
 [0.37472089 0.44021126 0.13453269]
 [0.12121979 0.7548293  0.94795934]]
```

### 7) np.asarray()/np.asmatrix()

矩阵总是二维的，而 ndarray 是一个 n 维数组。 两个对象都是可互换的。示例如下：

```python
#创建矩阵i
import numpy.matlib
import numpy as np 
i = np.matrix('1,2;3,4') 
print (i)
```

输出结果：

```
[[1 2]
 [3 4]]
```

实现 matrix 与 ndarray 之间的转换，如下所示：

```python
import numpy.matlib
import numpy as np 
j = np.asarray(i) 
print (j)
print(type(j))
k = np.asmatrix (j)
print (k)
print(type(k))
```

输出结果：

```
[[1 2]
 [3 4]]
<class 'numpy.ndarray'>

[[1 2]
 [3 4]]
<class 'numpy.matrix'>

```

## 线性代数

NumPy 提供了线性代数函数库 **linalg**，该库包含了线性代数所需的所有功能，可以看看下面的说明：

| 函数          | 描述                             |
| :------------ | :------------------------------- |
| `dot`         | 两个数组的点积，即元素对应相乘。 |
| `vdot`        | 两个向量的点积                   |
| `inner`       | 两个数组的内积                   |
| `matmul`      | 两个数组的矩阵积                 |
| `determinant` | 数组的行列式                     |
| `solve`       | 求解线性矩阵方程                 |
| `inv`         | 计算矩阵的乘法逆矩阵             |

### 1) numpy.dot()

numpy.dot() 对于两个一维的数组，计算的是这两个数组对应下标元素的乘积和（又称内积或点积）；对于二维数组，计算的是两个数组的矩阵乘积；对于多维数组，它的通用计算公式如下，即结果数组中的每个元素都是：数组a的最后一维上的所有元素与数组b的倒数第二位上的所有元素的乘积和： dot(a, b)[i,j,k,m] = sum(a[i,j,:] \* b[k,:,m])。语法格式：

```python
numpy.dot(a, b, out=None) 
```

参数说明：

- a : ndarray 数组
- b : ndarray 数组
- out : ndarray, 可选，用来保存dot()的计算结果

输入一维数组，示例如下：

```python
import numpy as np
A=[1,2,3]
B=[4,5,6]
print(np.dot(A,B))
```

输出结果：

```
32
```

输入二维数组时，示例如下：

```python
import numpy as np 
a = np.array([[1,2],
             [3,4]]) 
b = np.array([[5,6],
            [7,8]]) 
dot = np.dot(a,b) 
print(dot) 
```

输出结果：

```
[[19 22]
 [43 50]]
```

乘积计算式为：

```
[[1*5+2*7, 1*6+2*8],[3*5+4*7, 3*6+4*8]]
```

### 2) numpy.vdot()

numpy.vdot() 函数是两个向量的点积。 如果第一个参数是复数，那么它的共轭复数会用于计算。 如果参数是多维数组，它会被展开。

输入一维数组，示例如下：

```python
import numpy as np
A=[1,2,3]
B=[4,5,6]
print(np.vdot(A,B))
```

输出结果：

```
32
```

输入二维数组，示例如下：

```python
import numpy as np 
a = np.array([[1,2], [3,4]]) 
b = np.array([[5,6], [7,8]]) 
# vdot 将数组展开计算内积
vdot = np.vdot(a,b) 
print(vdot)  
```

输出结果：

```
70
```

点积计算式为：

```
1*5 + 2*6 + 3*7 + 4*8 = 130
```

### 3) numpy.inner()

inner() 方法用于计算数组之间的内积。当计算的数组是一维数组时，它与 dot() 函数相同，若输入的是多维数组则两者存在不同，下面看一下具体的实例。

输入一维数组，示例如下：

```python
import numpy as np
A=[1,2,3]
B=[4,5,6]
print(np.inner(A,B))
```

输出结果：

```
32
```

输入二维数组，示例如下：

```python
import numpy as np 
a = np.array([[1,2], 
              [3,4]]) 
b = np.array([[5,6], 
              [7,8]]) 
# vdot 将数组展开计算内积
inner = np.inner(a,b) 
print(inner)  
```

输出结果：

```
[[17 23]
 [39 53]]
```

dot() 则表示是 A 数组每一行与 B 数组的每一列相乘。

内积计算式为：

```
1*5+2*6, 1*7+2*8 
3*5+4*6, 3*7+4*8
```

### 4) numpy.matmul()

numpy.matmul 函数返回两个数组的矩阵乘积。 虽然它返回二维数组的正常乘积，但如果任一参数的维数大于2，则将其视为存在于最后两个索引的矩阵的栈，并进行相应广播。另一方面，如果任一参数是一维数组，则通过在其维度上附加 1 来将其提升为矩阵，并在乘法之后被去除。

对于二维数组，它就是矩阵乘法：

```python
import numpy as np 
a = np.array([[1,2,3],[4,5,6],[7,8,9]]) 
b = np.array([[9,8,7],[6,5,4],[3,2,1]]) 
mul = np.matmul(a,b) 
print(mul) 
```

输出结果：

```
[[ 30  24  18]
 [ 84  69  54]
 [138 114  90]]
```

二维和一维运算：

```python
import numpy.matlib 
import numpy as np 
a = [[1,0],[0,1]] 
b = [1,2] 
print (np.matmul(a,b))
print (np.matmul(b,a))
```

输出结果为：

```
[1  2] 
[1  2]
```

维度大于二的数组 ：

```python
import numpy.matlib 
import numpy as np 
a = np.arange(8).reshape(2,2,2) 
b = np.arange(4).reshape(2,2) 
print (np.matmul(a,b))
```

输出结果为：

```
[[[ 2  3]
  [ 6 11]]

 [[10 19]
  [14 27]]]
```

### 5) numpy.multiple()

multiple() 函数用于两个矩阵的逐元素乘法，示例如下：

```python
import numpy as np 
array1=np.array([[1,2,3],[4,5,6],[7,8,9]],ndmin=3) 
array2=np.array([[9,8,7],[6,5,4],[3,2,1]],ndmin=3) 
result=np.multiply(array1,array2) 
print(result)
```

输出结果：

```
[[[ 9 16 21]
  [24 25 24]
  [21 16  9]]]
```

### 6) numpy.linalg.det()

numpy.linalg.det() 函数计算输入矩阵的行列式。行列式在线性代数中是非常有用的值。 它从方阵的对角元素计算。 对于 2×2 矩阵，它是左上和右下元素的乘积与其他两个的乘积的差。换句话说，对于矩阵[[a，b]，[c，d]]，行列式计算为 ad-bc。 较大的方阵被认为是 2×2 矩阵的组合。示例如下：

```
[[1,2],
 [3,4]]
```

通过对角线元素求行列式的结果（口诀：“一撇一捺”计算法）：

```
1*4-2*3=-2
```

我们可以使用 numpy.linalg.det() 函数来完成计算。示例如下：

```python
import numpy as np 
a = np.array([[1,2],[3,4]]) 
print(np.linalg.det(a))  
```

输出结果：

```
-2.0000000000000004
```

3*3矩阵的行列式：

```python
import numpy as np
b = np.array([[6,1,1], [4, -2, 5], [2,8,7]]) 
print (b)
print (np.linalg.det(b))
print (6*(-2*7 - 5*8) - 1*(4*7 - 5*2) + 1*(4*8 - -2*2))
```

输出结果：

```
[[ 6  1  1]
 [ 4 -2  5]
 [ 2  8  7]]
 
-306.0

-306
```

### 7) numpy.linalg.solve()

该函数用于求解线性矩阵方程组，并以矩阵的形式表示线性方程的解，如下所示：

```
3X  +  2 Y + Z =  10  
X + Y + Z = 6
X + 2Y - Z = 2
```

首先将上述方程式转换为矩阵的表达形式：

```
方程系数矩阵：
3   2   1 
1   1   1 
1   2  -1
方程变量矩阵:
X 
Y 
Z  
方程结果矩阵：
10 
6
2
```

如果用 m 、x、n 分别代表上述三个矩阵，其表示结果如下：

```
m*x=n 或 x=n/m
```

将**系数矩阵**与**结果矩阵传**递给 numpy.solve() 函数，即可求出线程方程的解，如下所示：

```python
import numpy as np
m = np.array([[3,2,1],[1,1,1],[1,2,-1]])
#数组 m
print (m)
#矩阵 n
n = np.array([[10],[6],[2]])
print (n)
#计算：m^(-1)n
x = np.linalg.solve(m,n)
print (x)
```

输出结果：

```
[[ 3  2  1]
 [ 1  1  1]
 [ 1  2 -1]]
 
[[10]
 [ 6]
 [ 2]]
 
[[1.]
 [2.]
 [3.]]
```

### 8) numpy.linalg.inv()

numpy.linalg.inv() 函数计算矩阵的乘法逆矩阵。**逆矩阵（inverse matrix）**：设A是数域上的一个n阶矩阵，若在相同数域上存在另一个n阶矩阵B，使得： AB=BA=E ，则我们称B是A的逆矩阵，而A则被称为可逆矩阵。注：E为单位矩阵。示例如下：

```python
import numpy as np 
a = np.array([[1,2],[3,4]]) 
#原数组
print(a) 
b = np.linalg.inv(a)
#求逆
print(b)  
```

输出结果：

```
[[1 2]
 [3 4]]
 
[[-2.   1. ]
 [ 1.5 -0.5]]
```