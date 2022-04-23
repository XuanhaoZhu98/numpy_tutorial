# 12 NumPy 数学函数

NumPy 中包含了大量的数学函数，它们用于执行各种数学运算，其中包括三角函数、舍入函数等等。下面对它们做详细讲解。

## 三角函数

NumPy 中提供了用于弧度计算的的 sin()（正弦）、cos()（余弦）和 tan()（正切）三角函数。

示例如下：

```python
import numpy as np 
deg = np.array([0, 30, 60, 90, 120, 150, 180]) 
#计算arr数组中给定角度的三角函数值
#通过乘以np.pi/180将其转换为弧度
rad = deg * np.pi/180
print(np.sin(rad)) 
print(np.cos(rad)) 
print(np.tan(rad))
```

输出结果如下：

```
[0.00000000e+00 5.00000000e-01 8.66025404e-01 1.00000000e+00
 8.66025404e-01 5.00000000e-01 1.22464680e-16]
 
[ 1.00000000e+00  8.66025404e-01  5.00000000e-01  6.12323400e-17
 -5.00000000e-01 -8.66025404e-01 -1.00000000e+00]
 
[ 0.00000000e+00  5.77350269e-01  1.73205081e+00  1.63312394e+16
 -1.73205081e+00 -5.77350269e-01 -1.22464680e-16]
```

除了上述三角函数以外，NumPy 还提供了 arcsin，arcos 和 arctan 反三角函数。

若要想验证反三角函数的结果，可以通过 numpy.degrees() 将弧度转换为角度来实现，示例如下：

```python
import numpy as np 
arr = np.array([0, 30, 60, 90]) 
#正弦值数组
sinval = np.sin(arr*np.pi/180) 
print(sinval) 
#计算角度反正弦，返回值以弧度为单位
cosec = np.arcsin(sinval) 
print(cosec) 
#通过degrees函数转化为角度进行验证
print(np.degrees(cosec)) 

#余弦值数组
cosval = np.cos(arr*np.pi/180) 
print(cosval) 
#计算反余弦值，以弧度为单位
sec = np.arccos(cosval) 
print(sec) 
#通过degrees函数转化为角度进行验证
print(np.degrees(sec)) 

#下面是tan()正切函数 
tanval = np.tan(arr*np.pi/180) 
print(tanval) 
cot = np.arctan(tanval) 
print(cot) 
print(np.degrees(cot))  
```

输出结果：

```
[0.        0.5       0.8660254 1.       ]
[0.         0.52359878 1.04719755 1.57079633]
[ 0. 30. 60. 90.]

[1.00000000e+00 8.66025404e-01 5.00000000e-01 6.12323400e-17]
[0.         0.52359878 1.04719755 1.57079633]
[ 0. 30. 60. 90.]

[0.00000000e+00 5.77350269e-01 1.73205081e+00 1.63312394e+16]
[0.         0.52359878 1.04719755 1.57079633]
[ 0. 30. 60. 90.]
```

## 舍入函数

NumPy 提供了三个舍入函数，介绍如下：

### 1) numpy.around() 

该函数返回一个十进制值数，并将数值四舍五入到指定的小数位上。该函数的语法如下：

```
numpy.around(a,decimals)
```

参数说明：

- a：代表要输入的数组；
- decimals：要舍入到的小数位数。它的默认值为0，如果为负数，则小数点将移到整数左侧。

示例如下：

```python
import numpy as np 
arr = np.array([12.202, 90.23120, 123.020, 23.202]) 
print(arr) 
#数组值四舍五入到小数点后两位
print(np.around(arr, 2)) 
#数组值四舍五入到小数点后-1位
print(np.around(arr, -1))  
```

输出结果：

```
[ 12.202   90.2312 123.02    23.202 ]
[ 12.2   90.23 123.02  23.2 ]
[ 10.  90. 120.  20.]
```

### 2) numpy.floor()

该函数表示对数组中的每个元素向下取整数，即返回不大于数组中每个元素值的最大整数。示例如下：

```python
import numpy as np
a = np.array([-1.8,  1.1,  -0.4,  0.9,  18])
#对数组a向下取整
print (np.floor(a))
```

输出结果：

```
[-2.  1. -1.  0. 18.]
```

### 3) numpy.ceil()

该函数与 floor 函数相反，表示向上取整。示例如下：

```python
import numpy as np
a = np.array([-1.8,  1.1,  -0.4,  0.9,  18])
#对数组a向上取整
print (np.ceil(a))
```

输出结果：

```
[-1.  2. -0.  1. 18.]
```

