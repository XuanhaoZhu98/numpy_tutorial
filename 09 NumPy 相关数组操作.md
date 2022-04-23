# 09 NumPy 相关数组操作

NumPy 中包含了一些处理数组的常用方法，大致可分为以下几类：

- 数组变维操作
- 数组转置操作
- 修改数组维度操作
- 连接与分割数组操作

下面分别对它们进行介绍。

## 数组变维操作

| 函数名称 | 函数介绍                                                     |
| -------- | ------------------------------------------------------------ |
| reshape  | 在不改变数组元素的条件下，修改数组的形状。                   |
| flat     | 返回是一个迭代器，可以用 for 循环遍历其中的每一个元素。      |
| flatten  | 以一维数组的形式返回一份数组的副本，对副本的操作不会影响到原数组。 |
| ravel    | 返回一个连续的扁平数组（即展开的一维数组），与 flatten不同，它返回的是数组视图（修改视图会影响原数组）。 |

### 1) numpy.reshape()

数组的形状指的是多维数组的行数和列数。Numpy 模块提供 reshape() 函数可以在不改变数据的条件下修改形状改变多维数组行数和列数，从而达到数组变维的目的。因此数组变维即对数组形状的重塑，如图1所示：

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204201912073.png)
图1：reshape函数数组变维
reshape() 函数可以接受一个元组作为参数，用于指定了新数组的行数和列数，格式如下：

```python
numpy.reshape(arr, newshape, order='C')
```

参数说明：

- `arr`：要修改形状的数组
- `newshape`：整数或者整数数组，新的形状应当兼容原有形状
- order：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'k' -- 元素在内存中的出现顺序。

示例如下：

```python
import numpy as np 
e = np.array([[1,2],[3,4],[5,6]]) 
print(e) 
e=e.reshape(2,3) 
print(e)  
```

输出如下：

```
[[1 2]
 [3 4]
 [5 6]]
 
[[1 2 3]
 [4 5 6]]
```

### 2) numpy.ndarray.flat()

numpy.ndarray.flat 返回一个数组迭代器，实例如下:

```python
import numpy as np
a = np.arange(9).reshape(3,3)
print(a)
#使用flat属性：
for ele in a.flat:
    print (ele,end=' ')
```

输出结果如下：

```
[[0 1 2]
 [3 4 5]
 [6 7 8]]
 
0 1 2 3 4 5 6 7 8 
```

### 3) numpy.ndarray.flatten()

numpy.ndarray.flatten 返回一份数组副本，对副本修改不会影响原始数组，其语法格式如下：

```
ndarray.flatten(order='C')
```

实例如下：

```python
import numpy as np
a = np.arange(8).reshape(2,4)
print (a)
#默认按行C风格展开的数组
print (a.flatten())
#以F风格顺序展开的数组
print (a.flatten(order = 'F'))
```

输出结果：

```
[[0 1 2 3]
 [4 5 6 7]]
 
[0 1 2 3 4 5 6 7]

[0 4 1 5 2 6 3 7]
```

### 4) numpy.ravel()

numpy.ravel() 将多维数组中的元素以一维数组的形式展开，该方法返回数组的视图（view），如果修改，则会影响原始数组。

```python
numpy.ravel(a, order='C')
```

实例结果如下：

```python
import numpy as np
a = np.arange(8).reshape(2,4)
#原数组
print (a)
#调用 ravel 函数后
print (a.ravel())
#F 风格顺序调用 ravel 函数之后
print (a.ravel(order = 'F'))
```

输出结果如下：

```
[[0 1 2 3]
 [4 5 6 7]]
 
[0 1 2 3 4 5 6 7]

[0 4 1 5 2 6 3 7]
```

## 数组转置操作

| 函数名称  | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| transpose | 将数组的维度值进行对换，比如二维数组维度(2,4)使用该方法后为(4,2)。 |
| ndarray.T | 与 transpose 方法相同。                                      |
| rollaxis  | 沿着指定的轴向后滚动至规定的位置。                           |
| swapaxes  | 对数组的轴进行对换。                                         |

