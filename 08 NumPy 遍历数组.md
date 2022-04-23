# 08 NumPy 遍历数组

##  直接迭代数组

迭代意味着逐一遍历元素。当我们在 numpy 中处理多维数组时，可以使用 python 的基本 for 循环来完成此操作。

如果我们对 1-D 数组进行迭代，它将逐一遍历每个元素：

```python
import numpy as np
arr = np.array([1, 2, 3])
for x in arr:
  print(x)
```

输出结果：

```
1
2
3
```

在 2-D 数组中，它将遍历所有行：

```python
import numpy as np
arr = np.array([[1, 2, 3], [4, 5, 6]])
for x in arr:
  print(x)
```

输出结果：

```
[1 2 3]
[4 5 6]
```

如果我们迭代一个 n-D 数组，它将逐一遍历第 n-1 维。如需返回实际值、标量，我们必须迭代每个维中的数组。

迭代 2-D 数组的每个标量元素：

```python
import numpy as np
arr = np.array([[1, 2, 3], [4, 5, 6]])
for x in arr:
  for y in x:
    print(y, end=' ')
```

输出结果：

```
1 2 3 4 5 6 
```

在 3-D 数组中，它将遍历所有 2-D 数组：

```python
import numpy as np
arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
for x in arr:
  print(x)
```

输出结果：

```
[[1 2 3]
 [4 5 6]]
[[ 7  8  9]
 [10 11 12]]
```

## nditer() 迭代数组

NumPy 提供了一个 nditer 迭代器对象，它可以配合 for 循环完成对数组元素的遍历。

下面看一组示例，使用 arange() 函数创建一个 3*4 数组，并使用 nditer 生成迭代器对象：

```python
import numpy as np
a = np.arange(0,60,5)
a = a.reshape(3,4)
print(a)
#使用nditer迭代器,并使用for进行遍历
for x in np.nditer(a):
   print(x, end=' ')
```

输出结果：

```
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]

0 5 10 15 20 25 30 35 40 45 50 55 
```

## 遍历顺序

在内存中，Numpy 数组提供了两种存储数据的方式，分别是 C-order（行优先顺序）与 Fortrant-order（列优先顺序）。那么 nditer 迭代器又是如何处理具有特定存储顺序的数组呢？其实它选择了一种与数组内存布局一致的顺序，之所以这样做，是为了提升数据的访问效率。

在默认情况下，当我们遍历数组中元素的时候，不需要考虑数组的存储顺序，这一点可以通过遍历上述数组的转置数组来验证：

```python
import numpy as np
a = np.arange(0,60,5)
a = a.reshape(3,4)
#a的转置数组
b = a.T
print (b)
for x in np.nditer(b):
   print(x, end=" ")
```

输出结果：

```
[[ 0 20 40]
 [ 5 25 45]
 [10 30 50]
 [15 35 55]]
 
0 5 10 15 20 25 30 35 40 45 50 55 
```

从示例 1、2 的输出结果可以看出，a 和 a.T 的遍历顺序是一样的，也就是说，它们在内存中的存储顺序是一样的。

下面以 C 样式访问转置数组的副本：

```python
import numpy as np
a = np.arange(0,60,5).reshape(3,4)
#copy方法生成数组副本
for x in np.nditer(a.T.copy(order='C')):
    print (x, end=' ')
```

输出结果：

```
0 20 40 5 25 45 10 30 50 15 35 55 
```

 a.T.copy(order = 'C') 的遍历结果是不同的，那是因为它和前两种的存储方式是不一样的，默认是按行访问。

## 指定遍历顺序

您可以通过 nditer 对象的`order`参数来指定数组的遍历的顺序。示例 4 如下：

```python
import numpy as np
a = np.arange(0,60,5)
a = a.reshape(3,4)
print(a)
for x in np.nditer(a, order = 'C'):
   print (x,end=" ") 
print('')
for x in np.nditer(a, order = 'F'):
   print (x,end=" ")
```

输出结果如下：

```
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]
 
0 5 10 15 20 25 30 35 40 45 50 55 

0 20 40 5 25 45 10 30 50 15 35 55 
```

## 修改数组元素值