## 算术运算

### 1) numpy.add()/subtract()/multiple()/divide() 

NumPy 数组的“加减乘除”算术运算，分别对应 add()、subtract()、multiple() 以及 divide() 函数。

注意：做算术运算时，输入数组必须具有相同的形状，或者符合数组的广播规则，才可以执行运算。

下面看一组示例：

```python
import numpy as np
a = np.arange(9, dtype = np.float_).reshape(3,3)
#数组a
print(a)
#数组b
b = np.array([10,10,10])
print(b)
#数组加法运算
print(np.add(a,b))
#数组减法运算
print(np.subtract(a,b))
#数组乘法运算
print(np.multiply(a,b))
#数组除法运算
print(np.divide(a,b))
```

输出结果：

```python
#a数组
[[ 0. 1. 2.]
[ 3. 4. 5.]
[ 6. 7. 8.]]
#b数组
[10 10 10]
#加
[[ 10. 11. 12.]
[ 13. 14. 15.]
[ 16. 17. 18.]]
#减
[[-10. -9. -8.]
[ -7. -6. -5.]
[ -4. -3. -2.]]
#乘
[[ 0. 10. 20.]
[ 30. 40. 50.]
[ 60. 70. 80.]]
#除
[[ 0. 0.1 0.2]
[ 0.3 0.4 0.5]
[ 0.6 0.7 0.8]]
```

下面介绍了 NumPy 中其他重要的算术运算函数。

### 2) numpy.reciprocal()

该函数对数组中的每个元素取倒数，并以数组的形式将它们返回。

当数组元素的数据类型为整型（int）时，对于绝对值小于 1 的元素，返回值为 0，而当数组中包含 0 元素时，返回值将出现 overflow（inf） 溢出提示，示例如下：

```python
import numpy as np
#注意此处有0
a = np.array([0.25, 1.33, 1, 0, 100])
#数组a默认为浮点类型数据
print(a)
#对数组a使用求倒数操作
print (np.reciprocal(a))
#b数组的数据类型为整形int
b = np.array([100, 10, 1], dtype = int)
print(b)
#对数组b使用求倒数操作
print( np.reciprocal(b) )
```

输出结果：

```
[  0.25   1.33   1.     0.   100.  ]
RuntimeWarning: divide by zero encountered in reciprocal
[4.        0.7518797 1.              inf 0.01     ]

[100  10   1]
[0 0 1]
```

### 3) numpy.power()

该函数将 a 数组中的元素作为底数，把 b 数组中与 a 相对应的元素作幂 ，最后以数组形式返回两者的计算结果。示例如下：

```python
import numpy as np
a = np.array([10,100,1000]) 
#调用 power 函数
print (np.power(a,2))
b = np.array([1,2,3]) 
print (b)
print (np.power(a,b))
```

输出结果：

```
[  10  100 1000]
[    100   10000 1000000]
[1 2 3]
[        10      10000 1000000000]
```

### 4) numpy.mod()

返回两个数组相对应位置上元素相除后的余数，它与 numpy.remainder() 的作用相同 。

```python
import numpy as np
a = np.array([11,22,33])
b = np.array([3,5,7])
#a与b相应位置的元素做除法
print( np.mod(a,b))
#remainder方法一样
print(np.remainder(a,b)) 
```

输出结果：

```
[2 2 5]
[2 2 5]
```

## 复数处理函数

NumPy 提供了诸多处理复数类型数组的函数，主要有以下几个：

- numpy.real() 返回复数数组的实部；
- numpy.imag() 返回复数数组的虚部；
- numpy.conj() 通过更改虚部的符号，从而返回共轭复数；
- numpy.angle() 返回复数参数的角度，该函数的提供了一个 deg 参数，如果 deg=True，则返回的值会以角度制来表示，否则以以弧度制来表示。

示例如下：

```python
import numpy as np
a = np.array([-5.6j, 0.2j, 11. , 1+1j])
print(a)
#real() 
print np.real(a)
#imag() 
print np.imag(a)
#conj()
print np.conj(a)
#angle() 
print np.angle(a)
#angle() 带参数deg
print np.angle(a, deg = True)
```

输出结果：

```python
[ 0.-5.6j 0.+0.2j 11.+0.j 1.+1.j ]

#实部
[ 0. 0. 11. 1.]

#虚部
[-5.6 0.2 0. 1. ]

#复数
[ 0.+5.6j 0.-0.2j 11.-0.j 1.-1.j ]

#rad
[-1.57079633 1.57079633 0. 0.78539816]

#deg
[-90. 90. 0. 45.]
```