---
title: Python中序列学习笔记
date: 2017-12-06 05:09:26
tags: [python,序列]
categories: Python
---

**1.序列**

**(1) 序列的标准类型运算**

<、>、<=、>=、==、!= 值比较

is、is not 对象身份比较

and、or、not 逻辑运算

**(2) 通用序列类型操作**

seq[start: end]	切片操作

``*``	重复组合序列数据

``+``    连接 2 个序列

in、not in	判断元素是否存在序列中

**(3) 序列常用函数**

| 函数                         | 描述                                       |
| -------------------------- | ---------------------------------------- |
| list(iter)                 | 将可迭代对象iter转换成列表                          |
| tuple(iter)                | 将可迭代对象iter转换成元组                          |
| str(obj)                   | 将对象obj转换成字符串表示                           |
| len(sequence)              | 返回sequence的长度，为整型类型                      |
| sorted(iter, key, reverse) | 返回可迭代对象iter排序后的列表，key用来指定排序的规则，reverse用来指定顺序还是逆序排列 |
| reversed(sequence)         | 返回序列sequence逆序排列后的迭代器                    |
| sum(iter, start)           | 将iter中的数值和start参数的值相加，返回float类型数值        |
| max(iter)                  | 返回可迭代对象iter中的最大值                         |
| min(iter)                  | 返回可迭代对象iter中的最小值                         |
| enumerate(iter[, start])   | 返回一个enumerate对象，可生成一个迭代器，该迭代器的元素是由参数iter元素的索引和值组成的元组 |
| zip(iter1 [,iter2 [...]])  | 返回一个zip对象，可生成一个迭代器，该迭代器的第n个元素是每个可迭代对象的第n个元素组成的元组 |

**2.字符串**

**字符串常用方法**

| 方法                                   | 描述                                       |
| ------------------------------------ | ---------------------------------------- |
| s.capitalize()                       | 返回字符串s首字母大写其余小写的形式                       |
| s.lower()                            | 返回字符串s的小写形式                              |
| s.upper()                            | 返回字符串s的大写形式                              |
| s.title()                            | 返回字符串s的标题形式即单词首字母大写形式                    |
| s.format(*args, **kwargs)            | 格式化字符串操作                                 |
| s.count(sub[, start[, end]])         | 返回指定字符在[指定位置的]字符串s中出现的次数                 |
| s.find(sub[, start[, end]])          | 返回指定字符在[指定位置的]字符串s中出现的索引号，找不到则返回-1       |
| s.index(sub[, start[, end]])         | 与 find()类似，不同的是如果找不到会引发ValueError异常      |
| s.replace(old, new[, count])         | 把字符串s中的old（旧字符串）替换成new（新字符串）。如果指定第三个参数count，则仅仅替换前count次出现的子串 |
| s.lstrip([chars])                    | 移除字符串s左边的指定字符（默认为空格），返回移除字符串s左边指定字符后生成的新字符串 |
| s.rstrip([chars])                    | 移除字符串s末尾的指定字符（默认为空格），返回移除字符串s末尾指定字符后生成的新字符串 |
| s.strip([chars])                     | 移除字符串s头尾指定的字符（默认为空格），返回移除字符串s头尾指定字符后生成的新字符串 |
| s.join(iterable)                     | 用指定的字符串s连接元素为字符串的可迭代对象                   |
| s.split(sep=None, maxsplit=-1)       | 以指定的字符作为分隔符（默认为空格）分割字符串s，maxsplit指分割次数（默认为不限制次数） |
| s.endswith(suffix[, start[, end]])   | 判断字符串s[的指定位置]是否以后缀suffix结尾               |
| s.startswith(prefix[, start[, end]]) | 判断字符串s[的指定位置]是否以前缀prefix开头               |

**3.列表**

**列表常用方法**

| 方法                              | 描述                                       |
| ------------------------------- | ---------------------------------------- |
| l.append(obj)                   | 在列表l末尾添加新的对象                             |
| l.count(obj)                    | 统计某个元素在列表l中出现的次数                         |
| l.extend(seq)                   | 在列表l末尾一次性追加另一个序列seq中的多个值(用新列表扩展原来的列表)    |
| l.index(obj)                    | 从列表l中找出某个值第一个匹配项的索引位置，索引从0开始             |
| l.insert(index, obj)            | 将对象obj插入列表l中索引为index的元素前                 |
| l.pop(index)                    | 移除列表l中索引为index的一个元素(默认为最后一个元素)，并且返回该元素的值 |
| l.remove(obj)                   | 移除列表l中某个值的第一个匹配项                         |
| l.reverse()                     | 将列表l中的元素反转                               |
| l.sort(key=None, reverse=False) | 对原列表l进行排序，可通过参数key指定排序依据，通过参数reverse指定顺序（默认方式）或逆序排列 |

**4.元组**

**元组常用函数**

| 函数         | 描述           |
| ---------- | ------------ |
| len(t)     | 计算元组t的元素个数   |
| max(t)     | 返回元组t中元素的最大值 |
| min(t)     | 返回元组t中元素的最小值 |
| tuple(seq) | 将序列seq转换为元组  |