# 19 NumPy IO操作

NumPy IO 操作是以文件的形式从磁盘中加载 ndarray 对象。在这个过程中，NumPy 可以两种文件类型处理 ndarray 对象，一类是二进制文件（以`.npy`结尾），另一类是普通文本文件。npy 文件用于存储重建 ndarray 所需的数据、图形、dtype 和其他信息。常用的 IO 函数有：

- load() 和 save() 函数是读写文件数组数据的两个主要函数，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 .npy 的文件中。
- savez() 函数用于将多个数组写入文件，默认情况下，数组是以未压缩的原始二进制格式保存在扩展名为 .npz 的文件中。
- loadtxt() 和 savetxt() 函数处理正常的文本文件(.txt 等)

## 1) numpy.save()

numpy.save() 方法将输入数组存储在`.npy`文件中。

```python
numpy.save(file, arr, allow_pickle=True, fix_imports=True)
```

参数说明：

- file：保存后的文件名称，其文件类型为`.npy`；
- arr：要保存的数组；
- allow_pickle：可选项，布尔值参数，允许使用 pickle 序列化保存数组对象；
- fix_imports：可选项，为了便于在 Pyhton2 版本中读取 Python3 保存的数据。

示例如下：

```python
import numpy as np 
a = np.array([1,2,3,4,5]) 
# 保存到 outfile.npy 文件上
np.save('outfile.npy',a) 
# 保存到 outfile2.npy 文件上，如果文件路径末尾没有扩展名 .npy，该扩展名会被自动加上
np.save('outfile2',a)
```

我们可以查看文件内容：

```shell
$ cat outfile.npy 
?NUMPYv{'descr': '<i8', 'fortran_order': False, 'shape': (5,), }  
$ cat outfile2.npy 
?NUMPYv{'descr': '<i8', 'fortran_order': False, 'shape': (5,), } 
```

可以看出文件是乱码的，因为它们是 Numpy 专用的二进制格式后的数据。

我们可以使用 load() 函数来读取数据就可以正常显示了：

```python
import numpy as np 
b = np.load('outfile.npy')  
print (b)
```

输出结果：

```
[1, 2, 3, 4, 5]
```

## 2) numpy.save()

numpy.savez() 函数将多个数组保存到以 npz 为扩展名的文件中。

```python
numpy.savez(file, *args, **kwds)
```

参数说明：

- file：要保存的文件，扩展名为 .npz，如果文件路径末尾没有扩展名 .npz，该扩展名会被自动加上；
- args: 要保存的数组，可以使用关键字参数为数组起一个名字，非关键字参数传递的数组会自动起名为 arr_0, arr_1, …　；
- kwds: 要保存的数组使用关键字名称。

示例如下：

```python
import numpy as np 
a = np.array([[1,2,3],[4,5,6]])
b = np.arange(0, 1.0, 0.1)
c = np.sin(b)
# c 使用了关键字参数 sin_array
np.savez("xuanhao.npz", a, b, sin_array = c)
r = np.load("xuanhao.npz")  
print(r.files) # 查看各个数组名称
print(r["arr_0"]) # 数组 a
print(r["arr_1"]) # 数组 b
print(r["sin_array"]) # 数组 c
```

输出结果：

```
['sin_array', 'arr_0', 'arr_1']

[[1 2 3]
 [4 5 6]]
 
[0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9]

[0.         0.09983342 0.19866933 0.29552021 0.38941834 0.47942554
 0.56464247 0.64421769 0.71735609 0.78332691]
```

## 3) numpy.savetxt()

savetxt() 和 loadtxt() 分别表示以文本格式存储数据或加载数据。其中 savetxt() 的语法格式如下：

```python
np.loadtxt(FILENAME, dtype=int, delimiter=' ')
np.savetxt(FILENAME, a, fmt="%d", delimiter=",")
```

参数说明：

- filename：表示保存文件的路径；
- self.task： 要保存数组的变量名；
- fmt="%d"： 指定保存文件的格式，默认是十进制；
- delimiter=" "表示分隔符，默认以空格的形式隔开。


示例如下：

```python
import numpy as np 
a = np.array([1,2,3,4,5]) 
np.savetxt('xuanhao.txt',a) 
b = np.loadtxt('xuanhao.txt')  
print(b)
```

输出结果：

```
[1. 2. 3. 4. 5.]
```

使用 delimiter 参数：

```python
import numpy as np    
a=np.arange(0,10,0.5).reshape(4,-1) 
np.savetxt("xuanhao.txt",a,fmt="%d",delimiter=",") # 改为保存为整数，以逗号分隔 
b = np.loadtxt("xuanhao.txt",delimiter=",") # load 时也要指定为逗号分隔 
print(b)
```

输出结果为：

```
[[0. 0. 1. 1. 2.]
 [2. 3. 3. 4. 4.]
 [5. 5. 6. 6. 7.]
 [7. 8. 8. 9. 9.]]
```