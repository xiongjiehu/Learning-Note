# Python Basics

1.Assignment and Substitution

```python
#number,string,bool
num = 10
pi = 3.14
name = "Alice"
is_student = True

i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)


#list
my_list = []
numbers = [
    1, 2, 
    3, 4,
    ]

#tuple
my_tuple = (
    1, 2,
    3, 4,
    )

#dictionaries
my_dict = {}
person = {
    'name': 'Alice',
    'age': 30,
     }

#set
my_set = set()
my_set = {
    1, 2, 3,
    4, 5, 6,
    }
    

income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

2.Branches

```python
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
do_one()
do_two()
do_three()
```

3.Loops

4.Built-in Variables

<pre><code>dir(__builtins__)
help(XXX)

<strong>True：           #布尔类型，表示真。
</strong>False：          #布尔类型，表示假。
None：           #表示空值或缺失值。
__name__：       #表示模块的名称。
__doc__：        #用于存储模块的文档字符串。
__file__：       #表示模块的文件名。
__package__：    #表示包的名称。
__builtins__：   #一个包含内置函数和异常的字典。
__loader__：     #用于动态加载模块的模块加载器对象。
__spec__：       #用于存储模块的规范信息。
</code></pre>

4.Built-in functions

```
数学函数：
abs()：返回绝对值
round()：四舍五入
max()：返回最大值
min()：返回最小值
sum()：求和
类型转换函数：

int()：转为整型
float()：转为浮点型
str()：转为字符串
list()：转为列表
tuple()：转为元组
dict()：转为字典
序列操作函数：

len()：返回长度
sorted()：排序
reversed()：反转序列
enumerate()：枚举序列
zip()：打包元素
输入输出函数：

input()：获取用户输入
print()：打印输出
文件操作函数：

open()：打开文件
close()：关闭文件
read()：读取文件内容
write()：写入文件内容
其他常用函数：

range()：生成范围内的数字序列
isinstance()：判断对象是否是某个类的实例
type()：返回对象的类型
help()：获取帮助信息
```

5.White spaces

```python
spam(ham[1], {eggs: 2})
foo = (0,)
if x == 4: print(x, y); x, y = y, x
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]
```



6.Function

```python
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

def complex(real, imag=0.0):
    return magic(r=real, i=imag)

result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
```

7.Module

```python
#imports sequence
#Standard library -> Related third party -> Local application/library specific
import mypkg.sibling
from mypkg import sibling
from mypkg.sibling import example
```

8.Debbugging

```python
def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError as e:
        print("除数不能为零:", e)
    except TypeError as e:
        print("类型错误:", e)
    except Exception as e:
        print("发生了其他异常:", e)
    else:
        print("结果:", result)
    finally:
        print("无论是否发生异常，都会执行的清理代码")

# 调用函数并测试异常处理
divide(10, 2)  # 正常情况，输出结果: 5.0
divide(10, 0)  # 除以零，触发 ZeroDivisionError，输出除数不能为零
divide(10, 'a')  # 类型错误，触发 TypeError，输出类型错误
```

9.Script with Style

```python
# -*- coding: utf-8 -*-
"""Module docstring."""

import math
import os
import sys

CONSTANT = 42
ANOTHER_CONSTANT = 100

def add_numbers(
    a, 
    b):
    """Function docstring."""
    result = a + b
    return result

class MyClass:
    """Class docstring."""

    def __init__(
        self, 
        value):
        self.value = value

    def square_value(
        self):
        """Method docstring."""
        return self.value ** 2

if __name__ == "__main__":
    my_class = MyClass(CONSTANT)
    squared_value = my_class.square_value()
    print(f"The squared value is: {squared_value}")
```

10.Other advices

* Advice limit all lines to a maximum of 79 characters.



