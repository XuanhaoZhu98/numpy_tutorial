# 14 Numpy 随机函数

在矩阵应用的过程中，经常需要使用随机数，Numpy中的random模块用于生成随机数。下面是一些常用的函数用法。

## 1) numpy.random.seed()

设置随机数种子，作用为使随机生成的数据可预测。

* numpy.random.seed()中每一个数字代表一种随机数生成规则，当种子数确定后，每次调用numpy.random下的随机函数时，都会根据该种子数对应的规则，依次生成随机数或随机数组。

* 当第二次指定相同的种子数时，每次调用numpy.random下的随机函数，会依次生成跟上一次指定种子数再调用随机函数时，相同的随机数或随机数组，即两次随机数（组）生成结果依次一一对应。

* 当不指定种子数时，每次调用numpy.random下的随机函数，numpy会随机指定一个种子数，即随机地采用该种子数所对应的规则，生成随机数或随机数组，所以生成结果每次不同。

示例如下：

```python
np.random.seed(0)
a = np.random.rand(4)  
print(a)
```

输出结果：

```
[0.5488135  0.71518937 0.60276338 0.54488318]
```

## 2) numpy.random.rand()

通过本函数可以返回一个或一组服从“0~1”均匀分布的随机样本值。随机样本取值范围是[0,1)，不包括1。numpy.random.rand()可以接受多个整数作为参数：

* 当函数括号内没有参数时，则返回一个浮点数；
* 当函数括号内有一个参数时，则返回秩为1的数组，不能表示向量和矩阵；
* 当函数括号内有两个及以上参数时，则返回对应维度的数组，能表示向量或矩阵。

均匀分布:

也叫矩形分布，它是对称概率分布，在相同长度间隔的分布概率是等可能的。

均匀分布由两个参数a和b定义，它们是数轴上的最小值和最大值，通常缩写为U（a，b）。

均匀分布的概率密度函数为：

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204231659518.svg)

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204231659519.svg)

示例如下：

```python
import numpy as np
a = np.random.rand(2,3,4)
print(a)
print(a.shape)
```

输出结果：

```
[[[0.4236548  0.64589411 0.43758721 0.891773  ]
  [0.96366276 0.38344152 0.79172504 0.52889492]
  [0.56804456 0.92559664 0.07103606 0.0871293 ]]

 [[0.0202184  0.83261985 0.77815675 0.87001215]
  [0.97861834 0.79915856 0.46147936 0.78052918]
  [0.11827443 0.63992102 0.14335329 0.94466892]]]
(2, 3, 4)
```

## 3) numpy.random.randn()

通过本函数可以返回一个或一组服从标准正态分布的随机样本值。

标准正态分布是以0为均数、以1为标准差的正态分布，记为N（0，1）。对应的正态分布曲线如下所示：

<img src="https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204231711056.png" style="zoom:50%;" />

标准正态分布曲线下面积分布规律是：

在-1.96～+1.96范围内曲线下的面积等于0.9500（即取值在这个范围的概率为95%），在-2.58～+2.58范围内曲线下面积为0.9900（即取值在这个范围的概率为99%）.因此，由 np.random.randn()函数所产生的随机样本基本上取值主要在-1.96~+1.96之间，当然也不排除存在较大值的情形，只是概率较小而已。

示例如下：

```python
import numpy as np
a = np.random.randn(2,3,4)
print(a)
print(a.shape)
```

输出结果：

```
[[[ 2.26975462 -1.45436567  0.04575852 -0.18718385]
  [ 1.53277921  1.46935877  0.15494743  0.37816252]
  [-0.88778575 -1.98079647 -0.34791215  0.15634897]]

 [[ 1.23029068  1.20237985 -0.38732682 -0.30230275]
  [-1.04855297 -1.42001794 -1.70627019  1.9507754 ]
  [-0.50965218 -0.4380743  -1.25279536  0.77749036]]]
(2, 3, 4)
```

## 4) numpy.random.randint()

函数的作用是，返回一个随机整型数，其范围为[low, high)。如果没有写参数high的值，则返回[0,low)的值。语法格式：

```
numpy.random.randint(low, high=None, size=None, dtype='l')
```

参数列表：

- low: int，生成的数值最低要大于等于low。（hign = None时，生成的数值要在[0, low)区间内）；
- high: int (可选)，如果使用这个值，则生成的数值在[low, high)区间；
- size: int or tuple of ints(可选)，输出随机数的尺寸，比如size = (m * n* k)则输出同规模即m * n* k个随机数。默认是None的，仅仅返回满足要求的单一随机数；
- dtype: dtype(可选)，想要输出的格式。如`int64`、`int`等。

示例如下：

```python
import numpy as np
a = np.random.randint(low=6,high=10,size=(2,3,4),dtype='int')
print(a,a.shape)
```

输出结果：

```
[[[9 6 9 8]
  [9 9 7 7]
  [7 6 7 7]]

 [[7 9 6 9]
  [7 8 6 7]
  [8 6 8 6]]] (2, 3, 4)
```

## 5) numpy.random.choice()

np.random.choice()用于从给定的一维数组中随机选择数生成随机数。语法格式：

```python
numpy.random.choice(a, size=None, replace=True, p=None)
```

参数列表：

