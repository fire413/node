## 手写new

new的过程中：

1.创建了一个全新的对象。

2.这个对象会被执行`[[Prototype]]`（也就是`__proto__`）链接。

3.生成的新对象会绑定到函数调用的`this`。

4.通过`new`创建的每个对象将最终被`[[Prototype]]`链接到这个函数的`prototype`对象上。

5.如果函数没有返回对象类型`Object`(包含`Functoin`, `Array`, `Date`, `RegExg`, `Error`)，那么`new`表达式中的函数调用会自动返回这个新的对象。

```js
/**
 \* 模拟实现 new 操作符
 \* @param {Function} ctor [构造函数]
 \* @return {Object|Function|Regex|Date|Error}   [返回结果]
 */
function newOperator(ctor){
  // 判断参数
  if(typeof ctor !== 'function'){
   throw 'newOperator function the first param must be a function';
  }
  // ES6 new.target 是指向构造函数
  newOperator.target = ctor;
  // 创建一个新对象，并链接到该函数的prototype上
  let newObj = Object.create(ctor.prototype);
  // 除去ctor构造函数的其余参数
  var argsArr = [].slice.call(arguments, 1);
  // 生成的新对象绑定到函数调用的this
  var ctorReturnResult = ctor.apply(newObj, argsArr);
  // 如果有返回则返回，无返回则直接返回该新对象
  var isObject = typeof ctorReturnResult === 'object' && ctorReturnResult !== null;
  var isFunction = typeof ctorReturnResult === 'function';
  if(isObject || isFunction){
​    return ctorReturnResult;
  }
  // 5.如果函数没有返回对象类型`Object`(包含`Functoin`, `Array`, `Date`, `RegExg`, `Error`)，那么`new`表达式中的函数调用会自动返回这个新的对象。
  return newObj;
}
function Student(name, age){
  this.name = name;
  this.age = age;
  // this.doSth();
  // return Error();
}
Student.prototype.doSth = function() {
  console.log(this.name);
};
var student1 = newOperator(Student, '张', 18);
var student2 = newOperator(Student, '三', 18);
// var student1 = new Student('张');
// var student2 = new Student('三');
console.log(student1, student1.doSth()); // {name: '张'} '三'
console.log(student2, student2.doSth()); // {name: '张'} '三'
student1.__proto__ === Student.prototype; // true
student2.__proto__ === Student.prototype; // true
// __proto__ 是浏览器实现的查看原型方案。
// 用ES5 则是：
Object.getPrototypeOf(student1) === Student.prototype; // true
Object.getPrototypeOf(student2) === Student.prototype; // true
```

## 手写bind

1、`bind`是`Functoin`原型链中`Function.prototype`的一个属性，每个函数都可以调用它。
2、`bind`本身是一个函数名为`bind`的函数，返回值也是函数，函数名是`bound`。（打出来就是`bound加上一个空格`）。

函数内部原理：

 1、bind是Function原型链中的Function.prototype的一个属性，它是一个函数，修改this指向，合并参数传递给原函数，返回值是一个新的函数。

2、bind返回的函数可以通过new调用，这时提供的this的参数被忽略，指向了new生成的全新对象。内部模拟实现了new操作符。

