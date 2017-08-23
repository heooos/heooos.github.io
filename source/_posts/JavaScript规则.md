---
title: JavaScript规则
date: 2017-08-23 13:37:47
tags: JavaScript
---

**JavaScript有几条规则需要遵守:**

* 不要使用`new Number()`、`new Boolean()`、`new String()`创建包装对象；


* 用`parseInt()`或`parseFloat()`来转换任意类型到`number`；
* 用`String()`来转换任意类型到`string`，或者直接调用某个对象的`toString()`方法；
* 通常不必把任意类型转换为`boolean`再判断，因为可以直接写`if (myVar) {...}`；
* `typeof`操作符可以判断出`number`、`boolean`、`string`、`function`和`undefined`；
* 判断`Array`要使用`Array.isArray(arr)`；
* 判断`null`请使用`myVar === null`；
* 判断某个全局变量是否存在用`typeof window.myVar === 'undefined'`；
* 函数内部判断某个变量是否存在用`typeof myVar === 'undefined'`。



**常见问题**

* 任何对象都有`toString()`方法吗？

  `null`和`undefined`就没有！确实如此，这两个特殊值要除外，虽然`null`还伪装成了`object`类型。

* 如果我们在使用Number、Boolean和String时，没有写new会发生什么情况？

  此时，`Number()`、`Boolean`和`String()`被当做普通函数，把任何类型的数据转换为`number`、`boolean`和`string`类型（注意不是其包装类型）。