nditer 对象提供了一个可选参数`op_flags`，它表示能否在遍历数组时对元素进行修改。它提供了几种模式，如下所示：

| 模式         | 说明                       |
| ------------ | -------------------------- |
| readonly     | 只读取操作数               |
| readwrite    | 读取和写入操作数           |
| writeonly    | 操作数只会被写入           |
| no_broadcast | 防止操作数被广播           |
| contig       | 强制操作数数据是连续的     |
| aligned      | 强制操作数数据对齐         |
| copy         | 如果需要，允许临时只读副本 |
| updateifcopy | 如果需要，允许临时读写副本 |

示例如下：

```python
import numpy as np
a = np.arange(0,60,5)
a = a.reshape(3,4) 
print (a)
for x in np.nditer(a, op_flags=['readwrite']):
    x[...]=2*x
print (a)
```

输出结果：

```
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]
 
[[  0  10  20  30]
 [ 40  50  60  70]
 [ 80  90 100 110]]
```

## 外部循环使用

nditer 对象的构造函数有一个“flags”参数，它可以接受以下参数值：

| 参数值        | 描述说明                               |
| ------------- | -------------------------------------- |
| c_index       | 可以跟踪 C 顺序的索引。                |
| f_index       | 可以跟踪 Fortran 顺序的索引。          |
| multi_index   | 每次迭代都会跟踪一种索引类型。         |
| external_loop | 返回的遍历结果是具有多个值的一维数组。 |

在下面的实例中，迭代器遍历对应于每列，并组合为一维数组：

```python
import numpy as np
a = np.arange(0,60,5)
a = a.reshape(3,4)
print(a)
#修改后数组
for x in np.nditer(a, flags = ['external_loop'], order = 'F'):
   print(x, end=' ')
```

结果输出：

```
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]
 
[ 0 20 40] [ 5 25 45] [10 30 50] [15 35 55] 
```

## 迭代不同数据类型的数组

我们可以使用 op_dtypes 参数，并传递期望的数据类型，以在迭代时更改元素的数据类型。

NumPy 不会就地更改元素的数据类型（元素位于数组中），因此它需要一些其他空间来执行此操作，该额外空间称为 buffer，为了在 nditer() 中启用它，我们传参 flags=['buffered']。

以字符串形式遍历数组：

```python
import numpy as np
arr = np.array([1, 2, 3])
for x in np.nditer(arr, flags=['buffered'], op_dtypes=['S']):
  print(x)
```

结果输出：

```
b'1'
b'2'
b'3'
```

## 以不同的步长迭代

我们可以使用过滤，然后进行迭代。

每遍历 2D 数组的一个标量元素，跳过 1 个元素：

```python
import numpy as np
arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
for x in np.nditer(arr[:, ::2]):
  print(x, end=' ')
```

结果输出：

```
1 3 5 7 
```

## ndenumerate() 枚举迭代

枚举是指逐一提及事物的序号。有时，我们在迭代时需要元素的相应索引，对于这些用例，可以使用 ndenumerate() 方法。

枚举以下 2D 数组元素：

```python
import numpy as np
arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
for idx, x in np.ndenumerate(arr):
  print(idx, x)
```

结果输出：

```
(0, 0) 1
(0, 1) 2
(0, 2) 3
(0, 3) 4
(1, 0) 5
(1, 1) 6
(1, 2) 7
(1, 3) 8
```

## 迭代多个数组

如果两个数组都能够被广播，那么 nditer 对象就可以同时对它们迭代。

假设数组 a 的维度是 3*4，另一个数组 b 的维度是 1*4 （即维度较小的数组 b 可以被广播到数组 a 中），示例如下：

```python
import numpy as np
a = np.arange(0,60,5)
a = a.reshape(3,4)
print (a)
b = np.array([1, 2, 3, 4], dtype = int)
print (b)
#广播迭代
for x,y in np.nditer([a,b]):
    print ("%d:%d" % (x,y),end=" ")
```

输出结果：

```
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]
 
[1 2 3 4]

0:1 5:2 10:3 15:4 20:1 25:2 30:3 35:4 40:1 45:2 50:3 55:4 
```