---
title: JS中new关键字的执行流程
date: 2017-08-24 14:27:30
tags: JavaScript
---

> 来源：http://javascript.ruanyifeng.com/oop/basic.html

new命令简化的内部流程，可以使用如下代码表示：

```javascript
function _new(/*构造函数*/constructor,/*构造函数参数*/param){
  
  //将arguments对象转为数组
  var args = [].slice.call(arguments);
  //取出构造函数
  var constructor = args.shift();
  //创建一个空对象，继承构造函数的prototype属性
  var context = Object.create(constructor.prototype);
  //执行构造函数
  var result = constructor.apply(context,args);
  //如果返回结果是对象，就直接返回。否则，返回context对象
  return (typeof result === 'object' && result != null)?result:context;
  
}

//实例
var actor = _new(Person,'张三',28);
```

