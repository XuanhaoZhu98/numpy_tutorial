# 11 NumPy 字符串处理函数

NumPy 提供了许多字符串处理函数，它们被定义在用于处理字符串数组的 numpy.char 这个类中，这些函数的操作对象是 string_ 或者 unicode_ 字符串数组。如下表所示：

| 函数名称     | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| add()        | 对两个数组相应位置的字符串做连接操作。                       |
| multiply()   | 返回多个字符串副本，比如将字符串“ hello”乘以3，则返回字符串“ hello hello hello”。 |
| center()     | 用于居中字符串，并将指定的字符，填充在原字符串的左右两侧。   |
| capitalize() | 将字符串第一个字母转换为大写。                               |
| title()      | 标题样式，将每个字符串的第一个字母转换为大写形式。           |
| lower()      | 将数组中所有的字符串的大写转换为小写。                       |
| upper()      | 将数组中所有的字符串的小写转换为大写。                       |
| split()      | 通过指定分隔符对字符串进行分割，并返回一个数组序列，默认分隔符为空格。 |
| splitlines() | 以换行符作为分隔符来分割字符串，并返回数组序列。             |
| strip()      | 删除字符串开头和结尾处的空字符。                             |
| join()       | 返回一个新的字符串，该字符串是以指定分隔符来连接数组中的所有元素。 |
| replace()    | 用新的字符串替换原数组中指定的字符串。                       |
| decode()     | 用指定的编码格式对数组中元素依次执行解码操作。               |
| encode()     | 用指定的编码格式对数组中元素依次执行编码操作。               |

上述函数基于 Python 内置的字符串函数实现， 下面对一些常用函数进行讲解。

## numpy.char.add()

numpy.char.add() 将两个数组对应位置的字符串元素进行连接。示例如下：

```python
import numpy as np 
#连接两个字符串
print (np.char.add(['hello'],[' xuanhao']))
#连接多个字符串
print (np.char.add(['hello', 'pretty'],[' xuanhao', ' good']))
```

输出结果：

```
['hello xuanhao']
['hello xuanhao' 'pretty good']
```

## numpy.char.multiply()

该函数将指定的字符串进行多次拷贝，并将拷贝结果返回，示例如下：

```python
import numpy as np 
print (np.char.multiply('Ruby ',3))
```

输出结果：

```
Ruby Ruby Ruby 
```

## numpy.char.center()

numpy.char.center() 用于居中字符串，其语法格式如下：

```python
np.char.center(string, width, fillchar) 
```

示例如下：

```python
import numpy as np 
# str: 字符串，width: 长度，fillchar: 填充字符
print (np.char.center('Hello Xuanhao', 30,fillchar = '*'))
```

输出如下所示：

```
********Hello Xuanhao*********
```

## numpy.char.capitalize()

numpy.char.capitalize() 将字符串的第一个字母转换为大写，示例如下：

```python
import numpy as np 
print (np.char.capitalize('hello xuanhao'))
```

输出结果：

```
Hello xuanhao
```

## numpy.char.title()

numpy.char.title() 将字符串数组中每个元素的第一个字母转换为大写，示例如下：

```python
import numpy as np 
print (np.char.title('hello xuanhao'))
```

输出结果：

```
Hello Xuanhao
```

## numpy.char.lower()

numpy.char.lower() 将字符串数组中每个元素转换为小写，示例如下：

```python
import numpy as np 
print (np.char.title('HELLO XUANHAO'))
```

输出结果：

```
Hello Xuanhao
```

## numpy.char.upper()

numpy.char.upper() 将数组中的每个元素转换为大写，示例如下：

```py
import numpy as np 
print (np.char.upper('hello xuanhao'))
```

输出结果如下：

```
HELLO XUANHAO
```

## numpy.char.split()

该函数通过指定分隔符对字符串进行分割，并返回数组序列。默认情况下，分隔符为空格。

```python
import numpy as np  
print(np.char.split("hello xuanhao"),sep = " ")  
```

输出结果：

```
['hello', 'xuanhao']
```

## numpy.char.splitlines() 

numpy.char.splitlines() 以换行符作为分隔符来分割字符串，并返回一个数组序列。

```python
import numpy as np  
# 换行符 \n
print(np.char.splitlines("Welcome\nto\nMy\nGithub"))  
```

输出结果：

```
['Welcome', 'to', 'My', 'Github']
```

## numpy.char.strip() 

numpy.char.strip() 用于移除开头或结尾处的空格。

```python
import numpy as np  
str = "     Welcome to My Github     " 
print(str)  
print(np.char.strip(str))  
```

输出结果：

```
     Welcome to My Github     
Welcome to My Github
```

## numpy.char.join()

numpy.char.join() 通过指定的分隔符来连接数组中的元素或字符串。

```python
import numpy as np
print (np.char.join(':','Hello'))
#也可指定多个分隔符
print (np.char.join([':','-'],['Hello','Xuanhao']))
```

输出结果：

```
H:e:l:l:o
['H:e:l:l:o' 'X-u-a-n-h-a-o']
```

## numpy.char.replace() 

numpy.char.replace() 使用新字符替换字符串中的指定字符。示例如下：

```python
import numpy as np 
str = "Welcome to My Github" 
#原字符串
print(str) 
#更改后字符串
print(np.char.replace(str, "Welcome to","Hello"))  
```

输出结果：

```
Welcome to My Github
Hello My Github
```

## numpy.char.encode()

numpy.char.encode() 函数对数组中的每个元素调用 str.encode 函数。 默认编码是 utf-8，可以使用标准 Python 库中的编解码器，示例如下：

```python
import numpy as np 
a = np.char.encode('Xuanhao', 'cp500') 
print (a)
```

输出结果：

```
b'\xe7\xa4\x81\x95\x88\x81\x96'
```

## numpy.char.decode()

numpy.char.decode() 函数对编码的元素进行 str.decode() 解码，示例如下：

```python
import numpy as np 
a = np.char.encode('Xuanhao', 'cp500') 
print (a)
print (np.char.decode(a,'cp500'))
```

输出结果：

```
b'\xe7\xa4\x81\x95\x88\x81\x96'
Xuanhao
```