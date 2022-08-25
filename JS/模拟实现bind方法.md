1、`bind`是`Functoin`原型链中`Function.prototype`的一个属性，每个函数都可以调用它。
2、`bind`本身是一个函数名为`bind`的函数，返回值也是函数，函数名是`bound`。（打出来就是`bound加上一个空格`）。

```js
var isCallable = function isCallable(value){

  if(typeof value !== 'function'){

​    return false;

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

​    throw new TypeError('Function.prototype.bind called on incompatible ' + target);

  }

  var args = [].slice.call(arguments, 1); // 将参数化为整数

  var bound; //用于返回bound函数

  var binder = function () {

​    if (this instanceof bound) {

​      var result = Function.prototype.apply.call(

​        target,

​        this,

​        Array.prototype.concat.call(args, Array.prototype.slice.call(arguments))

​      );

​      if (Object(result) === result) {

​        return result;

​      }

​      return this;

​    } else {

​      return Function.prototype.apply.call(

​        target,

​        that,

​        Array.prototype.concat.call(args, Array.prototype.slice.call(arguments))

​      );

​    }

  };

  var boundLength = Math.max(0, target.length - args.length);

  var boundArgs = [];

  for (var i = 0; i < boundLength; i++) {

​    Array.prototype.push.call(boundArgs, '$' + i);

  }

  // 这里是Function构造方式生成形参length $1, $2, $3...

  bound = Function('binder', 'return function (' + Array.prototype.join.call(boundArgs, ',') + '){ return binder.apply(this, arguments); }')(binder);



  if (target.prototype) {

​    Empty.prototype = target.prototype;

​    bound.prototype = new Empty();

​    Empty.prototype = null;

  }

  return bound;

};


```





```js
// 手写bind

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
```

