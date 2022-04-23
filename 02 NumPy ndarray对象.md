# 02 NumPy ndarray对象

## ndarray对象结构

NumPy 定义了一个 n 维数组对象，简称 ndarray 对象，它是一个一系列**相同类型元素**组成的数组集合。数组中的每个元素都占有**大小相同的内存块**，您可以使用索引或切片的方式获取数组中的每个元素。

ndarray 对象采用了**数组的索引机制**，将数组中的每个元素映射到内存块上，并且按照一定的布局对内存块进行排列，常用的布局方式有两种，即按行或者按列。

ndarray 内部由以下内容组成：

- 一个指向数据（内存或内存映射文件中的一块数据）的指针。
- 数据类型或 dtype，描述在数组中的固定大小值的格子。
- 一个表示数组形状（shape）的元组，表示各维度大小的元组。
- 一个跨度元组（stride），其中的整数指的是为了前进到当前维度下一个元素需要"跨过"的字节数。

ndarray 的内部结构:

![img](https://www.runoob.com/wp-content/uploads/2018/10/ndarray.png)

跨度可以是负数，这样会使数组在内存中后向移动，切片中 **obj[::-1]** 或 **obj[:,::-1]** 就是如此。

## 创建ndarray对象

通过 NumPy 的内置函数 array() 可以创建 ndarray 对象，其语法格式如下：

```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```

下面表格对其参数做了说明：

| 序号 | 参数   | 描述说明                                                     |
| ---- | ------ | ------------------------------------------------------------ |
| 1    | object | 表示一个数组序列。                                           |
| 2    | dtype  | 可选参数，通过它可以更改数组的数据类型。                     |
| 3    | copy   | 可选参数，表示数组能否被复制，默认是 True。                  |
| 4    | order  | 以哪种内存布局创建数组，有 3 个可选值，分别是 C(行序列)/F(列序列)/A(默认)。 |
| 5    | subok  | 默认返回一个与基类类型一致的数组。                           |
| 6    | ndim   | 用于指定数组的维度。                                         |

创建零维数组：

```python
import numpy as np
arr = np.array(6)
print(arr)
```

输出结果：

```
6
```

创建一维数组：

```python
import numpy as np
#使用列表构建一维数组
a=np.array([1,2,3])
print(a)
#ndarray数组类型
print(type(a))
```

输出结果：

```
[1 2 3]

<class 'numpy.ndarray'>
```

创建多维数组：

```python
b=np.array([[1,2,3],[4,5,6]])
print(b)
```

输出结果：

```
[[1 2 3]
 [4 5 6]]
```

如果要改变数组元素的数据类型，可以使用通过设置 dtype，如下所示：

```python
c=np.array([2,4,6,8],dtype="complex")
print(c)
```

现在将 c 数组中的元素类型变成了复数类型：

```
[2.+0.j 4.+0.j 6.+0.j 8.+0.j]
```

array() 是创建 ndarray 对象的基本方法，在后续内容中还会介绍其他方法。

## ndim查看数组维数

通过 ndim 可以查看数组的维度：

```python
import numpy as np 
arr = np.array([[1, 2, 3, 4], [4, 5, 6, 7], [9, 10, 11, 23]]) 
print(arr.ndim) 
```

输出结果：

```
2
```

## ndmin更高维的数组

数组可以拥有任意数量的维。在创建数组时，可以使用 ndmin 参数定义维数：

```python
#输出一个四维数组
import numpy as np
a = np.array([1, 2, 3, 4, 5], ndmin = 4)
print(a)
print('number of dimensions :', a.ndim)
```

输出结果如下：

```
[[[[1 2 3 4 5]]]]
number of dimensions : 4
```