```js
// ES5精简版
var isCallable = function isCallable(value){
  if(typeof value !== 'function'){
    return false;
  }
  return true;
};
var Empty = function Empty() {};
// 源码是 defineProperties
// 源码是bind笔者改成bindFn便于测试
Function.prototype.bindFn = function bind(that) {
  var target = this;
  // 判断this是否是函数
  if (!isCallable(target)) {
    throw new TypeError('Function.prototype.bind called on incompatible ' + target);
  }
  var args = [].slice.call(arguments, 1); // 将参数化为整数
  var bound; //用于返回bound函数
  var binder = function () {
    if (this instanceof bound) { 
      var result = Function.prototype.apply.call(  
        target,    
        this,    
        Array.prototype.concat.call(args, Array.prototype.slice.call(arguments))  
      );  
      if (Object(result) === result) {    
        return result;    
      }    
      return this;    
    } else {    
      return Function.prototype.apply.call(    
        target,    
        that,  
        Array.prototype.concat.call(args, Array.prototype.slice.call(arguments))  
      );
    }
  };
  var boundLength = Math.max(0, target.length - args.length);
  var boundArgs = [];
  for (var i = 0; i < boundLength; i++) {
    Array.prototype.push.call(boundArgs, '$' + i);
  }
  // 这里是Function构造方式生成形参length $1, $2, $3...
  bound = Function('binder', 'return function (' + Array.prototype.join.call(boundArgs, ',') + '){ return binder.apply(this, arguments); }')(binder);
  if (target.prototype) {
    Empty.prototype = target.prototype;
    bound.prototype = new Empty();
    Empty.prototype = null;
  }
  return bound;
};
```



```js
 Function.prototype.myBind = function (obj, ...parameters) {
  // 存储源函数及其参数
  const fn = this;
  // 返回的函数 以及将要第二次传入的参数
  var retFn = function (...secondParameters) {
   // 对是否new做处理 instanceof 判断this是否是retFn这个函数的实例
   var isNew = this instanceof retFn;
​    // new调用就绑定到this上,否则就绑定到传入的objThis上
   var context = isNew ? this : Object(obj);
   return fn.call(context, ...parameters, ...secondParameters);
  };
  retFn.prototype = Object.create(fn.prototype);
  return retFn;
 }
var obj = {
  name: '张三',
};
function original(a, b){
  console.log('this', this); // original {}
  console.log('typeof this', typeof this); // object
  this.name = b;
  console.log('name', this.name); // 2
  console.log('this', this); // original {name: 2}
  console.log([a, b]); // 1, 2
}
var bound = original.myBind(obj, 1);
var newBoundResult = new bound(2);
console.log(newBoundResult, 'newBoundResult'); // original {name: 2}
```



## 手写call

```js
Function.prototype.myCall = function (context, ...parameters) {
  if (context === undefined || context === null) {
   context = window;
  } else {
   // 值为原始值（数字，字符串，布尔值）的 this 会指向该原始值的实例对象
   context = Object(context);
  }
  // 用于指向要绑定this的函数的一个临时属性 用Symbol()可以使其具备唯一性
  temp = Symbol('我是一个与众不同的属性');
  // this指的就是要执行的函数
  context[temp] = this;
  // 将context作为对象 调用它自身的方法 这样自然就隐式绑定了context
  var result = context[temp](...parameters);
  // 删除这个临时属性 （过河拆桥）
  delete context[temp];
  // 返回函数执行的结果
  return result;
 }
```



## 手写apply

```js
 Function.prototype.myApply = function (context) {
  if (context === undefined || context === null) {
   context = window;
  } else {
   context = Object(context);
  }
  // JavaScript权威指南判断是否为类数组对象
  function isArrayLike(o) {
   if (o &&                  // o不是null、undefined等
​    typeof o === 'object' &&        // o是对象
​    isFinite(o.length) &&          // o.length是有限数值
​    o.length >= 0 &&            // o.length为非负值
​    o.length === Math.floor(o.length) &&  // o.length是整数
​    o.length < 4294967296)         // o.length < 2^32
​    return true;
   else
​    return false;
  }
  var temp = Symbol('我是一个与众不同的属性');
  context[temp] = this;
  var args = arguments[1];
  var result;
  // 如果传了第二个参数
  if (args) {
   // 不是数组也不是类数组则应该抛出错误
   if (!Array.isArray(args) && !isArrayLike(args)) {
​    throw new TypeError('myApply 第二个参数不为数组并且不为类数组对象抛出错误');
   } else {
​    var arr = Array.from(args);
​    result = context[temp](...arr);
   }
  } else {
   result = context[temp]();
  }
  delete context[temp]
  return result;
 }
```