### 1) numpy.transpose()

numpy.transpose() 用于对换多维数组的维度，比如二维数组使用此方法可以实现矩阵转置，语法格式如下：

```python
numpy.transpose(arr, axes)
```

参数说明：

- arr：要操作的数组
- axes：可选参数，元组或者整数列表，将会按照该参数进行转置。

示例如下：

```python
import numpy as np
a = np.arange(12).reshape(3,4)
print (a)
print (np.transpose(a))
```

输出结果：

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
 
[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]
```

numpy.ndarray.T 类似 numpy.transpose：

```python
import numpy as np
a = np.arange(12).reshape(3,4)
print (a)
print (a.T)
```

输出结果：

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
 
[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]
```

### 2) numpy.rollaxis()

该方法表示沿着指定的轴，向后滚动至一个特定位置，格式如下：

```
numpy.rollaxis(arr, axis, start)
```

参数说明：

- arr：要传入的数组；
- axis：沿着哪条轴向后滚动，其它轴的相对位置不会改变；
- start：默认以 0 轴开始，可以根据数组维度调整它的值。

示例如下：

```python
import numpy as np
#创建了三维的 ndarray
a = np.arange(8).reshape(2,2,2) 
#原数组
print (a)
#where方法返回值在数组中的位置
print(np.where(a==6))  
#获取数组中一个值
print(a[1,1,0])

# 将轴 2 滚动到轴 0（宽度到深度）
b = np.rollaxis(a,2,0)
print (b)
# 查看元素 a[1,1,0]，即 6 的坐标，变成 [0, 1, 1]
# 最后一个 0 移动到最前面
print(np.where(b==6)) 

# 将轴 2 滚动到轴 1：（宽度到高度）
c = np.rollaxis(a,2,1)
print (c)
# 查看元素 a[1,1,0]，即 6 的坐标，变成 [1, 0, 1]
# 最后的 0 和 它前面的 1 对换位置
print(np.where(c==6))
```

输出结果：

```
[[[0 1]
  [2 3]]

 [[4 5]
  [6 7]]]
  
(array([1], dtype=int64), array([1], dtype=int64), array([0], dtype=int64))

6

[[[0 2]
  [4 6]]

 [[1 3]
  [5 7]]]
  
(array([0], dtype=int64), array([1], dtype=int64), array([1], dtype=int64))

[[[0 2]
  [1 3]]

 [[4 6]
  [5 7]]]
  
(array([1], dtype=int64), array([0], dtype=int64), array([1], dtype=int64))
```

总结来说就是：将数组`arr`所对应的`axis`轴 放在`start`轴的前面，`start`轴往后移一“列”

### 3) numpy.swapaxes()

该方法用于交换数组的两个轴，其语法格式如下：

```
numpy.swapaxes(arr, axis1, axis2) 
```

- `arr`：输入的数组
- `axis1`：对应第一个轴的整数
- `axis2`：对应第二个轴的整数

示例如下：

```python
import numpy as np
# 创建了三维的 ndarray
a = np.arange(8).reshape(2,2,2) 
print (a)
#对换0轴与2轴
print(np.swapaxes(a,2,0))
```

输出结果：

```
[[[0 1]
  [2 3]]

 [[4 5]
  [6 7]]]
  
[[[0 4]
  [2 6]]

 [[1 5]
  [3 7]]]
```

这个函数就更好理解了，即是将数组`arr`所对应的`axis1`轴和`axis2`轴交换位置即可

## 修改数组维度操作

修改数组维度的操作，主要有以下方法：

| 函数名称     | 描述说明                   |
| ------------ | -------------------------- |
| broadcast    | 生成一个模拟广播的对象。   |
| broadcast_to | 将数组广播为新的形状。     |
| expand_dims  | 扩展数组的形状。           |
| squeeze      | 从数组的形状中删除一维项。 |

### 1) numpy.broadcast()

用于模仿广播的对象，它返回一个对象，该对象封装了将一个数组广播到另一个数组的结果，该函数以两个数组作为输入参数，实例如下：

