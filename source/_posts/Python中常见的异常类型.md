---
title: python中常见的异常类型
date: 2017-11-30 04:08:09
tags: [python,Exception]
categories: Python
---

Python中常见的错误类型：

- **NameError**：尝试访问一个未申明的变量

```python
>>> v
NameError: name 'v' is not defined
```

- **ZeroDivisionError**：除数为0

```python
>>> v = 1/0
ZeroDivisionError: int division or modulo by zero
```

- **SyntaxError**：语法错误

```python
int int
SyntaxError: invalid syntax (<pyshell#14>, line 1)
```

- **IndexError**：索引超出范围

```python
List = [2]
>>> List[3]
Traceback (most recent call last):
  File "<pyshell#18>", line 1, in <module>
    List[3]
IndexError: list index out of range
```

- **KeyError**：字典关键字不存在

```python
Dic = {'1':'yes', '2':'no'}
>>> Dic['3']
Traceback (most recent call last):
  File "<pyshell#20>", line 1, in <module>
    Dic['3']
KeyError: '3'
```

- **IOError**：输入输出错误

```python
>>> f = open('abc')
IOError: [Errno 2] No such file or directory: 'abc'
```

- **AttributeError**：访问未知对象属性

```python
>>> class Worker:
 def Work():
  print("I am working")

>>> w = Worker()
>>> w.a
Traceback (most recent call last):
  File "<pyshell#51>", line 1, in <module>
    w.a
AttributeError: 'Worker' object has no attribute 'a'
```

- **ValueError**：数值错误

```python
>>> int('d')
Traceback (most recent call last):
  File "<pyshell#54>", line 1, in <module>
    int('d')
ValueError: invalid literal for int() with base 10: 'd'
```

- **TypeError**：类型错误

```python
>>> iStr = '22'
>>> iVal = 22
>>> obj = iStr + iVal;
Traceback (most recent call last):
  File "<pyshell#68>", line 1, in <module>
    obj = iStr + iVal;
TypeError: Can't convert 'int' object to str implicitly
```

- **AssertionError**：断言错误

```python
>>> assert 1 != 1
Traceback (most recent call last):
  File "<pyshell#70>", line 1, in <module>
    assert 1 != 1
AssertionError
```

- **MemoryError**:内存耗尽异常
- **NotImplementedError**：方法没实现引起的异常

```python
class Base(object):
    def __init__(self):
        pass

    def action(self):
        #抛出异常，说明该接口方法未实现
        raise NotImplementedError
```

- **LookupError**：键、值不存在引发的异常

LookupError异常是IndexError、KeyError的基类， 如果你不确定数据类型是字典还是列表时，可以用LookupError捕获此异常

- **StandardError**: 标准异常

除StopIteration, GeneratorExit, KeyboardInterrupt 和SystemExit外，其他异常都是StandarError的子类。