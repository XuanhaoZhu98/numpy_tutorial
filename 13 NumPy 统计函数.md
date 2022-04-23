# 13 NumPy 统计函数

NumPy 提供了许多统计功能的函数，比如查找数组元素的最值、百分位数、方差以及标准差等。

## numpy.amin() 和 numpy.amax()

这两个函数用于计算数组沿指定轴的最小值与最大值：

- amin() 沿指定的轴，查找数组中元素的最小值，并以数组形式返回；
- amax() 沿指定的轴，查找数组中元素的最大值，并以数组形式返回。

对于二维数组来说，axis=1 表示沿着水平方向，axis=0 表示沿着垂直方向。

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204221117313.png)

图1：axis轴

该函数的语法如下：

```python
numpy.amin(arr, axis = None, out = None, keepdims = <no value>)
numpy.amax(arr, axis = None, out = None, keepdims = <no value>)
```

参数说明：

- arr : 输入数组
- axis : 沿其操作的一个或多个轴。默认情况下，将考虑将arr展平。
- out : 用于放置结果的替代输出数组。必须与预期输出具有相同的形状和缓冲区长度
- keepdmis : 如果将其设置为 True，则缩小的轴将作为尺寸为 1 的尺寸留在结果中。

示例如下：

```python
import numpy as np
a = np.array([[3,7,5],[8,4,3],[2,4,9]]) 
#数组a
print(a)
#amin()函数，不指定axis，即axis=None
print (np.amin(a))
#amax()函数
print(np.amax(a))
#指定axis=1
print(np.amin(a,1))
#指定axis=0
print(np.amax(a,axis=0))
```

输出结果如下所示：

```
[[3 7 5]
 [8 4 3]
 [2 4 9]]
 
2
9

[3 3 2]
[8 7 9]
```

## numpy.ptp()

numpy.ptp() 用于计算数组元素中最值之差值，也就是（最大值 - 最小值）。

```py
numpy.ptp(arr, axis=None, out=None, keepdims=<no value>)
```

示例如下：

```python
import numpy as np 
a = np.array([[2,10,20],[80,43,31],[22,43,10]]) 
print(a) 
#不指定axis，即axis=None
print(np.ptp(a))
#指定axis=1
print(np.ptp(a,1)) 
#指定axis=0
print(np.ptp(a,0)) 
```

输出结果：

```
[[ 2 10 20]
 [80 43 31]
 [22 43 10]]
 
78
[18 49 33]
[78 33 21]
```

## numpy.percentile()

百分位数是统计中使用的度量，表示小于这个值的观察值的百分比。该函数表示沿指定轴，计算数组中任意百分比分位数，语法格式如下：

```python
numpy.percentile(a, q, axis=None, out=None, overwrite_input=False, interpolation='linear', keepdims=False)
```

参数说明：

- a：输入数组；
- q：要计算的百分位数，在 0~100 之间；
- axis：沿着指定的轴计算百分位数；
- out：输出数组，要求它必须具有相同的形状和缓冲区长度，所以一般来说可以不进行指定；
- interpolation：当为`True`的时候会将原始数组进行中间计算，简而言之，就是计算完成后销毁原始数组，原始数组就会成为未被定义的状态，这个参数仅仅在数据量非常大的时候才考虑被使用，为了节省内存，一般不做考虑；
- keepdims：有{‘linear’, ‘lower’, ‘higher’, ‘midpoint’, ‘nearest’}五种可选参数，不同种的插值方式。

百分位数含义：

第 p 个百分位数是这样一个值，它使得至少有 p% 的数据项小于或等于这个值，且至少有 (100-p)% 的数据项大于或等于这个值。

举个例子：高等院校的入学考试成绩经常以百分位数的形式报告。比如，假设某个考生在入学考试中的语文部分的原始分数为 54 分。相对于参加同一考试的其他学生来说，他的成绩如何并不容易知道。但是如果原始分数54分恰好对应的是第70百分位数，我们就能知道大约70%的学生的考分比他低，而约30%的学生考分比他高。这里的 p = 70。

示例如下：

```python
import numpy as np 
a = np.array([[2,10,20],[80,43,31],[22,43,10]]) 
print(a) 
#50%分位数，就是a里排序之后的中位数
print (np.percentile(a, 50)) 
#axis=0，在列上求
print (np.percentile(a, 50, axis=0)) 
#axis=1，在行上求
print (np.percentile(a, 50, axis=1)) 
#保持维度不变
print (np.percentile(a, 50, axis=1, keepdims=True))
#沿着axis=0计算25%分位数
print(np.percentile(a,25,0)) 
#沿着axis=1计算75%分位数
print(np.percentile(a,75,1))
```

