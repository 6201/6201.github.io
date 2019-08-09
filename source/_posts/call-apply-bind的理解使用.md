---
title: 'call,apply的理解使用'
date: 2018-05-17 13:33:08
tags: 学习
categories: 编程
---

call(),方法调用一个函数，改变函数中this的指向，和提供参数。

call方法的作用和apply方法类似，只有一个区别，就是call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组。

### 语法

```Javascript
fun.call(thisArg, arg1, arg2, ...)

fun.apply(thisArg, [arg1, arg2, ...])
```

**参数**

thisArg

在fun函数运行时指定的this值。非严格模式下，指定为null和undefined的this值会自动指向全局对象，同时值为原始值(数字，字符串，布尔值)的this会指向该原始值的自动包装对象。

arg1， arg2, ...

指定的参数列表。

### 返回值

返回值是你调用的方法的返回值，若该方法没有返回值，则返回undefined。

### 描述

可以让call()中的对象调用当前对象所拥有的function。你可以使用call()来实现继承：写一个方法，然后让另外一个新的对象来继承它（而不是在新对象中再写一次这个方法）。

### 示例

**使用call方法调用父构造函数**

``` Javascript
function Product(name, price) {
    this.name = name;
    this.price = price;
    
    if(price < 0) {
        throw RangError(
        'Cannot create product '+ this.name + ' with a negative price'
        );
    }
}

function Food(name, price) {
    Product.call(this, name, price);
    this.category = 'food';
}

//等同于
function Food(name, price) {
    this.name = name;
    this.price = price;
    if(price < 0) {
        thirow RangeError(
        'Cannot create product ' + this.name + ' with a negative price'
        );
    }
    this.category = 'food';
}

```

这里使用call方法后不需要再重新定义name和price属性。

**使用call方法调用匿名函数**

```javascript
var animals = [
  {species: 'Lion', name: 'King'},
  {species: 'Whale', name: 'Fail'}
];

for (var i = 0; i < animals.length; i++) {
  (function (i) { 
    this.print = function () { 
      console.log('#' + i  + ' ' + this.species + ': ' + this.name); 
    } 
    this.print();
  }).call(animals[i], i);
}
```

**使用call方法调用函数并且指定上下文的'this'**

```Javascript
function greet() {
  var reply = [this.person, 'Is An Awesome', this.role].join(' ');
  console.log(reply);
}

var i = {
  person: 'Douglas Crockford', role: 'Javascript Developer'
};

greet.call(i); // Douglas Crockford Is An Awesome Javascript Developer
```

