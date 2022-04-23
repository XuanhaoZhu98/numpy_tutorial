# 15 NumPy 排序和条件函数

## Numpy排序函数

NumPy 提供了多种排序函数， 这些排序函数可以实现不同的排序算法。

排序算法特征主要体现在以下四个方面：执行速度，最坏情况下的复杂度，所需的工作空间以及算法的稳定性。下表列举了三种排序算法：

| 种类                  | 速度 | 最坏复杂度     | 工作空间 | 稳定性 |
| --------------------- | ---- | -------------- | -------- | ------ |
| quicksort（快速排序） | 1    | O(n^2)         | 0        | 不稳定 |
| mergesort（归并排序） | 2    | O(n * log(n)） | ~n/2     | 稳定   |
| heapsort（堆排序）    | 3    | O(n * log(n))  | 0        | 不稳定 |

### 1) numpy.sort()

numpy.sort() 对输入数组执行排序，并返回一个数组副本。它具有以下参数：

```
numpy.sort(a, axis, kind, order)
```

参数说明：

- a：要排序的数组；
- axis：沿着指定轴进行排序，如果没有指定 axis，默认在最后一个轴上排序，若 axis=0 表示按列排序，axis=1 表示按行排序；
- kind：默认为 quicksort（快速排序）；
- order：若数组设置了字段，则 order 表示要排序的字段。


下面看一组示例：

```python
import numpy as np 
a = np.array([[3,7],[9,1]]) 
print(a)
#按行排序
print(np.sort(a))
#按列排序：
print(np.sort(a, axis = 0))

#设置在sort函数中排序字段
dt = np.dtype([('name',  'S10'),('age',  int)])
a = np.array([("raju",21),("anil",25),("ravi",  17),  ("amar",27)], dtype = dt) 
#再次打印a数组
print(a)
#按name字段排序
print(np.sort(a, order = 'name'))
```

输出结果：

```
[[3 7]
 [9 1]]
 
[[3 7]
 [1 9]]
 
[[3 1]
 [9 7]]
 
[(b'raju', 21) (b'anil', 25) (b'ravi', 17) (b'amar', 27)]

[(b'amar', 27) (b'anil', 25) (b'raju', 21) (b'ravi', 17)]

```

### 2) numpy.argsort()

argsort() 沿着指定的轴，对输入数组的元素值进行排序，并返回排序后的元素索引数组。示例如下：

```python
import numpy as np 
a = np.array([90, 29, 89, 12]) 
print(a) 
sort_ind = np.argsort(a) 
#打印排序元素索引值
print(sort_ind) 
#使用索引数组对原数组排序
sort_a = a[sort_ind] 
print(sort_a)
#打印排序数组
for i in sort_ind: 
    print(a[i],end = " ")  
```

输出结果：

```
[90 29 89 12]
[3 1 2 0]
[12 29 89 90]
12 29 89 90 
```

### 3) numpy.lexsort()

numpy.lexsort() 按键序列对数组进行排序，它返回一个已排序的索引数组，类似于 numpy.argsort()。序列中的最后一个键用于主排序顺序，倒数第二个键用于辅助排序顺序

函数语法：

```python
numpy.lexsort(keys, axis=- 1)
```

参数说明：

* keys： (k, N) 数组或包含 k (N,) 形序列的元组。k 个不同的“columns” 进行排序。最后一列(如果键是二维数组，则为行)是主排序键。

* axis： 整数，可选。要间接排序的轴。默认情况下，对最后一个轴进行排序。

示例如下：

```python
import numpy as np 
a = np.array(['a','b','c','d','e']) 
b = np.array([12, 90, 380, 12, 211]) 
ind = np.lexsort((a,b)) 
#打印排序元素的索引数组
print(ind) 
#使用索引数组对数组进行排序
for i in ind: 
    print(a[i],b[i])  
```

输出结果：

```
[0 3 1 4 2]

a 12
d 12
b 90
e 211
c 380
```


NumPy 提供了许多可以在数组内执行搜索功能的函数。比如查找最值或者满足一定条件的元素。

### 4) numpy.msort()

数组按第一个轴排序，返回排序后的数组副本。np.msort(a) 相等于 np.sort(a, axis=0)。示例如下：

```python
import numpy as np 
a = np.array([[3,7],[9,1]]) 
print(a)
#按列排序
print(np.msort(a))
```

输出结果：

```
[[3 7]
 [9 1]]
 
[[3 1]
 [9 7]]
```

### 5) numpy.sort_complex()

对复数按照先实部后虚部的顺序进行排序。示例如下：

```python
import numpy as np
print(np.sort_complex([5, 3, 6, 2, 1]))
print(np.sort_complex([1 + 2j, 2 - 1j, 3 - 2j, 3 - 3j, 3 + 5j]))
```

输出结果：

```
[1.+0.j 2.+0.j 3.+0.j 5.+0.j 6.+0.j]
[1.+2.j 2.-1.j 3.-3.j 3.-2.j 3.+5.j]
```

### 6) numpy.partition() 

numpy.partition()函数用于创建输入数组的分区副本，并对其元素进行重新排列。将其中的元素重新整理，**使得第k位的元素刚好是全排序第k位的元素**。所有小于第k个元素的元素都被移到这个元素前面，所有等于或大于这个元素的元素都被移到它后面。这两个**分区中元素的顺序是未定义的**。

平时用惯了全排序np.sort()，复杂度在O(n log n)到O(n^2)之间。如果待排序的数组特别大的话，时间开销不小。但通常特别大的数组排序不需要进行全排，可能**仅仅需要取Top K**。此时就可以使用部分排序，比如numpy.partition()和numpy.argpartition()。

函数语法：

```python
numpy.partition(arr, kth, axis=-1, kind=’introselect’, order=None)
```

参数说明：

arr：输入数组；
kth：分区依据的元素索引；
axis：要排序的轴。如果为None，则在排序之前将数组展平。默认值为-1，它沿着最后一个轴排序；
kind：选择算法。默认值为'introselect'；
order ：当arr是定义了字段的数组时，此参数指定要比较第一个，第二个等的字段。单个字段可以指定为字符串，并且不需要指定所有字段，但是仍将使用未指定的字段。

示例如下：

```python
a = np.array([3, 4, 2, 1, 5, 6 ,7])
k = 5
b = np.partition(a, k)
print(b)
print(a[k])
m = (1, 3)
c = np.partition(a, m)
print(c)
print(c[m[0]], c[m[1]])
```

输出结果：

```
[2 1 3 4 5 6 7]
6

[1 2 3 4 5 6 7]
2 4
```

### 7) numpy.argpartition()

*使用kind*关键字指定的算法沿给定轴执行间接分区。它以分区顺序沿给定轴返回与该索引数据具有相同形状*的*索引数组。

函数语法：

```python
numpy.argpartition(a, kth, axis=-1, kind='introselect', order=None) 
```

示例如下：

```python
#找到数组的第 3 小（index=2）的值和第 2 大（index=-2）的值
arr = np.array([46, 57, 23, 39, 1, 10, 0, 120])
index = np.argpartition(arr, 2)
print(index)
print(arr[index[2]]) 
index = np.argpartition(arr, -2)
print(index)
print(arr[index[-2]]) 
```

输出结果：

```
[6 4 5 3 1 2 0 7]
10
[5 3 2 6 4 0 1 7]
57
```

## Numpy条件函数

### 1) numpy.nonzero()

该函数从数组中查找非零元素的索引位置。示例如下：

```python
import numpy as np 
b = np.array([12, 9, 0, 38, 0, 12, 21, 1]) 
print(b) 
#非0元素的索引位置
print(b.nonzero())  
```


输出结果：

```
[12  9  0 38  0 12 21  1]

(array([0, 1, 3, 5, 6, 7], dtype=int64),)
```

### 2) numpy.where()

numpy.where() 的返回值是满足了给定条件的元素索引值。

```python
import numpy as np 
x = np.arange(9).reshape(3,  3)  
print (x)
#大于 3 的元素的索引
y = np.where(x >  3)  
print (y)
#使用这些索引来获取满足条件的元素
print (x[y])
```


输出结果：

```
[[0 1 2]
 [3 4 5]
 [6 7 8]]
 
(array([1, 1, 2, 2, 2], dtype=int64), array([1, 2, 0, 1, 2], dtype=int64))

[4 5 6 7 8]
```

### 3) numpy.argwhere()

该函数返回数组中非 0 元素的索引，若是多维数组则返回行、列索引组成的索引坐标。

* `arr`：输入数组

示例如下所示：

```python
import numpy as np
x = np.arange(6).reshape(2,3)
print(x)
#返回所有大于1的元素索引
y=np.argwhere(x>1)
print(y)
```

输出结果：

```
[[0 1 2]
 [3 4 5]]
 
[[0 2]
 [1 0]
 [1 1]
 [1 2]]
```

获得查找值的索引值案例：

```python
import numpy as np
arr = np.array([1,2,4,0,4,0])
n = np.argwhere(arr==4)
print(n)
```

输出结果：

```
[[2]
 [4]]
```

### 4) numpy.extract()

该函数的返回值是满足了给定条件的元素值，示例如下：

```python
import numpy as np
x = np.arange(9.).reshape(3, 3)
print(x) 
#设置条件选择偶数元素
condition = np.mod(x,2)== 0
#输出布尔值数组
print(condition)
#按condition提取满足条件的元素值
print np.extract(condition, x)
```

输出结果：

```
[[0. 1. 2.]
 [3. 4. 5.]
 [6. 7. 8.]]
 
[[ True False  True]
 [False  True False]
 [ True False  True]]
 
[0. 2. 4. 6. 8.]
```

### 5) numpy.argmax()

该函数返回最大值的的索引，与其相反的函数是 argmin() 求最小值索引 ，示例如下：

```python
import numpy as np
a = np.array([[30,40,70],[80,20,10],[50,90,60]]) 
#a数组
print (a)
#展开数组中的最大值索引
print (np.argmax(a))
#沿轴 0 的最大值索引：
maxindex = np.argmax(a, axis =  0) 
print (maxindex)
#沿轴 1 的最大值索引
maxindex = np.argmax(a, axis =  1) 
print (maxindex) 
```

输出结果：

```
[[30 40 70]
 [80 20 10]
 [50 90 60]]
 
7

[1 2 0]

[2 0 1]
```

### 6) numpy.argmin()

argmin() 求最小值索引。示例如下：

```python
import numpy as np
b= np.array([[3,4,7],[8,2,1],[5,9,6]]) 
print (b) 
#展开数组中的最小值索引
minindex = np.argmin(b) 
print (minindex)
#沿轴 0 的最小值索引
minindex = np.argmin(b, axis =  0) 
print (minindex)
#沿轴 1 的最小值索引
minindex = np.argmin(b, axis =  1) 
print (minindex)
```

输出结果：

```
[[3 4 7]
 [8 2 1]
 [5 9 6]]
 
5

1

[0 1 1]

[0 2 0]
```

