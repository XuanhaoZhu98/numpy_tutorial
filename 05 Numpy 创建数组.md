# 05 Numpy 创建数组

## numpy.empty()

numpy.empty() 创建未初始化的数组，可以指定创建数组的形状（shape）和数据类型（dtype），语法格式如下：

```python
numpy.empty(shape, dtype = float, order = 'C')
```

它接受以下参数：

- shape：指定数组的形状；
- dtype：数组元素的数据类型，默认值是值 float；
- order：有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序，默认顺序是“C”(行优先顺序)。

使用示例如下：

```python
import numpy as np 
arr = np.empty((3,2), dtype = int) 
print(arr) 
```

输出结果：

```
[[1678205957 1509983240]
 [1392665606 -636868352]
 [1868783371 1919252078]]
```

可以看到，numpy.empty() 返回的数组带有随机值，但这些数值并没有实际意义。切记 empty 并非创建空数组。empty与zeros不同，它不会将数组值设置为零，因此可能会稍微快一些。另一方面，它需要用户手动设置数组中的所有值，应谨慎使用。

## numpy.zeros()

该函数用来创建元素均为 0 的数组，同时还可以指定被数组的形状，语法格式如下：

```
numpy. zeros(shape,dtype=float,order="C")
```

| 参数名称 | 说明描述                                   |
| -------- | ------------------------------------------ |
| shape    | 指定数组的形状大小。                       |
| dtype    | 可选项，数组的数据类型                     |
| order    | “C”代表以行顺序存储，“F”则表示以列顺序存储 |

示例如下：

```python
import numpy as np
#默认数据类型为浮点数
a=np.zeros(6)
print(a)
b=np.zeros(6,dtype="complex64" )
print(b)
```

输出结果：

```
[0. 0. 0. 0. 0. 0.]

[0.+0.j 0.+0.j 0.+0.j 0.+0.j 0.+0.j 0.+0.j]
```

也可以使用自定义的数据类型创建数组，如下所示：

```python
c = np.zeros((3,3), dtype = [('x', 'i4'), ('y', 'i4')]) 
print(c)
```

输出结果：

```
[[(0, 0) (0, 0) (0, 0)]
 [(0, 0) (0, 0) (0, 0)]
 [(0, 0) (0, 0) (0, 0)]]
```

## numpy.ones()

返回指定形状大小与数据类型的新数组，并且新数组中每项元素均用 1 填充，语法格式如下：

```python
numpy.ones(shape, dtype = None, order = 'C')
```

示例如下：

```python
import numpy as np 
arr1 = np.ones((3,2), dtype = int) 
print(arr1)  
```

输出结果如下：

```
[[1 1]
 [1 1]
 [1 1]]
```

下面介绍如何使用 Python 列表、流对象、可迭代对象来创建一个 NumPy 数组。

## numpy.asarray()

asarray() 与 array() 类似，但是它比 array() 更为简单。asarray() 能够将一个 Python 序列  (list)转化为 ndarray 对象，语法格式如下：

```
numpy.asarray（sequence，dtype = None ，order = None ）
```

参数说明：

| 参数     | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| sequence | 任意形式的输入参数，可以是，列表, 列表的元组, 元组, 元组的元组, 元组的列表，多维数组 |
| dtype    | 数据类型，可选                                               |
| order    | 可选，有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |

将列表转化为 numpy 数组：

```python
import numpy as np 
l=[1,2,3,4,5,6,7] 
print(type(l))
a = np.asarray(l); 
print(type(a)) 
print(a) 
```

输出结果：

```
<class 'list'>
<class 'numpy.ndarray'>
[1 2 3 4 5 6 7]
```

使用元组创建 numpy 数组：

```python
import numpy as np 
l=(1,2,3,4,5,6,7)
print(type(l))
a = np.asarray(l); 
print(type(a)) 
print(a)  
```

输出结果：

```
<class 'tuple'>
<class 'numpy.ndarray'>
[1 2 3 4 5 6 7]
```

使用嵌套列表创建多维数组：

```python
import numpy as np 
l=[[1,2,3],[4, 5, 6]] 
a = np.asarray(l); 
print(type(a))
print(type(a[0])) 
print(a)

l=[[1,2,3,4,5,6,7],[8,9]] 
#不推荐从不规则的嵌套序列创建 ndarray
#如果打算这样做，则必须在创建 ndarray 时指定“dtype=object”
a = np.asarray(l, dtype=object); 
print(type(a))
print(type(a[0])) 
print(a) 
```

输出结果：

```
<class 'numpy.ndarray'>
<class 'numpy.ndarray'>
[[1 2 3]
 [4 5 6]]
 
<class 'numpy.ndarray'>
<class 'list'>
[list([1, 2, 3, 4, 5, 6, 7]) list([8, 9])]
```

## numpy.frombuffer()

表示使用指定的缓冲区创建数组，用于实现动态数组。numpy.frombuffer 接受 buffer 输入参数，以流的形式读入转化成 ndarray 对象。

下面给出了该函数的语法格式：

```python
numpy.frombuffer(buffer, dtype = float, count = -1, offset = 0)
```

它的参数说明如下所示：

