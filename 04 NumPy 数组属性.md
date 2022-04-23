# 04 NumPy 数组属性

NumPy 数组的维数称为秩（rank），秩就是轴的数量，即数组的维度，一维数组的秩为 1，二维数组的秩为 2，以此类推。

在 NumPy中，每一个线性的数组称为是一个轴（axis），也就是维度（dimensions）。比如说，二维数组相当于是两个一维数组，其中第一个一维数组中每个元素又是一个一维数组。所以一维数组就是 NumPy 中的轴（axis），第一个轴相当于是底层数组，第二个轴是底层数组里的数组。而轴的数量——秩，就是数组的维数。

很多时候可以声明 axis。axis=0，表示沿着第 0 轴进行操作，即对每一列进行操作；axis=1，表示沿着第1轴进行操作，即对每一行进行操作。

NumPy 的数组中比较重要 ndarray 对象属性有：

| 属性             | 说明                                                         |
| :--------------- | :----------------------------------------------------------- |
| ndarray.ndim     | 秩，即轴的数量或维度的数量                                   |
| ndarray.shape    | 数组的维度，对于矩阵，n 行 m 列                              |
| ndarray.size     | 数组元素的总个数，相当于 .shape 中 n*m 的值                  |
| ndarray.dtype    | ndarray 对象的元素类型                                       |
| ndarray.itemsize | ndarray 对象中每个元素的大小，以字节为单位                   |
| ndarray.flags    | ndarray 对象的内存信息                                       |
| ndarray.real     | ndarray元素的实部                                            |
| ndarray.imag     | ndarray 元素的虚部                                           |
| ndarray.data     | 包含实际数组元素的缓冲区，由于一般通过数组的索引获取元素，所以通常不需要使用这个属性。 |

## ndarray.shape()

shape 属性的返回值一个由数组维度构成的元组，比如 2 行 3 列的二维数组可以表示为`(2,3)`，该属性可以用来调整数组维度的大小。

示例如下，输出了数组的维度：

```python
import numpy as np
a = np.array([[2,4,6],[3,5,7]])
print(a.shape)
```

输出结果：

```
(2, 3)
```

通过 shape 属性修改数组的形状大小： 

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6]])
print(a.shape)
a.shape = (3,2)
print(a)
print(a.shape)
```

输出结果：

```
(2, 3)

[[1 2]
 [3 4]
 [5 6]]
 
(3, 2)
```

## ndarray.reshape()

NumPy 还提供了一个调整数组形状的 reshape() 函数。

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6]])
b = a.reshape(3,2)
print(b)
```

输出结果：

```
[[1 2]
 [3 4]
 [5 6]]
```

## ndarray.ndim()

该属性返回的是数组的维数，示例如下：

```python
import numpy as np
#随机生成一个一维数组
c = np.arange(24)
print(c)
print(c.ndim)
#将数组变为二维
e = c.reshape(4,6)
print(e) 
print(e.ndim)
#将数组变为三维
e = c.reshape(2,4,3)
print(e) 
print(e.ndim)
```

输出结果如下所示：

```
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23]
1

[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]]
2

[[[ 0  1  2]
  [ 3  4  5]
  [ 6  7  8]
  [ 9 10 11]]

 [[12 13 14]
  [15 16 17]
  [18 19 20]
  [21 22 23]]]
3
```

## ndarray.itemsize()

返回数组中每个元素的大小（以字节为单位），示例如下：

```python
#数据类型为int8，代表1字节
import numpy as np
x = np.array([1,2,3,4,5], dtype = np.int8)
print (x.itemsize)
#数据类型为int64，代表8字节
x = np.array([1,2,3,4,5], dtype = np.int64)
print (x.itemsize)
```

输出结果为：

```
1
8
```

## ndarray.flags()

返回 ndarray 数组的内存信息，比如 ndarray 数组的存储方式，以及是否是其他数组的副本等。\包含以下属性：

| 属性             | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| C_CONTIGUOUS (C) | 数据是在一个单一的C风格的连续段中                            |
| F_CONTIGUOUS (F) | 数据是在一个单一的Fortran风格的连续段中                      |
| OWNDATA (O)      | 数组拥有它所使用的内存或从另一个对象中借用它                 |
| WRITEABLE (W)    | 数据区域可以被写入，将该值设置为 False，则数据为只读         |
| ALIGNED (A)      | 数据和所有元素都适当地对齐到硬件上                           |
| UPDATEIFCOPY (U) | 这个数组是其它数组的一个副本，当这个数组被释放时，原数组的内容将被更新 |

示例如下：

```
import numpy as np
x = np.array([1,2,3,4,5])
print (x.flags)
```

输出结果如下：

```
  C_CONTIGUOUS : True
  F_CONTIGUOUS : True
  OWNDATA : True
  WRITEABLE : True
  ALIGNED : True
  WRITEBACKIFCOPY : False
  UPDATEIFCOPY : False
```

