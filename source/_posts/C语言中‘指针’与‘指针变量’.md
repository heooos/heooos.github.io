---
title: C语言中‘指针’与‘指针变量’
date: 2018-11-04 21:37:21
tags: [C语言]
categories: [C语言]
---
比较严格的说法是这样的：

系统为每一个内存单元分配一个地址值，C/C++把这个地址值称为“指针”。如有``int i=5``,存放变量``i``的内存单元的编号(地址)``&i``被称为指针。

“指针变量”则是存放前述“地址值”的变量，也可以表述为，“指针变量”是存放变量所占内存空间“首地址”的变量(因为一个变量通常要占用连续的多个字节空间)。比如在``int i=5``后有一句``int *p=&i``,就把i的指针``&i``赋给了``int *``型指针变量``p``，也就是说``p``中存入着``&i``。所以说指针变量是存放指针的变量。

**有一个事实值得注意，那就是有不少资料和教科书并没有如上区分，而是认为“指针是指针变量的简称”，如对``int *p=&i``的解释是：声明一个``int *``型指针p，并用变量i的地址初始化。而严格说应该是声明一个``int *``型指针变量``p``才对。**所以有时看书要根据上下文理解实质，而不能过于拘泥于文字表述。


**转自：[CSDN](https://blog.csdn.net/u011555996/article/details/79496203)**