| 参数   | 描述                                         |
| :----- | :------------------------------------------- |
| buffer | 可以是任意对象，会以流的形式读入。           |
| dtype  | 返回数组的数据类型，可选，默认是 float32；   |
| count  | 读取的数据数量，默认为-1，表示读取所有数据。 |
| offset | 读取的起始位置，默认为0。                    |

示例如下：

```python
import numpy as np 
#字节串类型
l = b'hello world' 
print(type(l)) 
a = np.frombuffer(l, dtype = "S1") 
print(a) 
print(type(a)) 
```

输出结果：

```
<class 'bytes'>
[b'h' b'e' b'l' b'l' b'o' b' ' b'w' b'o' b'r' b'l' b'd']
<class 'numpy.ndarray'>
```

## numpy.fromiter()

该方法可以把迭代对象转换为 ndarray 数组，其返回值是一个一维数组。

```python
numpy.fromiter(iterable, dtype, count = -1)
```

参数说明：

| 参数名称 | 描述说明                                  |
| -------- | ----------------------------------------- |
| iterable | 可迭代对象。                              |
| dtype    | 返回数组的数据类型。                      |
| count    | 读取的数据数量，默认为 -1，读取所有数据。 |

使用内置 range() 函数创建列表对象，然后使用迭代器创建 ndarray 对象，代码如下：

```python
import numpy as np
# 使用 range 函数创建列表对象 
list=range(6)
#生成可迭代对象i
i=iter(list)
print(type(i))
#使用i迭代器，通过fromiter方法创建ndarray
array=np.fromiter(i, dtype=float)
print(array)
```

输出结果：

```
<class 'range_iterator'>
[0. 1. 2. 3. 4. 5.]
```

## numpy.arange()

在 NumPy 中，您可以使用 arange() 来创建给定数值范围的数组，语法格式如下：

```python
numpy.arange(start, stop, step, dtype)
```

参数说明见下表：

| 参数名称 | 参数说明                                   |
| -------- | ------------------------------------------ |
| start    | 起始值，默认是 0。                         |
| stop     | 终止值，注意生成的数组元素值不包含终止值。 |
| step     | 步长，默认为 1。                           |
| dtype    | 可选参数，指定 ndarray 数组的数据类型。    |

根据`start`与`stop`指定的范围以及`step`步长值，生成一个 ndarray 数组，示例如下。

```python
import numpy as np
x = np.arange(8) 
print (x)
```

输出结果如下所示：

```
[0 1 2 3 4 5 6 7]
```

设置 start 、stop 值以及步长，最终输出 0-10 中的奇数：

```python
import numpy as np
x = np.arange(1,10,2) 
print (x)
```

输出结果如下所示：

```
[1 3 5 7 9]
```

## numpy.linspace()

表示在指定的数值区间内，返回均匀间隔的一维等差数组，默认均分 50 份，语法格式如下：

```python
np.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
```

参数说明：

| 参数       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| `start`    | 代表数值区间的起始值                                         |
| `stop`     | 代表数值区间的终止值，如果`endpoint`为`true`，该值包含于数列中 |
| `num`      | 要生成的等步长的样本数量，默认为`50`                         |
| `endpoint` | 该值为 `true` 时，数列中包含`stop`值，反之不包含，默认是True。 |
| `retstep`  | 如果为 True 时，生成的数组中会显示公差项，反之不显示。       |
| `dtype`    | `ndarray` 的数据类型                                         |

示例如下：

```python
import numpy as np
#生成10个样本
a = np.linspace(1,10,10)
print(a)
```

输出结果：

```
[ 1.  2.  3.  4.  5.  6.  7.  8.  9. 10.]
```

下面示例是 endpoint 为 Fasle 时，此时不包含终止值：

```python
import numpy as np 
arr = np.linspace(10, 20, 5, endpoint = False) 
print(arr)  
```

输出结果：

```
[10. 12. 14. 16. 18.]
```

retstep 参数使用示例如下：

```python
import numpy as np
x = np.linspace(1,2,5, retstep = True)
print(x) 
```

输出结果如下，其中 0.25 为等差数列的公差：

```
(array([1.  , 1.25, 1.5 , 1.75, 2.  ]), 0.25)
```

## numpy.logspace()

该函数同样返回一个 ndarray 数组，它用于创建等比数组，语法格式如下：

```python
np.logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None)
```

详细说明：

| 参数名称 | 说明描述                                |
| -------- | --------------------------------------- |
| start    | 序列的起始值：base**start。             |
| stop     | 序列的终止值：base**stop。              |
| num      | 数值范围区间内样本数量，默认为 50。     |
| endpoint | 默认为 True 包含终止值，反之不包含。    |
| base     | 对数函数的 log 底数，默认为10。         |
| dtype    | 可选参数，指定 ndarray 数组的数据类型。 |

使用示例如下：

```python
import numpy as np
a = np.logspace(1.0,2.0, num = 10)
print (a)
```

输出结果：

```
[ 10.          12.91549665  16.68100537  21.5443469   27.82559402
  35.93813664  46.41588834  59.94842503  77.42636827 100.        ]
```

下面是 base = 2 的对数函数，示例如下：

```python
import numpy as np
a = np.logspace(1,10,num = 10, base = 2)
print(a)
```

输出结果:

```
[   2.    4.    8.   16.   32.   64.  128.  256.  512. 1024.]
```