```python
import numpy as np
a = np.array([[1], [2], [3]])
b = np.array([4, 5, 6]) 
# 对b广播a
d = np.broadcast(a,b) 
#d它拥有 iterator 属性
r,c = d.iters
print (next(r), next(c))
print (next(r), next(c))
# 使用broadcast将a与b相加
e = np.broadcast(a,b)
f=np.zeros(e.shape)
f.flat=[x+y for (x,y) in e]
print(f)
print(a+b)
```

输出结果：

```
1 4

1 5

[[5. 6. 7.]
 [6. 7. 8.]
 [7. 8. 9.]]
 
[[5 6 7]
 [6 7 8]
 [7 8 9]]
```

### 2) numpy.broadcast_to()

该函数将数组广播到新形状中，它在原始数组的基础上返回一个只读视图。 如果新形状不符合 NumPy 的广播规则，则会抛出 ValueError 异常。函数的语法格式如下：

```
numpy.broadcast_to(array, shape, subok)
```

使用实例如下所示：

```python
import numpy as np
a = np.arange(4).reshape(1,4)
#原数组
print(a)
#调用 broadcast_to 函数之后
print (np.broadcast_to(a,(4,4)))
```

最后的输出结果如下：

```
[[0 1 2 3]]

[[0 1 2 3]
 [0 1 2 3]
 [0 1 2 3]
 [0 1 2 3]]
```

### 3) numpy.expand_dims()

在指定位置插入新的轴，从而扩展数组的维度，语法格式如下:

```python
numpy.expand_dims(arr, axis)
```

参数说明：

- arr：输入数组
- axis：新轴插入的位置

实例如下：

```python
import numpy as np
x = np.array(([1,2],[3,4]))
#数组 x
print (x)
# 在 0 轴处插入新的轴
y = np.expand_dims(x, axis = 0)
#数组 y
print (y)
#数组 x 和 y 的形状
print (x.shape, y.shape)
```

输出结果：

```
[[1 2]
 [3 4]]
 
[[[1 2]
  [3 4]]]
  
(2, 2) (1, 2, 2)
```

### 4) numpy.squeeze()

删除数组中维度为 1 的项，例如，一个数组的 shape 是 (5,1)，经此函数后，shape 变为 (5,) 。其函数语法格式如下：

```
numpy.squeeze(arr, axis)
```

参数说明：

- arr：输入数的组；
- axis：取值为整数或整数元组，用于指定需要删除的维度所在轴，指定的维度值必须为 1 ，否则将会报错，若为 None，则删除数组维度中所有为 1 的项。

下面是带有 axis 参数的实例：

```python
import numpy as np
x = np.array([[[0], [1], [2]]])
print(x.shape)
print(np.squeeze(x).shape)
print(np.squeeze(x, axis=(2,)).shape)
```

输出结果：

```
(1, 3, 1)
(3,)
(1, 3)
```

## 连接数组操作

| 函数          | 描述                           |
| :------------ | :----------------------------- |
| `concatenate` | 连接沿现有轴的数组序列         |
| `stack`       | 沿着新的轴加入一系列数组。     |
| `hstack`      | 水平堆叠序列中的数组（列方向） |
| `vstack`      | 竖直堆叠序列中的数组（行方向） |

### 1) numpy.concatenate() 

沿指定轴连接相同形状的两个或多个数组，格式如下：

```
numpy.concatenate((a1, a2, ...), axis)
```

参数说明：

- a1, a2, ...：表示一系列相同类型的数组；
- axis：沿着该参数指定的轴连接数组，默认为 0。

实例说明：创建两个 a 、b 数组，并沿指定轴将它们连接起来。注意两个数组的形状要保持一致。

```python
import numpy as np
#创建数组a
a = np.array([[10,20],[30,40]])
print (a)
#创建数组b
b = np.array([[50,60],[70,80]])
print (b)
#沿轴 0 连接两个数组
print (np.concatenate((a,b)))
#沿轴 1 连接两个数组
print (np.concatenate((a,b),axis = 1))
```

