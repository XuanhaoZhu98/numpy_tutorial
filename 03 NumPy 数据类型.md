# 03 NumPy 数据类型

NumPy 作为 Python 的扩展包，它提供了比 Python 更加丰富的数据类型，如表 1 所示：

| 序号 | 数据类型   | 语言描述                                                     |
| ---- | ---------- | ------------------------------------------------------------ |
| 1    | bool_      | 布尔型数据类型（True 或者 False）                            |
| 2    | int_       | 默认整数类型，类似于 C 语言中的 long，取值为 int32 或 int64  |
| 3    | intc       | 和 C 语言的 int 类型一样，一般是 int32 或 int 64             |
| 4    | intp       | 用于索引的整数类型（类似于 C 的 ssize_t，通常为 int32 或 int64） |
| 5    | int8       | 代表与1字节相同的8位整数。值的范围是-128到127。              |
| 6    | int16      | 代表 2 字节（16位）的整数。范围是-32768至32767。             |
| 7    | int32      | 代表 4 字节（32位）整数。范围是-2147483648至2147483647。     |
| 8    | int64      | 表示 8 字节（64位）整数。范围是-9223372036854775808至9223372036854775807。 |
| 9    | uint8      | 代表1字节（8位）无符号整数。                                 |
| 10   | uint16     | 2 字节（16位）无符号整数。                                   |
| 11   | uint32     | 4 字节（32位）的无符号整数。                                 |
| 12   | uint64     | 8 字节（64位）的无符号整数。                                 |
| 13   | float_     | float64 类型的简写。                                         |
| 14   | float16    | 半精度浮点数，包括：1 个符号位，5 个指数位，10个尾数位。     |
| 15   | float32    | 单精度浮点数，包括：1 个符号位，8 个指数位，23个尾数位。     |
| 16   | float64    | 双精度浮点数，包括：1 个符号位，11 个指数位，52个尾数位。    |
| 17   | complex_   | 复数类型，与 complex128 类型相同。                           |
| 18   | complex64  | 表示实部和虚部共享 32 位的复数。                             |
| 19   | complex128 | 表示实部和虚部共享 64 位的复数。                             |
| 20   | str_       | 表示字符串类型                                               |
| 21   | string_    | 表示字节串类型                                               |

numpy 的数值类型实际上是 dtype 对象的实例，并对应唯一的字符，包括 np.bool_，np.int32，np.float32等。

## 数据类型对象 (dtype)

数据类型对象（numpy.dtype 类的实例）用来描述与数组对应的内存区域是如何使用，它描述了数据的以下几个方面：

- 数据的类型（整数，浮点数或者 Python 对象）
- 数据的大小（例如， 整数使用多少个字节存储）
- 数据的字节顺序（小端法或大端法）
- 在结构化类型的情况下，字段的名称、每个字段的数据类型和每个字段所取的内存块的部分
- 如果数据类型是子数组，那么它的形状和数据类型是什么。

字节顺序是通过对数据类型预先设定 **<** 或 **>** 来决定的。 **<** 意味着小端法(最小值存储在最小的地址，即低位组放在最前面)。**>** 意味着大端法(最重要的字节存储在最小的地址，即高位组放在最前面)。

dtype 对象是使用以下语法构造的：

```python
numpy.dtype(object, align, copy)
```

- object：要转换为的数据类型对象
- align：如果为 true，填充字段使其类似 C 的结构体。
- copy：复制 dtype 对象 ，如果为 false，则是对内置数据类型对象的引用

示例：

```python
import numpy as np 
a= np.dtype(np.int64) 
print(a) 
```

输出结果：

```
int64
```

常用的一些方法：

```python
#查询数值类型
print(type(float))

#查询字符代码
print(np.dtype('f'), np.dtype('d'))

# 查询双字符代码
print(np.dtype('f8'))

# 获取所有字符代码
print(np.sctypeDict.keys())
  
# char 属性用来获取字符代码
t = np.dtype('float64')
print(t.char)

# type 属性用来获取类型
print(t.type)

# 获取大小
print(t.itemsize)
```

输出结果：