输出结果：

```
[[ 2 10 20]
 [80 43 31]
 [22 43 10]]
 
22.0

[22. 43. 20.]
[10. 43. 22.]

[[10.]
 [43.]
 [22.]]
 
[12.  26.5 15. ]
[15.  61.5 32.5]
```

## numpy.median()

numpy.median() 用于计算 a 数组元素的中位数（中值）：

```python
import numpy as np
a = np.array([[30,65,70],[80,95,10],[50,90,60]])
print(a)
#axis=None
print (np.median(a))
#沿着axis=0
print (np.median(a, axis = 0))
#沿着axis=1
print(np.median(a, axis = 1))
```

输出结果如下：

```
[[30 65 70]
 [80 95 10]
 [50 90 60]]
 
65.0

[50. 90. 60.]

[65. 80. 60.]
```

## numpy.mean()

该函数表示沿指定的轴，计算数组中元素的算术平均值（即元素之总和除以元素数量）。示例如下：

```python
import numpy as np
a = np.array([[1,2,3],[3,4,5],[4,5,6]]) 
print (a)
#axis=None
print (np.mean(a))
#沿着axis=0
print (np.mean(a, axis =  0))
#沿着axis=1
print (np.mean(a, axis =  1))
```

输出结果：

```
[[1 2 3]
 [3 4 5]
 [4 5 6]]
 
3.6666666666666665

[2.66666667 3.66666667 4.66666667]

[2. 4. 5.]
```

## numpy.average()

加权平均值是将数组中各数值乘以相应的权数，然后再对权重值求总和，最后以权重的总和除以总的单位数（即因子个数）。

numpy.average() 根据在数组中给出的权重，计算数组元素的加权平均值。该函数可以接受一个轴参数 axis，如果未指定，则数组被展开为一维数组。

下面举一个简单的示例：现有数组 [1,2,3,4] 和相应的权重数组 [4,3,2,1]，它的加权平均值计算如下：

```
加权平均值=（1 * 4 + 2 * 3 + 3 * 2 + 4 * 1）/（4 + 3 + 2 + 1）
```

语法格式：

```
numpy.average(a, axis=None, weights=None, returned=False)
```

参数说明：

* 包含要平均的数据的数组；
* axis：沿着指定的轴计算加权平均数；
* weights ：与 a 中的值关联的权重数组。 a 中的每个值都根据其关联的权重对平均值做出贡献。权重数组可以是一维的(在这种情况下，它的长度必须是沿给定轴的 a 的大小)或与 a 具有相同的形状；
* returned：默认为False。如果为True，则返回元组 ( average, sum_of_weights )，否则只返回平均值。

使用 average() 计算加权平均值，代码如下：

```python
import numpy as np
a = np.array([1,2,3,4]) 
print(a)
#average()函数：
print (np.average(a))
# 若不指定权重相当于对数组求均值
we = np.array([4,3,2,1]) 
#调用 average() 函数
print(np.average(a,weights = we))
#returned 为Ture，则返回权重的和 
print(np.average([1,2,3,4],weights = we, returned =  True))
```

输出结果：

```
[1 2 3 4]
2.5
2.0
(2.0, 10.0)
```

在多维数组中，您也可以指定 axis 轴参数。示例如下：

```python
import numpy as np
a = np.arange(6).reshape(3,2) 
#多维数组a
print (a)
#修改后数组
wt = np.array([3,5]) 
print (np.average(a, axis = 1, weights = wt))
#修改后数组
print (np.average(a, axis = 1, weights = wt, returned =  True))
```

输出结果为：

```
[[0 1]
 [2 3]
 [4 5]]
 
[0.625 2.625 4.625]

(array([0.625, 2.625, 4.625]), array([8., 8., 8.]))
```

## np.var() 

方差，在统计学中也称样本方差，如何求得方差呢？首先我们要知道全体样本的的平均值，然后再求得每个样本值与均值之差的平方和，最后对差的平方和求均值，公式如下（其中 n 代表元素个数）：

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204221236894.svg)

图1：方差公式

示例如下：

```python
import numpy as np
print (np.var([1,2,3,4]))
```

输出结果：

```
1.25
```

## np.std()

标准差是方差的算术平方根，用来描述一组数据平均值的分散程度。若一组数据的标准差较大，说明大部分的数值和其平均值之间差异较大；若标准差较小，则代表这组数值比较接近平均值。它的公式如下：

![](https://raw.githubusercontent.com/XuanhaoZhu98/image_hosting/main/img/202204221236893.svg)

NumPy 中使用 np.std() 计算标准差。示例如下：

```python
import numpy as np
print (np.std([1,2,3,4]))
```

输出结果：

```
1.118033988749895
```