输出结果：

```
[[10 20]
 [30 40]]
 
[[50 60]
 [70 80]]
 
[[10 20]
 [30 40]
 [50 60]
 [70 80]]
 
[[10 20 50 60]
 [30 40 70 80]]
```

数组连接操作至少需要两个维度相同的数组，才允许对它们进行垂直或者水平方向上的操作。

### 2) numpy.stack()

numpy.stack 函数用于沿新轴连接数组序列，格式如下：

```
numpy.stack(arrays, axis)
```

参数说明：

- `arrays`相同形状的数组序列
- `axis`：返回数组中的轴，输入数组沿着它来堆叠

```python
import numpy as np
#创建数组a
a = np.array([[10,20],[30,40]])
print (a)
#创建数组b
b = np.array([[50,60],[70,80]])
print (b)
#沿轴 0 堆叠两个数组
print (np.stack((a,b),0))
print ('\n')
#沿轴 1 堆叠两个数组
print (np.stack((a,b),1))
```

输出结果：

```
[[10 20]
 [30 40]]
 
[[50 60]
 [70 80]]
 
[[[10 20]
  [30 40]]

 [[50 60]
  [70 80]]]

[[[10 20]
  [50 60]]

 [[30 40]
  [70 80]]]
```

### 3) numpy.hstack()

numpy.hstack 是 numpy.stack 函数的变体，它通过水平堆叠来生成数组。示例如下：

```python
import numpy as np
a = np.array([[1,2],[3,4]])
b = np.array([[5,6],[7,8]])
#水平堆叠
c = np.hstack((a,b))
print (c)
```

输出结果：

```
[[1 2 5 6]
 [3 4 7 8]]
```

### 4) numpy.vstack()

numpy.vstack 是 numpy.stack 函数的变体，它通过垂直堆叠来生成数组。示例如下：

```python
import numpy as np
a = np.array([[1,2],[3,4]])
b = np.array([[5,6],[7,8]])
#垂直堆叠
c = np.vstack((a,b))
print (c)
```

输出结果：

```
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
```

## 分割数组操作

| 函数     | 数组及操作                             |
| :------- | :------------------------------------- |
| `split`  | 将一个数组分割为多个子数组             |
| `hsplit` | 将一个数组水平分割为多个子数组（按列） |
| `vsplit` | 将一个数组垂直分割为多个子数组（按行） |

### 1) numpy.split()

numpy.split() 沿指定的轴将数组分割为多个子数组，语法格式如下：

```python
numpy.split(ary, indices_or_sections, axis)
```

参数说明：

- ary：被分割的数组
- indices_or_sections：若是一个整数，代表用该整数平均切分，若是一个数组，则代表沿轴切分的位置（左开右闭）；
- axis：默认为0，表示横向切分；为1时表示纵向切分。

示例如下所示：

```python
import numpy as np
a = np.arange(9)
#原数组
print (a)
#将数组分为三个形状大小相等的子数组
b = np.split(a,3)
print (b)
#将数组在一维数组中标明要位置分割
b = np.split(a,[4,7])
print (b)
```

输出结果：

```
[0 1 2 3 4 5 6 7 8]

[array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]

[array([0, 1, 2, 3]), array([4, 5, 6]), array([7, 8])]
```

axis 为 0 时在水平方向分割，axis 为 1 时在垂直方向分割：

```python
import numpy as np
a = np.arange(16).reshape(4, 4)
#第一个数组
print(a)
#默认分割（0轴）
b = np.split(a,2)
print(b)
#沿水平方向分割
c = np.split(a,2,1)
print(c)
```

输出结果：

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]]
 
[array([[0, 1, 2, 3],
       [4, 5, 6, 7]]), array([[ 8,  9, 10, 11],
       [12, 13, 14, 15]])]
       
[array([[ 0,  1],
       [ 4,  5],
       [ 8,  9],
       [12, 13]]), array([[ 2,  3],
       [ 6,  7],
       [10, 11],
       [14, 15]])]
