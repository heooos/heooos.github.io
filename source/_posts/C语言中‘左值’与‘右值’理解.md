---
title: C语言中‘左值’与‘右值’理解
date: 2018-11-05 12:49:51
tags: [C语言]
categories: [C语言]
---
## 前言
在C语言学习过程中，大家或许听到过左值和右值的概念，甚至在调试程序时编译器也会给出"left operand must be l-value" 即左操作数必须为左值！今天我们将为大家详细解释这两个词，以及两者的区别！

简单而言，在赋值运算符“=”左边的就是左值，在赋值运算符“=”后边的就是右值，感觉像是废话，但非常好理解。但更多时候，我们是为了学习和理解不同情况下左值和右值的区别，下面来举例依次说明，着层深入，来让大家解渴！

## 1.变量做左值和右值的区别:
如``x = 2``;
这里x为整形变量，这里作为左值，代表的是一块内存单元，表示的是地址。

再如``x = y``;
现在看变量做右值情况，y做右值，这里呢就不在表示地址，而是代表该内存单元上的值！然后赋给x。

## 2.常量做左值和右值的区别:
继续``x = 2``;
这里2做右值，2是一个常量，没有任何疑问。

而如果``1 = 2``;
这里我们看左值，是1是常量，这里就会有问题了，编译会报错！因为常量不可被修改、不可以被赋值！所以大家可能会听过或见过“可修改/不可修改的左值”。
![](https://raw.githubusercontent.com/heooos/ImageResourceRepo/master/20181105/C%E8%AF%AD%E8%A8%80%E4%B8%AD%E2%80%98%E5%B7%A6%E5%80%BC%E2%80%99%E4%B8%8E%E2%80%98%E5%8F%B3%E5%80%BC%E2%80%99%E7%90%86%E8%A7%A3-001.png)


## 3.数组名做左值和右值的区别:
例如有字符数组char a[100];

当a做右值时候，我们可以把它赋给``char *``类型的指针，用来指向这个数组，这种情况下数组名做右值代表该数组首元素的首地址，是常量，是完全可以的。

而数组名无论右值和还是左值，都代表是地址，是常量，因此它不可以做左值，因为常量不可被修改！所以不少同学试图再定义数组之后再试图对数组赋字符串都是错误的！
![](https://raw.githubusercontent.com/heooos/ImageResourceRepo/master/20181105/C%E8%AF%AD%E8%A8%80%E4%B8%AD%E2%80%98%E5%B7%A6%E5%80%BC%E2%80%99%E4%B8%8E%E2%80%98%E5%8F%B3%E5%80%BC%E2%80%99%E7%90%86%E8%A7%A3-002.png)

## 4.字符串常量做右值
字符串常量想必大家都很清楚，是用双引号括起来的字符串，既然也是常量，也理所当然不可以做左值，但做右值呢？

答案是，会表示该字符串在内存中存储位置的首地址。就是``char *  p = “dotcpp.com”``用法的原因。

以上四种，希望对大家深入理解左值和右值有帮助！大家有任何问题，请随时留言讨论！


转自:[C语言网, 版权所有丨如未注明,均为原创丨本网站采用BY-NC-SA协议进行授权,转载请注明](http://www.dotcpp.com/wp/692.html)