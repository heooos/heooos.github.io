---
title: JS中的概念解读
date: 2017-08-24 21:32:25
tags: JavaScript
categories: JavaScript概念
---

- 原型链

  ![js原型链](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/js_prototypes.jpeg)

- 字面量对象or对象字面量

- 作用域

  - 全局作用域
  - 函数作用域
  - eval作用域（严格模式下）

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
    ```


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
    ​```
    
    - 构造函数内部会创建一个实例，调用普通函数时则不会创建新的对象。
    - 构造函数内部的this指向是新创建的person实例，而普通函数内部的this指向调用函数的对象（如果没有对象调用，默认为window）

  - 返回值方面，对于构造函数而言，如果构造函数内部有`return`语句，而且`return`后面跟着一个对象，`new`命令会返回`return`语句指定的对象；否则，就会不管`return`语句，返回`this`对象。

- 立即执行函数

  **函数声明、函数表达式、匿名函数**

  - **函数声明**:使用function关键字声明一个函数，再指定一个函数名，叫函数声明。如下：

  ```javascript
  function fnName () {
  	//...
  };
  ```

  - **函数表达式**:使用function关键字声明一个函数，但未给函数命名，最后将匿名函数赋予一个变量，叫函数表达式，这是最常见的函数表达式语法形式。如下：

  ```javascript
  var fnName = function () {
  	//...
  };
  ```

  - **匿名函数**:使用function关键字声明一个函数，但未给函数命名，所以叫匿名函数，匿名函数属于函数表达式，匿名函数有很多作用，赋予一个变量则创建函数，赋予一个事件则成为事件处理程序或创建闭包等等。

  ```javascript
  function () {
    
  }; 
  ```

  函数声明和函数表达式不同之处在于:

  1. Javascript引擎在解析javascript代码时会‘函数声明提升'（Function declaration Hoisting）当前执行环境（作用域）上的函数声明，而函数表达式必须等到Javascirtp引擎执行到它所在行时，才会从上而下一行一行地解析函数表达式。
  2. 函数表达式后面可以加括号立即调用该函数，函数声明不可以，只能以fnName()形式调用 。

  区别如下：

  ```javascript
  fnName();
  function fnName(){
    ...
  }
  //正常，因为‘提升'了函数声明，函数调用可在函数声明之前
   
  fnName();
  var fnName=function(){
    ...
  }
  //报错，变量fnName还未保存对函数的引用，函数调用必须在函数表达式之后
  var fnName=function(){
    alert('Hello World');
  }();
  //函数表达式后面加括号，当javascript引擎解析到此处时能立即调用函数
  function fnName(){
    alert('Hello World');
  }();
  //不会报错，但是javascript引擎只解析函数声明，忽略后面的括号，函数声明不会被调用
  function(){
    console.log('Hello World');  
  }();
  //语法错误，虽然匿名函数属于函数表达式，但是未进行赋值操作，
  //所以javascript引擎将开头的function关键字当做函数声明，报错：要求需要一个函数名
  ```

  在理解了一些函数基本概念后，回头看看( function(){…} )()和( function (){…} () )这两种立即执行函数的写法，最初我以为是一个括号包裹匿名函数，并后面加个括号立即调用函数，当时不知道为什么要加括号，后来明白，要在函数体后面加括号就能立即调用，则这个函数必须是函数表达式，不能是函数声明。

  在function前面加！、+、 -甚至是逗号等到都可以起到函数定义后立即执行的效果，而（）、！、+、-、=等运算符，都将函数声明转换成函数表达式，消除了javascript引擎识别函数表达式和函数声明的歧义，告诉javascript引擎这是一个函数表达式，不是函数声明，可以在后面加括号，并立即执行函数的代码。

  加括号是最安全的做法，因为！、+、-等运算符还会和函数的返回值进行运算，有时造成不必要的麻烦。

  **不过这样的写法有什么用呢？**

  javascript中没用私有作用域的概念，如果在多人开发的项目上，你在全局或局部作用域中声明了一些变量，可能会被其他人不小心用同名的变量给覆盖掉，根据javascript函数作用域链的特性，可以使用这种技术可以模仿一个私有作用域，用匿名函数作为一个“容器”，“容器”内部可以访问外部的变量，而外部环境不能访问“容器”内部的变量，所以( function(){…} )()内部定义的变量不会和外部的变量发生冲突，俗称“匿名包裹器”或“命名空间”。

> 参考文档：
>
> http://www.w3cplus.com/js/a-plain-english-guide-to-javascript-prototypes.html
>
> http://javascript.ruanyifeng.com/oop/basic.html#toc1