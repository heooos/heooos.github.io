---
title: JS中的概念解读
date: 2017-08-24 21:32:25
tags: JavaScript
categories: JavaScript概念
---

- 原型链

  ![js原型链](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/js_prototypes.jpeg)

- 字面量对象or对象字面量

- 构造函数

  **在JavaScript中，构造函数是用来创建原型链最常用的方法。构造函数如此流行的原因在于：它是创建类型的唯一途径。并且大部分引擎都对构造函数进行了高度优化。**

- `_proto_`和`prototype`

- 原型继承机制(概念同『原型链』)

- 显示原型&隐式原型

- 构造函数与普通函数的区别？

  - 在命名规则上，构造函数一般是首字母大写，普通函数则是遵照小驼峰式命名法。

  - 在函数调用时：

    ```javascript
    //构造函数
     function Egperson (name,age) {
         this.name = name;
         this.age = age;
         this.sayName = function () {
             alert(this.name);
          }
     }
     var person = new Egperson('mike','18'); //this-->person
     person.sayName();  //'mike'


     //普通函数
     function egPerson (name,age) {
         this.name = name;
         this.age = age;
         this.sayName = function () {
             alert(this.name);
          }
     }
     egPerson('alice','23'); //this-->window
     window.sayName();  //'alice'
    ```

    - 构造函数内部会创建一个实例，调用普通函数时则不会创建新的对象。
    - 构造函数内部的this指向是新创建的person实例，而普通函数内部的this指向调用函数的对象（如果没有对象调用，默认为window）

  - 返回值方面，对于构造函数而言，如果构造函数内部有`return`语句，而且`return`后面跟着一个对象，`new`命令会返回`return`语句指定的对象；否则，就会不管`return`语句，返回`this`对象。





> 参考文档：
>
> http://www.w3cplus.com/js/a-plain-english-guide-to-javascript-prototypes.html
>
> http://javascript.ruanyifeng.com/oop/basic.html#toc1