```

### 2) numpy.hsplit()

numpy.hsplit 函数用于水平分割数组，通过指定要返回的相同形状的数组数量来拆分原数组，示例如下：

```python
import numpy as np
#arr1数组
arr1 = np.floor(10 * np.random.random((2, 6)))
print(arr1)
#拆分后数组
print(np.hsplit(arr1, 3))
```

输出结果：

```
[[6. 8. 2. 6. 3. 6.]
 [1. 4. 6. 4. 0. 0.]]
 
[array([[6., 8.],
       [1., 4.]]), array([[2., 6.],
       [6., 4.]]), array([[3., 6.],
       [0., 0.]])]
```

### 3) numpy.vsplit()

numpy.vsplit 沿着垂直轴分割，其分割方式与hsplit用法相同，示例如下：

```python
import numpy as np
#arr1数组
arr1 = np.floor(10 * np.random.random((6, 2)))
print(arr1)
#拆分后数组
print(np.vsplit(arr1, 3))
```

输出结果：

```
[[0. 7.]
 [6. 3.]
 [9. 6.]
 [8. 8.]
 [8. 6.]
 [6. 2.]]
 
[array([[0., 7.],
       [6., 3.]]), array([[9., 6.],
       [8., 8.]]), array([[8., 6.],
       [6., 2.]])]
```

## 数组元素的添加与删除

| 函数       | 元素及描述                               |
| :--------- | :--------------------------------------- |
| `resize`   | 返回指定形状的新数组                     |
| `append`   | 将值添加到数组末尾                       |
| `insert`   | 沿指定轴将值插入到指定下标之前           |
| `delete`   | 删掉某个轴的子数组，并返回删除后的新数组 |
| `argwhere` | 返回数组内符合条件的元素的索引值         |
| `unique`   | 查找数组内的唯一元素                     |

### 1) numpy.resize()

numpy.resize 函数返回指定大小的新数组。如果新数组大小大于原始大小，则包含原始数组中的元素的副本。

```python
numpy.resize(arr, shape)
```

参数说明：

- `arr`：要修改大小的数组
- `shape`：返回数组的新形状

示例如下：

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6]])
print(a)
#a数组的形状
print(a.shape)
b = np.resize(a,(3,2))
#b数组
print (b)
#b数组的形状
print(b.shape)
#修改b数组使其形状大于原始数组
b = np.resize(a,(3,3))
print(b)
```

输出结果：

```
[[1 2 3]
 [4 5 6]]
 
(2, 3)

[[1 2]
 [3 4]
 [5 6]]
 
(3, 2)

[[1 2 3]
 [4 5 6]
 [1 2 3]]
```

这里需要区别 resize() 和 reshape() 的使用方法，它们看起来相似，实则不同。resize 仅对原数组进行修改，没有返回值，而 reshape 不仅对原数组进行修改，同时返回修改后的结果。看一组示例，如下所示：

```python
import numpy as np
x=np.arange(12)
#调用resize方法
x_resize=x.resize(2,3,2)
print(x)
print(x_resize)

x_reshape=x.reshape(2,3,2)
print(x)
print(x_reshape)
```

输出结果：

```
[[0 1 2]
 [3 4 5]]
 
None

[[0 1 2]
 [3 4 5]]
 
[[0 1 2]
 [3 4 5]]
```

### 2) numpy.append()

numpy.append 函数在数组的末尾添加值。 追加操作会分配整个数组，并把原来的数组复制到新数组中。 此外，输入数组的维度必须匹配否则将生成ValueError。

append 函数返回的始终是一个一维数组。

```python
numpy.append(arr, values, axis=None)
```

参数说明：

- `arr`：输入数组
- `values`：要向`arr`添加的值，需要和`arr`形状相同（除了要添加的轴）
- `axis`：默认为 None。当axis无定义时，是横向加成，返回总是为**一维数组**！当axis有定义的时候，分别为0和1的时候。当axis有定义的时候，分别为0和1的时候（列数要相同）。当axis为1时，数组是加在右边（行数要相同）。