```
<class 'type'>

float32 float64

float64

dict_keys(['?', 0, 'byte', 'b', 1, 'ubyte', 'B', 2, 'short', 'h', 3, 'ushort', 'H', 4, 'i', 5, 'uint', 'I', 6, 'intp', 'p', 9, 'uintp', 'P', 10, 'long', 'l', 7, 'L', 8, 'longlong', 'q', 'ulonglong', 'Q', 'half', 'e', 23, 'f', 11, 'double', 'd', 12, 'longdouble', 'g', 13, 'cfloat', 'F', 14, 'cdouble', 'D', 15, 'clongdouble', 'G', 16, 'O', 17, 'S', 18, 'unicode', 'U', 19, 'void', 'V', 20, 'M', 21, 'm', 22, 'bool8', 'b1', 'int64', 'i8', 'uint64', 'u8', 'float16', 'f2', 'float32', 'f4', 'float64', 'f8', 'complex64', 'c8', 'complex128', 'c16', 'object0', 'bytes0', 'str0', 'void0', 'datetime64', 'M8', 'timedelta64', 'm8', 'Bytes0', 'Datetime64', 'Str0', 'Uint64', 'int32', 'i4', 'uint32', 'u4', 'int16', 'i2', 'uint16', 'u2', 'int8', 'i1', 'uint8', 'u1', 'complex_', 'int0', 'uint0', 'single', 'csingle', 'singlecomplex', 'float_', 'intc', 'uintc', 'int_', 'longfloat', 'clongfloat', 'longcomplex', 'bool_', 'bytes_', 'string_', 'str_', 'unicode_', 'object_', 'int', 'float', 'complex', 'bool', 'object', 'str', 'bytes', 'a'])

d

<class 'numpy.float64'>

8
```

## 数据类型标识码

NumPy 中每种数据类型都有一个唯一标识的字符码，如下所示：

| 字符   | 对应类型                           |
| ------ | ---------------------------------- |
| ?, b1  | 代表布尔型, bool                   |
| b, i1  | 带符号八位整型, int8               |
| B, u1  | 无符号八位整型, uint8              |
| h, i2  | 带符号十六位整型, int16            |
| H, u2  | 无符号十六位整型, uint16           |
| i, i4  | 带符号三十二位整型, int32          |
| I, u4  | 无符号三十二位整型, uint32         |
| q, i8  | 带符号六十四位整型, int64          |
| Q, u8  | 无符号六十四位整型, uint64         |
| f2, e  | 十六位浮点数, float16              |
| f4, f  | 三十二位浮点数, float32            |
| f8, d  | 六十四位浮点数, float64            |
| c8, F  | 六十四位复数浮点数, complex64      |
| c16, D | 一百二十八位复数浮点数, complex128 |
| m      | 时间间隔（timedelta）              |
| M      | datatime（日期时间）               |
| O      | Python对象                         |
| S,a    | 字节串（S）与字符串（a）           |
| U      | Unicode                            |
| V      | 原始数据（void）                   |

下面使用数据类型标识码，创建一组结构化数据：

```python
#创建数据类型score
import numpy as np
dt = np.dtype([('score','i1')])
print(dt) 
```

输出如下：

```
[('score', 'i1')]
```

将上述的数据类型对象 dt，应用到 ndarray 中：

```python
#定义字段名score，以及数组数据类型i1
# int8, int16, int32, int64 四种数据类型可以使用字符串 'i1', 'i2','i4','i8' 代替
dt = np.dtype([('score','i1')])
a = np.array([(55,),(75,),(85,)], dtype = dt)
#获取a数组
print(a)
#数据类型对象dtype
print(a.dtype)
#获取'score'字段分数
print(a['score'])
```

输出结果：

```
[(55,) (75,) (85,)]
[('score', 'i1')]
[55 75 85]
```

再举个例子：

```python
import numpy as np
#定义t的各个字段类型
t = np.dtype([('name', str, 40), ('numitems', numpy.int32), ('price',numpy.float32)])
print(t)
  
#获取字段类型
print(t['name'])
  
#使用记录类型创建数组
itemz = np.array([('Meaning of life DVD', 42, 3.14), ('Butter', 13,2.72)], dtype=t)
print(itemz[1])
```

输出结果：

```
[('name', '<U40'), ('numitems', '<i4'), ('price', '<f4')]
<U40
('Butter', 13, 2.72)
```

## 定义结构化数据

通常情况下，结构化数据使用字段的形式来描述某个对象的特征。以下示例描述一位老师的姓名、年龄、工资的特征，该结构化数据其包含以下字段：

- str 字段：name
- int 字段：age
- float 字段：salary

定义过程如下：

```python
import numpy as np
teacher = np.dtype([('name','S20'), ('age', 'i1'), ('salary', 'f4')])
#输出结构化数据teacher
print(teacher)
#将其应用于ndarray对象
b = np.array([('James', 32, 6357.50),('Robert', 28, 6856.80)], dtype = teacher) 
print(b)
```

输出结果：

```
[('name', 'S20'), ('age', 'i1'), ('salary', '<f4')]
[(b'James', 32, 6357.5) (b'Robert', 28, 6856.8)]
```