- a：一维数组或者整数，如果是ndarray，则从其元素生成随机样本。如果是int，则生成随机样本，就像a是np.arange（a）
- size：整数的int或元组，可选,输出形状。如果给定的形状是例如（m，n，k），则绘制m * n * k个样本。默认值为None，在这种情况下返回单个值。
- replace：boolean类型，可选。抽样之后还放不放回去，如果是False的话，那么通一次挑选出来的数都不一样，如果是True的话， 有可能会出现重复的，因为前面的抽的放回去了；
- p：一维数组，可选，指定与a中每个条目相关的概率。如果没有给出，则样本假设在a中的所有条目上均匀分布。

示例如下：

```python
import numpy as np
a = np.random.choice(a = [3,5,6],size=(2,3,4),replace=True,p=[0.1,0.5,0.4])
print(a,a.shape)
```

输出结果：

```
[[[6 5 6 6]
  [6 3 5 5]
  [5 5 5 5]]

 [[3 6 5 5]
  [5 3 5 6]
  [5 6 5 6]]] (2, 3, 4)
```

## 6) numpy.random.normal()

np.random.normal()用于生成符合指定分布的正态分布。

```python
numpy.random.normal(loc, scale, size)
```

参数列表：

* loc：float，正态分布的均值，对应着这个分布的中心。loc=0说明这一个以Y轴为对称轴的正态分布；
* scale：float，正态分布的标准差，对应分布的宽度，scale越大，正态分布的曲线越矮胖，scale越小，曲线越高瘦；
* size：int or tuple of ints，输出的shape，默认为None，只输出一个值。

示例如下：

```python
import numpy as np
a = np.random.normal(loc=4,scale=6,size=(2,3,4))
print(a,a.shape)
```

输出结果：

```
[[[-1.2247829   0.52690201  2.13068481  4.33699205]
  [-2.99089904  9.40495892  6.79397464 -5.21746212]
  [12.92951316 15.37533506 11.07267743  2.92045099]]

 [[-2.42451573 10.32671036  1.58093832 11.33467042]
  [ 5.24964987  9.85983422  6.13819838  8.23943901]
  [ 4.06300012 14.71522296  4.76147256  6.41193618]]] (2, 3, 4)
```

## 7) numpy.random.random()

np.random.random(),生成符合0到1的均匀分布数组。示例如下：

```python
import numpy as np
a = np.random.random((2,3,4))
print(a,a.shape)
```

输出结果：

```
[[[0.42385505 0.60639321 0.0191932  0.30157482]
  [0.66017354 0.29007761 0.61801543 0.4287687 ]
  [0.13547406 0.29828233 0.56996491 0.59087276]]

 [[0.57432525 0.65320082 0.65210327 0.43141844]
  [0.8965466  0.36756187 0.43586493 0.89192336]
  [0.80619399 0.70388858 0.10022689 0.91948261]]] (2, 3, 4)
```

## 8) numpy.random.uniform()

np.random.uniform()从一个均匀分布[low,high)中随机采样，注意定义域是左闭右开，即包含low，不包含high。语法格式：

```
numpy.random.uniform(low=0.0, high=1.0, size=None)
```

参数列表:

* low: 采样下界，float类型，默认值为0；
* high: 采样上界，float类型，默认值为1；
* size: 输出样本数目，为int或元组(tuple)类型，例如，size=(m,n,k), 则输出 m * n * k 个样本，缺省时输出1个值。

示例如下：

```python
import numpy as np
a=np.random.uniform(-1,1,10)#指定均匀分布
print(a,a.shape)
```

输出结果：

```
[ 0.4284826   0.99769401 -0.70110339  0.73625211 -0.67501413  0.23111913
 -0.75236003  0.69601646  0.61463792  0.13820148] (10,)
```

## 9) numpy.random.shuffle()

np.random.shuffle()用于随机打乱数组顺序。操作在原数组上进行，改变自身序列，无返回值。

一维数组示例：

```python
import numpy as np
arr = np.arange(10)
print(arr)
np.random.shuffle(arr)
print(arr)
```

输出结果：

```
[0 1 2 3 4 5 6 7 8 9]
[5 0 4 2 9 6 8 1 7 3]
```

对多维数组进行打乱排列时，默认是列维度：

```python
arr = np.arange(12).reshape(3,4)
print(arr)
np.random.shuffle(arr)
print(arr)
```

输出结果：

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
[[ 8  9 10 11]
 [ 4  5  6  7]
 [ 0  1  2  3]]
```

## 10) numpy.random.permutation()

np.random.permutation()用来随机排列一个数组。不在原数组上进行，返回新的数组，不改变自身数组。

可直接生成一个随机排列的数组：

```python
import numpy as np
a = np.random.permutation(10)
print(a)
```

输出结果：

```
array([2, 1, 6, 5, 4, 7, 8, 9, 3, 0])
```

一维数组示例：

```python
import numpy as np
arr = np.arange(10)
print(arr)
arr = np.random.permutation(arr)
print(arr)
```

输出结果：

```
[0 1 2 3 4 5 6 7 8 9]
[0 6 5 8 1 2 9 4 7 3]
```

对多维数组进行打乱排列时，默认是列维度：

```python
arr = np.arange(12).reshape(3,4)
print(arr)
arr = np.random.permutation(arr)
print(arr)
```

输出结果：

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
[[ 8  9 10 11]
 [ 0  1  2  3]
 [ 4  5  6  7]]
```

## 11) 产生其他分布的函数

| 函数名                   | 分布类型 |
| ------------------------ | -------- |
| numpy.random.binomial()  | 二项分布 |
| numpy.random.chisquare() | 卡方分布 |
| numpy.random.poisson()   | 泊松分布 |
| numpy.random.uiform()    | 均匀分布 |
| numpy.random.normal()    | 正态分布 |