使用示例：

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6]])
#向数组a添加元素
print (np.append(a, [7,8,9]))
#沿轴 0 添加元素
print (np.append(a, [[7,8,9]],axis = 0))
#沿轴 1 添加元素
print (np.append(a, [[5,5,5],[7,8,9]],axis = 1))
```

输出结果：

```
[[1 2 3]
 [4 5 6]]
 
[1 2 3 4 5 6 7 8 9]

[[1 2 3]
 [4 5 6]
 [7 8 9]]
 
[[1 2 3 5 5 5]
 [4 5 6 7 8 9]]
```

### 3) numpy.insert()

numpy.insert 函数在给定索引之前，沿给定轴在输入数组中插入值。如果未提供轴，则输入数组会被展开。

```python
numpy.insert(arr, obj, values, axis)
```

参数说明：

- `arr`：输入数组
- `obj`：在其之前插入值的索引
- `values`：要插入的值
- `axis`：沿着它插入的轴，如果未提供，则输入数组会被展开

示例如下：

```python
import numpy as np
a = np.array([[1,2],[3,4],[5,6]])
#不提供axis的情况，会将数组展开
print (np.insert(a,3,[11,12]))
#沿轴 0 垂直方向
print (np.insert(a,1,[11],axis = 0))
#沿轴 1 水平方向
print (np.insert(a,1,11,axis = 1))
```

输出结果：

```
[ 1  2  3 11 12  4  5  6]

[[ 1  2]
 [11 11]
 [ 3  4]
 [ 5  6]]
 
[[ 1 11  2]
 [ 3 11  4]
 [ 5 11  6]]
```

### 4) numpy.delete()

numpy.delete 函数返回从输入数组中删除指定子数组的新数组。 与 insert() 函数的情况一样，如果未提供轴参数，则输入数组将展开。

```
Numpy.delete(arr, obj, axis)
```

参数说明：

- `arr`：输入数组
- `obj`：可以被切片，整数或者整数数组，表明要从输入数组删除的子数组
- `axis`：沿着它删除给定子数组的轴，如果未提供，则输入数组会被展开

使用示例：

```python
import numpy as np
a = np.arange(12).reshape(3,4)
#a数组
print(a)
#不提供axis参数情况
print(np.delete(a,5))
#删除第二列
print(np.delete(a,1,axis = 1))
#删除经切片后的数组
print (np.delete(a, np.s_[::2]))
```

输出结果：

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
 
[ 0  1  2  3  4  6  7  8  9 10 11]

[[ 0  2  3]
 [ 4  6  7]
 [ 8 10 11]]
 
[ 1  3  5  7  9 11]
```

### 5) numpy.unique()

numpy.unique 函数用于去除数组中的重复元素。

```
numpy.unique(arr, return_index, return_inverse, return_counts)
```

- `arr`：输入数组，如果不是一维数组则会展开
- `return_index`：如果为`true`，返回新列表元素在旧列表中的位置（下标），并以列表形式储
- `return_inverse`：如果为`true`，返回旧列表元素在新列表中的位置（下标），并以列表形式储
- `return_counts`：如果为`true`，返回去重数组中的元素在原数组中的出现次数

示例如下：

```python
import numpy as np
a = np.array([5,2,6,2,7,5,6,8,2,9])
print (a)
#对a数组的去重
uq = np.unique(a)
print (uq)
#数组去重后的数字在原数组的索引
u,indices = np.unique(a, return_index = True)
#打印去重后数组的索引
print(indices)
#去重数组的下标：
ui,indices = np.unique(a,return_inverse = True)
print (indices)
#返回去重元素的重复数量
uc,indices = np.unique(a,return_counts = True)
print (indices)
```

输出结果为：

```
#a数组
[5 2 6 2 7 5 6 8 2 9]
#去重后的a数组
[2 5 6 7 8 9]
#去重数组的索引数组
[1 0 2 4 7 9]
#原数组在新数组中的下标
[1 0 2 0 3 1 2 4 0 5]
#统计重复元素出现次数
[3 2 2 1 1 1]
```



